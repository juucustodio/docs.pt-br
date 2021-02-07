---
description: 'Saiba mais sobre: rastreamento analítico do WCF'
title: Rastreamento analítico do WCF
ms.date: 03/30/2017
ms.assetid: 6029c7c7-3515-4d36-9d43-13e8f4971790
ms.openlocfilehash: 1f5ec26828bba99a127fea6a81f57fed717943a2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755688"
---
# <a name="wcf-analytic-tracing"></a>Rastreamento analítico do WCF

Este exemplo demonstra como adicionar seus próprios eventos de rastreamento no fluxo de rastreamentos analíticos que Windows Communication Foundation (WCF) grava no ETW no [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] . Os rastreamentos analíticos destinam-se a facilitar a visibilidade de seus serviços sem pagar uma penalidade de alto desempenho. Este exemplo mostra como usar as <xref:System.Diagnostics.Eventing?displayProperty=nameWithType> APIs para gravar eventos que se integram aos serviços WCF.  
  
 Para obter mais informações sobre as <xref:System.Diagnostics.Eventing?displayProperty=nameWithType> APIs, consulte <xref:System.Diagnostics.Eventing?displayProperty=nameWithType> .  
  
 Para saber mais sobre o rastreamento de eventos no Windows, consulte [melhorar a depuração e o ajuste de desempenho com o ETW](/archive/msdn-magazine/2007/april/event-tracing-improve-debugging-and-performance-tuning-with-etw).  
  
## <a name="disposing-eventprovider"></a>Descartando EventProvider  

 Este exemplo usa a <xref:System.Diagnostics.Eventing.EventProvider?displayProperty=nameWithType> classe, que implementa <xref:System.IDisposable?displayProperty=nameWithType> . Ao implementar o rastreamento para um serviço WCF, é provável que você possa usar os <xref:System.Diagnostics.Eventing.EventProvider> recursos do tempo de vida do serviço. Por esse motivo, e para facilitar a leitura, esse exemplo nunca descarta o encapsulado <xref:System.Diagnostics.Eventing.EventProvider> . Se, por algum motivo, seu serviço tiver requisitos diferentes para rastreamento e você precisar descartar esse recurso, você deverá modificar esse exemplo de acordo com as práticas recomendadas para descartar recursos não gerenciados. Para obter mais informações sobre como descartar recursos não gerenciados, consulte [implementando um método Dispose](../../../standard/garbage-collection/implementing-dispose.md).  
  
## <a name="self-hosting-vs-web-hosting"></a>Self-Hosting vs. hospedagem na Web  

 Para serviços hospedados na Web, os rastreamentos analíticos do WCF fornecem um campo, chamado "HostReference", que é usado para identificar o serviço que está emitindo os rastreamentos. Os rastreamentos extensível de usuário podem participar desse modelo e este exemplo demonstra as práticas recomendadas para fazer isso. O formato de uma referência de host Web quando o caractere do pipe ' &#124; ' aparece na cadeia de caracteres resultante pode ser qualquer um dos seguintes:  
  
- Se o aplicativo não estiver na raiz.  
  
     \<SiteName>\<ApplicationVirtualPath>&#124;\<ServiceVirtualPath>&#124;\<ServiceName>  
  
- Se o aplicativo estiver na raiz.  
  
     \<SiteName>&#124;\<ServiceVirtualPath>&#124;\<ServiceName>  
  
 Para serviços hospedados internamente, os rastreamentos analíticos do WCF não preenchem o campo "HostReference". A `WCFUserEventProvider` classe neste exemplo se comporta de forma consistente quando usada por um serviço hospedado internamente.  
  
## <a name="custom-event-details"></a>Detalhes do evento personalizado  

 O manifesto do provedor de eventos do ETW do WCF define três eventos que são criados para serem emitidos por autores de serviço do WCF de dentro do código de serviço. A tabela a seguir mostra uma divisão dos três eventos.  
  
|Evento|Descrição|ID do evento|  
|-----------|-----------------|--------------|  
|UserDefinedInformationEventOccurred|Emita esse evento quando algo de observação acontecer em seu serviço que não é um problema. Por exemplo, você pode emitir um evento depois de fazer uma chamada com êxito para um banco de dados.|301|  
|UserDefinedWarningOccurred|Emita esse evento quando ocorrer um problema que possa resultar em uma falha no futuro. Por exemplo, você pode emitir um evento de aviso quando uma chamada a um banco de dados falha, mas você conseguiu recuperar-se voltando a um armazenamento de dados redundante.|302|  
|UserDefinedErrorOccurred|Emita este evento quando o serviço não se comportar conforme o esperado. Por exemplo, você poderá emitir um evento se uma chamada a um banco de dados falhar e não for possível recuperar os dados de outro lugar.|303|  
  
#### <a name="to-use-this-sample"></a>Para usar este exemplo  
  
1. Usando o Visual Studio 2012, abra o arquivo de solução WCFAnalyticTracingExtensibility. sln.  
  
