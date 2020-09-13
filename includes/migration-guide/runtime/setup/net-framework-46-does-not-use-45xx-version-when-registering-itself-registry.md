---
ms.openlocfilehash: a9011514c7c4393ec44de2c7fae88768cdccf435
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89496429"
---
### <a name="the-net-framework-46-does-not-use-a-45xx-version-when-registering-itself-in-the-registry"></a>.NET Framework 4.6 não usa uma versão 4.5.x.x ao se registrar no registro

#### <a name="details"></a>Detalhes

Como é de se esperar, a chave de versão definida no registro (em <code>HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\NET Framework Setup\NDP\v4\Full</code>) do .NET Framework 4.6 começa com "4.6", e não "4.5". Os aplicativos que dependem dessas chaves do Registro para saber quais versões do .NET Framework estão instaladas em um computador precisam ser atualizados para compreenderem que 4.6 é uma nova versão possível, compatível com as versões 4.5.x anteriores.

#### <a name="suggestion"></a>Sugestão

Atualize os aplicativos que estão investigando uma instalação do .NET Framework 4.5 procurando por chaves do Registro 4.5 que também aceitam 4.6.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Microsoft Edge|
|Versão|4.6|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
