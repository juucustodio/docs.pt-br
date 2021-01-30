---
title: Suprimir avisos de análise de código
description: Conheça as diferentes maneiras pelas quais você pode suprimir violações de análise de código .NET.
ms.date: 01/28/2021
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- code analysis, suppress warnings
- suppress code analysis warnings
ms.openlocfilehash: b08e93089975a59fabfeb0daaf6a2a6454b2c7e8
ms.sourcegitcommit: 68c9d9d9a97aab3b59d388914004b5474cf1dbd7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2021
ms.locfileid: "99217246"
---
# <a name="how-to-suppress-code-analysis-warnings"></a>Como suprimir avisos de análise de código

Este artigo aborda as várias maneiras pelas quais você pode suprimir avisos da análise de código ao compilar seu aplicativo .NET.

> [!TIP]
> Se você estiver usando o Visual Studio como seu ambiente de desenvolvimento, o menu de *lâmpada* fornecerá opções que geram o código para suprimir os avisos para você. Para obter mais informações, consulte [suprimir violações](/visualstudio/code-quality/use-roslyn-analyzers?#suppress-violations).

## <a name="disable-the-rule"></a>Desabilitar a regra

Ao desabilitar a regra de análise de código que está causando o aviso, você desabilita a regra para todo o arquivo ou projeto (dependendo do escopo do arquivo de [configuração](configuration-files.md) que você usa). Para desabilitar a regra, defina sua severidade como `none` no arquivo de configuração.

```ini
[*.{cs,vb}]
dotnet_diagnostic.<rule-ID>.severity = none
```

Para obter mais informações sobre severidades de regra, consulte [Configurar a severidade da regra](~/docs/fundamentals/code-analysis/configuration-options.md#severity-level).

## <a name="use-a-preprocessor-directive"></a>Usar uma diretiva de pré-processador

Use uma diretiva [#pragma warning (C#)](../../csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning.md) ou [Disable (Visual Basic)](../../visual-basic/language-reference/directives/disable-enable.md) para suprimir o aviso apenas para uma linha de código específica.

```csharp
    try { ... }
    catch (Exception e)
    {
#pragma warning disable CA2200 // Rethrow to preserve stack details
        throw e;
#pragma warning restore CA2200 // Rethrow to preserve stack details
    }
```

```vb
    Try
        ...
    Catch e As Exception
#Disable Warning CA2200 ' Rethrow to preserve stack details
        Throw e
#Enable Warning CA2200 ' Rethrow to preserve stack details
    End Try
```

## <a name="use-the-suppressmessageattribute"></a>Usar o SuppressMessageAttribute

Você pode usar um <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> para suprimir um aviso no arquivo de origem ou em um arquivo de supressões global para o projeto (*GlobalSuppressions.cs* ou *GlobalSuppressions. vb*). Esse atributo fornece uma maneira de suprimir um aviso em apenas algumas partes do seu projeto ou arquivo.

Os dois parâmetros de posição obrigatórios para o <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo são a *categoria* da regra e a *ID da regra*. O trecho de código a seguir passa `"Usage"` e `"CA2200:Rethrow to preserve stack details"` para esses parâmetros.

```csharp
[System.Diagnostics.CodeAnalysis.SuppressMessage("Usage", "CA2200:Rethrow to preserve stack details", Justification = "Not production code.")]
private static void IngorableCharacters()
{
    try
    {
        ...
    }
    catch (Exception e)
    {
        throw e;
    }
}
```

Se você adicionar o atributo ao arquivo de supressões global, você [delimitará](xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope) a supressão ao nível desejado, por exemplo `"member"` . Você especifica a API em que o aviso deve ser suprimido usando a <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Target> propriedade.

```csharp
[assembly: SuppressMessage("Usage", "CA2200:Rethrow to preserve stack details", Justification = "Not production code.", Scope = "member", Target = "~M:MyApp.Program.IngorableCharacters")]
```

Para suprimir avisos do código gerado pelo compilador que não é mapeado para a fonte de usuário fornecida explicitamente, você deve colocar o atributo de supressão em um arquivo de supressão global. Por exemplo, o código a seguir suprime uma violação em relação a um Construtor emitido pelo compilador:

```csharp
[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="MyTools.Type..ctor()")]
```

## <a name="see-also"></a>Confira também

- [Suprimir violações (Visual Studio)](/visualstudio/code-quality/use-roslyn-analyzers?#suppress-violations)
