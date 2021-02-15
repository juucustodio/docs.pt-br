---
title: Visão geral de segurança do SQL Server
description: Saiba mais sobre a arquitetura de segurança de SQL Server para entender quais recursos e funcionalidades ameaçam ameaças conhecidas e para prever futuras ameaças.
ms.date: 03/30/2017
ms.assetid: ae66dd75-5c16-4cc0-9e12-774dd26d3fb9
ms.openlocfilehash: ba396774e760a550246d0f0507984d3f7212204b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91172652"
---
# <a name="overview-of-sql-server-security"></a>Visão geral de segurança do SQL Server

Uma estratégia de defesa aprofundada, com camadas sobrepostas de segurança, é a melhor maneira de combater as ameaças à segurança. O SQL Server fornece uma arquitetura de segurança projetada para permitir que administradores de banco de dados e desenvolvedores criem aplicativos de banco de dados e ameaças de contador seguros. Cada versão do SQL Server foi aprimorada em versões anteriores do SQL Server com a introdução de novos recursos e funcionalidades. No entanto, a segurança não é fornecida na caixa. Cada aplicativo é exclusivo em seus requisitos de segurança. Os desenvolvedores precisam entender qual combinação de recursos e funcionalidades são mais apropriadas para combater ameaças conhecidas e para prever ameaças que possam surgir no futuro.  
  
 Uma instância de SQL Server contém uma coleção hierárquica de entidades, começando com o servidor. Cada servidor contém vários bancos de dados e cada um deles contém uma coleção de objetos protegíveis. Cada SQL Server protegível tem *permissões* associadas que podem ser concedidas a uma *entidade de segurança*, que é um indivíduo, grupo ou processo com acesso concedido a SQL Server. A estrutura de segurança SQL Server gerencia o acesso a entidades protegíveis por meio de *autenticação* e *autorização*.  
  
- A autenticação é o processo de fazer logon no SQL Server pelo qual uma entidade de segurança solicita acesso enviando as credenciais que o servidor avalia. A autenticação estabelece a identidade do usuário ou processo que está sendo autenticado.  
  
- A autorização é o processo usado para determinar quais recursos protegíveis podem ser acessados por uma entidade de segurança e quais operações são permitidas para esses recursos.  
  
 Os tópicos nesta seção abrangem SQL Server conceitos básicos de segurança, fornecendo links para a documentação completa na versão relevante do Manuais Online do SQL Server.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Autenticação no SQL Server](authentication-in-sql-server.md)  
 Descreve logons e a autenticação no SQL Server e fornece links para recursos adicionais.  
  
 [Funções de servidor e banco de dados no SQL Server](server-and-database-roles-in-sql-server.md)  
 Descreve as funções de servidor e banco de dados fixas, funções de banco de dados personalizadas e contas internas e fornece links para recursos adicionais.  
  
 [Propriedade e separação do esquema do usuário no SQL Server](ownership-and-user-schema-separation-in-sql-server.md)  
 Descreve a propriedade do objeto e a separação de esquema de usuário e fornece links para recursos adicionais.  
  
 [Autorização e permissões no SQL Server](authorization-and-permissions-in-sql-server.md)  
 Descreve como conceder permissões usando o princípio de privilégios mínimos e fornece links para recursos adicionais.  
  
 [Criptografia de dados no SQL Server](data-encryption-in-sql-server.md)  
 Descreve as opções de criptografia de dados no SQL Server e fornece links para recursos adicionais.  
  
 [Segurança da integração CLR no SQL Server](clr-integration-security-in-sql-server.md)  
 Fornece links para os recursos de segurança da integração CLR.  
  
## <a name="see-also"></a>Confira também

- [Protegendo aplicativos ADO.NET](../securing-ado-net-applications.md)
- [Segurança de SQL Server](sql-server-security.md)
- [Cenários de Segurança de Aplicativo no SQL Server](application-security-scenarios-in-sql-server.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
