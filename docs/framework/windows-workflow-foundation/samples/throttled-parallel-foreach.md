---
description: 'Saiba mais sobre: ForEach paralelo limitado'
title: Paralelo estrangulado ForEach
ms.date: 03/30/2017
ms.assetid: f2855b5f-e9a7-433d-96a4-40fc31025215
ms.openlocfilehash: 2c1d1386f0b8c5b3c68d60bc83386ccfdf5e7875
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99741673"
---
# <a name="throttled-parallel-foreach"></a>Paralelo estrangulado ForEach

A atividade de `ThrottleParallelForEach` é semelhante à atividade de <xref:System.Activities.Statements.ParallelForEach%601> com uma exceção que permite que define um fator de simultaneidade para restringir o número de ramificações simultâneas para executar. A atividade de `ThrottleParallelForEach` deriva de <xref:System.Activities.NativeActivity>, porque precisa agendar outras atividades (as atividades filho) e isso é acessível somente por meio da classe <xref:System.Activities.NativeActivityContext> .

## <a name="projects"></a>Projetos

|**ProjectName**|**Descrição**|**Arquivos de chave**|
|-|-|-|
|ThrottledParallelForEach|Contém a atividade de `ThrottledParallelForEach` e o designer.|ThrottledParallelForEach.cs<br /><br /> A definição de atividade de `ThrottledParallelForEach` .|
|CodeTestClient|Exemplo do aplicativo cliente que configura e executa um fluxo de trabalho com `ThrottledParallelForEach` usando o código obrigatório.|Module.vb<br /><br /> Define e executa uma instância de fluxo de trabalho de exemplo.|

## <a name="to-use-this-sample"></a>Para usar este exemplo

1. Usando o Visual Studio 2010, abra o arquivo ThrottledParallelForEach. sln.

2. Para criar a solução, pressione CTRL+SHIFT+B.

3. Para executar a solução, pressione F5.

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\ThrottledParallelForEach`
