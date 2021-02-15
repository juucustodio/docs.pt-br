---
ms.openlocfilehash: 53860bb867522503c5cb9bd35e25fadd00a116a2
ms.sourcegitcommit: 97405ed212f69b0a32faa66a5d5fae7e76628b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2020
ms.locfileid: "91609149"
---
### <a name="multi-line-aspnet-textbox-spacing-changed-when-using-antixssencoder"></a>O espaçamento da caixa de texto ASP.NET de várias linhas foi alterado ao usar AntiXSSEncoder

#### <a name="details"></a>Detalhes

No .NET Framework 4.0, linhas extras eram inseridas entre as linhas de uma caixa de texto de várias linhas no postback, se usando o <xref:System.Web.Security.AntiXss.AntiXssEncoder?displayProperty=fullName>. No .NET Framework 4.5, essas quebras de linhas extras não são incluídas, mas somente se o aplicativo Web for direcionado ao .NET 4.5

#### <a name="suggestion"></a>Sugestão

Lembre-se de que os aplicativos web 4.0 redirecionados para o .NET Framework 4.5 podem ter caixas de texto multilinha melhoradas para não inserir quebras de linha extras. Se isso não for desejável, o aplicativo poderá ter o comportamento antigo durante a execução no .NET Framework 4.5 visando o .NET Framework 4.0.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   | Secundária       |
| Versão | 4.5         |
| Tipo    | Redirecionando |
