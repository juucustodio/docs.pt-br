---
description: 'Saiba mais sobre: inspeção de árvore de atividade'
title: Inspeção da árvore de atividade
ms.date: 03/30/2017
ms.assetid: 100d00e4-8c1d-4233-8fbb-dd443a01155d
ms.openlocfilehash: aac19dd99199481e6ad0d1a554ad1846678c160e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787949"
---
# <a name="activity-tree-inspection"></a>Inspeção da árvore de atividade

A inspeção da árvore de atividade é usada por autores de aplicativo de fluxo de trabalho para inspecionar os fluxos de trabalho hospedados pelo aplicativo. Usando <xref:System.Activities.WorkflowInspectionServices>, os fluxos de trabalho podem ser pesquisados para atividades filhos específicas, as atividades individuais e suas propriedades podem ser enumeradas, e os metadados de runtime das atividades podem ser armazenados em cachê em um horário específico. Este tópico fornece uma visão geral de <xref:System.Activities.WorkflowInspectionServices> e como usá-la para inspecionar uma árvore de atividade.  
  
## <a name="using-workflowinspectionservices"></a>Usando WorkflowInspectionServices  

 O método de <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> é usado para enumerar todas as atividades na árvore de atividade especificada. retorna um<xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> enumerável que toque em todas as atividades dentro da árvore que inclui filhos, manipuladores de representante opções, variáveis, e expressões de argumento. No exemplo a seguir, uma definição de fluxo de trabalho é criada usando <xref:System.Activities.Statements.Sequence>, <xref:System.Activities.Statements.While>, <xref:System.Activities.Statements.ForEach%601>, <xref:System.Activities.Statements.WriteLine>, e expressões. Depois que a definição de fluxo de trabalho é criada, invoca-se e o método de `InspectActivity` é então chamado.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#45](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#45)]  
  
 Para enumerar as atividades, <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> é chamado a atividade de raiz, e novamente recursivamente em cada atividade retornado. No exemplo a seguir, <xref:System.Activities.Activity.DisplayName%2A> de cada atividade e expressão na árvore de atividade é escrito no console.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#46](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#46)]  
  
 Esse código de exemplo fornece a seguinte saída.  
  
 **Item de lista 1**  
**Item de lista 2** 
 **Item de lista 3** 
 **Item de lista 4** 
 **Item de lista 5** 
 **Itens adicionados à coleção.** 
  **Lista \<String> de ><literal** de sequência  
 **While**  
 **AddToCollection\<String>**  
 **VariableValue<ICollection\<String>>**  
 **LambdaValue\<String>**  
 **Lista de<de LocationReferenceValue\<String>>**  
 **LambdaValue\<Boolean>**  
 **Lista de<de LocationReferenceValue\<String>>**  
 **ForEach\<String>**  
 **VariableValue<IEnumerable\<String>>**  
 **WriteLine**  
 **DelegateArgumentValue\<String>**  
 **Sequência**  
 **WriteLine**  
 **Literal \<String>**  Para recuperar uma atividade específica em vez de enumerar todas as atividades, <xref:System.Activities.WorkflowInspectionServices.Resolve%2A> é usado. <xref:System.Activities.WorkflowInspectionServices.Resolve%2A> e <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> executam o cachê de metadados `WorkflowInspectionServices.CacheMetadata` se não tiver sido chamado anteriormente. Se <xref:System.Activities.WorkflowInspectionServices.CacheMetadata%2A> tiver sido chamado em <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> é baseado nos metadados existentes. Portanto, se as alterações de árvore foram feitas desde a última chamada a <xref:System.Activities.WorkflowInspectionServices.CacheMetadata%2A>, <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> pode dar resultados inesperados. Se forem feitas alterações no fluxo de trabalho após a chamada <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> , os metadados poderão ser armazenados em cache novamente chamando o <xref:System.Activities.Validation.ActivityValidationServices> <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> método. Armazenando em cachê metadados é abordado na seção a seguir.  
  
### <a name="caching-metadata"></a>Metadados de Caching  

 Armazenando em cachê os metadados para uma atividade compila e valida uma descrição dos argumentos de atividade, variáveis, as atividades filhos, e os representantes de atividade. Os metadados, são armazenados em cachê por padrão no runtime em que uma atividade é preparada para a execução. Se um autor de host de fluxo de trabalho deseja armazenar em cachê os metadados para uma atividade ou a árvore de atividade antes disso, por exemplo tomar com antecedência todos os custos, então <xref:System.Activities.WorkflowInspectionServices.CacheMetadata%2A> pode ser usada para armazenar em cachê os metadados em tempo desejado.
