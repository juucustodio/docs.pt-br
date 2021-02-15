---
title: Criando e implementando atividades personalizadas
description: Este artigo fornece recursos para a criação de atividades personalizadas no Workflow Foundation criando atividades compostas ou criando novos tipos de atividade.
ms.date: 03/30/2017
ms.assetid: 4e30e63d-6e33-4842-a7a4-ce807cef1fad
ms.openlocfilehash: cb6e189cf5f59630ce8d89610eb0c2fc2acc92a7
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96280384"
---
# <a name="designing-and-implementing-custom-activities"></a>Criando e implementando atividades personalizadas

As atividades personalizadas no [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] são criadas montando atividades fornecida pelo sistema em atividades compostas ou criando novos tipos que derivam de <xref:System.Activities.CodeActivity>, <xref:System.Activities.AsyncCodeActivity> ou <xref:System.Activities.NativeActivity>. Esta seção descreve como criar atividades personalizadas com um dos métodos.  
  
> [!IMPORTANT]
> Atividades personalizadas por padrão são exibidas no designer de fluxo de trabalho como um retângulo simples com o nome da atividade. Para fornecer uma representação visual de sua atividade personalizada no designer de fluxo de trabalho, você também deverá criar um designer personalizado. Para obter mais informações, consulte [usando modelos e designers de atividades personalizados](using-custom-activity-designers-and-templates.md).  
  
## <a name="in-this-section"></a>Nesta seção  

 [Opções de criação de atividades](activity-authoring-options-in-wf.md)  
 Discute os estilos de criação disponíveis no [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)].  
  
 [Usando uma atividade personalizada](using-a-custom-activity.md)  
 Descreve como adicionar uma atividade personalizada a um projeto do fluxo de trabalho.  
  
  [Criar atividades assíncronas](creating-asynchronous-activities-in-wf.md)  
 Descreve como criar atividades assíncronas.  
  
 [Configurando a validação de atividades](configuring-activity-validation.md)  
 Descreve como a validação de atividade pode ser usada para identificar e relatar erros na configuração de uma atividade antes de sua execução.  
  
 [Criar uma atividade em runtime](creating-an-activity-at-runtime-with-dynamicactivity.md)  
 Discute como criar atividades em runtime usando <xref:System.Activities.DynamicActivity>.  
  
 [Propriedades de execução de fluxo de trabalho](workflow-execution-properties.md)  
 Descreve como usar as propriedades de execução do fluxo de trabalho para adicionar propriedades específicas de contexto ao ambiente de uma atividade  
  
 [Usando representantes de atividades](using-activity-delegates.md)  
 Discute como criar e usar as atividades que contêm representantes de atividade.
  
 [Usando extensões de atividade](using-activity-extensions.md)  
 Descreve como criar e usar extensões de atividade.  
  
 [Consumir feeds do OData de um fluxo de trabalho](consuming-odata-feeds-from-a-workflow.md)  
 Descreve vários métodos para chamar um WCF Data Service de um fluxo de trabalho.  
  
 [Escopo e visibilidade de definição de atividades](activity-definition-scoping-and-visibility.md)  
 Descreve as opções e as regras para definir o escopo de dados e a visibilidade de membros para atividades.
