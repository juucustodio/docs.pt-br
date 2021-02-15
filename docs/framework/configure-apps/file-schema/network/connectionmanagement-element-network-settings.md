---
title: Elemento <connectionManagement> (Configurações de Rede)
description: O <connectionManagement> elemento de configurações de rede especifica o número máximo de conexões a um host de rede no .NET Framework.
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/connectionManagement
- http://schemas.microsoft.com/.NetConfiguration/v2.0#connectionManagement
helpviewer_keywords:
- <connectionManagement> element
- connectionManagement element
ms.assetid: bedccaab-12a2-4511-8f67-e961f249aec6
ms.openlocfilehash: 52b780c739a00cb53694b547ee1a33c1b5d98c86
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91167308"
---
# <a name="connectionmanagement-element-network-settings"></a>Elemento \<connectionManagement> (Configurações de Rede)

Especifica o número máximo de conexões com um host de rede.  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<connectionManagement>**

## <a name="syntax"></a>Sintaxe  
  
```xml  
<connectionManagement>
</connectionManagement>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  

 Nenhum.  
  
### <a name="child-elements"></a>Elementos filho  
  
|**Element**|**Descrição**|  
|-----------------|---------------------|  
|[add](add-element-for-connectionmanagement-network-settings.md)|Adiciona um endereço IP ou nome DNS à lista de gerenciamento de conexão.|  
|[clear](clear-element-for-connectionmanagement-network-settings.md)|Limpa a lista de gerenciamento de conexão.|  
|[remove](remove-element-for-connectionmanagement-network-settings.md)|Remove um endereço IP ou nome DNS da lista de gerenciamento de conexão.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|**Element**|**Descrição**|  
|-----------------|---------------------|  
|[system.net](system-net-element-network-settings.md)|Contém configurações que especificam como o .NET Framework se conecta à rede.|  
  
## <a name="remarks"></a>Comentários  

 O `connectionManagement` elemento define o número máximo de conexões com um servidor ou grupo de servidores.  
  
## <a name="configuration-files"></a>Arquivos de Configuração  

 Esse elemento pode ser usado no arquivo de configuração do aplicativo ou no arquivo de configuração do computador (Machine.config).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir configura um aplicativo para usar quatro conexões com o servidor `www.contoso.com` e duas conexões com todos os outros servidores.  
  
```xml  
<configuration>  
  <system.net>  
    <connectionManagement>  
      <add address = "http://www.contoso.com" maxconnection = "4" />  
      <add address = "*" maxconnection = "2" />  
    </connectionManagement>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Confira também

- <xref:System.Net.ServicePoint>
- <xref:System.Net.ServicePointManager>
- [Esquema de configurações de rede](index.md)
