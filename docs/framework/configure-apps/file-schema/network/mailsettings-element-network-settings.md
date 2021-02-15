---
title: Elemento <mailSettings> (Configurações de Rede)
description: O <mailSettings> elemento de configurações de rede configura as opções de envio de email no .NET Framework.
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#mailSettings
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings
helpviewer_keywords:
- mailSettings element
- <mailSettings> element
ms.assetid: 54f0f153-17e5-4f49-afdc-deadb940c9c1
ms.openlocfilehash: a146874acc21f52507b37b1751c648792e23c8bb
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91158845"
---
# <a name="mailsettings-element-network-settings"></a>Elemento \<mailSettings> (Configurações de Rede)

Configura as opções de envio de email.  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<mailSettings>**

## <a name="syntax"></a>Syntax  
  
```xml  
<mailSettings>
  <smtp>...</smtp>  
</mailSettings>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  

 Nenhum.  
  
### <a name="child-elements"></a>Elementos filho  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|[\<smtp> Elemento (configurações de rede)](smtp-element-network-settings.md)|Configura opções de protocolo de transporte de email simples.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|**Element**|**Descrição**|  
|-----------------|---------------------|  
|[\<system.Net> Elemento (configurações de rede)](system-net-element-network-settings.md)|Contém configurações que especificam como o .NET Framework se conecta à rede.|  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir especifica os parâmetros de SMTP apropriados para enviar email usando as credenciais de rede padrão.  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="Network">  
        <network  
          host="localhost"  
          port="25"  
          defaultCredentials="true"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Confira também

- <xref:System.Net.Mail.SmtpClient>
- [Esquema de configurações de rede](index.md)
