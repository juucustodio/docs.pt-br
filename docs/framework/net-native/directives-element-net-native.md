---
description: 'Saiba mais sobre: <Directives> elemento (.net Native)'
title: <Directives> (.NET Nativo)
ms.date: 03/30/2017
ms.assetid: 444846f3-48d5-4341-a43e-69f7221389eb
ms.openlocfilehash: 7aa3bf3718f32d55ba8189c65705868c6fb399ae
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99662904"
---
# <a name="directives-element-net-native"></a>\<Directives> (.NET Nativo)

O elemento raiz em cada arquivo de diretivas de tempo de execução para .NET Native.  
  
 `<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">`
  
## <a name="syntax"></a>Syntax  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <!-- child elements -->
</Directives>  
```  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`xmlns`|O namespace XML. Seu valor é sempre `http://schemas.microsoft.com/netfx/2013/01/metadata` .|  
  
## <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<Application>](application-element-net-native.md)|Serve como um contêiner para os tipos amplos de aplicativos cujos metadados estão disponíveis para reflexão.|  
|[\<Library>](library-element-net-native.md)|Define o assembly cujos tipos de filho e membros de tipo necessitam de metadados no tempo de execução.|  
  
## <a name="remarks"></a>Comentários  

 Cada arquivo de diretivas de runtime pode conter somente um elemento `<Directives>`.  
  
 O `<Directives>` elemento pode conter zero ou um [\<Application>](application-element-net-native.md) elemento e zero, um ou mais [\<Library>](library-element-net-native.md) elementos.  
  
## <a name="see-also"></a>Consulte também

- [Referência do arquivo de configuração de diretivas do runtime (rd.xml)](runtime-directives-rd-xml-configuration-file-reference.md)
- [Elementos da diretiva de runtime](runtime-directive-elements.md)
