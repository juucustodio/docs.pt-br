---
description: 'Saiba mais sobre: Criando funções de aplicativo no SQL Server'
title: Criando funções de aplicativo no SQL Server
ms.date: 03/30/2017
ms.assetid: 27442435-dfb2-4062-8c59-e2960833a638
ms.openlocfilehash: 20047d12a004230aebca1cf9d42b3893d36f3844
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786154"
---
# <a name="creating-application-roles-in-sql-server"></a>Criando funções de aplicativo no SQL Server

As funções de aplicativo fornecem uma maneira de atribuir permissões para um aplicativo em vez de uma função ou usuário do banco de dados. Os usuários podem se conectar ao banco de dados, ativar a função de aplicativo e presumir as permissões concedidas ao aplicativo. As permissões concedidas para a função de aplicativo são impostas para a duração da conexão.  
  
> [!IMPORTANT]
> As funções de aplicativo são ativadas quando um aplicativo cliente fornece um nome da função de aplicativo e uma senha na cadeia de conexão. Eles apresentam uma vulnerabilidade de segurança em um aplicativo de duas camadas porque a senha deve ser armazenada no computador cliente. Em um aplicativo de três camadas, você pode armazenar a senha para que não possa ser acessada por usuários do aplicativo.  
  
## <a name="application-role-features"></a>Recursos da função de aplicativo  

 As funções de aplicativo têm os seguintes recursos:  
  
- Ao contrário das funções de banco de dados, as funções de aplicativo não contêm nenhum membro.  
  
- As funções de aplicativo são ativadas quando um aplicativo fornece o nome da função de aplicativo e uma senha para o procedimento armazenado do sistema `sp_setapprole`.  
  
- A senha deve ser armazenado no computador cliente e ser fornecida em tempo de execução; uma função de aplicativo não pode ser ativada de dentro do SQL Server.  
  
- A senha não é criptografada. A senha do parâmetro é armazenada como um hash unidirecional.  
  
- Quando forem ativadas, as permissões adquiridas por meio da função de aplicativo permanecem aplicadas para a duração da conexão.  
  
- A função de aplicativo herda as permissões concedidas para a função `public`.  
  
- Se um membro da função de servidor fixa do `sysadmin` ativar uma função de aplicativo, o contexto de segurança mudará para a função de aplicativo para a duração da conexão.  
  
- Se você criar uma conta de `guest` em um banco de dados que tenha uma função de aplicativo, não precisará criar um usuário de banco de dados para a função de aplicativo ou para nenhum dos logons que a chamam. As funções de aplicativo poderão acessar diretamente outro banco de dados somente se uma conta de `guest` existir no segundo banco de dados  
  
- As funções internas que retornam os nomes de logon, como SYSTEM_USER, retornam o nome do logon que chamou a função de aplicativo. As funções internas que retornam os nomes de usuário de banco de dados retornam o nome da função de aplicativo.  
  
### <a name="the-principle-of-least-privilege"></a>O princípio de privilégios mínimos  

 As funções de aplicativo devem receber somente as permissões necessárias no caso de a senha ser comprometida. As permissões para a função `public` devem ser revogadas em qualquer banco de dados usando uma função de aplicativo. Desative a conta de `guest` em qualquer banco de dados ao qual você não queira que chamadores da função de aplicativo tenham acesso.  
  
### <a name="application-role-enhancements"></a>Aprimoramentos da função de aplicativo  

 O contexto de execução pode ser alternado de volta para o chamador original após ter ativado uma função do aplicativo, eliminando a necessidade de desativar o pool de conexões. O procedimento `sp_setapprole` tem uma nova opção que cria um cookie, que contém informações de contexto sobre o chamador. Você pode reverter a sessão chamando o procedimento `sp_unsetapprole`, passando o cookie.  
  
## <a name="application-role-alternatives"></a>Alternativas a funções de aplicativo  

 As funções de aplicativo dependem da segurança de uma senha, que apresenta uma vulnerabilidade de segurança em potencial. As senhas podem ser expostas sendo inseridas no código do aplicativo ou salvas no disco.  
  
 Você pode querer considerar as seguintes alternativas.  
  
- Use a troca de contexto com a instrução EXECUTE AS com suas cláusulas NO REVERT e WITH COOKIE. Você pode criar uma conta de usuário em um banco de dados que não seja mapeado para um logon. Em seguida, você atribui permissões para essa conta. Usar EXECUTE AS a um usuário sem logon é mais seguro porque é baseado em permissão, não baseado em senha. Para obter mais informações, consulte [Personalizando permissões com representação em SQL Server](customizing-permissions-with-impersonation-in-sql-server.md).  
  
- Assine procedimentos armazenados com certificados, concedendo permissão somente para executar os procedimentos. Para obter mais informações, consulte [assinando procedimentos armazenados em SQL Server](signing-stored-procedures-in-sql-server.md).  
  
## <a name="external-resources"></a>Recursos externos  

 Para obter mais informações, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Funções de aplicativo](/sql/relational-databases/security/authentication-access/application-roles)|Descreve como criar e usar funções de aplicativo no SQL Server 2008.|  
  
## <a name="see-also"></a>Consulte também

- [Protegendo aplicativos ADO.NET](../securing-ado-net-applications.md)
- [Visão geral de segurança do SQL Server](overview-of-sql-server-security.md)
- [Cenários de Segurança de Aplicativo no SQL Server](application-security-scenarios-in-sql-server.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
