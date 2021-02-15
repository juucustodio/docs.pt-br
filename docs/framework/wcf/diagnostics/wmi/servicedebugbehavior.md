---
description: 'Saiba mais sobre: ServiceDebugBehavior'
title: ServiceDebugBehavior
ms.date: 03/30/2017
ms.assetid: a5ec9061-1e95-43fb-b0d9-dbd0a7bc3c44
ms.openlocfilehash: 3b384c209524267c72a12d96bc845b694144ba19
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99715529"
---
# <a name="servicedebugbehavior"></a>ServiceDebugBehavior

ServiceDebugBehavior  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ServiceDebugBehavior : Behavior  
{  
  boolean HttpHelpPageEnabled;  
  string HttpHelpPageUrl;  
  boolean HttpsHelpPageEnabled;  
  string HttpsHelpPageUrl;  
  boolean IncludeExceptionDetailInFaults;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe ServiceDebugBehavior não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe ServiceDebugBehavior tem as seguintes propriedades:  
  
### <a name="httphelppageenabled"></a>HttpHelpPageEnabled  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Controla se o serviço publica seu WSDL no endereço controlado pelo `HttpGetUrl` atributo.  
  
### <a name="httphelppageurl"></a>HttpHelpPageUrl  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Define o local no qual o serviço WSDL é publicado para recuperação usando HTTP.  
  
### <a name="httpshelppageenabled"></a>HttpsHelpPageEnabled  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Controla se o serviço publica seu WSDL sobre HTTPS no endereço controlado pelo `HttpsGetUrl` atributo.  
  
### <a name="httpshelppageurl"></a>HttpsHelpPageUrl  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Define o local no qual o serviço WSDL é publicado para recuperação usando HTTPS.  
  
### <a name="includeexceptiondetailinfaults"></a>IncludeExceptionDetailInFaults  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Especifica se as informações de exceção gerenciadas devem ser incluídas nos detalhes de falhas de SOAP retornadas aos clientes para fins de depuração.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Description.ServiceDebugBehavior>
