---
description: 'Saiba mais sobre: <add> de <entries>'
title: <add> de <entries>
ms.date: 03/30/2017
ms.assetid: 3af4805b-dc72-4f68-b168-da4fba8c6170
ms.openlocfilehash: 0be24fb9d2327d411368dd05afc21156dfaf3d3a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803965"
---
# <a name="add-of-entries"></a>\<add> de \<entries>

Representa uma entrada de roteamento que mapeia um filtro para um ponto de extremidade do cliente que foi definido anteriormente. As mensagens correspondentes a este filtro serão enviadas para esse destino.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<routing>**](routing.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<filterTables>**](filtertables.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<filterTable>**](filtertable.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<entries>**](entries.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  
  
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
  
|Atributo|Descrição|  
|---------------|-----------------|  
|backupList|Uma cadeia de caracteres que especifica uma referência a uma lista de pontos de extremidade de backup.|  
|endpoint|Uma cadeia de caracteres que especifica uma referência a um ponto de extremidade do cliente que receberá mensagens que correspondem ao filtro especificado pelo `filterName` atributo.|  
|Filter|Uma cadeia de caracteres que especifica uma referência a um elemento de filtro.|  
|priority|Um inteiro que especifica a prioridade desta entrada.<br /><br /> As entradas na tabela de roteamento serão avaliadas com base na prioridade, sendo que 0 é a prioridade mais baixa. Todas as entradas de uma prioridade específica são avaliadas simultaneamente, se nenhuma entrada correspondente for encontrada para a prioridade atual, o próximo nível de prioridade será avaliado.<br /><br /> Esse valor é opcional.|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<routing>](routing.md)|Uma seção de configuração que contém entradas de mapeamento de roteamento.|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Routing.Configuration.RoutingSection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Routing.Configuration.FilterTableEntryElement?displayProperty=nameWithType>
