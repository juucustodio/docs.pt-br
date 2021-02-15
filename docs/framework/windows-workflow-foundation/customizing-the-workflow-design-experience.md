---
description: 'Saiba mais sobre: Personalizando a experiência de design do fluxo de trabalho'
title: Personalizando a experiência design de fluxo de trabalho
ms.date: 03/30/2017
helpviewer_keywords:
- extending [WF], Workflow Designer
ms.assetid: 98135077-0f5d-4d16-9337-01094e843537
ms.openlocfilehash: 02049f8b42de3de6e4dfdfe8a4151be1500bcca9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99742648"
---
# <a name="customizing-the-workflow-design-experience"></a>Personalizando a experiência design de fluxo de trabalho

Os cenários para criar atividades personalizadas e rehospedar as Designer de Fluxo de Trabalho do Windows foram bastante simplificados no .NET Framework 4. O desenvolvimento e implantação agora são mais fácil e mais flexível. A chave infraestrutura alterada é que o novo modelo de programação do designer de atividade é criado sobre Windows Presentation Foundation (WPF). Isso permite que você defina os designers de atividade declarativamente e rehospede o Designer de Fluxo de Trabalho em outros aplicativos com o comparativa fácil. Ao rehosting, um editor de expressão personalizado pode ser desenvolvido para oferecer suporte IntelliSense ou um domínio simplificado da expressão. A integração com o Windows Communication Foundation (WCF) se tornou mais direta com o uso dos serviços de fluxo de trabalho. Designers personalizados de atividade e a árvore modelo de item podem ser usados para aprimorar experiências de tempo de design em designer rehosted de fluxo de trabalho.

## <a name="in-this-section"></a>Nesta seção

 [Usando designers personalizados e modelos de atividades](using-custom-activity-designers-and-templates.md)

 Descreve como criar novos designer personalizadas e modelos de atividade.

 [Hospedando novamente o designer de fluxo de trabalho](rehosting-the-workflow-designer.md)

 Descreve como hospedar novamente o Designer de Fluxo de Trabalho do Windows fora do Visual Studio e como exibir erros de validação.

 [Usando um editor de expressão personalizado](using-a-custom-expression-editor.md)

 Descreve como implementar um editor de expressão personalizado para usar com designers de fluxo de trabalho rehospedados fora do Visual Studio 2010.

## <a name="reference"></a>Referência

<xref:System.Activities.Presentation.ActivityDesigner>

## <a name="see-also"></a>Consulte também

- [Estendendo Windows Workflow Foundation](extend.md)
- [Designer](./samples/designer.md)
- [Designers personalizados de atividades](./samples/custom-activity-designers.md)
- [Hospedagem do designer](./samples/designer-rehosting.md)