2. Para criar a solução, pressione CTRL+SHIFT+B.  
  
3. Para executar a solução, pressione CTRL+F5.  
  
     No navegador da Web, clique em **Calculator. svc**. O URI do documento WSDL para o serviço deve aparecer no navegador. Copie esse URI.  
  
4. Execute o cliente de teste do WCF (WcfTestClient.exe).  
  
     O cliente de teste do WCF (WcfTestClient.exe) está localizado em `\<Visual Studio 2012 Install Dir>\Common7\IDE\WcfTestClient.exe` . O dir de instalação padrão do Visual Studio 2012 é `C:\Program Files\Microsoft Visual Studio 10.0` .  
  
5. No cliente de teste do WCF, adicione o serviço selecionando **arquivo** e, em seguida, **Adicionar serviço**.  
  
     Adicione o endereço do ponto de extremidade na caixa de entrada.  
  
6. Clique em **OK** para fechar o diálogo.  
  
     O serviço ICalculator é adicionado no painel esquerdo em **meus projetos de serviço**.  
  
7. Abra o aplicativo visualizador de eventos.  
  
     Antes de invocar o serviço, inicie Visualizador de Eventos e verifique se o log de eventos está escutando eventos emitidos do serviço WCF.  
  
8. No menu **Iniciar** , selecione **Ferramentas administrativas** e, em seguida, **Visualizador de eventos**. Habilite os logs **analíticos** e de **depuração** .  
  
9. No modo de exibição de árvore no Visualizador de Eventos, navegue até **Visualizador de eventos**, **logs de aplicativos e serviços**, **Microsoft**, **Windows** e, em seguida, **servidor de aplicativos-aplicativos**. Clique com o botão direito do mouse em **servidor de aplicativos**, selecione **Exibir** e, em seguida, **Mostrar logs analíticos e de depuração**.  
  
     Verifique se a opção **Mostrar logs analíticos e de depuração** está marcada. Habilite o log **analítico** .  
  
     No modo de exibição de árvore no Visualizador de Eventos, navegue até **Visualizador de eventos**, **logs de aplicativos e serviços**, **Microsoft**, **Windows**, **servidor de aplicativos-aplicativos** e, em seguida, **análise**. Clique com o botão direito do mouse em **analítica** e selecione **habilitar log**.  
  
10. Testar o serviço usando a Test usuário.  
  
    1. No cliente de teste do WCF, clique duas vezes em **Adicionar ()** no nó do serviço ICalculator.  
  
         O método **Add ()** aparece no painel direito com dois parâmetros.  
  
    2. Digite 2 para o primeiro parâmetro e 3 para o segundo parâmetro.  
  
    3. Clique em **invocar** para invocar o método.  
  
11. Vá para a janela de **Visualizador de eventos** que você já abriu. Navegue até **Visualizador de eventos**, **logs de aplicativos e serviços**, **Microsoft**, **Windows**, **servidor de aplicativos-aplicativos**.  
  
12. Clique com o botão direito do mouse no nó **analítico** e selecione **Atualizar**.  
  
     Os eventos aparecem no painel direito.  
  
13. Localize o evento com a ID 303 e clique duas vezes nele para abri-lo e inspecionar seu conteúdo.  
  
     Esse evento foi emitido pelo `Add()` método do serviço ICalculator e tem uma carga igual a "2 + 3 = 5".  
  
#### <a name="to-clean-up-optional"></a>Para limpar (opcional)  
  
1. Abra o **Visualizador de Eventos**.  
  
2. Navegue até **Visualizador de eventos**, **logs de aplicativos e serviços**, **Microsoft**, **Windows** e, em seguida, aplicativos **-Server-** Applications. Clique com o botão direito do mouse em **analítica** e selecione **desabilitar log**.  
  
3. Navegue até **Visualizador de eventos**, **logs de aplicativos e serviços**, **Microsoft**, **Windows**, **Application-Server-Applications** e, em seguida, **análise**. Clique com o botão direito do mouse em **analítica** e selecione **limpar log**.  
  
4. Clique em **limpar** para limpar os eventos.  
  
## <a name="known-issue"></a>Problema conhecido  

 Há um problema conhecido no **Visualizador de eventos** em que pode falhar ao decodificar eventos ETW. Você pode ver uma mensagem de erro que diz: "a descrição para a ID \<id> de evento da origem Microsoft-Windows-Application Server-Applications não pode ser encontrada. O componente que gera esse evento não está instalado no computador local ou a instalação está corrompida. Você pode instalar ou reparar o componente no computador local. " Se você encontrar esse erro, selecione **Atualizar** no menu **ações** . O evento deve então ser decodificado corretamente.  
  
> [!IMPORTANT]
> Os exemplos podem mais ser instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ETWTrace`  
  
## <a name="see-also"></a>Consulte também

- [AppFabric que monitora Exemplos](/previous-versions/appfabric/ff383407(v=azure.10))
