---
ms.openlocfilehash: e450c53008e7562e37518fdfd6872ff9b63b6ac3
ms.sourcegitcommit: 97405ed212f69b0a32faa66a5d5fae7e76628b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2020
ms.locfileid: "91609122"
---
### <a name="sharing-session-state-with-aspnet-stateserver-requires-all-servers-in-the-web-farm-to-use-the-same-net-framework-version"></a>O compartilhamento do estado de sessão com o ASP.NET StateServer exige que todos os servidores na web farm usem a mesma versão de .NET Framework

#### <a name="details"></a>Detalhes

Ao habilitar o estado de sessão <xref:System.Web.SessionState.SessionStateMode.StateServer?displayProperty=fullName>, todos os servidores no web farm fornecido devem usar a mesma versão do .NET Framework para o estado ser compartilhado corretamente.

#### <a name="suggestion"></a>Sugestão

Certifique-se de atualizar as versões do .NET Framework em servidores Web que compartilham o estado ao mesmo tempo.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Microsoft Edge|
|Versão|4.5|
|Tipo|Runtime

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Web.SessionState.SessionStateMode.StateServer?displayProperty=nameWithType>

<!--

#### Affected APIs

- `F:System.Web.SessionState.SessionStateMode.StateServer`

-->
