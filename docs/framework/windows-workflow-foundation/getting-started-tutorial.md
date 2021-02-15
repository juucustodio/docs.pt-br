---
title: Introdução Tutorial2
description: Este artigo inicia uma sequência de tutoriais que apresentam a programação de Windows Workflow Foundation aplicativos.
ms.date: 03/30/2017
helpviewer_keywords:
- WF [WF], getting started
- Windows Workflow Foundation [WF], getting started
ms.assetid: c2d3585f-6b1a-4d4f-9865-bd7cd31c5d42
ms.openlocfilehash: e9856320faa82becf12dda04d02f6f1c08081feb
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293592"
---
# <a name="getting-started-tutorial"></a>Guia de introdução ao tutorial

Esta seção contém um conjunto de tópicos explicativos que apresentam a programação de aplicativos Windows Workflow Foundation (WF). Siga os procedimentos deste tópico para criar um aplicativo que é um jogo de adivinhação de números. O primeiro tópico no tutorial conduziu pelas etapas para criar as atividades personalizadas necessárias para o fluxo de trabalho. No segundo tópico, estas atividades são montadas junto com atividades internas de fluxo de trabalho em um fluxo de trabalho de fluxograma. No terceiro tópico, o aplicativo host é configurado para executar o fluxo de trabalho e, no tópico final, é apresentada a persistência. Cada etapa neste processo depende das etapas anteriores. Portanto, é recomendável que você as conclua na ordem.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Como: criar uma atividade](how-to-create-an-activity.md)  
 Descreve como criar uma atividade personalizada que deriva de <xref:System.Activities.NativeActivity%601>, e como compor essa atividade junto com uma atividade interna em uma atividade composta usando o designer de atividade.  
  
 [Como: criar um fluxo de trabalho](how-to-create-a-workflow.md)  
 Descreve como criar fluxos de trabalho de fluxograma, sequenciais e de máquina de estado usando atividades internas e atividades personalizadas do tutorial anterior.  
  
 [Como: executar um fluxo de trabalho](how-to-run-a-workflow.md)  
 Descreve como chamar um fluxo de trabalho de um ambiente de host, transmitir dados para dentro e para fora de um fluxo de trabalho e como retomar indicadores.  
  
 [Como: criar e executar um fluxo de trabalho de execução prolongada](how-to-create-and-run-a-long-running-workflow.md)  
 Descreve como adicionar persistência a um aplicativo de fluxo de trabalho.  
  
 [Como: criar um participante de acompanhamento personalizado](how-to-create-a-custom-tracking-participant.md)  
 Descreve como criar um participante de rastreamento personalizado e um perfil de controle.  
  
 [Como: hospedar várias versões de um fluxo de trabalho lado a lado](how-to-host-multiple-versions-of-a-workflow-side-by-side.md)  
 Descreve como usar `WorkflowIdentity` para hospedar várias versões de um fluxo de trabalho lado a lado.  
  
 [Como: atualizar a definição de uma instância de fluxo de trabalho em execução](how-to-update-the-definition-of-a-running-workflow-instance.md)  
 Descreve como usar a atualização dinâmica para modificar instâncias de fluxo de trabalho em execução.  
  
## <a name="see-also"></a>Veja também

- [Programação do Windows Workflow Foundation](programming.md)
