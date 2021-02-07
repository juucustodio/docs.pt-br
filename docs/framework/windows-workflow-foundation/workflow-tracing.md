---
description: 'Saiba mais sobre: rastreamento de fluxo de trabalho'
title: Rastreamento de fluxo de trabalho
ms.date: 03/30/2017
ms.assetid: 18737989-0502-4367-b5f6-617ebfb77c96
ms.openlocfilehash: 6d976cce1310a072f8d1c98db138696921b382c2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754843"
---
# <a name="workflow-tracing"></a>Rastreamento de fluxo de trabalho

Oferece de rastreamento de fluxo de trabalho uma maneira para capturar informações de diagnóstico usando os ouvintes de rastreamento do .NET Framework. O rastreamento podem ser ativado se é um problema detectado com o aplicativo e desativado novamente o problema é resolvido uma vez. Há duas maneiras que você pode ativar o rastreamento de depuração para fluxos de trabalho. Você poderá configurá-lo usando o visualizador de rastreamento do evento ou você pode usar <xref:System.Diagnostics> para enviar os eventos de rastreamento em um arquivo.  
  
## <a name="enabling-debug-tracing-in-etw"></a>Ativar o rastreamento de depuração em ETW  

 Para ativar o rastreamento usando ETW, ative o canal de depuração no visualizador de eventos:  
  
1. Navegue para o nó analítico e de depuração dos logs no visualizador de eventos.  
  
2. No modo de exibição de árvore no Visualizador de Eventos, navegue até **Visualizador de eventos->logs de aplicativos e serviços->Microsoft->Windows->Application Server-Applications**. Clique com o botão direito do mouse em **servidor de aplicativos** e selecione **Exibir->Mostrar logs analíticos e de depuração**. Clique com o botão direito do mouse em **depurar** e selecione **habilitar log**.  
  
3. Quando um fluxo de trabalho executa a depuração e os rastreamentos são emitidas ao canal de depuração de ETW, podem ser exibidos no visualizador de eventos. Navegue até **Visualizador de eventos->logs de serviços e aplicativos->Microsoft->Windows->Application Server – Applications**. Clique com o botão direito do mouse em **depurar** e selecione **Atualizar**.  
  
4. O tamanho do buffer analítico padrão de rastreamento é apenas 4 quilobytes de (KB); é recomendável aumentar o tamanho para 32 KB. Para fazer isso, execute as seguintes etapas.  
  
    1. Execute o seguinte comando no diretório atual do framework (por exemplo, C:\Windows\Microsoft.NET\Framework\v4.0 .21203): `wevtutil um Microsoft.Windows.ApplicationServer.Applications.man`  
  
    2. Altere o \<bufferSize> valor no arquivo Windows. ApplicationServer. Applications. Man para 32.  
  
        ```xml  
        <channel name="Microsoft-Windows-Application Server-Applications/Analytic" chid="ANALYTIC_CHANNEL" symbol="ANALYTIC_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ANALYTIC_CHANNEL.message)" >  
                    <publishing>  
                      <bufferSize>32</bufferSize>  
                    </publishing>  
                  </channel>  
        ```  
  
    3. Execute o seguinte comando no diretório atual do framework (por exemplo, C:\Windows\Microsoft.NET\Framework\v4.0 .21203): `wevtutil im Microsoft.Windows.ApplicationServer.Applications.man`  
  
> [!NOTE]
> Se você estiver usando o perfil de cliente .NET Framework 4, deverá primeiro registrar o manifesto do ETW executando o seguinte comando no diretório .NET Framework 4: `ServiceModelReg.exe –i –c:etw`  
  
## <a name="enabling-debug-tracing-using-systemdiagnostics"></a>Ativar o rastreamento de depuração usando System.Diagnostics  

 Essas ouvintes podem ser configuradas no arquivo App.config do aplicativo de fluxo de trabalho, ou no Web.config para um serviço de fluxo de trabalho. Neste exemplo, um <xref:System.Diagnostics.TextWriterTraceListener> é configurado para salvar informações de rastreamento no arquivo de MyTraceLog.txt no diretório atual.  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="System.Activities" switchValue="Information">  
        <listeners>  
          <add name="textListener" />  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"  
           type="System.Diagnostics.TextWriterTraceListener"  
           initializeData="MyTraceLog.txt"  
           traceOutputOptions="ProcessId, DateTime" />  
    </sharedListeners>  
    <trace autoflush="true" indentsize="4">  
      <listeners>  
        <add name="textListener" />  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também

- [Monitoramento do Windows Server app Fabric](/previous-versions/appfabric/ee677251(v=azure.10))
- [Monitorando aplicativos com o app Fabric](/previous-versions/appfabric/ee677276(v=azure.10))
