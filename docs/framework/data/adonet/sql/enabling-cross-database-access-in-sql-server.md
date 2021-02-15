---
description: 'Saiba mais sobre: Habilitando o acesso entre bancos de dados no SQL Server'
title: Habilitando o acesso entre bancos de dados no SQL Server
ms.date: 03/30/2017
ms.assetid: 10663fb6-434c-4c81-8178-ec894b9cf895
ms.openlocfilehash: 4e818b4f0294fdc7edd351a1e60203357579a320
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99695860"
---
# <a name="enabling-cross-database-access-in-sql-server"></a>Habilitando o acesso entre bancos de dados no SQL Server

O encadeamento de propriedade entre bancos de dados ocorre quando um procedimento em um banco de dados depende dos objetos em outro banco de dados. Uma cadeia de propriedade entre bancos de dados funciona como a cadeia de propriedade dentro de um único banco de dados, exceto que uma cadeia de propriedade exige que todos os proprietários de objetos sejam mapeados para a mesma conta de logon. Se o objeto de origem no banco de dados de origem e os objetos de destino nos bancos de dados de destino forem de propriedade da mesma conta de logon, o SQL Server não verificará permissões nos objetos de destino.  
  
## <a name="off-by-default"></a>Desativado por padrão  

 A cadeia de propriedade nos bancos de dados é desativada por padrão. A Microsoft recomenda que você desabilite a propriedade do banco de dados porque o encadeamento expõe você aos seguintes riscos de segurança:  
  
- Os proprietários de banco de dados e os membros de `db_ddladmin` ou das funções de banco de dados de `db_owners` podem criar os objetos pertencentes a outros usuários. Esses objetos podem potencialmente ser destinados a objetos em outros bancos de dados. Isso significa que, se você habilitar o encadeamento de propriedades entre banco de dados, deverá confiar completamente nesses usuários com dados em todos os bancos de dados.  
  
- Os usuários com a permissão CREATE DATABASE podem criar novos bancos de dados e anexar bancos de dados existentes. Se o encadeamento de propriedades entre banco de dados estiver habilitado, esses usuários poderão acessar objetos em outros bancos de dados que possam não ter privilégios nos bancos de dados recém-criados ou anexados.  
  
## <a name="enabling-cross-database-ownership-chaining"></a>Habilitando o encadeamento de propriedades entre banco de dados  

 O encadeamento de propriedades entre banco de dados deve ser habilitado apenas em ambientes onde você possa confiar completamente em usuários altamente privilegiados. Ele pode ser configurado durante a instalação para todos os bancos de dados ou seletivamente para bancos de dados específicos usando os comandos Transact-SQL `sp_configure` e `ALTER DATABASE` .  
  
 Para configurar seletivamente o encadeamento de propriedades entre banco de dados, use `sp_configure` para desativá-lo para o servidor. Use o comando ALTER DATABASE com SET DB_CHAINING ON para configurar o encadeamento de propriedades entre banco de dados para somente os bancos de dados que exigirem isso.  
  
 O exemplo a seguir ativa o encadeamento de propriedades entre banco de dados para todos os bancos de dados:  
  
```sql
EXECUTE sp_configure 'show advanced', 1;  
RECONFIGURE;  
EXECUTE sp_configure 'cross db ownership chaining', 1;  
RECONFIGURE;  
```  
  
 O exemplo a seguir ativa o encadeamento de propriedades entre banco de dados para bancos de dados específicos:  
  
```sql
ALTER DATABASE Database1 SET DB_CHAINING ON;  
ALTER DATABASE Database2 SET DB_CHAINING ON;  
```  
  
### <a name="dynamic-sql"></a>SQL dinâmico  

 O encadeamento de propriedades entre bancos de dados não funciona nos casos em que as instruções SQL criadas dinamicamente são executadas a menos que o mesmo usuário exista em ambos os bancos de dados. Você pode solucionar isso no SQL Server criando um procedimento armazenado que acessa dados em outro banco de dados e assinando o procedimento armazenado com um certificado existente em ambos os bancos de dados. Isso dá aos usuários acesso aos recursos do banco de dados usados pelo procedimento, sem conceder a eles permissões nem acesso ao banco de dados.  
  
## <a name="external-resources"></a>Recursos externos  

 Para obter mais informações, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Estendendo a representação do banco de dados usando](/previous-versions/sql/sql-server-2008-r2/ms188304(v=sql.105)) a opção de encadeamento de propriedades execute as e [cross db](/sql/database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option).|Os artigos descrevem como configurar o encadeamento de propriedade de bancos de dados para uma instância do SQL Server.|  
  
## <a name="see-also"></a>Consulte também

- [Protegendo aplicativos ADO.NET](../securing-ado-net-applications.md)
- [Visão geral de segurança do SQL Server](overview-of-sql-server-security.md)
- [Gerenciando permissões com procedimentos armazenados no SQL Server](managing-permissions-with-stored-procedures-in-sql-server.md)
- [Gravação de SQL Dinâmico Seguro no SQL Server](writing-secure-dynamic-sql-in-sql-server.md)
- [Assinando procedimentos armazenados no SQL Server](signing-stored-procedures-in-sql-server.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
