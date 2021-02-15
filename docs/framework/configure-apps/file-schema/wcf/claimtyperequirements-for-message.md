---
description: 'Saiba mais sobre: <claimTypeRequirements> para <message>'
title: <claimTypeRequirements> para <message>
ms.date: 03/30/2017
ms.assetid: f95c5ecd-abb6-4b77-a6d7-a38727f4a142
ms.openlocfilehash: a393a075c64f4a46e5ac055b3c417514861c9661
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638893"
---
# <a name="claimtyperequirements-for-message"></a>\<claimTypeRequirements> para \<message>

Especifica uma coleção de tipos de declaração necessários.  
  
 A coleção é usada pelo serviço para especificar quaisquer declarações obrigatórias e opcionais que devem estar no token emitido que o cliente usa para acessar o serviço. O serviço expõe os tipos de declaração necessários nos metadados se a publicação WSDL estiver habilitada, mas o WCF não exigir que o token emitido contenha os tipos de declaração especificados. Os serviços que desejam impor os tipos de declaração necessários estão presentes devem usar a política de autorização.  
  
 Em clientes federados, essa coleção contém a lista de declarações obrigatórias e opcionais que são enviadas para o serviço de token de segurança na solicitação do cliente para um token emitido.  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.ClaimTypeRequirements%2A>
- <xref:System.ServiceModel.Security.Tokens.ClaimTypeRequirement>
- <xref:System.ServiceModel.Configuration.FederatedMessageSecurityOverHttpElement.ClaimTypeRequirements%2A>
- <xref:System.ServiceModel.Configuration.ClaimTypeElementCollection>
- <xref:System.ServiceModel.Configuration.ClaimTypeElement>
