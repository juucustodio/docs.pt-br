---
description: 'Saiba mais sobre: criação de atividade de fluxo de trabalho usando a classe de atividade'
title: Criação de atividade de fluxo de trabalho usando a classe de atividades
ms.date: 03/30/2017
ms.assetid: 7b7b1c66-f093-43c3-b4d1-7173b46516da
ms.openlocfilehash: 0d3ffc88bacfd941dfa0c853991bf72045468323
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754934"
---
# <a name="workflow-activity-authoring-using-the-activity-class"></a>Criação de atividade de fluxo de trabalho usando a classe de atividades

A maneira mais básica de criar uma atividade usando Windows Workflow Foundation (WF) no [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] é criar uma classe que herda de <xref:System.Activities.Activity> que cria a funcionalidade montando atividades personalizadas ou atividades da [biblioteca de atividades interna](net-framework-4-5-built-in-activity-library.md). Este tópico demonstra como criar uma atividade duas mensagens que grava no console.

### <a name="to-create-a-custom-activity-using-the-activity-designer"></a>Para criar uma atividade personalizado utilizando o designer de atividades

1. Abra o Visual Studio 2012.

2. Arquivo, Selecione Novo, Projeto. Selecione **fluxo de trabalho 4,0** em **Visual C#** na janela **tipos de projeto** e selecione o nó **v2010** . Selecione **biblioteca de atividades** na janela **modelos** . Nomeie o novo projeto HelloActivity.

3. Abra a nova atividade.  Arraste uma atividade de <xref:System.Activities.Statements.Sequence> da caixa de ferramentas para a superfície de designer.

4. Arraste uma atividade de <xref:System.Activities.Statements.WriteLine> na atividade de <xref:System.Activities.Statements.Sequence> . Insira `"Hello World"` (com aspas) no campo de **texto** .

5. Arraste uma atividade de <xref:System.Activities.Statements.WriteLine> de segundo na atividade de <xref:System.Activities.Statements.Sequence> , abaixo da primeira. Insira `"Goodbye"` (com aspas) no campo de **texto** .
