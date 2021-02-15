---
title: Implementando objetos de valor
description: Arquitetura de microsserviços do .NET para aplicativos .NET em contêineres | Obtenha os detalhes e as opções para implementar objetos de valor usando as novas funcionalidades do Entity Framework.
ms.date: 08/21/2020
ms.openlocfilehash: 1cb7ce04b3ab2f6da25f398e016baf60b863fb6b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91169200"
---
# <a name="implement-value-objects"></a>Implementar objetos de valor

Conforme discutido nas seções anteriores sobre entidades e agregações, a identidade é fundamental para entidades. No entanto, existem muitos objetos e itens de dados em um sistema que não exigem uma identidade e um acompanhamento de identidade, como objetos de valor.

Um objeto de valor pode fazer referência a outras entidades. Por exemplo, em um aplicativo que gera uma rota que descreve como ir de um ponto para outro, essa rota deve ser um objeto de valor. Seria um instantâneo de pontos em uma rota específica, mas essa rota sugerida não teria uma identidade, embora internamente possa fazer referência a entidades, como Cidade, Estrada etc.

A Figura 7-13 mostra o objeto de valor Endereço dentro da agregação Ordem.

![Diagrama que mostra o valor de endereço-objeto dentro da agregação de ordem.](./media/implement-value-objects/value-object-within-aggregate.png)

**Figura 7-13**. Tratar objeto de valor no agregado de Ordem

Conforme mostrado na Figura 7-13, uma entidade geralmente é composta por vários atributos. Por exemplo, a `Order` entidade pode ser modelada como uma entidade com uma identidade e composta internamente por um conjunto de atributos, como OrderID, OrderDate, OrderItems, etc. Mas o endereço, que é simplesmente um valor complexo composto de país/região, rua, cidade etc. e não tem nenhuma identidade nesse domínio, deve ser modelado e tratado como um objeto de valor.

## <a name="important-characteristics-of-value-objects"></a>Características importantes de objetos de valor

Existem duas características principais para objetos de valor:

- Eles não têm identidade.

- Eles são imutáveis.

A primeira característica já foi discutida. A imutabilidade é um requisito importante. Os valores de um objeto de valor devem ser imutáveis depois que o objeto for criado. Portanto, quando o objeto é construído, você deve fornecer os valores necessários, mas não deve permitir que eles sejam alterados durante o tempo de vida do objeto.

Objetos de valor permitem que você execute certos truques para desempenho graças à sua natureza imutável. Isso é especialmente verdadeiro em sistemas em que pode haver milhares de instâncias de objeto de valor, muitas das quais com os mesmos valores. Sua natureza imutável permite que sejam reutilizados; eles podem ser objetos intercambiáveis, desde que seus valores sejam os mesmos e não tenham identidade. Esse tipo de otimização às vezes pode ser a diferença entre o software executado lentamente e o software com bom desempenho. Obviamente, todos esses casos dependem do ambiente do aplicativo e do contexto de implantação.

## <a name="value-object-implementation-in-c"></a>Implementação de objeto de valor em C\#

Em termos de implementação, você pode ter uma classe base de objeto de valor que tenha métodos de utilitário básicos como igualdade com base na comparação entre todos os atributos (já que um objeto de valor não deve ser baseado em identidade) e outras características fundamentais. O exemplo a seguir mostra uma classe base do objeto de valor usada no microsserviço de ordenação de eShopOnContainers.

```csharp
public abstract class ValueObject
{
    protected static bool EqualOperator(ValueObject left, ValueObject right)
    {
        if (ReferenceEquals(left, null) ^ ReferenceEquals(right, null))
        {
            return false;
        }
        return ReferenceEquals(left, null) || left.Equals(right);
    }

    protected static bool NotEqualOperator(ValueObject left, ValueObject right)
    {
        return !(EqualOperator(left, right));
    }

    protected abstract IEnumerable<object> GetEqualityComponents();

    public override bool Equals(object obj)
    {
        if (obj == null || obj.GetType() != GetType())
        {
            return false;
        }

        var other = (ValueObject)obj;

        return this.GetEqualityComponents().SequenceEqual(other.GetEqualityComponents());
    }

    public override int GetHashCode()
    {
        return GetEqualityComponents()
            .Select(x => x != null ? x.GetHashCode() : 0)
            .Aggregate((x, y) => x ^ y);
    }
    // Other utility methods
}
```

Você pode usar essa classe durante a implementação do seu objeto de valor real, assim como acontece com o objeto de valor Endereço mostrado no exemplo a seguir:

