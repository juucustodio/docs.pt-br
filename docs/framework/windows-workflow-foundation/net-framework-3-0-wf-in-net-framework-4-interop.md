---
description: 'Saiba mais sobre: usando atividades .NET Framework WF 3,0 no .NET Framework 4 com a atividade de interoperabilidade'
title: Usando atividades do .NET Framework 3.0 WF no .NET Framework 4 com a atividade de Interoperabilidade
ms.date: 03/30/2017
ms.assetid: 71f112ba-abb0-46f7-b05f-a5d2eb9d0c5c
ms.openlocfilehash: 8a91e9488b9885682d2d46f7b6afd512700157d9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99720105"
---
# <a name="using-net-framework-30-wf-activities-in-net-framework-4-with-the-interop-activity"></a>Usando atividades do .NET Framework 3.0 WF no .NET Framework 4 com a atividade de Interoperabilidade

A <xref:System.Activities.Statements.Interop> atividade é uma [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] atividade (WF 4,5) que encapsula uma atividade .NET Framework 3,5 (WF 3,5) em um [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] fluxo de trabalho. A atividade de WF 3 pode ser uma única atividade de folha ou uma árvore inteira de atividades. A execução (incluindo o cancelamento e a manipulação de exceções) e a persistência da atividade .NET Framework 3,5 ocorrem no contexto da [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] instância de fluxo de trabalho que está sendo executada.  
  
> [!NOTE]
> A <xref:System.Activities.Statements.Interop> atividade não aparecerá na caixa de ferramentas do designer de fluxo de trabalho, a menos que o projeto do fluxo de trabalho tenha sua configuração de **estrutura de destino** definida como **.NET Framework 4,5**.  
  
## <a name="criteria-for-using-a-wf-3-activity-with-an-interop-activity"></a>Critérios para usar uma atividade de WF 3 com uma atividade de Interoperabilidade  

 Para uma atividade de WF 3 execute com êxito em uma atividade de <xref:System.Activities.Statements.Interop> , os seguintes critérios devem ser encontrados:  
  
- A atividade de WF 3 deve derivar de <xref:System.Workflow.ComponentModel.Activity?displayProperty=nameWithType>.  
  
- A atividade de WF 3 deve ser declarada como `public` e não pode ser `abstract`.  
  
- A atividade do WF 3 deve ter um construtor público sem parâmetros.  
  
- Devido às restrições nos tipos de interface que a atividade de <xref:System.Activities.Statements.Interop> pode oferecer suporte, <xref:System.Workflow.Activities.HandleExternalEventActivity> e <xref:System.Workflow.Activities.CallExternalMethodActivity> não podem ser usados diretamente, mas as atividades derivadas criadas usando a ferramenta de atividade de comunicação de fluxo de trabalho (WCA.exe) podem ser usadas. Consulte [Windows Workflow Foundation Tools](/previous-versions/dotnet/netframework-3.5/ms734408(v=vs.90)) para obter detalhes.  
  
## <a name="configuring-a-wf-3-activity-within-an-interop-activity"></a>Configurando uma atividade de WF 3 em uma atividade de Interoperabilidade  

 Para configurar e passar e retirar dados de uma atividade de WF 3, até o limite de interoperação, as propriedades de atividade de WF 3 e propriedades de metadados são expostos pela atividade de <xref:System.Activities.Statements.Interop> . As propriedades de metadados de atividade de WF 3 (como <xref:System.Workflow.ComponentModel.Activity.Name%2A>) são identificadas através da coleção de <xref:System.Activities.Statements.Interop.ActivityMetaProperties%2A> . Esta sido uma coleção de pares nome-valor usados para definir os valores para as propriedades de metadados de atividade de WF 3. Uma propriedade de metadados é uma propriedade suportada pela propriedade de dependência para que o sinalizador de <xref:System.Workflow.ComponentModel.DependencyPropertyOptions.Metadata> é definido.  
  
 As propriedades de atividade de WF 3 são expostas através da coleção de <xref:System.Activities.Statements.Interop.ActivityProperties%2A> . Este é um conjunto de pares nome-valor, onde cada valor é um objeto de <xref:System.Activities.Argument> , usado para definir os argumentos para as propriedades de atividade de WF 3. Como a direção de uma propriedade de atividade do WF 3 não pode ser inferida, cada propriedade é exposta como um <xref:System.Activities.InArgument> / <xref:System.Activities.OutArgument> par. Dependendo do uso de atividade de propriedade, convém fornecer uma entrada de <xref:System.Activities.InArgument> , uma entrada de <xref:System.Activities.OutArgument> , ou ambos. O nome esperado de entrada de <xref:System.Activities.InArgument> na coleção é o nome da propriedade conforme definido na atividade de WF 3. O nome esperado da <xref:System.Activities.OutArgument> entrada na coleção é uma concatenação do nome da propriedade e da cadeia de caracteres "out".  
  
