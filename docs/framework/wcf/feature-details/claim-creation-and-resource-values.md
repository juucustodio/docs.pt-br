---
description: 'Saiba mais sobre: criação de declaração e valores de recurso'
title: Valores de recursos e criação de declarações
ms.date: 03/30/2017
helpviewer_keywords:
- claims [WCF], creation and resource values
ms.assetid: 30431f76-cbe7-4bad-bad7-8e43e23a82d4
ms.openlocfilehash: 20763c683c5bf5734a21a4315576a8f9f354ff35
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99734978"
---
# <a name="claim-creation-and-resource-values"></a>Valores de recursos e criação de declarações

A <xref:System.IdentityModel.Claims.Claim> classe fornece vários métodos para criar instâncias de tipos de declarações internas. Desses métodos, o seguinte não executa nenhuma verificação semântica ou de formato no recurso fornecido:  
  
- <xref:System.IdentityModel.Claims.Claim.CreateDnsClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateHashClaim%2A> (não verifica o comprimento ou o conteúdo da matriz de bytes)  
  
- <xref:System.IdentityModel.Claims.Claim.CreateNameClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateSpnClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateThumbprintClaim%2A> (não verifica o comprimento ou o conteúdo da matriz de bytes)  
  
- <xref:System.IdentityModel.Claims.Claim.CreateUpnClaim%2A>  
  
 Deve-se ter cuidado ao chamar os métodos acima para garantir que os valores de recurso passados sejam do formato correto ou contenham o tipo correto de informação (ou ambos).  
  
 Os métodos a seguir usam tipos específicos:  
  
- <xref:System.IdentityModel.Claims.Claim.CreateDenyOnlyWindowsSidClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateMailAddressClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateRsaClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateUriClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateWindowsSidClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateX500DistinguishedNameClaim%2A>  
  
## <a name="see-also"></a>Consulte também

- <xref:System.IdentityModel.Claims.Claim>
- <xref:System.IdentityModel.Claims.ClaimSet>
- [Gerenciamento de declarações e autorizações com o modelo de identidade](managing-claims-and-authorization-with-the-identity-model.md)
