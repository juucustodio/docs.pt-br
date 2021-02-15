---
description: 'Saiba mais sobre: usando uma atividade personalizada'
title: Usando uma atividade personalizada
ms.date: 03/30/2017
ms.assetid: 8f356419-681a-4175-ae93-878eee970249
ms.openlocfilehash: f036b3851878f83b461e6d692002501ea7d87649
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755103"
---
# <a name="using-a-custom-activity"></a>Usando uma atividade personalizada

As atividades que derivam de <xref:System.Activities.Activity> ou suas subclasses podem ser compostas em fluxos de trabalho maiores ou criadas diretamente no código. Este tópico descreve como usar atividades personalizadas em fluxos de trabalho criados no código ou no designer.  
  
> [!NOTE]
> As atividades personalizadas podem ser usadas no mesmo projeto no qual elas são definidas, desde que a atividade personalizada e a atividade que as utiliza sejam compiladas (ou seja, carregadas por um tipo de instanciação gerado pelo processo de compilação) se a atividade de referência for carregada dinamicamente (por exemplo, usando ActivityXamlServices encontraram), o assembly referenciado deverá ser colocado em um projeto diferente ou o XAML gerado pelo designer precisa ser editado manualmente para habilitar isso.  
  
#### <a name="using-a-custom-activity-to-a-workflow-project"></a>Usando uma atividade personalizada para um projeto de fluxo de trabalho  
  
1. Adicione uma referência do projeto de host para o projeto de biblioteca de atividade que contém a atividade personalizada.  
  
2. Compile a solução.  
  
3. Para usar a atividade personalizada no designer, localize a atividade personalizada na caixa de ferramentas e arraste a atividade na superfície do designer.  
  
4. Para usar a atividade personalizada no código, adicione uma instrução Using que se refere ao projeto de atividade personalizada, e transmita uma nova instância da atividade para <xref:System.Activities.WorkflowInvoker.Invoke%2A>.