```csharp
public class Address : ValueObject
{
    public String Street { get; private set; }
    public String City { get; private set; }
    public String State { get; private set; }
    public String Country { get; private set; }
    public String ZipCode { get; private set; }

    public Address() { }

    public Address(string street, string city, string state, string country, string zipcode)
    {
        Street = street;
        City = city;
        State = state;
        Country = country;
        ZipCode = zipcode;
    }

    protected override IEnumerable<object> GetEqualityComponents()
    {
        // Using a yield return statement to return each element one at a time
        yield return Street;
        yield return City;
        yield return State;
        yield return Country;
        yield return ZipCode;
    }
}
```

Você pode ver como essa implementação de objeto de valor do Endereço não tem nenhuma identidade e, portanto, nenhum campo de ID, nem na classe Address, nem mesmo na classe ValueObject.

Não foi possível ter nenhum campo de ID em uma classe a ser usado pelo Entity Framework (EF) até EF Core 2,0, o que ajuda muito a implementar objetos de valor melhores sem ID. Essa é justamente a explicação da próxima seção.

Pode ser argumentado que os objetos de valor, sendo imutáveis, devem ser somente leitura (ou seja, têm propriedades somente obtenção) e isso é verdade. No entanto, os objetos de valor geralmente são serializados e desserializados para passar pelas filas de mensagens e ser somente leitura interrompe o desserializador de atribuir valores, de modo que você apenas os deixa como `private set` , o que é somente leitura o suficiente para ser prático.

## <a name="how-to-persist-value-objects-in-the-database-with-ef-core-20-and-later"></a>Como persistir objetos de valor no banco de dados com EF Core 2,0 e posterior

Você acabou de ver como definir um objeto de valor em seu modelo de domínio. Mas como você pode realmente mantê-lo no banco de dados usando Entity Framework Core, já que ele normalmente visa entidades com identidade?

### <a name="background-and-older-approaches-using-ef-core-11"></a>Tela de fundo e abordagens mais antigas usando EF Core 1.1

Como segundo plano, uma limitação ao usar EF Core 1,0 e 1,1 era que você não podia usar [tipos complexos](xref:System.ComponentModel.DataAnnotations.Schema.ComplexTypeAttribute) , conforme definido no EF 6. x na .NET Framework tradicional. Portanto, se estiver usando EF Core 1.0 ou 1.1, precisará armazenar seu objeto de valor como uma entidade EF com um campo de ID. Então, para que se pareça mais com um objeto de valor sem nenhuma identidade, você pode ocultar a ID para deixar claro que a identidade de um objeto de valor não é importante no modelo de domínio. Você pode ocultar essa ID usando a ID como um [propriedade de sombra](/ef/core/modeling/shadow-properties). Uma vez que a configuração para ocultar a ID do modelo é configurada no nível de infraestrutura do EF, seria transparente para o seu modelo de domínio.

Na versão inicial do eShopOnContainers (.NET Core 1.1), a ID oculta necessária para a infraestrutura do EF Core foi implementada da seguinte maneira no nível de DbContext, usando a API Fluente no projeto de infraestrutura. Portanto, a ID foi oculta do ponto de vista do domínio modelo de domínio, mas ainda está na infraestrutura.

```csharp
// Old approach with EF Core 1.1
// Fluent API within the OrderingContext:DbContext in the Infrastructure project
void ConfigureAddress(EntityTypeBuilder<Address> addressConfiguration)
{
    addressConfiguration.ToTable("address", DEFAULT_SCHEMA);

    addressConfiguration.Property<int>("Id")  // Id is a shadow property
        .IsRequired();
    addressConfiguration.HasKey("Id");   // Id is a shadow property
}
```

No entanto, a persistência desse objeto de valor no banco de dados foi executada como uma entidade normal em uma tabela diferente.

Com o EF Core 2,0 e posterior, há novas e melhores maneiras de persistir objetos de valor.

## <a name="persist-value-objects-as-owned-entity-types-in-ef-core-20-and-later"></a>Persistir objetos de valor como tipos de entidade pertencentes no EF Core 2,0 e posterior

Mesmo com algumas lacunas entre o padrão de objeto de valor canônico em DDD e o tipo de entidade de propriedade no EF Core, atualmente, é a melhor maneira de persistir objetos de valor com o EF Core 2,0 e posterior. Você pode ver as limitações no final desta seção.

O recurso de tipo de entidade própria foi adicionado ao EF Core desde a versão 2.0.

