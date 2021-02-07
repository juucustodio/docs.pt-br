---
description: 'Saiba mais sobre: SymmetricSecurityBindingElement'
title: SymmetricSecurityBindingElement
ms.date: 03/30/2017
ms.assetid: b2e182b6-c041-4d80-a926-6058068d9f79
ms.openlocfilehash: c158f0bedec91a74b305f359889dd307cff48079
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99715295"
---
# <a name="symmetricsecuritybindingelement"></a>SymmetricSecurityBindingElement

SymmetricSecurityBindingElement  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class SymmetricSecurityBindingElement : SecurityBindingElement  
{  
  string MessageProtectionOrder;  
  boolean RequireSignatureConfirmation;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe SymmetricSecurityBindingElement não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe SymmetricSecurityBindingElement tem as seguintes propriedades:  
  
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

- <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>
