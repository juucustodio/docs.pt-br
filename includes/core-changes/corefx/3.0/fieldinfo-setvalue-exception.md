---
ms.openlocfilehash: 02c9305a36f47dfaf0b1fa8d19b07cd2d34badae
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96031960"
---
### <a name="fieldinfosetvalue-throws-exception-for-static-init-only-fields"></a>FieldInfo. SetValue gera uma exceção para campos estáticos somente de inicialização

A partir do .NET Core 3,0, uma exceção é lançada quando você tenta definir um valor em um campo estático, <xref:System.Reflection.FieldAttributes.InitOnly> chamando <xref:System.Reflection.FieldInfo.SetValue%2A?displayProperty=fullName> .

#### <a name="change-description"></a>Descrição das alterações

Em .NET Framework e versões do .NET Core anteriores a 3,0, você pode definir o valor de um campo estático que é constante depois que ele é inicializado ([ReadOnly em C#](~/docs/csharp/language-reference/keywords/readonly.md)) chamando <xref:System.Reflection.FieldInfo.SetValue%2A?displayProperty=fullName> . No entanto, a definição desse campo dessa forma resultou em um comportamento imprevisível com base na estrutura de destino e nas configurações de otimização.

No .NET Core 3,0 e versões posteriores, quando você chama <xref:System.Reflection.FieldInfo.SetValue%2A> em um campo estático, <xref:System.Reflection.FieldAttributes.InitOnly> uma <xref:System.FieldAccessException?displayProperty=nameWithType> exceção é lançada.

> [!TIP]
> Um <xref:System.Reflection.FieldAttributes.InitOnly> campo é aquele que só pode ser definido no momento em que é declarado ou no construtor para a classe que a contém. Em outras palavras, é constante depois que ela é inicializada.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="recommended-action"></a>Ação recomendada

Inicialize os campos estáticos <xref:System.Reflection.FieldAttributes.InitOnly> em um construtor estático. Isso se aplica a tipos dinâmicos e não dinâmicos.

Como alternativa, você pode remover o <xref:System.Reflection.FieldAttributes.InitOnly?displayProperty=nameWithType> atributo do campo e, em seguida, chamar <xref:System.Reflection.FieldInfo.SetValue%2A?displayProperty=nameWithType> .

#### <a name="category"></a>Categoria

Bibliotecas principais do .NET

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Reflection.FieldInfo.SetValue(System.Object,System.Object)?displayProperty=nameWithType>
- <xref:System.Reflection.FieldInfo.SetValue(System.Object,System.Object,System.Reflection.BindingFlags,System.Reflection.Binder,System.Globalization.CultureInfo)?displayProperty=nameWithType>

<!--

#### Affected APIs

- `M:System.Reflection.FieldInfo.SetValue(System.Object,System.Object)`
- `M:System.Reflection.FieldInfo.SetValue(System.Object,System.Object,System.Reflection.BindingFlags,System.Reflection.Binder,System.Globalization.CultureInfo)`

-->