Um tipo de entidade própria permite mapear tipos que não têm a própria identidade definida explicitamente no modelo de domínio e são usados como propriedades, como um objeto de valor, em uma de suas entidades. Um tipo de entidade de propriedade compartilha o mesmo tipo CLR com outro tipo de entidade (ou seja, é apenas uma classe regular). A entidade que contém a navegação de definição é a entidade proprietária. Ao consultar o proprietário, os tipos próprios serão incluídos por padrão.

Apenas olhando o modelo de domínio, um tipo de propriedade parece que ele não tem nenhuma identidade. No entanto, nos bastidores, os tipos de propriedade têm a identidade, mas a propriedade de navegação do proprietário faz parte dessa identidade.

A identidade de instâncias de tipos próprios não é completamente própria. Consiste em três componentes:

- A identidade do proprietário

- A propriedade de navegação apontando para elas

- No caso de coleções de tipos de propriedade, um componente independente (com suporte no EF Core 2,2 e posterior).

Por exemplo, no modelo de domínio Ordenação em eShopOnContainers, como parte da entidade de Ordem, o objeto de valor de endereço é implementado como um tipo de entidade própria dentro da entidade de proprietário, que é a entidade Ordem. `Address` é um tipo sem nenhuma propriedade de identidade definida no modelo de domínio. Ele é usado como uma propriedade do tipo Ordem para especificar o endereço para entrega para uma ordem específica.

Por convenção, uma chave primária de sombra será criada para o tipo próprio e será mapeada para a mesma tabela que a do proprietário usando a divisão de tabela. Isso permite usar tipos próprios de modo similar a como os tipos complexos são usados no EF6 no .NET Framework tradicional.

É importante observar que tipos próprios nunca são descobertos pela convenção no núcleo do EF, assim, você precisa declará-los explicitamente.

No eShopOnContainers, no arquivo OrderingContext.cs, dentro do `OnModelCreating()` método, várias configurações de infraestrutura são aplicadas. Um deles está relacionado à entidade Ordem.

```csharp
// Part of the OrderingContext.cs class at the Ordering.Infrastructure project
//
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.ApplyConfiguration(new ClientRequestEntityTypeConfiguration());
    modelBuilder.ApplyConfiguration(new PaymentMethodEntityTypeConfiguration());
    modelBuilder.ApplyConfiguration(new OrderEntityTypeConfiguration());
    modelBuilder.ApplyConfiguration(new OrderItemEntityTypeConfiguration());
    //...Additional type configurations
}
```

No código a seguir, a infraestrutura de persistência é definida para a entidade Ordem:

```csharp
// Part of the OrderEntityTypeConfiguration.cs class
//
public void Configure(EntityTypeBuilder<Order> orderConfiguration)
{
    orderConfiguration.ToTable("orders", OrderingContext.DEFAULT_SCHEMA);
    orderConfiguration.HasKey(o => o.Id);
    orderConfiguration.Ignore(b => b.DomainEvents);
    orderConfiguration.Property(o => o.Id)
        .ForSqlServerUseSequenceHiLo("orderseq", OrderingContext.DEFAULT_SCHEMA);

    //Address value object persisted as owned entity in EF Core 2.0
    orderConfiguration.OwnsOne(o => o.Address);

    orderConfiguration.Property<DateTime>("OrderDate").IsRequired();

    //...Additional validations, constraints and code...
    //...
}
```

No código anterior, o método `orderConfiguration.OwnsOne(o => o.Address)` especifica que a propriedade `Address` é uma entidade própria do tipo `Order`.

Por padrão, as colunas de nome e banco de dados de convenções do EF Core para as propriedades do tipo de entidade própria como `EntityProperty_OwnedEntityProperty`. Portanto, as propriedades internas do aparecerão `Address` na `Orders` tabela com os nomes `Address_Street` `Address_City` (e assim por diante para `State` , `Country` e `ZipCode` ).

Você pode acrescentar o método fluente `Property().HasColumnName()` para renomear as colunas. No caso em que `Address` é uma propriedade pública, os mapeamentos seriam semelhantes ao seguinte:

```csharp
orderConfiguration.OwnsOne(p => p.Address)
                            .Property(p=>p.Street).HasColumnName("ShippingStreet");

orderConfiguration.OwnsOne(p => p.Address)
                            .Property(p=>p.City).HasColumnName("ShippingCity");
```

É possível encadear o `OwnsOne` método em um mapeamento fluente. No exemplo hipotético a seguir, `OrderDetails` tem `BillingAddress` e `ShippingAddress`, que são tipos `Address`. Então `OrderDetails` pertence ao tipo `Order`.

