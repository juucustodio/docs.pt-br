---
title: Reflexão (C#)
description: A reflexão fornece objetos que descrevem assemblies, módulos e tipos em C#. Se o código incluir atributos, a reflexão permitirá que você o acesse.
ms.date: 07/20/2015
ms.assetid: f80a2362-953b-4e8e-9759-cd5f334190d4
ms.openlocfilehash: 91d6d9bbd54199f3468f867d8804596f4a7546d9
ms.sourcegitcommit: 38999dc0ec4f7c4404de5ce0951b64c55997d9ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2021
ms.locfileid: "99427055"
---
# <a name="reflection-c"></a>Reflexão (C#)

A reflexão fornece objetos (do tipo <xref:System.Type> ) que descrevem assemblies, módulos e tipos. É possível usar a reflexão para criar dinamicamente uma instância de um tipo, associar o tipo a um objeto existente ou obter o tipo de um objeto existente e invocar seus métodos ou acessar suas propriedades e campos. Se você estiver usando atributos em seu código, a reflexão permite acessá-los. Para obter mais informações, consulte [Atributos](../../../standard/attributes/index.md).

Veja um exemplo simples de reflexão usando o <xref:System.Object.GetType> método herdado por todos os tipos da `Object` classe base – para obter o tipo de uma variável:

> [!NOTE]
> Certifique-se `using System;` de adicionar e `using System.Reflection;` na parte superior do seu arquivo *. cs* .

```csharp
// Using GetType to obtain type information:
int i = 42;
Type type = i.GetType();
Console.WriteLine(type);
```

A saída é: `System.Int32` .

O exemplo a seguir usa a reflexão para obter o nome completo do assembly carregado.

```csharp
// Using Reflection to get information of an Assembly:
Assembly info = typeof(int).Assembly;
Console.WriteLine(info);
```

A saída é: `System.Private.CoreLib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=7cec85d7bea7798e` .

> [!NOTE]
> As palavras-chave do C# `protected` e não `internal` têm significado na Il (linguagem intermediária) e não são usadas nas APIs de reflexão. Os termos correspondentes na IL são *Família* e *Assembly*. Para identificar um método `internal` usando a reflexão, use a propriedade <xref:System.Reflection.MethodBase.IsAssembly%2A>. Para identificar um método `protected internal`, use o <xref:System.Reflection.MethodBase.IsFamilyOrAssembly%2A>.

## <a name="reflection-overview"></a>Visão geral da reflexão

A reflexão é útil nas seguintes situações:

- Quando você precisa acessar atributos nos metadados do seu programa. Para obter mais informações, consulte [Recuperando informações armazenadas em atributos](../../../standard/attributes/retrieving-information-stored-in-attributes.md).
- Para examinar e instanciar tipos em um assembly.
- Para criar novos tipos em runtime. Usar as classes em <xref:System.Reflection.Emit>.
- Para executar a associação tardia, acessar métodos em tipos criados em tempo de execução. Consulte o tópico [Carregando e usando tipos dinamicamente](../../../framework/reflection-and-codedom/dynamically-loading-and-using-types.md).

## <a name="related-sections"></a>Seções relacionadas

Para mais informações:

- [Reflexão](../../../framework/reflection-and-codedom/reflection.md)
- [Exibindo informações de tipo](../../../framework/reflection-and-codedom/viewing-type-information.md)
- [Reflexão e tipos genéricos](../../../framework/reflection-and-codedom/reflection-and-generic-types.md)
- <xref:System.Reflection.Emit>
- [Recuperando informações armazenadas em atributos](../../../standard/attributes/retrieving-information-stored-in-attributes.md)

## <a name="see-also"></a>Confira também

- [Guia de programação C#](../index.md)
- [Assemblies no .NET](../../../standard/assembly/index.md)
