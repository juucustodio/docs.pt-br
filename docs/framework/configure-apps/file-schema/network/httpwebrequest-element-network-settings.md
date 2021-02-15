---
title: Elemento <httpWebRequest> (Configurações de Rede)
description: O <httpWebRequest> elemento de configurações de rede personaliza os parâmetros de solicitação da Web no .NET Framework.
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/httpWebRequest
- http://schemas.microsoft.com/.NetConfiguration/v2.0#httpWebRequest
helpviewer_keywords:
- <httpWebRequest> element
- httpWebRequest element
ms.assetid: 52acd9d2-5bdc-4dc4-9c2a-f0a476ccbb31
ms.openlocfilehash: 86960a33d0924013e2bfbfa743eab372181033b5
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91195422"
---
# <a name="httpwebrequest-element-network-settings"></a>Elemento \<httpWebRequest> (Configurações de Rede)

Personaliza os parâmetros de solicitação da Web.  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<settings>**](settings-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<httpWebRequest>**

## <a name="syntax"></a>Sintaxe  
  
```xml  
<httpWebRequest  
  maximumResponseHeadersLength="size"  
  maximumErrorResponseLength="size"  
  maximumUnauthorizedUploadLength="size"  
  useUnsafeHeaderParsing="true|false"  
/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|**Atributo**|**Descrição**|  
|-------------------|---------------------|  
|`maximumResponseHeadersLength`|Especifica o comprimento máximo de um cabeçalho de resposta, em kilobytes. O padrão é 64. Um valor de-1 indica que nenhum limite de tamanho será imposto nos cabeçalhos de resposta.|  
|`maximumErrorResponseLength`|Especifica o comprimento máximo de uma resposta de erro, em quilobytes. O padrão é 64. Um valor de-1 indica que nenhum limite de tamanho será imposto sobre a resposta de erro.|  
|`maximumUnauthorizedUploadLength`|Especifica o comprimento máximo de um carregamento em resposta a um código de erro não autorizado, em bytes. O padrão é -1. Um valor de-1 indica que nenhum limite de tamanho será imposto no carregamento.|  
|`useUnsafeHeaderParsing`|Especifica se a análise de cabeçalho não seguro está habilitada. O valor padrão é `false`.|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|**Element**|**Descrição**|  
|-----------------|---------------------|  
|[configurações](settings-element-network-settings.md)|Configura as opções de rede básicaspara o namespace <xref:System.Net>.|  
  
## <a name="remarks"></a>Comentários  

 Por padrão, o .NET Framework impõe estritamente a RFC 2616 para análise de URI. Algumas respostas do servidor podem incluir caracteres de controle em campos proibidos, o que fará com que o <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType> método gere um <xref:System.Net.WebException> . Se **UseUnsafeHeaderParsing** for definido como **true**, <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType> o não será lançado nesse caso; no entanto, seu aplicativo ficará vulnerável a várias formas de ataques de análise de URI. A melhor solução é alterar o servidor para que a resposta não inclua caracteres de controle.  
  
## <a name="configuration-files"></a>Arquivos de Configuração  

 Esse elemento pode ser usado no arquivo de configuração do aplicativo ou no arquivo de configuração do computador (Machine.config).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como especificar um comprimento de cabeçalho máximo de tamanho maior que normal.  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <httpWebRequest  
        maximumResponseHeadersLength="128"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Veja também

- <xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A>
- [Esquema de configurações de rede](index.md)
