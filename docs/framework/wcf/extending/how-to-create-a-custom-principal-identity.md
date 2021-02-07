---
description: 'Saiba mais sobre: como criar uma identidade de entidade personalizada'
title: 'Como: criar uma identidade principal personalizada'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- IPrincipal
- IAuthorizationPolicy
- PrincipalPermissionMode
- PrincipalPermissionAttribute
ms.assetid: c4845fca-0ed9-4adf-bbdc-10812be69b61
ms.openlocfilehash: 0967257021ba6cdb68426dfa48f9078afe1256fd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99743675"
---
# <a name="how-to-create-a-custom-principal-identity"></a>Como: criar uma identidade principal personalizada

O <xref:System.Security.Permissions.PrincipalPermissionAttribute> é um meio declarativo de controlar o acesso aos métodos de serviço. Ao usar esse atributo, a <xref:System.ServiceModel.Description.PrincipalPermissionMode> enumeração Especifica o modo para executar verificações de autorização. Quando esse modo é definido como <xref:System.ServiceModel.Description.PrincipalPermissionMode.Custom> , ele permite que o usuário especifique uma <xref:System.Security.Principal.IPrincipal> classe personalizada retornada pela <xref:System.Threading.Thread.CurrentPrincipal%2A> propriedade. Este tópico ilustra o cenário quando o <xref:System.ServiceModel.Description.PrincipalPermissionMode.Custom> é usado em combinação com uma política de autorização personalizada e uma entidade personalizada.  
  
 Para obter mais informações sobre como usar o <xref:System.Security.Permissions.PrincipalPermissionAttribute> , consulte [como: restringir o acesso com a classe PrincipalPermissionAttribute](../how-to-restrict-access-with-the-principalpermissionattribute-class.md).  
  
## <a name="example"></a>Exemplo  

 [!code-csharp[PrincipalPermissionMode#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/principalpermissionmode/cs/source.cs#8)]
 [!code-vb[PrincipalPermissionMode#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/principalpermissionmode/vb/source.vb#8)]  
  
## <a name="compiling-the-code"></a>Compilando o código  

 As referências aos seguintes namespaces são necessárias para compilar o código:  
  
- <xref:System>  
  
- <xref:System.Collections.Generic>  
  
- <xref:System.Security.Permissions>  
  
- <xref:System.Security.Principal>  
  
- <xref:System.Threading>  
  
- <xref:System.ServiceModel>  
  
- <xref:System.ServiceModel.Channels>  
  
- <xref:System.ServiceModel.Description>  
  
- <xref:System.IdentityModel.Claims>  
  
- <xref:System.IdentityModel.Policy>  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Description.PrincipalPermissionMode>
- <xref:System.Security.Permissions.PrincipalPermissionAttribute>
- [Como: usar o provedor de função do ASP.NET com um serviço](../feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)
- [Como: restringir o acesso com a classe PrincipalPermissionAttribute](../how-to-restrict-access-with-the-principalpermissionattribute-class.md)
