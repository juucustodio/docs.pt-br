---
description: 'Saiba mais sobre: fábrica de canais de configuração'
title: Factory do canal de configuração
ms.date: 03/30/2017
ms.assetid: 3b749493-bd8a-4ccb-893e-5948901a1486
ms.openlocfilehash: 7868f9b9e3a97a67ac513668be09de4d9c5073bf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99778406"
---
# <a name="configuration-channel-factory"></a>Factory do canal de configuração

Este exemplo aborda o uso do <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> . O <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> permite o gerenciamento central da configuração do cliente WCF. Isso também pode ser útil em cenários em que a configuração é selecionada ou alterada após o tempo de carregamento do domínio do aplicativo.

## <a name="demonstrates"></a>Demonstra

 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>

## <a name="discussion"></a>Discussão

 Este exemplo mostra como usar <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> o para adicionar um arquivo de configuração específico a um aplicativo cliente, sem precisar usar o arquivo de configuração de aplicativo padrão.

 O exemplo consiste em dois projetos. O primeiro projeto é um serviço simples que é executado para responder às mensagens provenientes dos clientes. O segundo projeto é um aplicativo cliente que cria dois <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> objetos usando um <xref:System.Configuration.ExeConfigurationFileMap> para o arquivo de configuração Test.config e os usa para se comunicar com o serviço. Ambos os clientes se comunicam com o serviço usando a configuração especificada em Test.config.

 O código a seguir adiciona um arquivo de configuração personalizado a um aplicativo cliente.

```csharp
ExeConfigurationFileMap fileMap = new ExeConfigurationFileMap();
fileMap.ExeConfigFilename = "Test.config";
Configuration newConfiguration = ConfigurationManager.OpenMappedExeConfiguration(fileMap, ConfigurationUserLevel.None);

ConfigurationChannelFactory<ICalculatorChannel> factory1 = new ConfigurationChannelFactory<ICalculatorChannel>("endpoint1", newConfiguration, new EndpointAddress("http://localhost:8000/servicemodelsamples/service"));
ICalculatorChannel client1 = factory1.CreateChannel();
```

#### <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo

1. Abra o Visual Studio 2012 com privilégios de administrador.

2. Clique com o botão direito do mouse na solução ConfigurationChannelFactory (2 projetos) e selecione **Propriedades**.

3. Em **Propriedades comuns**, selecione **projeto de inicialização** e clique em **vários projetos de inicialização**.

4. Mova o projeto de **serviço** para o início da lista, com a **ação ' Iniciar '** e, em seguida, mova o projeto **cliente** após o projeto de **serviço** , também com a **ação ' Iniciar '**, para que o projeto **cliente** seja executado após o projeto de **serviço** .

5. Clique em **OK** e pressione F5 (ou CTRL + F5) para executar o exemplo.

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\ConfigurationChannelFactory`
