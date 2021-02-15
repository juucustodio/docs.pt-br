---
ms.openlocfilehash: e65ba0edb132f5cded244a69d58e43ffea76a039
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606518"
---
### <a name="sqlconnection-can-no-longer-connect-to-sql-server-1997-or-databases-using-the-via-adapter"></a>SqlConnection não pode mais se conectar ao SQL Server 1997 ou a bancos de dados usando o adaptador VIA

#### <a name="details"></a>Detalhes

Conexões a bancos de dados do SQL Server usando o [Protocolo VIA (Virtual Interface Adapter)](/previous-versions/sql/sql-server-2008-r2/ms191229(v=sql.105)) não têm mais suporte. O protocolo usado para se conectar a um banco de dados do SQL Server fica visível na cadeia de conexão. Uma conexão VIA conterá via:&lt;nomedoservidor&gt;. Se esse aplicativo estiver se conectando ao SQL por meio de um protocolo diferente de VIA (TCP: ou NP: por exemplo), nenhuma alteração significativa será encontrada. Além disso, não há mais suporte para conexões com SQL Server 7 (1997).

#### <a name="suggestion"></a>Sugestão

O protocolo VIA foi preterido, de modo que um protocolo alternativo deve ser usado para se conectar a bancos de dados SQL. O protocolo mais usado é o TCP/IP. Para obter mais informações sobre como se conectar por meio de TCP/IP, confira [Habilitar o protocolo TCP/IP para uma instância de banco de dados](/previous-versions/visualstudio/visual-studio-2008/bb909712(v=vs.90)). Se o banco de dados for acessado somente de dentro de uma intranet, o protocolo de pipes compartilhado poderá fornecer um melhor desempenho se a rede estiver lenta.

| Name    | Valor       |
|:--------|:------------|
| Escopo   |Microsoft Edge|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Data.SqlClient.SqlConnection.%23ctor(System.String)>
- <xref:System.Data.SqlClient.SqlConnection.%23ctor(System.String,System.Data.SqlClient.SqlCredential)>

<!--

#### Affected APIs

- `M:System.Data.SqlClient.SqlConnection.#ctor(System.String)`
- `M:System.Data.SqlClient.SqlConnection.#ctor(System.String,System.Data.SqlClient.SqlCredential)`

-->
