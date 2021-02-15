---
title: Elemento <xmlSerializer>
description: O <xmlSerializer> elemento especifica se uma verificação adicional de progresso do XmlSerializer é feita.
ms.date: 03/30/2017
helpviewer_keywords:
- <xmlSerializer> element
- XML serialization, configuration
- xmlSerializer element
ms.assetid: d129d10c-3eb7-45d9-8098-5fa853825e47
ms.openlocfilehash: 6f368880c97a21dc3e9593ecb2319d265a1b8932
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95676485"
---
# <a name="xmlserializer-element"></a>Elemento \<xmlSerializer>

Especifica se uma verificação adicional de progresso do <xref:System.Xml.Serialization.XmlSerializer> é feita.  
  
 \<configuration>  
\<system.xml.serialization>  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<xmlSerializer checkDeserializerAdvance = "true|false" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|**checkDeserializeAdvances**|Especifica se o progresso do <xref:System.Xml.Serialization.XmlSerializer> é verificado. Defina o atributo como "true" ou "false". O padrão é "true".|  
|**useLegacySerializationGeneration**|Especifica se o <xref:System.Xml.Serialization.XmlSerializer> usa a geração de serialização herdada que gera assemblies escrevendo código C# em um arquivo e, em seguida, compilando-o em um assembly. O padrão é **false**.|  
  
### <a name="child-elements"></a>Elementos filho  

 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|DESCRIÇÃO|  
|-------------|-----------------|  
|[\<system.xml.serialization> Elementos](system-xml-serialization-element.md)|Contém definições de configuração para as classes <xref:System.Xml.Serialization.XmlSerializer> e <xref:System.Xml.Serialization.XmlSchemaImporter>.|  
  
## <a name="remarks"></a>Comentários  

 Por padrão, o <xref:System.Xml.Serialization.XmlSerializer> fornece uma camada adicional de segurança contra potenciais ataques de negação de serviço ao desserializar dados não confiáveis. Ele faz isso tentando detectar loops infinitos durante a desserialização. Se uma condição desse tipo for detectada, uma exceção será gerada com a seguinte mensagem: “Erro interno: a desserialização não pôde avançar sobre o fluxo subjacente”.  
  
 Receber essa mensagem não necessariamente indica que um ataque de negação de serviço esteja em andamento. Em algumas circunstâncias raras, o mecanismo de detecção de loop infinito produz um falso positivo e a exceção é gerada para uma mensagem de entrada legítima. Se você achar que em seus aplicativos específicos mensagens legítimas estão sendo rejeitadas por essa camada extra de proteção, defina o atributo **checkDeserializeAdvances** como “false”.  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir define o atributo **checkDeserializeAdvances** como “false”.  
  
```xml  
<configuration>  
  <system.xml.serialization>  
    <xmlSerializer checkDeserializeAdvances="false" />  
  </system.xml.serialization>  
</configuration>  
```  
  
## <a name="see-also"></a>Confira também

- <xref:System.Xml.Serialization.XmlSerializer>
- [\<system.xml.serialization> Elementos](system-xml-serialization-element.md)
- [Serialização XML e SOAP](xml-and-soap-serialization.md)
