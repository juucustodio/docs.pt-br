---
description: 'Saiba mais sobre: Personalizando permissões com representação no SQL Server'
title: Personalizando permissões com representação no SQL Server
ms.date: 03/30/2017
ms.assetid: dc733d09-1d6d-4af0-9c4b-8d24504860f1
ms.openlocfilehash: 1c2cada004b8f604ccbb9448f40e00bea472771f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786115"
---
# <a name="customizing-permissions-with-impersonation-in-sql-server"></a>Personalizando permissões com representação no SQL Server

Muitos aplicativos usam procedimentos armazenados para acessar os dados, dependendo do encadeamento de propriedade para restringir o acesso a tabelas base. Você pode conceder permissões EXECUTE em procedimentos armazenados, revogando ou negando permissões nas tabelas base. O SQL Server não verifica as permissões do chamador se o procedimento armazenado e as tabelas têm o mesmo proprietário. No entanto, o encadeamento de propriedades não funcionará se os objetos tiverem proprietários diferentes ou no caso de SQL dinâmico.  
  
 Você pode usar a cláusula EXECUTE AS em um procedimento armazenado quando o chamador não tiver permissões nos objetos de banco de dados referenciados. O efeito da cláusula EXECUTE AS é que o contexto de execução é alternado para o usuário do proxy. Qualquer código, assim como as chamadas para os procedimentos armazenados ou gatilhos aninhados, é executado sob o contexto de segurança do usuário do proxy. O contexto de execução é revertido para o chamador original somente após a execução do procedimento ou quando uma instrução REVERT é emitida.  
  
## <a name="context-switching-with-the-execute-as-statement"></a>Alternância de contexto com a instrução EXECUTE AS  

 A instrução EXECUTE AS do Transact-SQL permite a troca do contexto de execução de uma instrução representando outro logon ou usuário do banco de dados. Essa é uma técnica útil para testar consultas e procedimentos como outro usuário.  
  
```sql  
EXECUTE AS LOGIN = 'loginName';  
EXECUTE AS USER = 'userName';  
```  
  
 Você deve ter permissões IMPERSONATE no logon ou usuário que você está representando. Essa permissão é implícita para `sysadmin` para todos os bancos de dados e os membros de função `db_owner` nos bancos de dados que eles possuem.  
  
## <a name="granting-permissions-with-the-execute-as-clause"></a>Concedendo permissões com a cláusula EXECUTE AS  

 Você pode usar a cláusula EXECUTE AS no cabeçalho da definição de um procedimento armazenado, gatilho, ou uma função definida pelo usuário (com exceção das funções com valor de tabela embutida). Isso faz o procedimento ser executado no contexto do nome de usuário ou palavra-chave especificada na cláusula EXECUTE AS. Você pode criar um usuário de proxy no banco de dados que não seja mapeado para um logon, permitindo apenas as permissões necessárias sobre os objetos acessados pelo procedimento. Apenas o usuário do proxy especificado na cláusula EXECUTE AS deve ter permissões em todos os objetos acessados pelo módulo.  
  
> [!NOTE]
> Algumas ações, como TRUNCATE TABLE, não têm permissões concessíveis. Incorporando a instrução dentro de um procedimento e especificando um usuário de proxy que tenha permissões ALTER TABLE, você pode estender as permissões para truncar a tabela para chamadores que têm somente as permissões EXECUTE no procedimento.  
  
 O contexto especificado na cláusula EXECUTE AS é válido para a duração do procedimento, inclusive procedimentos aninhados e gatilhos. O contexto será revertido para o chamador quando a execução estiver concluída ou a instrução REVERT for emitida.  
  
 Há três etapas envolvidas no uso da cláusula EXECUTE AS em um procedimento.  
  
1. Crie um usuário de proxy no banco de dados que não seja mapeado para um logon. Isso não é obrigatório, mas ajuda a gerenciar permissões.  
  
```sql
CREATE USER proxyUser WITHOUT LOGIN  
```  
  
1. Conceda ao usuário de proxy as permissões necessárias.  
  
2. Adicione a cláusula EXECUTE AS no procedimento armazenado ou função definida pelo usuário.  
  
```sql
CREATE PROCEDURE [procName] WITH EXECUTE AS 'proxyUser' AS ...  
```  
  
> [!NOTE]
> Os aplicativos que exigem a auditoria podem ser interrompidos porque o contexto de segurança original do chamador não é retido. As funções internas que retornam a identidade do usuário atual, como SESSION_USER, USER ou USER_NAME retornarão o usuário associado com a cláusula EXECUTE AS, não o chamador original.  
  
### <a name="using-execute-as-with-revert"></a>Usando EXECUTE AS com REVERT  

 Você pode usar a instrução REVERT do Transact-SQL para reverter para o contexto da execução original.  
  
 A cláusula opcional, sem COOKIE de reversão = @variableName , permite que você alterne o contexto de execução de volta para o chamador se a @variableName variável contiver o valor correto. Isso permite a troca do contexto de execução de volta para o chamador em ambientes em que o pool de conexões é usado. Como o valor de @variableName é conhecido somente pelo chamador da instrução execute as, o chamador pode garantir que o contexto de execução não possa ser alterado pelo usuário final que invoca o aplicativo. Quando a conexão é fechada, ela será retornada para o pool. Para obter mais informações sobre o pool de conexões no ADO.NET, consulte [SQL Server pooling de conexão (ADO.net)](../sql-server-connection-pooling.md).  
  
### <a name="specifying-the-execution-context"></a>Especificando o contexto de execução  

 Além de especificar um usuário, você também poderá usar EXECUTE AS com qualquer uma das palavras-chave a seguir.  
  
- CALLER. Executar como CALLER é o padrão; se nenhuma outra opção for especificada, o procedimento será executado no contexto de segurança do chamador.  
  
- OWNER. Executar como OWNER executa o procedimento no contexto do proprietário do procedimento. Se o procedimento for criado em um esquema de propriedade do `dbo` ou pelo proprietário do banco de dados, o procedimento será executado com permissões ilimitadas.  
  
- SELF. Executar como SELF executa no contexto de segurança do criador do procedimento armazenado. Isso é equivalente a executar como usuário especificado, onde o usuário especificado é a pessoa que cria ou altera o procedimento.  
  
## <a name="see-also"></a>Consulte também

- [Protegendo aplicativos ADO.NET](../securing-ado-net-applications.md)
- [Visão geral de segurança do SQL Server](overview-of-sql-server-security.md)
- [Cenários de Segurança de Aplicativo no SQL Server](application-security-scenarios-in-sql-server.md)
- [Gerenciando permissões com procedimentos armazenados no SQL Server](managing-permissions-with-stored-procedures-in-sql-server.md)
- [Gravação de SQL Dinâmico Seguro no SQL Server](writing-secure-dynamic-sql-in-sql-server.md)
- [Assinando procedimentos armazenados no SQL Server](signing-stored-procedures-in-sql-server.md)
- [Modificando dados com procedimentos armazenados](../modifying-data-with-stored-procedures.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
