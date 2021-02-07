---
description: 'Saiba mais sobre: gerenciamento de instância suspenso'
title: Gerenciamento suspenso da instância
ms.date: 03/30/2017
ms.assetid: f5ca3faa-ba1f-4857-b92c-d927e4b29598
ms.openlocfilehash: d68dd8b61b6e0e7a618cf05f1df07e58ab75e27f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99741712"
---
# <a name="suspended-instance-management"></a>Gerenciamento suspenso da instância

Este exemplo demonstra como gerenciar as instâncias de fluxo de trabalho que foram suspensas.  A ação padrão para <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> é `AbandonAndSuspend`. Isso significa que por padrão, as exceções não tratadas lançadas de uma instância de fluxo de trabalho hospedada em <xref:System.ServiceModel.WorkflowServiceHost> causarão a instância a ser descartado de memória (abandonada) e de bens/versão armazenado de instância a ser marcada como suspendida. Uma instância suspendida de fluxo de trabalho não poderá executar até que estado unsuspended.

 O exemplo mostra como um utilitário de linha de comando pode ser implementado para consultar instâncias suspensas, e como conceder ao usuário a opção continuar ou finalizar a instância. Nesse exemplo, um serviço de fluxo de trabalho intencionalmente lança uma exceção, fazendo com que fique suspenso. O utilitário de linha de comando pode então ser usado para consultar a instância e posteriormente para continuar ou finalizar a instância.

## <a name="demonstrates"></a>Demonstra

 <xref:System.ServiceModel.WorkflowServiceHost> com <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> e <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> em Windows Workflow Foundation (WF).

## <a name="discussion"></a>Discussão

 O utilitário de linha de comando implementado nesse exemplo é específico da implementação da instância do SQL que envia em [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]. Se você tiver uma implementação personalizada de armazenamento de instância, então você pode adaptar este utilitário substituindo as implementações de `WorkflowInstanceCommand` no exemplo com as implementações que são específicas para seu armazenamento de instância.

 Os comandos SQL fornecidos de blocos de implementação no armazenamento da instância do SQL diretamente listar suspenderam instâncias, e depende em <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> adicionado a <xref:System.ServiceModel.WorkflowServiceHost> para continuar ou finalizar as instâncias.

#### <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo

1. Esse exemplo requer que os seguintes componentes do Windows estão ativados:

    1. Servidor das filas de mensagens da Microsoft (MSMQ)

    2. SQL Server Express

2. Configurar o base de dados SQL Server.

    1. Em um prompt de comando do Visual Studio 2010, execute "setup. cmd" no diretório de exemplo SuspendedInstanceManagement, que faz o seguinte:

        1. Cria um base de dados de persistência usando o SQL Server Express. Se o base de dados de persistência já existir, então é solto e re-criada

        2. Configura de base de dados para persistência.

        3. Adiciona o IIS APPPOOL \ AUTORIDADE de DefaultAppPool e NT \ serviço de rede para a função de InstanceStoreUsers que foi definida para configurar o base de dados para persistência.

3. Configurar a fila de serviço.

    1. No Visual Studio 2010, clique com o botão direito do mouse no projeto **SampleWorkflowApp** e clique em **definir como projeto de inicialização**.

    2. Compile e execute o SampleWorkflowApp pressionando **F5**. Isso criará a fila necessário.

    3. Pressione **Enter** para parar o SampleWorkflowApp.

    4. Abra o console de Gerenciamento do Computador executando Compmgmt.msc de um prompt de comando.

    5. Expanda **serviço e aplicativos**, **enfileiramento de mensagens**, **filas privadas**.

    6. Clique com o botão direito do mouse na fila **ReceiveTx** e selecione **Propriedades**.

    7. Selecione a **guia Segurança** e permitir **que todos** tenham permissões para **receber mensagens**, **Inspecionar mensagem** e **Enviar mensagem**.

4. Agora, executar o exemplo.

    1. No Visual Studio 2010, execute o projeto SampleWorkflowApp novamente sem Depurar pressionando **Ctrl + F5**. Dois endereços de ponto de extremidade será impresso na janela do console: um para o ponto final do aplicativo e então outro de <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>. Uma instância de fluxo de trabalho é criada em seguida, e os registros de controle para essa instância aparecerá na janela do console. A instância de fluxo de trabalho irá acionar uma exceção que causou a instância a ser suspendida e anuladas.

    2. O utilitário de linha de comando pode então ser usado para executar uma ação adicional em uma destas instâncias. A sintaxe para argumentos de linha de comando é como o follows::

         `SuspendedInstanceManagement -Command:[CommandName] -Server:[ServerName] -Database:[DatabaseName] -InstanceId:[InstanceId]`

         Os comandos são suportados: `Query`, `Resume`, e `Terminate`.  Alterne de InstanceId é necessário somente para `Resume` e operações de `Terminate` .

#### <a name="to-cleanup-optional"></a>A limpeza (opcional)

1. Abra o console de Gerenciamento do Computador executando Compmgmt.msc de um prompt de comando `vs2010` .

2. Expanda **serviço e aplicativos**, **enfileiramento de mensagens**, **filas privadas**.

3. Exclua a fila **ReceiveTx** .

4. Para remover o base de dados de persistência, cleanup.cmd execução.

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Application\SuspendedInstanceManagement`