## <a name="limitations-of-using-a-wf-3-activity-within-an-interop-activity"></a>Limitações de usar uma atividade de WF 3 em uma atividade de Interoperabilidade  

 O WF 3 sistema forneceu atividades não pode diretamente ser empacotado em uma atividade de <xref:System.Activities.Statements.Interop> . Para atividades de qualquer WF 3, como <xref:System.Workflow.Activities.DelayActivity>, isso ocorre porque há uma atividade análoga de WF 4,5. Para outro, isso ocorre porque a funcionalidade de atividade não é suportada. Muitos WF 3 sistema fornecidos atividades podem ser usados dentro de fluxos de trabalho envolvidos pela atividade de <xref:System.Activities.Statements.Interop> , sujeitos às restrições:  
  
1. <xref:System.ServiceModel.Activities.Send> e <xref:System.ServiceModel.Activities.Receive> não podem ser usados em uma atividade de <xref:System.Activities.Statements.Interop> .  
  
2. <xref:System.Workflow.Activities.WebServiceInputActivity>, <xref:System.Workflow.Activities.WebServiceOutputActivity>, e <xref:System.Workflow.Activities.WebServiceFaultActivity> não podem ser usados em uma atividade de <xref:System.Activities.Statements.Interop> .  
  
3. <xref:System.Workflow.Activities.InvokeWorkflowActivity> não pode ser usado em uma atividade de <xref:System.Activities.Statements.Interop> .  
  
4. <xref:System.Workflow.ComponentModel.SuspendActivity> não pode ser usado em uma atividade de <xref:System.Activities.Statements.Interop> .  
  
5. As atividades relacionadas Compensação- não podem ser usadas em uma atividade de <xref:System.Activities.Statements.Interop> .  
  
 Há também alguns específicos comportamentais a compreender sobre o uso de atividades de WF 3 dentro de atividade de <xref:System.Activities.Statements.Interop> :  
  
1. As atividades de WF 3 contidas dentro de uma atividade de <xref:System.Activities.Statements.Interop> são inicializadas quando a atividade de <xref:System.Activities.Statements.Interop> é executada. Em WF 4,5 não há nenhuma estágio de inicialização para uma instância de fluxo de trabalho antes da execução.  
  
2. O runtime de WF 4,5 não faz estado da instância de fluxo de trabalho de nível de verificação quando uma transação começa, independentemente de onde a transação (começa dentro ou fora de uma atividade de <xref:System.Activities.Statements.Interop> ).  
  
3. Os registros de rastreamento de WF 3 para atividades em uma atividade de <xref:System.Activities.Statements.Interop> são fornecidos para os participantes através de WF 4,5 como objetos de <xref:System.Activities.Tracking.InteropTrackingRecord> . <xref:System.Activities.Tracking.InteropTrackingRecord> é derivado de um <xref:System.Activities.Tracking.CustomTrackingRecord>.  
  
4. Uma atividade personalizado de WF 3 pode acessar dados usando filas de fluxo de trabalho no ambiente de interoperação exatamente a mesma forma como no runtime de fluxo de trabalho WF 3. Nenhuma alteração de código personalizado de atividade é necessária. No host, os dados são enviados a fila para uma fila de fluxo de trabalho WF 3 continuando <xref:System.Activities.Bookmark>. O nome do marcador é a forma de cadeia de caracteres o nome da fila de fluxo de trabalho de <xref:System.IComparable> .
