---
description: 'Saiba mais sobre: <authenticationModules> elemento (configurações de rede)'
title: Elemento <authenticationModules> (Configurações de Rede)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#authenticationModules
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/authenticationModules
helpviewer_keywords:
- authenticationModules element
- <authenticationModules> element
ms.assetid: 10fcfaad-82ef-4692-871a-0aec9dfbe75e
ms.openlocfilehash: 2c2dc3c6a3d8fc064bb24c3d86a4441c269e43f0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99698603"
---
# <a name="authenticationmodules-element-network-settings"></a>Elemento \<authenticationModules> (Configurações de Rede)

Especifica os módulos usados para autenticar solicitações de rede.  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<authenticationModules>**

## <a name="syntax"></a>Syntax  
  
```xml  
<authenticationModules>
</authenticationModules>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  

 Nenhum.  
  
### <a name="child-elements"></a>Elementos filho  
  
|**Element**|**Descrição**|  
|-----------------|---------------------|  
|[add](add-element-for-authenticationmodules-network-settings.md)|Adiciona um módulo de autenticação ao aplicativo.|  
|[clear](clear-element-for-authenticationmodules-network-settings.md)|Limpa todos os módulos de autenticação do aplicativo.|  
|[remove](remove-element-for-authenticationmodules-network-settings.md)|Remove um módulo de autenticação do aplicativo.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|**Element**|**Descrição**|  
|-----------------|---------------------|  
|[system.net](system-net-element-network-settings.md)|Contém configurações que especificam como o .NET Framework se conecta à rede.|  
  
## <a name="remarks"></a>Comentários  

 O `authenticationModule` elemento Especifica os módulos de autenticação que conduzem o processo de autenticação com um servidor. Um módulo de autenticação deve implementar a <xref:System.Net.IAuthenticationModule> interface.  
  
## <a name="configuration-files"></a>Arquivos de Configuração  

 Esse elemento pode ser usado no arquivo de configuração do aplicativo ou no arquivo de configuração do computador (Machine.config).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir habilita um módulo de autenticação. Você deve substituir os valores de Version e PublicKeyToken pelos valores corretos para o módulo especificado.  
  
```xml  
<configuration>  
  <system.net>  
    <authenticationModules>  
      <add type="System.Net.DigestClient, System, Version=2.0.3600.0,  
                 Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
    </authenticationModules>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Net.IAuthenticationModule>
- <xref:System.Net.AuthenticationManager>
- [Esquema de configurações de rede](index.md)
