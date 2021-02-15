---
description: 'Saiba mais sobre: ServiceToEndpointAssociation'
title: ServiceToEndpointAssociation
ms.date: 03/30/2017
ms.assetid: 03c3cd15-e1b2-4dc2-bdc2-59fdccdae110
ms.openlocfilehash: 1ae2ce2bcc0b3494b00fffa750f3ca46d26fe08f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99715334"
---
# <a name="servicetoendpointassociation"></a>ServiceToEndpointAssociation

Mapeia um serviço para um ponto de extremidade.  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ServiceToEndpointAssociation  
{  
  Service ref;  
  Endpoint ref;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe ServiceToEndpointAssociation não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe ServiceToEndpointAssociation tem as seguintes propriedades:  
  
### <a name="ref"></a>ref  

 Tipo de dados: serviço  
  
 Tipo de acesso: Somente leitura  
Qualificadores: Chave  
  
 O serviço associado ao ponto de extremidade.  
  
### <a name="ref"></a>ref  

 Tipo de dados: ponto de extremidade  
  
 Tipo de acesso: Somente leitura  
Qualificadores: Chave  
  
 O ponto de extremidade associado ao serviço.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|
