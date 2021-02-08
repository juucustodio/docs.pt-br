---
description: 'Saiba mais sobre: <etwEnable> elemento'
title: Elemento <etwEnable>
ms.date: 03/30/2017
helpviewer_keywords:
- etwEnable element
- <etwEnable> element
ms.assetid: 29dde982-6d8b-4099-8867-ad0d7733f6dc
ms.openlocfilehash: 224784f47d15788ded41a5756e1d179a5a25907b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787039"
---
# <a name="etwenable-element"></a>Elemento \<etwEnable>

Especifica se deseja-se habilitar o rastreamento de eventos para Windows (ETW) para eventos de Common Language Runtime.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<etwEnabled>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<etwEnable enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|Habilitado|Atributo obrigatório.<br /><br /> Especifica se o ETW deve ser habilitado.|  
  
## <a name="enabled-attribute"></a>Atributo habilitado  
  
|Valor|Descrição|  
|-----------|-----------------|  
|true|Habilite o ETW. Esse é o padrão para versões do Windows começando com os sistemas operacionais Windows Vista e Windows Server 2008.|  
|false|Desabilite o ETW. Esse é o padrão para versões anteriores do Windows.|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`configuration`|O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework.|  
|`runtime`|Contém informações sobre associação do assembly e coleta de lixo.|  
  
## <a name="remarks"></a>Comentários  

 A partir do Windows Vista, o ETW é habilitado por padrão. Use este elemento para desabilitar o ETW para um aplicativo. Em versões anteriores do Windows, use esse elemento para habilitar o ETW para um aplicativo.  
  
> [!NOTE]
> O ETW pode ser habilitado ou desabilitado globalmente em um servidor usando uma configuração de registro. Consulte [controlando o log de .NET Framework](../../../performance/controlling-logging.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como habilitar o rastreamento ETW para um aplicativo.  
  
```xml  
<configuration>  
   <runtime>  
      <etwEnable enabled="true" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também

- [Esquema de configurações do runtime](index.md)
- [Esquema do arquivo de configuração](../index.md)
- [Controlando o registro em log no .NET Framework](../../../performance/controlling-logging.md)
