---
description: 'Saiba mais sobre: rastreamento de variável e de argumentos'
title: Rastreamento de variável e argumento
ms.date: 03/30/2017
ms.assetid: 8f3d9d30-d899-49aa-b7ce-a8d0d32c4ff0
ms.openlocfilehash: f2663e585ca280739f9c4ec176c31cf1d7c30657
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754973"
---
# <a name="variable-and-argument-tracking"></a>Rastreamento de variável e argumento

Para controlar a execução de um fluxo de trabalho, geralmente é útil extrair dados. Isso fornece um contexto extra para acessar uma execução de postagem de registro de rastreamento. Em [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)], você pode extrair qualquer variável ou argumento visível no escopo de qualquer atividade em um fluxo de trabalho usando o rastreamento. Controlando os perfis facilitam extrair dados.  
  
## <a name="variables-and-arguments"></a>Variáveis e argumentos  

 Variáveis e os argumentos são extraídos quando uma atividade se emite um ActivityStateRecord.  Uma variável está disponível para a extração somente se está no escopo da atividade. Uma variável para ser extraído dentro de uma atividade é especificado da seguinte maneira:  
  
- Se uma variável é especificado pelo nome de variável, então o rastreamento para a variável dentro da atividade sendo controlada e em atividades pai. A variável é procurada no escopo da atividade atual e o escopo pai.  
  
- Se as variáveis a serem extraídas forem especificadas usando name = " \* ", todas as variáveis dentro da atividade atual que está sendo controlada serão extraídas. Variáveis que estão no escopo mas são definidos em atividades pai não são extraídos nesse caso.  
  
 Para extrair argumentos, os argumentos extraídos dependem de estado da atividade. Quando o estado de uma atividade é executado, então somente `InArguments` está disponível para a extração. Para qualquer outro estado da atividade (zipado, criticado, cancelado), todos os argumentos, InArguments e OutArguments, estão disponíveis para a extração.  
  
 O exemplo a seguir mostra uma consulta de estado da atividade que extrai variáveis e argumentos quando `Closed` de atividade que controla o registro é emitida. Variáveis e os argumentos podem ser extraídos somente com <xref:System.Activities.Tracking.ActivityStateRecord> e são assinados bem em um perfil de rastreamento usando <xref:System.Activities.Tracking.ActivityStateQuery>.  
  
```xml  
<activityStateQuery activityName="SendEmailActivity">  
  <states>  
    <state name="Closed"/>  
  </states>  
  <variables>  
    <variable name="FromAddress"/>  
  </variables>  
  <arguments>  
    <argument name="Result"/>  
  </arguments>  
</activityStateQuery>  
```  
  
## <a name="protecting-information-stored-within-variables-and-arguments"></a>Informações de proteção armazenada em variáveis e os argumentos  

 Uma variável ou um argumento controlado por padrão são feitas visível no runtime de WF. Um desenvolvedor de fluxo de trabalho de protegê-lo pode ser acessado colocando as seguintes etapas:  
  
1. Criptografar o valor de uma variável.  
  
2. Controle a criação de um perfil de rastreamento para evitar a extração de uma variável ou um argumento.  
  
3. Para participantes personalizados de rastreamento certifique-se de que o código de WF não divulgue informações sigilosas que é armazenada em variáveis ou nos argumentos.  
  
## <a name="see-also"></a>Consulte também

- [Monitoramento do Windows Server app Fabric](/previous-versions/appfabric/ee677251(v=azure.10))
- [Monitorando aplicativos com o app Fabric](/previous-versions/appfabric/ee677276(v=azure.10))
