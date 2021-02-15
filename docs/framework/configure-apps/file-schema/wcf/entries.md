---
description: 'Saiba mais sobre: <entries>'
title: <entries>
ms.date: 03/30/2017
ms.assetid: 202e430c-c1b9-4343-abe2-ac78c181a3b7
ms.openlocfilehash: e5aefce4328c341b6d132765c8e726910241aae1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99782098"
---
# \<entries>

Uma entrada de roteamento que contém mapeamentos entre os filtros de roteamento e os pontos de extremidade de destino para envio de mensagens quando o filtro é correspondente.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<routing>**](routing.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<filterTables>**](filtertables.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<filterTable>**](filtertable.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<entries>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<routing>
  <filterTables>
    <filterTable name="String">
      <entries>
        <add backupList="String"
             endpointName="String"
             filterName="String"
             priority="Integer" />
      </entries>
    </filterTable>
  </filterTables>
</routing>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  

 Nenhum.  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<filters>](filters-of-routing.md)|Mapeia um filtro para um ponto de extremidade do cliente que foi definido anteriormente. As mensagens correspondentes a este filtro serão enviadas para esse destino.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<routing>](routing.md)|Uma seção de configuração que contém uma tabela de roteamento.|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Routing.Configuration.RoutingSection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Routing.Configuration.FilterTableEntryElement?displayProperty=nameWithType>
