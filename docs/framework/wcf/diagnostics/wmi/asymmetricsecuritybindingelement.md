---
description: 'Saiba mais sobre: AsymmetricSecurityBindingElement'
title: AsymmetricSecurityBindingElement
ms.date: 03/30/2017
ms.assetid: 7bd3b6be-8f77-4927-93ae-6fa371893cca
ms.openlocfilehash: 25d0ac205491e9ce27c59d3a0670d1e4a3150e21
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99757937"
---
# <a name="asymmetricsecuritybindingelement"></a>AsymmetricSecurityBindingElement

AsymmetricSecurityBindingElement  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class AsymmetricSecurityBindingElement : SecurityBindingElement  
{  
  string MessageProtectionOrder;  
  boolean RequireSignatureConfirmation;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe AsymmetricSecurityBindingElement não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe AsymmetricSecurityBindingElement tem as seguintes propriedades:  
  
### <a name="messageprotectionorder"></a>MessageProtectionOrder  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 A ordem de criptografia e assinatura de mensagem para esta associação.  
  
### <a name="requiresignatureconfirmation"></a>RequireSignatureConfirmation  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Se a associação requer confirmação de assinatura.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>
