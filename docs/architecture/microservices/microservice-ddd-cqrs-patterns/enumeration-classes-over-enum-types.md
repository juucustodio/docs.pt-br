---
title: Usando classes Enumeration em vez de tipos enum
description: Arquitetura de microsserviços do .NET para aplicativos .NET em contêineres | Saiba como você pode usar classes de enumeração, em vez de enumerações, como uma maneira de resolver algumas limitações dessa última.
ms.date: 11/25/2020
ms.openlocfilehash: a45347d7cc9c3fc6378198ca1c44ba6fecfd54f5
ms.sourcegitcommit: 88fbb019b84c2d044d11fb4f6004aec07f2b25b1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2021
ms.locfileid: "97899522"
---
# <a name="use-enumeration-classes-instead-of-enum-types"></a>Usar classes de enumeração em vez de tipos enumerados

[Enumerations](../../../csharp/language-reference/builtin-types/enum.md) (ou *tipos enum*) são um wrapper de idioma fino em torno de um tipo integral. Talvez convenha limitar seu uso para quando você estiver armazenando um valor de um conjunto fechado de valores. A classificação com base em tamanhos (pequeno, médio ou grande) é um bom exemplo. Usar enumerações para fluxo de controle ou abstrações mais robustas pode ser um [code smell](https://deviq.com/antipatterns/code-smells). Esse tipo de uso leva a um código frágil com muitas instruções de fluxo de controle que verificam os valores da enumeração.

Em vez disso, é possível criar classes Enumeration que habilitam todos os recursos avançados de uma linguagem orientada a objeto.

No entanto, isso não é um tópico crítico e, em muitos casos, para simplificar, ainda será possível usar [tipos enum](../../../csharp/language-reference/builtin-types/enum.md) regulares se você preferir. O uso de classes de enumeração está mais relacionado aos conceitos relacionados aos negócios.

## <a name="implement-an-enumeration-base-class"></a>Implementar uma classe base de enumeração

O microsserviço de ordenação em eShopOnContainers fornece uma implementação de exemplo de classe base Enumeration, conforme mostrado no exemplo a seguir:

```csharp
public abstract class Enumeration : IComparable
{
    public string Name { get; private set; }

    public int Id { get; private set; }

    protected Enumeration(int id, string name) => (Id, Name) = (id, name);

    public override string ToString() => Name;

    public static IEnumerable<T> GetAll<T>() where T : Enumeration =>
        typeof(T).GetFields(BindingFlags.Public |
                            BindingFlags.Static |
                            BindingFlags.DeclaredOnly)
                 .Select(f => f.GetValue(null))
                 .Cast<T>();

    public override bool Equals(object obj)
    {
        if (obj is not Enumeration otherValue)
        {
            return false;
        }

        var typeMatches = GetType().Equals(obj.GetType());
        var valueMatches = Id.Equals(otherValue.Id);

        return typeMatches && valueMatches;
    }

    public int CompareTo(object other) => Id.CompareTo(((Enumeration)other).Id);

    // Other utility methods ...
}
```

Use essa classe como um tipo em qualquer entidade ou objeto de valor, como para a seguinte classe `CardType`: `Enumeration`:

```csharp
public class CardType
    : Enumeration
{
    public static CardType Amex = new CardType(1, nameof(Amex));
    public static CardType Visa = new CardType(2, nameof(Visa));
    public static CardType MasterCard = new CardType(3, nameof(MasterCard));

    public CardType(int id, string name)
        : base(id, name)
    {
    }
}
```

## <a name="additional-resources"></a>Recursos adicionais

- **Jimmy Bogard. Classes de enumeração** \
  <https://lostechies.com/jimmybogard/2008/08/12/enumeration-classes/>

- **Steve Smith. Enumerar alternativas em C #** \
  <https://ardalis.com/enum-alternatives-in-c>

- **Enumeration.cs.** Classe base de enumeração em eShopOnContainers \
  <https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/SeedWork/Enumeration.cs>

- **CardType.cs**. Exemplo de classe de enumeração em eShopOnContainers. \
  <https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/AggregatesModel/BuyerAggregate/CardType.cs>

- **SmartEnum**. Ardalis – Classes para ajudar a produzir enumerações fortemente tipadas mais inteligentes no .NET. \
  <https://www.nuget.org/packages/Ardalis.SmartEnum/>

>[!div class="step-by-step"]
>[Anterior](implement-value-objects.md) 
> [Avançar](domain-model-layer-validations.md)
