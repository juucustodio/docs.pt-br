---
description: 'Saiba mais sobre: <claimTypeRequirements> elemento'
title: Elemento <claimTypeRequirements>
ms.date: 03/30/2017
ms.assetid: a26efe73-4bad-4731-8cad-27f00d54354b
ms.openlocfilehash: 9553c129c246a5f4980d597406bee19ea949bdcc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638906"
---
# <a name="claimtyperequirements-element"></a>Elemento \<claimTypeRequirements>

Especifica uma coleção de tipos de declaração necessários.  
  
 Em um cenário federado, os serviços atendem aos requisitos de credenciais de entrada. Por exemplo, as credenciais de entrada devem ter um determinado conjunto de tipos de declaração. Cada elemento filho nessa coleção especifica os tipos de declarações obrigatórias e opcionais que devem aparecer em uma credencial federada.  
  
 Um requisito de tipo de declaração consiste no URI do tipo de declaração solicitado no token emitido junto com um parâmetro booliano que indica se esse tipo de declaração é necessário no token emitido ou é opcional.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters.ClaimTypeRequirements%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement.ClaimTypeRequirements%2A>
- <xref:System.ServiceModel.Configuration.ClaimTypeElementCollection>
- <xref:System.ServiceModel.Configuration.ClaimTypeElement>
- <xref:System.ServiceModel.Configuration.SecurityElementBase.IssuedTokenParameters%2A>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [Identidade e autenticação de serviço](../../../wcf/feature-details/service-identity-and-authentication.md)
- [Federação e tokens emitidos](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [Recursos de segurança com associações personalizadas](../../../wcf/feature-details/security-capabilities-with-custom-bindings.md)
- [Federação e tokens emitidos](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [\<add>](add-of-claimtyperequirements.md)
- [Associações](../../../wcf/bindings.md)
- [Estendendo associações](../../../wcf/extending/extending-bindings.md)
- [Associações personalizadas](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [Como: criar uma associação personalizada utilizando o SecurityBindingElement](../../../wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [Segurança de associação personalizada](../../../wcf/samples/custom-binding-security.md)
