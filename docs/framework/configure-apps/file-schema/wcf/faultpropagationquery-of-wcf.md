---
description: 'Saiba mais sobre: <faultPropagationQuery> do WCF'
title: <faultPropagationQuery> do WCF
ms.date: 03/30/2017
ms.assetid: fabafbc8-3e45-4feb-8321-0725e9f4079c
ms.openlocfilehash: cd26bf76fec54371ef0455b93c98650bdab19068
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99782059"
---
# <a name="faultpropagationquery-of-wcf"></a>\<faultPropagationQuery> do WCF

Representa uma consulta que é usada para rastrear a manipulação de falhas que ocorrem em uma atividade.  Esse evento ocorre toda vez que um FaultHandler processa uma falha. Você deve usar essa consulta para controlar o tratamento de falhas que ocorrem dentro de uma atividade. A consulta é necessária para um participante de rastreamento assinar os registros de propagação de falhas.

Para obter mais informações sobre consultas de perfil de rastreamento, consulte [perfis de rastreamento](../../../windows-workflow-foundation/tracking-profiles.md).

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<tracking>**](tracking-of-wcf.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<profiles>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<trackingProfile>**](trackingprofile-of-wcf.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<workflow>**](workflow-of-wcf.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<faultPropagationQueries>**](faultpropagationqueries-of-wcf.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<faultPropagationQuery>**  

## <a name="syntax"></a>Syntax

```xml
<tracking>
  <profiles>
    <trackingProfile name="Name">
      <workflow>
        <faultPropagationQueries>
          <faultPropagationQuery faultSourceActivityName="String"
                                 faultHandlerActivityName="String" />
        </faultPropagationQueries>
      </workflow>
    </trackingProfile>
  </profiles>
</tracking>
```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|`faultSourceActivityName`|Uma cadeia de caracteres que especifica o nome da atividade do manipulador de falhas que propagaram a falha. O padrão é \* , que indica que os registros de propagação de falha são retornados para todas as atividades.|
|`faultHandlerActivityName`|Uma cadeia de caracteres que especifica o nome da atividade que foi a origem da falha.|

### <a name="child-elements"></a>Elementos filho

Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[\<faultPropagationQueries>](faultpropagationqueries-of-wcf.md)|Representa uma lista de elementos de configuração que são usados para rastrear a manipulação de falhas que ocorrem dentro de uma atividade.  Esse evento ocorre toda vez que um FaultHandler processa uma falha.|

## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Activities.Tracking.Configuration.FaultPropagationQueryElement?displayProperty=nameWithType>
- <xref:System.Activities.Tracking.FaultPropagationQuery?displayProperty=nameWithType>
- [Rastreamento e rastreamento de fluxo de trabalho](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [Controlando perfis](../../../windows-workflow-foundation/tracking-profiles.md)
