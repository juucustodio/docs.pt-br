---
description: 'Saiba mais sobre: resolvedor de indicadores para WorkflowHostingEndpoint'
title: Resolução do indexador para WorkflowHostingEndpoint
ms.date: 03/30/2017
ms.assetid: 97fd5816-935e-4625-ad04-e6f6befa07de
ms.openlocfilehash: fc2a21a33560452b141069e88b4d7ff816712d96
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99653804"
---
# <a name="bookmark-resolver-for-workflowhostingendpoint"></a>Resolução do indexador para WorkflowHostingEndpoint

Este exemplo demonstra como <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> pode ser usado com <xref:System.ServiceModel.Activities.WorkflowServiceHost> para criar instâncias de fluxo de trabalho.  
  
## <a name="demonstrates"></a>Demonstra  

 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>, <xref:System.ServiceModel.Activities.WorkflowServiceHost>  
  
## <a name="discussion"></a>Discussão  

 Este exemplo usa <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> para criar instâncias de fluxo de trabalho usando <xref:System.ServiceModel.Activities.WorkflowServiceHost>hospedados. <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> é um ponto de extensibilidade para <xref:System.ServiceModel.Activities.WorkflowServiceHost> que pode ser usada nos seguintes situações:  
  
- Criando novas instâncias de fluxo de trabalho.  
  
- Continuando indicadores na instância de fluxo de trabalho hospedada em <xref:System.ServiceModel.Activities.WorkflowServiceHost>.  
  
 O ponto final de exemplo que é expõe incluídas o contrato que fornece operações para criar um fluxo de trabalho e retorna a identificação da instância ou cria uma instância com uma identificação específica O aplicativo de console do exemplo cria uma instância de <xref:System.ServiceModel.Activities.WorkflowServiceHost> com uma definição de fluxo de trabalho e adiciona `CreationEndpoint` para o host. Então chama a operação de `Create` no ponto de extremidade para criar uma nova instância de fluxo de trabalho.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo  
  
1. Compile a solução.  
  
2. Execute o aplicativo. O console de `CreationEndpoint` mostra uma mensagem que inclui a ID da instância quando a instância do fluxo de trabalho é criada. A mensagem "Olá, Mundo!" é impresso pela instância de fluxo de trabalho.  
  
> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Execution\CreationEndpoint`
