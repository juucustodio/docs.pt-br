---
description: 'Saiba mais sobre: <remove> elemento para schemeSettings (configurações de URI)'
title: Elemento <remove> para schemeSettings (Configurações de URI)
ms.date: 03/30/2017
ms.assetid: 4095ba51-de20-4f87-b562-018abe422c91
ms.openlocfilehash: 125a347cfcbb1393ea70032b7e1b198a1a5a4ed0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99713020"
---
# <a name="remove-element-for-schemesettings-uri-settings"></a>Elemento \<remove> para schemeSettings (Configurações de URI)

Remove uma configuração de esquema para um nome de esquema.  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<uri>**](uri-element-uri-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<schemeSettings>**](schemesettings-element-uri-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<remove>**

## <a name="syntax"></a>Syntax  
  
```xml  
<remove
  name="http|https"
/>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|name|O nome do esquema ao qual essa configuração se aplica. Os únicos valores com suporte são Name = "http" e Name = "https".|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<schemeSettings> Elemento (configurações de URI)](schemesettings-element-uri-settings.md)|Especifica como um <xref:System.Uri> será analisado quanto a esquemas específicos.|  
  
## <a name="remarks"></a>Comentários  

 Por padrão, a <xref:System.Uri?displayProperty=nameWithType> classe não escapa os delimitadores de caminho codificados por porcentagem antes de executar a compactação de caminho. Isso foi implementado como um mecanismo de segurança contra ataques como o seguinte:  
  
 `http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 Se esse URI for passado para os módulos que não manipulam a porcentagem de caracteres codificados corretamente, isso pode fazer com que o seguinte comando seja executado pelo servidor:  
  
 `c:\Windows\System32\cmd.exe /c dir c:\`  
  
 Por esse motivo, a <xref:System.Uri?displayProperty=nameWithType> classe não escapa primeiro os delimitadores de caminho e, em seguida, aplica a compactação de caminho. O resultado da passagem da URL mal-intencionada acima para o <xref:System.Uri?displayProperty=nameWithType> Construtor de classe resulta no seguinte URI:  
  
 `http://www.microsoft.com/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 Esse comportamento padrão pode ser modificado para não cancelar o escape de delimitadores de caminho codificados por porcentagem usando a opção de configuração schemeSettings para um esquema específico.  
  
## <a name="configuration-files"></a>Arquivos de Configuração  

 Esse elemento pode ser usado no arquivo de configuração do aplicativo ou no arquivo de configuração do computador (Machine.config).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra uma configuração usada pela <xref:System.Uri> classe que remove as configurações de esquema para o esquema http.  
  
```xml  
<configuration>  
  <uri>  
    <schemeSettings>  
      <remove name="http"/>  
    </schemeSettings>  
  </uri>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Configuration.SchemeSettingElement?displayProperty=nameWithType>
- <xref:System.Configuration.SchemeSettingElementCollection?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection.SchemeSettings%2A?displayProperty=nameWithType>
- <xref:System.GenericUriParserOptions?displayProperty=nameWithType>
- <xref:System.Uri?displayProperty=nameWithType>
- [Esquema de configurações de rede](index.md)
