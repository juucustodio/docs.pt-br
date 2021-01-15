---
title: Atualizar sua base de código para usar tipos de referência anuláveis
description: Escolha a melhor estratégia para atualizar sua base de código para usar tipos de referência anuláveis.
ms.technology: csharp-null-safety
ms.date: 07/31/2019
ms.openlocfilehash: ab0970247c7e3f3c20d7fdb40ef035c4ba1d8b01
ms.sourcegitcommit: 30e9e11dfd90112b8eec6406186ba3533f21eba1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2020
ms.locfileid: "95099322"
---
# <a name="update-libraries-to-use-nullable-reference-types-and-communicate-nullable-rules-to-callers"></a>Atualizar bibliotecas para usar tipos de referência anuláveis e comunicar regras anuláveis a chamadores

A adição de [tipos de referência anuláveis](nullable-references.md) significa que você pode declarar se um `null` valor é permitido ou não ou esperado para cada variável. Além disso, você pode aplicar um número de atributos:,,,,, `AllowNull` `DisallowNull` `MaybeNull` `NotNull` `NotNullWhen` `MaybeNullWhen` e `NotNullIfNotNull` para descrever completamente os Estados nulos dos valores de argumento e de retorno. Isso fornece uma ótima experiência à medida que você escreve o código. Você receberá avisos se uma variável não anulável puder ser definida como `null` . Você receberá avisos se uma variável anulável não for marcada como nula antes de você desreferenciá-la. Atualizar suas bibliotecas pode levar tempo, mas os benefícios valem a pena. Quanto mais informações você fornecer ao compilador sobre *quando* um `null` valor é permitido ou proibido, os melhores avisos que os usuários da sua API receberão. Vamos começar com um exemplo familiar. Imagine que sua biblioteca tenha a seguinte API para recuperar uma cadeia de caracteres de recurso:

```csharp
bool TryGetMessage(string key, out string message)
```

O exemplo anterior segue o `Try*` padrão familiar no .net. Há dois argumentos de referência para essa API: o `key` e o `message` parâmetro. Essa API tem as seguintes regras relacionadas à nulidade desses argumentos:

- Os chamadores não devem passar `null` como o argumento para `key` .
- Os chamadores podem passar uma variável cujo valor é `null` como o argumento para `message` .
- Se o `TryGetMessage` método retornar `true` , o valor de `message` não será nulo. Se o valor de retorno for `false,` o valor de `message` (e seu estado nulo) for NULL.

A regra para `key` pode ser totalmente expressa pelo tipo de variável: `key` deve ser um tipo de referência não anulável. O `message` parâmetro é mais complexo. Ele permite `null` como o argumento, mas garante que, em caso de sucesso, esse `out` argumento não seja nulo. Para esses cenários, você precisa de um vocabulário mais rico para descrever as expectativas.

Atualizar sua biblioteca para referências anuláveis requer mais do que `?` a inundação em algumas das variáveis e nomes de tipo. O exemplo anterior mostra que você precisa examinar suas APIs e considerar suas expectativas para cada argumento de entrada. Considere as garantias para o valor de retorno e quaisquer `out` `ref` argumentos ou no retorno do método. Em seguida, comunique essas regras ao compilador, e o compilador fornecerá avisos quando os chamadores não obedecem a essas regras.

Esse trabalho leva tempo. Vamos começar com as estratégias para tornar sua biblioteca ou reconhecimento anulável de aplicativo, ao mesmo tempo em que equilibra outros requisitos. Você verá como balancear o desenvolvimento contínuo habilitando tipos de referência anuláveis. Você aprenderá os desafios para definições de tipo genérico. Você aprenderá a aplicar atributos para descrever as condições anteriores e posteriores em APIs individuais.

## <a name="choose-a-strategy-for-nullable-reference-types"></a>Escolher uma estratégia para tipos de referência anuláveis

A primeira opção é se os tipos de referência anuláveis devem estar ativados ou desativados por padrão. Você tem duas estratégias:

- Habilite tipos de referência anuláveis para o projeto inteiro e desabilite-o no código que não está pronto.
- Só habilite tipos de referência anuláveis para o código anotado para tipos de referência anuláveis.

