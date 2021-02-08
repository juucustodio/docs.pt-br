---
description: 'Saiba mais sobre: PeerSecuritySettings'
title: PeerSecuritySettings
ms.date: 03/30/2017
ms.assetid: 24ae0d35-f3a3-419b-afd6-686e22aae27b
ms.openlocfilehash: a8b5b8c88e71cb46110fa35186599c0f9c366d17
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803003"
---
# <a name="peersecuritysettings"></a>PeerSecuritySettings

PeerSecuritySettings  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class PeerSecuritySettings  
{  
  string Mode;  
  PeerTransportSecuritySettings Transport;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe PeerSecuritySettings não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe PeerSecuritySettings tem as seguintes propriedades:  
  
### <a name="mode"></a>Modo  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Se a segurança em nível de transporte e nível de mensagem são usadas por um ponto de extremidade configurado com a associação.  
  
### <a name="transport"></a>Transport  

 Tipo de dados: PeerTransportSecuritySettings  
  
 Tipo de acesso: Somente leitura  
  
 Configurações de segurança de transporte.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.PeerSecuritySettings>
