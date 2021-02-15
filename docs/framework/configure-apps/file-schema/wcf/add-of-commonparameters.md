---
description: 'Saiba mais sobre: <add> de <commonParameters>'
title: <add> de <commonParameters>
ms.date: 03/30/2017
ms.assetid: 3713bf25-20c8-455f-bb85-de46b6487932
ms.openlocfilehash: d7a1b78ed79b7eab472460b364b90bd372ecf6bf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99804004"
---
# <a name="add-of-commonparameters"></a>\<add> de \<commonParameters>

Especifica um par de nome-valor de parâmetros que são usados globalmente em vários serviços. Normalmente, esse parâmetro inclui a cadeia de conexão de banco de dados que pode ser compartilhada por serviços duráveis.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<workflowRuntime>**](workflowruntime.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<commonParameters>**](commonparameters.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<workflowRuntime>
  <commonParameters>
    <add name="String" value="String" />
  </commonParameters>
</workflowRuntime>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|name|O nome do parâmetro especificado para um serviço.|  
|value|O valor do parâmetro especificado para um serviço.|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<commonParameters>](commonparameters.md)|Uma coleção de parâmetros comuns usados por serviços. Normalmente, essa coleção inclui a cadeia de conexão do banco de dados que pode ser compartilhada por serviços duráveis.|  
  
## <a name="remarks"></a>Comentários  

 O `<commonParameters>` elemento define todos os parâmetros que são usados globalmente em vários serviços, por exemplo, `ConnectionString` ao usar o <xref:System.Workflow.Runtime.Hosting.SharedConnectionWorkflowCommitWorkBatchService> .  
  
 Para serviços que confirmam lotes de trabalho para repositórios de persistência, como <xref:System.Workflow.Runtime.Hosting.DefaultWorkflowCommitWorkBatchService> e <xref:System.Workflow.Runtime.Hosting.SqlWorkflowPersistenceService> , você pode habilitá-los para repetir sua transação usando o `EnableRetries` parâmetro, conforme mostrado no exemplo a seguir:  
  
```xml  
<workflowRuntime name="SampleApplication"
                 unloadOnIdle="false">
  <commonParameters>
    <add name="ConnectionString"
         value="Initial Catalog=WorkflowStore;Data Source=localhost;Integrated Security=SSPI;" />
    <add name="EnableRetries"
         value="True" />
  </commonParameters>
  <services>
    <add type="System.Workflow.Runtime.Hosting.SqlWorkflowPersistenceService, System.Workflow.Runtime, Version=3.0.00000.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35"
         enableRetries="False" />
  </services>
</workflowRuntime>
```  
  
 Observe que o `EnableRetries` parâmetro pode ser definido em um nível global (conforme mostrado na seção *CommonParameters* ) ou para serviços individuais que dão suporte `EnableRetries` (conforme mostrado na seção de *Serviços* ).  
  
 Para obter mais informações sobre como usar um arquivo de configuração para controlar o comportamento de um <xref:System.Workflow.Runtime.WorkflowRuntime> objeto de um aplicativo host Windows Workflow Foundation, consulte [arquivos de configuração de fluxo de trabalho](/previous-versions/dotnet/netframework-3.5/ms732240(v=vs.90)).  
  
## <a name="example"></a>Exemplo  
  
```xml  
<commonParameters>
  <add name="ConnectionString"
       value="Initial Catalog=WorkflowStore;Data Source=localhost;Integrated Security=SSPI;" />
  <add name="EnableRetries"
       value="true" />
</commonParameters>
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Configuration.WorkflowRuntimeElement>
- <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>
- <xref:System.Workflow.Runtime.WorkflowRuntime>
- <xref:System.Workflow.Runtime.Hosting.DefaultWorkflowCommitWorkBatchService>
- <xref:System.Workflow.Runtime.Hosting.SqlWorkflowPersistenceService>
- [Arquivos de configuração de fluxo de trabalho](/previous-versions/dotnet/netframework-3.5/ms732240(v=vs.90))
- [\<commonParameters>](commonparameters.md)