A primeira estratégia funciona melhor quando você está adicionando outros recursos à biblioteca ao atualizá-los para tipos de referência anuláveis. Todo o novo desenvolvimento tem reconhecimento anulável. À medida que você atualiza o código existente, você habilita os tipos de referência anuláveis nessas classes.

Seguindo essa primeira estratégia, você executa as seguintes etapas:

1. Habilite tipos de referência anuláveis para todo o projeto adicionando o `<Nullable>enable</Nullable>` elemento aos seus arquivos *csproj* .
1. Adicione o `#nullable disable` pragma a cada arquivo de origem em seu projeto.
1. Conforme você trabalha em cada arquivo, remova o pragma e resolva os avisos.

Essa primeira estratégia tem mais trabalho antecipado para adicionar o pragma a cada arquivo. A vantagem é que todos os novos arquivos de código adicionados ao projeto serão habilitados para permitir valor nulo. Qualquer trabalho novo terá reconhecimento de Nullable; somente o código existente deve ser atualizado.

A segunda estratégia funciona melhor se a biblioteca estiver estável e o foco principal do desenvolvimento é adotar tipos de referência anuláveis. Você ativa os tipos de referência anuláveis ao anotar APIs. Quando tiver terminado, habilite os tipos de referência anuláveis para o projeto inteiro.

Seguindo essa segunda estratégia, você realiza as seguintes etapas:

1. Adicione o `#nullable enable` pragma ao arquivo que você deseja que o reconheça de forma anulável.
1. Resolva os avisos.
1. Continue essas duas primeiras etapas até que você tenha feito o reconhecimento de toda a biblioteca.
1. Habilite tipos anuláveis para todo o projeto adicionando o `<Nullable>enable</Nullable>` elemento aos seus arquivos *csproj* .
1. Remova os `#nullable enable` pragmas, pois eles não são mais necessários.

Essa segunda estratégia tem menos trabalho de antecedência. A desvantagem é que a primeira tarefa quando você cria um novo arquivo é adicionar o pragma e torná-lo indesejado de forma anulável. Se algum desenvolvedor da sua equipe esquecer, esse novo código estará no registro posterior do trabalho para tornar todos os incompatíveis com o código anulável.

Qual dessas estratégias você escolhe depende de quanto o desenvolvimento ativo está ocorrendo em seu projeto. Quanto mais maduro e estável for seu projeto, melhor a segunda estratégia. Quanto mais recursos estiverem sendo desenvolvidos, melhor será a primeira estratégia.

> [!IMPORTANT]
> O contexto anulável global não se aplica a arquivos de código gerados. Em qualquer estratégia, o contexto anulável é *desabilitado* para qualquer arquivo de origem marcado como gerado. Isso significa que qualquer API em arquivos gerados não é anotada. Há quatro maneiras de um arquivo ser marcado como gerado:
>
> 1. Em. editorconfig, especifique `generated_code = true` em uma seção que se aplica a esse arquivo.
> 1. Put `<auto-generated>` ou `<auto-generated/>` em um comentário na parte superior do arquivo. Ele pode estar em qualquer linha nesse comentário, mas o bloco de comentário deve ser o primeiro elemento no arquivo.
> 1. Inicie o nome do arquivo com *TemporaryGeneratedFile_*
> 1. Termine o nome do arquivo com *. designer.cs*, *. generated.cs*, *. g.cs* ou *. g.i.cs*.
>
> Os geradores podem optar por usar a [`#nullable`](language-reference/preprocessor-directives/preprocessor-nullable.md) diretiva de pré-processador.

## <a name="should-nullable-warnings-introduce-breaking-changes"></a>Os avisos de anuláveis introduzem alterações interruptivas?

Antes de habilitar tipos de referência anuláveis, as variáveis são consideradas *alheios anuláveis*. Depois de habilitar tipos de referência anuláveis, todas essas variáveis são *não anuláveis*. O compilador emitirá avisos se essas variáveis não forem inicializadas para valores não nulos.

Outra provável fonte de avisos é retornar valores quando o valor não tiver sido inicializado.