```csharp
orderConfiguration.OwnsOne(p => p.OrderDetails, cb =>
    {
        cb.OwnsOne(c => c.BillingAddress);
        cb.OwnsOne(c => c.ShippingAddress);
    });
//...
//...
public class Order
{
    public int Id { get; set; }
    public OrderDetails OrderDetails { get; set; }
}

public class OrderDetails
{
    public Address BillingAddress { get; set; }
    public Address ShippingAddress { get; set; }
}

public class Address
{
    public string Street { get; set; }
    public string City { get; set; }
}
```

### <a name="additional-details-on-owned-entity-types"></a>Detalhes adicionais sobre tipos de entidade própria

- Os tipos próprios são definidos quando você configura uma propriedade de navegação com um tipo específico usando a API fluente OwnsOne.

- A definição de um tipo próprio em nosso modelo de metadados é uma composição de: o tipo de proprietário, a propriedade de navegação e o tipo CLR do tipo próprio.

- A identidade (chave) de uma instância de tipo próprio na nossa pilha é uma composição da identidade do tipo de proprietário e a definição do tipo próprio.

#### <a name="owned-entities-capabilities"></a>Recursos de entidades de propriedade

- Os tipos próprios podem referenciar outras entidades, tanto próprias (tipos próprios aninhados) quanto não próprias (propriedades de navegação de referência comuns para outras entidades).

- Você pode mapear o mesmo tipo CLR como diferentes tipos próprios na mesma entidade de proprietário por meio de propriedades de navegação separadas.

- A divisão de tabela é configurada por convenção, mas você pode recusar mapeando o tipo de propriedade para uma tabela diferente usando ToTable.

- O carregamento adiantado é executado automaticamente em tipos de propriedade, ou seja, não há necessidade de chamar `.Include()` na consulta.

- Pode ser configurado com o atributo `[Owned]` , usando EF Core 2,1 e posterior.

- Pode lidar com coleções de tipos de propriedade (usando a versão 2,2 e posteriores).

#### <a name="owned-entities-limitations"></a>Limitações de entidades pertencentes

- Você não pode criar um `DbSet<T>` de um tipo de propriedade (por Design).

- Você não pode chamar `ModelBuilder.Entity<T>()` em tipos de propriedade (atualmente por Design).

- Não há suporte para tipos de propriedade opcionais (ou seja, anuláveis) que são mapeados com o proprietário na mesma tabela (ou seja, usando divisão de tabela). Isso ocorre porque o mapeamento é feito para cada propriedade, não há um sentinela separado para o valor complexo nulo como um todo.

- Não há suporte para mapeamento de herança para tipos de propriedade, mas você deve ser capaz de mapear dois tipos folha das mesmas hierarquias de herança como tipos de propriedade diferentes. O EF Core não argumentará sobre o fato de que fazem parte da mesma hierarquia.

#### <a name="main-differences-with-ef6s-complex-types"></a>Principais diferenças com tipos complexos do EF6

- A divisão de tabela é opcional, ou seja, pode, opcionalmente, ser mapeada para uma tabela separada e ainda ser de tipos de propriedade.

- Eles podem referenciar outras entidades (ou seja, eles podem atuar como o lado dependente em relações com outros tipos de propriedade diferente).

## <a name="additional-resources"></a>Recursos adicionais

- **Martin Fowler. Padrão valorobject** \
  <https://martinfowler.com/bliki/ValueObject.html>

- **Eric Evans. Design controlado por domínio: solução de complexidade no coração do software.** (Livro; inclui uma discussão sobre objetos de valor) \
  <https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/>

- **Vaughn Vernon. Implementando o design controlado por domínio.** (Livro; inclui uma discussão sobre objetos de valor) \
  <https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577/>

- **Tipos de entidade pertencentes** \
  <https://docs.microsoft.com/ef/core/modeling/owned-entities>

- **Propriedades da sombra** \
  <https://docs.microsoft.com/ef/core/modeling/shadow-properties>

- **Tipos complexos e/ou objetos de valor**. Discussão no repositório GitHub do EF Core (guia Problemas) \
  <https://github.com/dotnet/efcore/issues/246>

- **ValueObject.cs.** Classe de objeto de valor base no eShopOnContainers. \
  <https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/SeedWork/ValueObject.cs>

- **Classe de endereços.** Exemplo de classe de objeto de valor em eShopOnContainers. \
  <https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/AggregatesModel/OrderAggregate/Address.cs>

> [!div class="step-by-step"]
> [Anterior](seedwork-domain-model-base-classes-interfaces.md) 
>  [Avançar](enumeration-classes-over-enum-types.md)
