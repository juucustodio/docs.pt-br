---
description: 'Saiba mais sobre: serviços WCF e rastreamento de eventos para Windows'
title: Serviços e rastreamento de eventos WCF para Windows
ms.date: 03/30/2017
ms.assetid: eda4355d-0bd0-4dc9-80a2-d2c832152272
ms.openlocfilehash: ba2d323322a2d3481f1414ac58fbf0b44508bb03
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755675"
---
# <a name="wcf-services-and-event-tracing-for-windows"></a>Serviços e rastreamento de eventos WCF para Windows

Este exemplo demonstra como usar o rastreamento analítico no Windows Communication Foundation (WCF) para emitir eventos no ETW (rastreamento de eventos para Windows). Os rastreamentos analíticos são eventos emitidos em pontos-chave na pilha do WCF que permitem a solução de problemas de serviços WCF no ambiente de produção.

 O rastreamento analítico nos serviços WCF é o rastreamento que pode ser ativado em um ambiente de produção com impacto mínimo sobre o desempenho. Esses rastreamentos são emitidos como eventos para uma sessão do ETW.

 Este exemplo inclui um serviço WCF básico no qual os eventos são emitidos do serviço para o log de eventos, que pode ser exibido usando Visualizador de Eventos. Também é possível iniciar uma sessão de ETW dedicada que escuta eventos do serviço WCF. O exemplo inclui um script para criar uma sessão de ETW dedicada que armazena eventos em um arquivo binário que pode ser lido usando Visualizador de Eventos.

#### <a name="to-use-this-sample"></a>Para usar este exemplo

1. Usando o Visual Studio 2012, abra o arquivo de solução EtwAnalyticTraceSample. sln.

2. Para criar a solução, pressione CTRL+SHIFT+B.

3. Para executar a solução, pressione CTRL+F5.

     No navegador da Web, clique em **Calculator. svc**. O URI do documento WSDL para o serviço deve aparecer no navegador. Copie esse URI.

     Por padrão, o serviço começa a escutar solicitações na porta 1378 `http://localhost:1378/Calculator.svc` .

4. Execute o cliente de teste do WCF (WcfTestClient.exe).

     O cliente de teste do WCF (WcfTestClient.exe) está localizado em `\<Visual Studio 2012 Install Dir>\Common7\IDE\WcfTestClient.exe` .  O dir de instalação padrão do Visual Studio 2012 é `C:\Program Files\Microsoft Visual Studio 10.0` .

5. No cliente de teste do WCF, adicione o serviço selecionando **arquivo** e, em seguida, **Adicionar serviço**.

     Adicione o endereço do ponto de extremidade na caixa de entrada. O padrão é `http://localhost:1378/Calculator.svc`.

6. Abra o aplicativo visualizador de eventos.

     Antes de invocar o serviço, inicie Visualizador de Eventos e verifique se o log de eventos está escutando eventos emitidos do serviço WCF.

7. No menu **Iniciar** , selecione **Ferramentas administrativas** e, em seguida, **Visualizador de eventos**.  Habilite os logs **analíticos** e de **depuração** .

8. No modo de exibição de árvore no Visualizador de Eventos, navegue até **Visualizador de eventos**, **logs de aplicativos e serviços**, **Microsoft**, **Windows** e, em seguida, **servidor de aplicativos-aplicativos**. Clique com o botão direito do mouse em **servidor de aplicativos**, selecione **Exibir** e, em seguida, **Mostrar logs analíticos e de depuração**.

     Verifique se a opção **Mostrar logs analíticos e de depuração** está marcada.

9. Habilite o log **analítico** .

     No modo de exibição de árvore no Visualizador de Eventos, navegue até **Visualizador de eventos**, **logs de aplicativos e serviços**, **Microsoft**, **Windows** e, em seguida, **servidor de aplicativos-aplicativos**. Clique com o botão direito do mouse em **analítica** e selecione **habilitar log**.

#### <a name="to-test-the-service"></a>Para testar o serviço

1. Volte para o cliente de teste do WCF e clique duas vezes `Divide` e mantenha os valores padrão, que especificam um denominador de 0.

     Se o denominador for 0, o serviço lançará uma falha.

2. Observe os eventos emitidos do serviço.

     Volte para Visualizador de Eventos e navegue até **Visualizador de eventos**, **logs de aplicativos e serviços**, **Microsoft**, **Windows** e, em seguida, **aplicativos de servidor de aplicativos**. Clique com o botão direito do mouse em **analítica** e selecione **Atualizar**.

     Os eventos de rastreamento analítico do WCF são exibidos no Visualizador de eventos. Observe que, como uma falha foi gerada pelo serviço, um evento de rastreamento de erro é exibido no Visualizador de eventos.

3. Repita as etapas 1 e 2, mas com entradas válidas. O valor do `N2` parâmetro pode ser qualquer número diferente de 0.

     Atualize o canal analítico para exibir os eventos do WCF não inclua nenhum evento de erro.

 O exemplo demonstra os eventos de rastreamento analítico emitidos de um serviço WCF.

#### <a name="to-cleanup-optional"></a>A limpeza (opcional)

1. Visualizador de EventosAberto.

2. Navegue até **Visualizador de eventos**, **logs de aplicativos e serviços**, **Microsoft**, **Windows** e, em seguida, aplicativos **-Server-** Applications. Clique com o botão direito do mouse em **analítica** e selecione **desabilitar log**.

3. Navegue até **Visualizador de eventos**, **logs de aplicativos e serviços**, **Microsoft**, **Windows** e, em seguida, aplicativos **-Server-** Applications. Clique com o botão direito do mouse em **analítica** e selecione **limpar log**.

4. Escolha a opção **limpar** para limpar os eventos.

> [!IMPORTANT]
> Os exemplos podem mais ser instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ETWTracing`  
  
## <a name="see-also"></a>Consulte também

- [AppFabric que monitora Exemplos](/previous-versions/appfabric/ff383407(v=azure.10))