A primeira etapa para abordar os avisos do compilador é usar `?` anotações em tipos de parâmetro e de retorno para indicar quando argumentos ou valores de retorno podem ser nulos. Quando variáveis de referência não devem ser nulas, a declaração original está correta. Conforme você faz essa tarefa, seu objetivo não é apenas corrigir avisos. A meta mais importante é fazer com que o compilador entenda sua intenção por possíveis valores nulos. Ao examinar os avisos, você chegará à sua próxima decisão principal para sua biblioteca. Deseja considerar a modificação de assinaturas de API para comunicar mais claramente sua intenção de design? Uma assinatura de API melhor para o `TryGetMessage` método examinado anteriormente poderia ser:

```csharp
string? TryGetMessage(string key);
```

O valor de retorno indica êxito ou falha e transporta o valor se o valor foi encontrado. Em muitos casos, a alteração de assinaturas de API pode melhorar a forma como elas comunicam valores nulos.

No entanto, para bibliotecas públicas ou bibliotecas com grandes bases de usuários, você pode preferir não introduzir nenhuma alteração de assinatura de API. Para esses casos e outros padrões comuns, você pode aplicar atributos para definir de forma mais clara quando um argumento ou valor de retorno pode ser `null` . Se você considerar ou não a alteração da superfície de sua API, provavelmente descobrirá que as anotações de tipo sozinhas não são suficientes para descrever `null` valores para argumentos ou valores de retorno. Nessas instâncias, você pode aplicar atributos para descrever mais claramente uma API.

## <a name="attributes-extend-type-annotations"></a>Atributos estendem anotações de tipo

Vários atributos foram adicionados para expressar informações adicionais sobre o estado nulo de variáveis. Todo o código que você escreveu antes do C# 8 introduziu tipos de referência anuláveis era *nulo alheios*. Isso significa que qualquer variável de tipo de referência pode ser nula, mas verificações nulas não são necessárias. Depois que o código estiver com *reconhecimento nulo*, essas regras serão alteradas. Os tipos de referência nunca devem ser o `null` valor, e os tipos de referência anuláveis devem ser verificados `null` antes de serem desreferenciados.

As regras para suas APIs são provavelmente mais complicadas, como vimos com o `TryGetValue` cenário de API. Muitas de suas APIs têm regras mais complexas para quando as variáveis podem ou não ser `null` . Nesses casos, você usará atributos para expressar essas regras. Os atributos que descrevem a semântica de sua API são encontrados no artigo sobre [atributos que afetam a análise anulável](./language-reference/attributes/nullable-analysis.md).

## <a name="generic-definitions-and-nullability"></a>Definições genéricas e nulidade

Comunicar corretamente o estado nulo de tipos genéricos e métodos genéricos requer um cuidado especial. O cuidado extra deriva do fato de que um tipo de valor anulável e um tipo de referência anulável são fundamentalmente diferentes. Um `int?` é sinônimo de `Nullable<int>` , enquanto `string?` é `string` um atributo adicionado pelo compilador. O resultado é que o compilador não pode gerar o código correto para `T?` sem saber se `T` é um `class` ou um `struct` .

Esse fato não significa que você não pode usar um tipo anulável (tipo de valor ou tipo de referência) como o argumento de tipo para um tipo genérico fechado. `List<string?>`E `List<int?>` são instanciações válidas do `List<T>` .

O que significa é que você não pode usar `T?` em uma classe genérica ou declaração de método sem restrições. Por exemplo, <xref:System.Linq.Enumerable.FirstOrDefault%60%601(System.Collections.Generic.IEnumerable%7B%60%600%7D)?displayProperty=nameWithType> não será alterado para retornar `T?` . Você pode superar essa limitação adicionando a `struct` `class` restrição ou. Com qualquer uma dessas restrições, o compilador sabe como gerar código para o `T` e o `T?` .

Talvez você queira restringir os tipos usados para que um argumento de tipo genérico seja de tipos não anuláveis. Você pode fazer isso adicionando a `notnull` restrição a esse argumento de tipo. Quando essa restrição é aplicada, o argumento de tipo não deve ser um tipo anulável.

## <a name="late-initialized-properties-data-transfer-objects-and-nullability"></a>Propriedades inicializadas tardias, objetos Transferência de Dados e nulidade

Indicando a nulidade das propriedades que são inicializadas com atraso, o que significa que definir após a construção, pode exigir uma consideração especial para garantir que sua classe continue expressando corretamente a intenção de design original.

