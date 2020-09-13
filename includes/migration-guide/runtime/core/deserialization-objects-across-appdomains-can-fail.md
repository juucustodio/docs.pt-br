---
ms.openlocfilehash: 3f82a4daac3b5d8981532f0c82e9a76f13c68b6e
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89496761"
---
### <a name="deserialization-of-objects-across-appdomains-can-fail"></a>Desserialização de objetos em domínios de aplicativo podem falhar

#### <a name="details"></a>Detalhes

Em alguns casos, quando um aplicativo usa dois ou mais domínios de aplicativo com bases de aplicativo diferentes, a tentativa de desserializar objetos no contexto da chamada lógica nos domínios de aplicativo aciona uma exceção.

#### <a name="suggestion"></a>Sugestão

Consulte [Mitigação: desserialização de objetos em domínios de aplicativos](~/docs/framework/migration-guide/mitigation-deserialization-of-objects-across-app-domains.md).

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Microsoft Edge|
|Versão|4.5.1|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
