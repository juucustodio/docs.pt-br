---
description: 'Saiba mais sobre: <states> do WCF, <workflowInstanceQuery>'
title: <states> do WCF, <workflowInstanceQuery>
ms.date: 03/30/2017
ms.assetid: d17f7525-8035-4e9e-85a0-4cddae59f85d
ms.openlocfilehash: 66b3008b352d1f76c30aab9a0ec038836f33d408
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786636"
---
# <a name="states-of-wcf-workflowinstancequery"></a>\<states> do WCF, \<workflowInstanceQuery>

Representa uma coleção de estados inscritos da instância do fluxo de trabalho controladas quando os registros de rastreamento são criados.  
  
Para obter mais informações sobre consultas de perfil de rastreamento, consulte [perfis de rastreamento](../../../windows-workflow-foundation/tracking-profiles.md)  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<tracking>**](tracking-of-wcf.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<profiles>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<trackingProfile>**](trackingprofile-of-wcf.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<workflow>**](workflow-of-wcf.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<workflowInstanceQueries>**](workflowinstancequeries-of-wcf.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<workflowInstanceQuery>**](workflowinstancequery-of-wcf.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<states>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<tracking>
  <profiles>
    <trackingProfile name="Name">
      <workflow>
        <workflowInstanceQueries>
          <workflowInstanceQuery>
            <states>
              <state name="Name" />
            </states>
          </workflowInstanceQuery>
        </workflowInstanceQueries>
      </workflow>
    </trackingProfile>
  </profiles>
</tracking>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  

Nenhum.  
  
### <a name="child-elements"></a>Elementos filho
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<states>](state-of-wcf-workflowinstancequery.md)|Um estado inscrito da instância do fluxo de trabalho controladas quando o registro de rastreamento é criado.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<workflowInstanceQuery>](../windows-workflow-foundation/workflowinstancequery.md)|Uma consulta que controla as alterações de ciclo de vida de instância de fluxo de trabalho como um evento iniciado ou concluído.|  
  
## <a name="remarks"></a>Comentários

Os registros retornados são filtrados por estados nesta coleção.  
  
Estado de possíveis valores é descritos na tabela a seguir.  
  
|Estado|Descrição|  
|-----------|-----------------|  
|Anulado|A instância de fluxo de trabalho será anulada.|  
|Concluído|A instância de fluxo de trabalho for concluída.|  
|Excluído|A instância de fluxo de trabalho é excluída.|  
|Idle|A instância de fluxo de trabalho está ociosa.|  
|Persistente|A instância de fluxo de trabalho é mantida.|  
|Retomada|A instância de fluxo de trabalho é retomada.|  
|Iniciado|A instância de fluxo de trabalho é iniciada.|  
|UnhandledException|A instância de fluxo de trabalho encontrou uma exceção sem tratamento.|  
|Descarregado|A instância de fluxo de trabalho é descarregada.|  
|Canceled|A instância de fluxo de trabalho é cancelada.|  
|Suspenso|A instância de fluxo de trabalho é suspensa.|  
|Terminado|A instância de fluxo de trabalho é encerrada.|  
|Não suspenso|A instância de fluxo de trabalho é unsuspended.|  
  
## <a name="example"></a>Exemplo

A configuração a seguir assina o fluxo de trabalho em nível de instância registros de controle para o `Started` estado da instância usando esta consulta.  
  
```xml  
<workflowInstanceQueries>
  <workflowInstanceQuery>
    <states>
      <state name="Started" />
    </states>
  </workflowInstanceQuery>
</workflowInstanceQueries>
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Activities.Tracking.Configuration.WorkflowInstanceQueryElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Activities.Tracking.Configuration.StateElementCollection?displayProperty=nameWithType>
- <xref:System.Activities.Tracking.WorkflowInstanceQuery?displayProperty=nameWithType>
- [Rastreamento e rastreamento de fluxo de trabalho](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [Controlando perfis](../../../windows-workflow-foundation/tracking-profiles.md)