Os tipos que contêm propriedades de inicialização tardia, como os objetos de Transferência de Dados (DTOs), geralmente são instanciados por uma biblioteca externa, como um ORM de banco de dados (mapeador relacional de objeto), um desserializador ou algum outro componente que preenche automaticamente as propriedades de outra fonte.

Considere a seguinte classe DTO, antes de habilitar tipos de referência anuláveis, que representa um aluno:

```csharp
class Student
{
    [Required]
    public string FirstName { get; set; }

    [Required]
    public string LastName { get; set; }

    public string VehicleRegistration { get; set; }
}
```

A intenção de design (indicada neste caso pelo `Required` atributo) sugere que, nesse sistema, as `FirstName` Propriedades e `LastName` são **obrigatórias** e, portanto, não nulas.

A `VehicleRegistration` propriedade **não é obrigatória**, portanto pode ser nula.

Quando você habilita tipos de referência anuláveis, você deseja indicar quais propriedades em seu DTO podem ser anuláveis, consistentes com sua intenção original:

```csharp
class Student
{
    [Required]
    public string FirstName { get; set; }

    [Required]
    public string LastName { get; set; }

    public string? VehicleRegistration { get; set; }
}
```

Para este DTO, a única propriedade que pode ser NULL é ``VehicleRegistration`` .

No entanto, o compilador gera `CS8618` avisos para `FirstName` e `LastName` , indicando que as propriedades não anuláveis não são inicializadas.

Há três opções disponíveis que resolvem os avisos do compilador de uma maneira que mantém a intenção original. Qualquer uma dessas opções é válida; Você deve escolher aquele que melhor atenda ao seu estilo de codificação e requisitos de design.

### <a name="initialize-in-the-constructor"></a>Inicializar no Construtor

A maneira ideal de resolver os avisos não inicializados é inicializar as propriedades no construtor:

```csharp
class Student
{
    public Student(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
    }

    [Required]
    public string FirstName { get; set; }

    [Required]
    public string LastName { get; set; }

    public string? VehicleRegistration { get; set; }
}
```

Essa abordagem só funciona se a biblioteca que você usa para instanciar a classe dá suporte à passagem de parâmetros no construtor.

Uma biblioteca pode dar suporte à passagem de *algumas* Propriedades no construtor, mas não todas. Por exemplo, EF Core dá suporte à [Associação de Construtor](/ef/core/modeling/constructors) para propriedades de coluna normais, mas não a propriedades de navegação.

Verifique a documentação na biblioteca que instancia sua classe para entender a extensão para a qual ela dá suporte à associação de construtor.

### <a name="property-with-nullable-backing-field"></a>Propriedade com campo de backup anulável

Se a associação de construtor não funcionar para você, uma maneira de lidar com esse problema é ter uma propriedade não anulável com um campo de backup anulável:

```csharp
private string? _firstName;

[Required]
public string FirstName
{
    set => _firstName = value;
    get => _firstName
           ?? throw new InvalidOperationException("Uninitialized " + nameof(FirstName))
}
```

Nesse cenário, se a `FirstName` propriedade for acessada antes de ser inicializada, o código lançará um `InvalidOperationException` , pois o contrato de API foi usado incorretamente.

Considere que algumas bibliotecas podem ter considerações especiais ao usar campos de backup. Por exemplo, EF Core pode precisar ser configurado para usar os [campos de backup](/ef/core/modeling/backing-field) corretamente.

### <a name="initialize-the-property-to-null"></a>Inicializar a propriedade como nula

Como alternativa terser ao uso de um campo de backup anulável, ou se a biblioteca que instancia a classe não for compatível com essa abordagem, você poderá inicializar a propriedade `null` diretamente, com a ajuda do operador NULL-tolerante ( `!` ):

```csharp
[Required]
public string FirstName { get; set; } = null!;

[Required]
public string LastName { get; set; } = null!;

public string? VehicleRegistration { get; set; }
```

Você nunca observará um valor nulo real no tempo de execução, exceto como resultado de um bug de programação, acessando a propriedade antes que ela tenha sido inicializada corretamente.

## <a name="see-also"></a>Confira também

- [Migrar uma base de código para referências que permitem valor nulo](tutorials/upgrade-to-nullable-references.md)
- [Trabalhando com tipos de referência anuláveis no EF Core](/ef/core/miscellaneous/nullable-reference-types)
