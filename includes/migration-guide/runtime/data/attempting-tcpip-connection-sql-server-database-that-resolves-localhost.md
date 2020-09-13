---
ms.openlocfilehash: bbeca87b3f498213b91d942cc4f197c9d80457a8
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497734"
---
### <a name="attempting-a-tcpip-connection-to-a-sql-server-database-that-resolves-to-localhost-fails"></a>Falha ao tentar uma conexão TCP/IP com um banco de dados do SQL Server resolvida para `localhost`

#### <a name="details"></a>Detalhes

No .NET Framework 4.6 e 4.6.1, tentar uma conexão TCP/IP com um banco de dados do SQL Server resolvida para <code>localhost</code> falha com o erro &quot;Ocorreu um erro relacionado à rede ou específico da instância durante o estabelecimento de uma conexão com o SQL Server. O servidor não foi encontrado ou não estava acessível. Verifique se o nome de instância está correto e se o SQL Server está configurado para permitir conexões remotas. (provedor: Adaptadores de Rede do SQL, erro: 26 – Erro ao Localizar Servidor/Instância Especificada)&quot;

#### <a name="suggestion"></a>Sugestão

Esse problema foi resolvido e o comportamento anterior restaurado no .NET Framework 4.6.2. Para se conectar a um banco de dados do SQL Server que seja resolvido para <code>localhost</code>, faça a atualização para o .NET Framework 4.6.2.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Secundária|
|Versão|4.6|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
