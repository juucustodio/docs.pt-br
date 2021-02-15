---
title: Analisadores de código para .NET Framework
titleSuffix: ''
description: Saiba como usar os analisadores no pacote .NET Framework analisadores para encontrar e resolver problemas em seu código.
author: billwagner
ms.author: wiwagn
ms.date: 10/23/2020
ms.openlocfilehash: 69dfbc9f9645c7f602ffbce46308b241c119fd96
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687815"
---
# <a name="code-analysis"></a>Análise de código

Você pode usar analisadores de código para encontrar possíveis problemas em seu .NET Framework código do aplicativo. Os analisadores encontram possíveis problemas e sugerem correções para eles.

Os analisadores de código baseados em Roslyn são executados interativamente no Visual Studio à medida que você escreve seu código ou como parte de uma compilação de CI. Você deve adicionar os analisadores ao seu projeto o mais cedo possível no ciclo de desenvolvimento. Quanto antes você encontrar potenciais problemas no seu código, mais fácil será corrigi-los. Os analisadores sinalizam problemas no código existente e avisam sobre novos problemas à medida que você continua o desenvolvimento.

## <a name="install-and-configure-analyzers"></a>Instalar e configurar analisadores

O Analisador do .NET Framework é fornecido no pacote do NuGet [Microsoft.NetFramework.Analyzers](https://www.nuget.org/packages/Microsoft.NetFramework.Analyzers/). Este pacote fornece analisadores específicos para .NET Framework APIs, que incluem analisadores de segurança. O pacote está incluído no [pacote Microsoft. CodeAnalysis. FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers), portanto, se você instalar esse pacote, não será necessário instalar os analisadores de .NET Framework separadamente.

Instale o pacote NuGet em todos os projetos em que você deseja que os analisadores sejam executados. Somente um desenvolvedor precisa adicioná-los ao projeto. O pacote de analisador é uma dependência de projeto e será executado no computador de cada um dos desenvolvedores assim que ele tiver a solução atualizada.

Para instalar o pacote, clique com o botão direito do mouse no projeto e selecione "gerenciar dependências". No Gerenciador do NuGet, pesquise por "Microsoft. NetFramework. Analyzers". Instale a versão estável mais recente em todos os projetos na solução.

## <a name="use-the-analyzers"></a>Usar os analisadores

Depois de instalar o pacote do NuGet, compile a solução. O analisador relatará eventuais problemas que ele localize na base de código. Os problemas são relatados como avisos na janela Lista de Erros do Visual Studio, conforme mostrado na imagem a seguir:

![Problemas relatados por .NET Framework analisadores.](./media/framework-analyzers-2.png)

Ao escrever código, você vê linhas onduladas sob qualquer problema potencial existente nele.
Passe o mouse sobre qualquer problema para obter mais informações e veja sugestões para qualquer correção possível, conforme mostrado na imagem a seguir:

![Relatório interativo de problemas encontrados por analisadores de código.](./media/framework-analyzers-1.png)

Para obter mais informações, consulte [análise de código no Visual Studio](/visualstudio/code-quality/roslyn-analyzers-overview).

## <a name="types-of-rules"></a>Tipos de regras

Os analisadores examinam o código em sua solução e os avisos de superfície com um `CA` prefixo. Para obter uma lista de todos os avisos possíveis, consulte [regras de qualidade de código](../fundamentals/code-analysis/quality-rules/index.md). Somente alguns desses avisos se aplicam a APIS .NET Framework, incluindo:

- [CA1058: Tipos não devem estender determinados tipos base](../fundamentals/code-analysis/quality-rules/ca1058.md)

- [CA2153: não capturar exceções de estado corrompido](../fundamentals/code-analysis/quality-rules/ca2153.md)

- [CA2229: Implementar construtores de serialização](../fundamentals/code-analysis/quality-rules/ca2229.md)

- [CA2235: Marcar todos os campos não serializáveis](../fundamentals/code-analysis/quality-rules/ca2235.md)

- [CA2237: marcar tipos ISerializable com serializable](../fundamentals/code-analysis/quality-rules/ca2237.md)

- [CA3075: processamento de DTD inseguro em XML](../fundamentals/code-analysis/quality-rules/ca3075.md)

- [CA5350: não use algoritmos de criptografia fracos](../fundamentals/code-analysis/quality-rules/ca5350.md)

- [CA5351 não usam algoritmos de criptografia desfeitos](../fundamentals/code-analysis/quality-rules/ca5351.md)

## <a name="see-also"></a>Veja também

- [Análise de código no Visual Studio](/visualstudio/code-quality/roslyn-analyzers-overview)
- [Análise de código no SDK do .NET](../fundamentals/code-analysis/overview.md)
