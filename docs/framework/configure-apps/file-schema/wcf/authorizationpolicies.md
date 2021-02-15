---
description: 'Saiba mais sobre: <authorizationPolicies>'
title: <authorizationPolicies>
ms.date: 03/30/2017
ms.assetid: 5b367489-54d7-408b-8f56-cb157dd68eaf
ms.openlocfilehash: 4b0f341a1bb6ebb4918a5d71aba82270c31ba863
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99749825"
---
# \<authorizationPolicies>

Esta seção de configuração contém uma coleção de tipos de política de autorização, que podem ser adicionados usando a `add` palavra-chave. Cada política de autorização contém um único `policyType` atributo necessário que é uma cadeia de caracteres. O atributo especifica uma política de autorização, que permite a transformação de um conjunto de declarações de entrada em outro conjunto de declarações. Controle de acesso pode ser concedido ou negado com base nisso. Para obter mais informações sobre como funciona uma diretiva de autorização, consulte <xref:System.IdentityModel.Policy.IAuthorizationPolicy> e [política de autorização](../../../wcf/samples/authorization-policy.md).  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Configuration.ServiceAuthorizationElement>
- <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ExternalAuthorizationPolicies%2A>
- <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>
- <xref:System.ServiceModel.Configuration.AuthorizationPolicyTypeElement>
- <xref:System.ServiceModel.Configuration.ServiceAuthorizationElement.AuthorizationPolicies%2A>
- <xref:System.ServiceModel.Configuration.AuthorizationPolicyTypeElementCollection>
- <xref:System.IdentityModel.Policy.IAuthorizationPolicy>
- [Autorizando o acesso às operações de serviço](../../../wcf/samples/authorizing-access-to-service-operations.md)
- [Como: criar gerenciador de autorização personalizado para um serviço](../../../wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md)
- [\<add>](add-of-authorizationpolicies.md)
- [Política de autorização](../../../wcf/samples/authorization-policy.md)
