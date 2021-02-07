---
description: 'Saiba mais sobre: execução lado a lado em ADO.NET'
title: Execução lado a lado
ms.date: 03/30/2017
ms.assetid: 9f9ba96d-9f89-4f65-bb2f-6860879f4393
ms.openlocfilehash: ab55430382f49c40a577d5cac8501c0136c9f0a4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99718766"
---
# <a name="side-by-side-execution-in-adonet"></a>Execução lado a lado no ADO.NET

A execução lado a lado no .NET Framework é a capacidade de executar um aplicativo em um computador que tenha várias versões do .NET Framework instaladas, exclusivamente usando a versão para a qual o aplicativo foi compilado. Para obter informações detalhadas sobre como configurar a execução lado a lado, consulte [execução lado a lado](../../deployment/side-by-side-execution.md).  
  
 Um aplicativo compilado usando uma versão do .NET Framework pode ser executado em uma versão diferente do .NET Framework. No entanto, recomendamos que você compile uma versão do aplicativo para cada versão instalada do .NET Framework e as execute separadamente. Em qualquer cenário, você deve estar ciente das alterações no ADO.NET entre as versões que podem afetar a compatibilidade posterior ou a compatibilidade com versões anteriores do seu aplicativo.  
  
## <a name="forward-compatibility-and-backward-compatibility"></a>Compatibilidade posterior e compatibilidade com versões anteriores  

 A compatibilidade de encaminhamento significa que um aplicativo pode ser compilado com uma versão anterior do .NET Framework, mas ainda será executado com êxito em uma versão posterior do .NET Framework. O código ADO.NET escrito para a versão 1,1 do .NET Framework é compatível com versões posteriores.  
  
 Compatibilidade com versões anteriores significa que um aplicativo é compilado para uma versão mais recente do .NET Framework, mas continua sendo executado em versões anteriores do .NET Framework sem perda de funcionalidade. É claro que esse não será o caso dos recursos introduzidos em uma nova versão do .NET Framework.  
  
## <a name="the-net-framework-data-provider-for-odbc"></a>O Provedor de Dados .NET Framework para ODBC  

 A partir da versão 1,1, o .NET Framework Provedor de Dados para ODBC ( <xref:System.Data.Odbc> ) é incluído como parte da .NET Framework.
  
 Se você tiver um aplicativo desenvolvido para a versão 1,0 do .NET Framework que usa o provedor de dados ODBC para se conectar à sua fonte de dados e desejar executar esse aplicativo na versão 1,1 ou .NET Framework em uma versão posterior, atualize o namespace do provedor de dados ODBC para **System. Data. ODBC**. Em seguida, você deve recompilá-lo para a versão mais recente do .NET Framework.  
  
 Se você tiver um aplicativo desenvolvido para o .NET Framework versão 2,0 ou posterior que usa o provedor de dados ODBC para se conectar à fonte de dados e desejar executar esse aplicativo na versão 1,0 do .NET Framework, você deverá baixar o provedor de dados ODBC e instalá-lo no sistema .NET Framework versão 1,0. Em seguida, você deve alterar o namespace do provedor de dados ODBC para **Microsoft. Data. ODBC** e recompilar o aplicativo para o .NET Framework versão 1,0.  
  
## <a name="the-net-framework-data-provider-for-oracle"></a>O Provedor de Dados .NET Framework para Oracle  

 A partir da versão 1,1, o .NET Framework Provedor de Dados para Oracle ( <xref:System.Data.OracleClient> ) é incluído como parte da .NET Framework.
  
 Se você tiver um aplicativo desenvolvido para o .NET Framework versão 2,0 ou posterior que usa o provedor de dados para se conectar à sua fonte de dados e desejar executar esse aplicativo na versão 1,0 do .NET Framework, você deverá baixar o provedor de dados e instalá-lo no sistema .NET Framework versão 1,0.  
  
## <a name="code-access-security"></a>Segurança de Acesso do Código  

 Os provedores de dados de .NET Framework na versão .NET Framework 1,0 ( <xref:System.Data.SqlClient> , <xref:System.Data.OleDb> ) devem ser executados com a permissão FullTrust. Qualquer tentativa de usar os provedores de dados .NET Framework k do .NET Framework versão 1,0 em uma zona com permissão inferior a FullTrust causa um <xref:System.Security.SecurityException> .  
  
 No entanto, a partir do .NET Framework versão 2,0, todos os provedores de dados de .NET Framework podem ser usados em zonas parcialmente confiáveis. Além disso, um novo recurso de segurança foi adicionado aos provedores de dados de .NET Framework no .NET Framework versão 1,1. Esse recurso permite que você restrinja quais cadeias de conexão podem ser usadas em uma zona de segurança específica. Você também pode desabilitar o uso de senhas em branco para uma zona de segurança específica. Para obter mais informações, consulte [Segurança de acesso do código e ADO.NET](code-access-security.md).  
  
 Como cada instalação do .NET Framework tem um arquivo Security.config separado, não há problemas de compatibilidade com as configurações de segurança. No entanto, se seu aplicativo depende dos recursos de segurança adicionais do ADO.NET incluídos no .NET Framework versão 1,1 e posterior, você não poderá distribuí-lo para um sistema da versão 1,0.  
  
## <a name="sqlcommand-execution"></a>Execução de SqlCommand  

 A partir do .NET Framework versão 1,1, a maneira como o <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> executa comandos na fonte de dados foi alterada.  
  
 No .NET Framework versão 1,0, <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> executou todos os comandos no contexto do procedimento armazenado **sp_executesql** . Como resultado, os comandos que afetam o estado da conexão (por exemplo, definir NOCOUNT ON) aplicam-se somente à execução do comando atual. O estado da conexão não é modificado para os comandos subsequentes executados enquanto a conexão está aberta.  
  
 No .NET Framework versão 1,1 e posterior, o <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> só executará um comando no contexto do procedimento armazenado **sp_executesql** se o comando contiver parâmetros, o que fornecerá um benefício de desempenho. Como resultado, se um comando que afeta o estado da conexão estiver incluído em um comando sem parâmetros, ele modificará o estado da conexão para todos os comandos subsequentes executados enquanto a conexão estiver aberta.  
  
 Considere o seguinte lote de comandos executados em uma chamada para <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> .  
  
```sql
SET NOCOUNT ON;  
SELECT * FROM dbo.Customers;  
```  
  
 No .NET Framework versão 1,1 e posterior, NOCOUNT permanecerá em todos os comandos subsequentes executados enquanto a conexão estiver aberta. Na versão .NET Framework 1,0, NOCOUNT só está ATIVAda para a execução do comando atual.  
  
 Essa alteração pode afetar a compatibilidade de frente e para trás do seu aplicativo se você depender do comportamento do <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> para qualquer versão do .NET Framework.  
  
 Para aplicativos executados em versões anteriores e posteriores do .NET Framework, você pode escrever seu código para certificar-se de que o comportamento é o mesmo, independentemente da versão em que você está executando. Se você quiser ter certeza de que um comando modifica o estado da conexão para todos os comandos subsequentes, recomendamos que execute o comando usando <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> . Se você quiser garantir que um comando não modifique a conexão para todos os comandos subsequentes, recomendamos que você inclua os comandos para redefinir o estado da conexão no comando. Por exemplo:  
  
```sql
SET NOCOUNT ON;  
SELECT * FROM dbo.Customers;  
SET NOCOUNT OFF;  
```  
  
## <a name="see-also"></a>Confira também

- [Visão geral do ADO.NET](ado-net-overview.md)
- [Recuperando e modificando dados no ADO.NET](retrieving-and-modifying-data.md)
