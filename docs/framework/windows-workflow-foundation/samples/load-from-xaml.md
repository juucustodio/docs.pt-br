---
description: 'Saiba mais sobre: carregar do XAML'
title: Carregamento XAML
ms.date: 03/30/2017
ms.assetid: 1f103ef6-7bed-4f16-ae52-9e665c5a43d7
ms.openlocfilehash: fd0eca487c0245c7bfa46ca80c06f2adfa577353
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99742024"
---
# <a name="load-from-xaml"></a>Carregamento XAML

Este exemplo demonstra como carregar dinamicamente um fluxo de trabalho XAML sem ter que execute a ferramenta de XamlBuildTask. Em vez disso, o exemplo chama o método de <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A> . O exemplo é um aplicativo cliente Windows Presentation Foundation (WPF) que carrega fluxos de trabalho XAML usando a <xref:System.Activities.XamlIntegration.ActivityXamlServices> classe e os executa. Depois que foram carregados usando a classe de <xref:System.Activities.XamlIntegration.ActivityXamlServices> , <xref:System.Activities.DynamicActivity%601> é retornado que pode ser executado.

#### <a name="to-use-this-sample"></a>Para usar este exemplo

1. Usando o Visual Studio 2010, abra o arquivo de solução LoadFromXAML. sln.

2. Para criar a solução, pressione CTRL+SHIFT+B.

3. Para executar a solução, pressione CTRL+F5.

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Built-InActivities\DynamicActivity\LoadFromXAML`
