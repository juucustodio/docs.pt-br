---
title: Arquitetura de fluxo de trabalho do Windows
description: O Windows Workflow Foundation encapsula unidades de trabalho como atividades, que são executadas em um ambiente com controle de fluxo, manipulação de exceção e outros recursos.
ms.date: 03/30/2017
ms.assetid: 1d4c6495-d64a-46d0-896a-3a01fac90aa9
ms.openlocfilehash: 81d1414fe5c6e17871dbbd0a2dd78cd8ace21ec6
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96289133"
---
# <a name="windows-workflow-architecture"></a>Arquitetura de fluxo de trabalho do Windows

Windows Workflow Foundation (WF) gera o nível de abstração para o desenvolvimento de aplicativos interativos de longa execução. As unidades de trabalho são encapsuladas como atividades. As atividades executam em um ambiente que fornece recursos para o controle de fluxo, manipulação de exceção, a propagação de falha, persistência de dados do estado, ao carregamento e descarregamento de fluxos de trabalho em andamento de memória, de rastreamento, e de fluxo de transação.  
  
## <a name="activity-architecture"></a>Arquitetura de atividades  

 As atividades são desenvolvidas como os tipos de CLR que derivam de <xref:System.Activities.Activity>, de <xref:System.Activities.CodeActivity>, de <xref:System.Activities.AsyncCodeActivity>, ou de <xref:System.Activities.NativeActivity>, ou as suas variantes que retornam um valor, <xref:System.Activities.Activity%601>, <xref:System.Activities.CodeActivity%601>, <xref:System.Activities.AsyncCodeActivity%601>, ou <xref:System.Activities.NativeActivity%601>. Desenvolver as atividades que derivam de <xref:System.Activities.Activity> permite que o usuário reúne atividades pré-compilação existentes para criar rapidamente as unidades de trabalho que executam no ambiente de fluxo de trabalho. <xref:System.Activities.CodeActivity>, por outro lado, permite a lógica de execução a ser criado em código gerenciado usando <xref:System.Activities.CodeActivityContext> principalmente para acesso aos argumentos de atividade. <xref:System.Activities.AsyncCodeActivity> é semelhante a <xref:System.Activities.CodeActivity> exceto que pode ser usado para implementar tarefas assíncronas. Desenvolver as atividades que derivam de <xref:System.Activities.NativeActivity> permite que os usuários acessem o runtime com <xref:System.Activities.NativeActivityContext> para a funcionalidade como filhos de programação, criando indexadores, invocando o trabalho assíncrona, registrando transações, e mais.  
  
 As atividades de design que derivam de <xref:System.Activities.Activity> são declarativas e essas atividades podem ser criadas em XAML. No exemplo a seguir, uma atividade chamada `Prompt` é criada usando outras atividades para o corpo de execução.  
  
```xml  
<Activity x:Class='Prompt'  
  xmlns:x='http://schemas.microsoft.com/winfx/2006/xaml'  
    xmlns:z='http://schemas.microsoft.com/netfx/2008/xaml/schema'  
xmlns:my='clr-namespace:XAMLActivityDefinition;assembly=XAMLActivityDefinition'  
xmlns:s="clr-namespace:System;assembly=mscorlib"  
xmlns="http://schemas.microsoft.com/2009/workflow">  
<z:SchemaType.Members>  
    <z:SchemaType.SchemaProperty Name='Text' Type=' InArgument(s:String)' />  
  <z:SchemaType.SchemaProperty Name='Response' Type='OutArgument(s:String)' />  
</z:SchemaType.Members>  
  <Sequence>  
    <my:WriteLine Text='[Text]' />  
    <my:ReadLine BookmarkName='r1' Result='[Response]' />  
  </Sequence>  
</Activity>  
```  
  
## <a name="activity-context"></a>Contexto de atividades  

 <xref:System.Activities.ActivityContext> é a interface de autor de atividade do runtime de fluxo de trabalho e fornece acesso a riqueza de runtime dos recursos. No exemplo a seguir, uma atividade é definida que usa o contexto de execução para criar um marcador (o mecanismo que permite uma atividade registra um ponto de continuação de linha em sua execução que pode ser continuada por um host que passa dados na atividade).  
  
 [!code-csharp[CFX_WorkflowApplicationExample#15](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#15)]  
  
## <a name="activity-life-cycle"></a>Ciclo de vida de atividades  

 Uma instância de uma atividade começa em estado de <xref:System.Activities.ActivityInstanceState.Executing> . A menos que as exceções são localizadas, permanece nesse estado até que todas as atividades filho sejam executar completo e qualquer outro trabalho pendente (<xref:System.Activities.Bookmark> objetos, por exemplo) está concluído, ao ponto que ele faz a transição de estado de <xref:System.Activities.ActivityInstanceState.Closed> . O pai de uma instância da atividade pode solicitar um filho; cancelar se o filho pode ser cancelado termina em estado de <xref:System.Activities.ActivityInstanceState.Canceled> . Se uma exceção é lançada durante a execução, o runtime coloca a atividade no estado de <xref:System.Activities.ActivityInstanceState.Faulted> e propaga a exceção acima da cadeia pai de atividades. A seguir estão os três Estados de conclusão de uma atividade:
  
- **Fechado:** A atividade concluiu seu trabalho e foi encerrada.  
  
- **Cancelado:** A atividade abandonou seu trabalho e saiu. O trabalho não será revertido explicitamente quando esse estado está conectado.  
  
- **Com falha:** A atividade encontrou um erro e foi encerrada sem concluir seu trabalho.  
  
 As atividades permanecem no estado de <xref:System.Activities.ActivityInstanceState.Executing> quando são persistentes ou descarregadas.
