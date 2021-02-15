---
title: Erro de SYSLIB0002
description: Saiba mais sobre o obsoletion que gera erros de tempo de compilação SYSLIB0002.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 774675e96d11a8e1b5d82767695d0defd1e8cfad
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596434"
---
# <a name="syslib0002-principalpermissionattribute-is-obsolete"></a>SYSLIB0002: PrincipalPermissionattribute está obsoleto

O <xref:System.Security.Permissions.PrincipalPermissionAttribute> Construtor é obsoleto e produz erro de tempo de compilação `SYSLIB0002` , a partir do .NET 5,0. Não é possível instanciar esse atributo ou aplicá-lo a um método.

Ao contrário de outros avisos do obsoletion, não é possível suprimir o erro.

## <a name="workarounds"></a>Soluções Alternativas

- Se você estiver aplicando o atributo a um método de ação ASP.NET MVC:

  Considere o uso do ASP. A infraestrutura de autorização interna da rede. O código a seguir demonstra como anotar um controlador com um <xref:System.Web.Mvc.AuthorizeAttribute> atributo. O tempo de execução do ASP.NET autorizará o usuário antes de executar a ação.

  ```csharp
  using Microsoft.AspNetCore.Authorization;

  namespace MySampleApp
  {
      [Authorize(Roles = "Administrator")]
      public class AdministrationController : Controller
      {
          public ActionResult MyAction()
          {
              // This code won't run unless the current user
              // is in the 'Administrator' role.
          }
      }
  }
  ```

  Para obter mais informações, consulte [autorização baseada em função no ASP.NET Core](/aspnet/core/security/authorization/roles) e [introdução à autorização no ASP.NET Core](/aspnet/core/security/authorization/introduction).

- Se você estiver aplicando o atributo ao código de biblioteca fora do contexto de um aplicativo Web:

  Execute as verificações manualmente no início do método chamando o <xref:System.Security.Principal.IPrincipal.IsInRole(System.String)?displayProperty=nameWithType> método.

  ```csharp
  using System.Threading;

  void DoSomething()
  {
      if (Thread.CurrentPrincipal == null
          || !Thread.CurrentPrincipal.IsInRole("Administrators"))
      {
          throw new Exception("User is anonymous or isn't an admin.");
      }

      // Code that should run only when user is an administrator.
  }
  ```

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a>Confira também

- [PrincipalPermissionattribute está obsoleto como erro](../core-libraries/5.0/principalpermissionattribute-obsolete.md)
