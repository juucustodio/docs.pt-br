---
description: 'Saiba mais sobre: como examinar o contexto de segurança'
title: 'Como: examinar o contexto de segurança'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ServiceSecurityContext class
- WCF, security
- Claimset class
ms.assetid: 389b5a57-4175-4bc0-ada0-fc750d51149f
ms.openlocfilehash: e82491a877cf1f741767c91d1e7c304ba7676e6c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99779394"
---
# <a name="how-to-examine-the-security-context"></a>Como: examinar o contexto de segurança

Ao programar serviços Windows Communication Foundation (WCF), o contexto de segurança do serviço permite que você determine detalhes sobre as credenciais do cliente e as declarações usadas para autenticar com o serviço. Isso é feito usando as propriedades da <xref:System.ServiceModel.ServiceSecurityContext> classe.  
  
 Por exemplo, você pode recuperar a identidade do cliente atual usando a <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> propriedade ou. Para determinar se o cliente é anônimo, use a <xref:System.ServiceModel.ServiceSecurityContext.IsAnonymous%2A> propriedade.  
  
 Você também pode determinar quais declarações estão sendo feitas em nome do cliente Iterando pela coleção de declarações na <xref:System.ServiceModel.ServiceSecurityContext.AuthorizationContext%2A> propriedade.  
  
### <a name="to-get-the-current-security-context"></a>Para obter o contexto de segurança atual  
  
- Acesse a propriedade estática <xref:System.ServiceModel.ServiceSecurityContext.Current%2A> para obter o contexto de segurança atual. Examine qualquer uma das propriedades do contexto atual da referência.  
  
### <a name="to-determine-the-identity-of-the-caller"></a>Para determinar a identidade do chamador  
  
1. Imprima o valor das <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> Propriedades e <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> .  
  
### <a name="to-parse-the-claims-of-a-caller"></a>Para analisar as declarações de um chamador  
  
1. Retornar a <xref:System.IdentityModel.Policy.AuthorizationContext> classe atual. Use a <xref:System.ServiceModel.ServiceSecurityContext.Current%2A> propriedade para retornar o contexto de segurança do serviço atual e, em seguida, retorne o `AuthorizationContext` usando a <xref:System.ServiceModel.ServiceSecurityContext.AuthorizationContext%2A> propriedade.  
  
2. Analise a coleção de <xref:System.IdentityModel.Claims.ClaimSet> objetos retornados pela <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A> propriedade da <xref:System.IdentityModel.Policy.AuthorizationContext> classe.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir imprime os valores <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> das <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> Propriedades e do contexto de segurança atual e a <xref:System.IdentityModel.Claims.Claim.ClaimType%2A> propriedade, o valor do recurso da declaração e a <xref:System.IdentityModel.Claims.Claim.Right%2A> propriedade de cada declaração no contexto de segurança atual.  
  
 [!code-csharp[c_PrincipalPermissionAttribute#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_principalpermissionattribute/cs/source.cs#4)]
 [!code-vb[c_PrincipalPermissionAttribute#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_principalpermissionattribute/vb/source.vb#4)]  
  
## <a name="compiling-the-code"></a>Compilando o código  

 O código usa os seguintes namespaces:  
  
- <xref:System>  
  
- <xref:System.ServiceModel>  
  
- <xref:System.IdentityModel.Policy>  
  
- <xref:System.IdentityModel.Claims>  
  
## <a name="see-also"></a>Consulte também

- [Serviços de segurança](securing-services.md)
- [Identidade e autenticação de serviço](./feature-details/service-identity-and-authentication.md)
