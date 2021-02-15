---
description: 'Saiba mais sobre: ServiceMetadataBehavior'
title: ServiceMetadataBehavior
ms.date: 03/30/2017
ms.assetid: 0f194476-72f1-467e-bdce-674306316e64
ms.openlocfilehash: 1b1438013ec667b10b300d898687abf6f33f96fb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99715477"
---
# <a name="servicemetadatabehavior"></a>ServiceMetadataBehavior

ServiceMetadataBehavior  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ServiceMetadataBehavior : Behavior  
{  
  string ExternalMetadataLocation;  
  boolean HttpGetEnabled;  
  string HttpGetUrl;  
  boolean HttpsGetEnabled;  
  string HttpsGetUrl;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe ServiceMetadataBehavior não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe ServiceMetadataBehavior tem as seguintes propriedades:  
  
### <a name="externalmetadatalocation"></a>ExternalMetadataLocation  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Define o local para o qual o serviço redireciona solicitações de metadados.  
  
### <a name="httpgetenabled"></a>HttpGetEnabled  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Controla se o serviço publica seu WSDL no endereço controlado pelo `HttpGetUrl` atributo.  
  
### <a name="httpgeturl"></a>HttpGetUrl  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Define o local no qual o serviço WSDL é publicado para recuperação usando HTTP.  
  
### <a name="httpsgetenabled"></a>HttpsGetEnabled  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Controla se o serviço publica seu WSDL sobre HTTPS no endereço controlado pelo `HttpsGetUrl` atributo.  
  
### <a name="httpsgeturl"></a>HttpsGetUrl  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Define o local no qual o serviço WSDL é publicado para recuperação usando HTTPS.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Description.ServiceMetadataBehavior>
