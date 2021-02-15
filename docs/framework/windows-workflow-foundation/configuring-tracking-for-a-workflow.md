---
description: 'Saiba mais sobre: Configurando o acompanhamento de um fluxo de trabalho'
title: Configurando o rastreamento para um fluxo de trabalho
ms.date: 03/30/2017
ms.assetid: 905adcc9-30a0-4918-acd6-563f86db988a
ms.openlocfilehash: 061a0edf107296e04d86ed1a50b9a8bfefd7bfce
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792759"
---
# <a name="configuring-tracking-for-a-workflow"></a>Configurando o rastreamento para um fluxo de trabalho

Um fluxo de trabalho pode executar em três maneiras:

- Hospedada no <xref:System.ServiceModel.Activities.WorkflowServiceHost>

- Executado como <xref:System.Activities.WorkflowApplication>

- Executado diretamente usando <xref:System.Activities.WorkflowInvoker>

Dependendo do fluxo de trabalho que hospeda a opção, um participante de rastreamento pode ser adicionado ao código ou em um arquivo de configuração. Este tópico descreve como controlando é configurado adicionando um participante de rastreamento a <xref:System.Activities.WorkflowApplication> e a <xref:System.ServiceModel.Activities.WorkflowServiceHost>, e como ativar o rastreamento para usar <xref:System.Activities.WorkflowInvoker>.

## <a name="configuring-workflow-application-tracking"></a>Configurando o rastreamento de aplicativo de fluxo de trabalho

Um fluxo de trabalho pode executar usando a classe de <xref:System.Activities.WorkflowApplication> . Este tópico demonstra como controlando é configurado para um aplicativo de fluxo de trabalho [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] adicionando um participante de rastreamento para o host do fluxo de trabalho <xref:System.Activities.WorkflowApplication> . Nesse caso, o fluxo de trabalho é executado como um aplicativo de fluxo de trabalho. Você configura um aplicativo de fluxo de trabalho com o código (em vez de usar um arquivo de configuração), que é um arquivo .exe são hospedado usando a classe de <xref:System.Activities.WorkflowApplication> . O participante de rastreamento é adicionado como uma extensão para instância de <xref:System.Activities.WorkflowApplication> . Isso é feito adicionando <xref:System.Activities.Tracking.TrackingParticipant> a coleção de extensões para a instância de WorkflowApplication.

Para um aplicativo de fluxo de trabalho, você pode adicionar a extensão do comportamento de <xref:System.Activities.Tracking.EtwTrackingParticipant> conforme mostrado no código a seguir.

```csharp
LogActivity activity = new LogActivity();

WorkflowApplication instance = new WorkflowApplication(activity);
EtwTrackingParticipant trackingParticipant =
    new EtwTrackingParticipant
{

        TrackingProfile = new TrackingProfile
           {
               Name = "SampleTrackingProfile",
               ActivityDefinitionId = "ProcessOrder",
               Queries = new WorkflowInstanceQuery
               {
                  States = { "*" }
              }
          }
       };
instance.Extensions.Add(trackingParticipant);
```

### <a name="configuring-workflow-service-tracking"></a>Configurando acompanhar de Serviço de Fluxo de Trabalho

Um fluxo de trabalho pode ser exposto como um serviço WCF quando hospedado no <xref:System.ServiceModel.Activities.WorkflowServiceHost> host de serviço. <xref:System.ServiceModel.Activities.WorkflowServiceHost> é uma implementação específica do .NET ServiceHost para um serviço fluxo de trabalho- base. Esta seção explica como configurar o controle para uma execução de serviço do fluxo de trabalho [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] em <xref:System.ServiceModel.Activities.WorkflowServiceHost>. É configurada por um arquivo web.config (para um serviço web hospedado) ou um arquivo App.config (para um serviço hospedado em um aplicativo autônomo, como um aplicativo de console) especificando um comportamento do serviço ou com o código adicionando um comportamento acompanhamento- específico à coleção de <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A> para o host serviço.

Para um serviço de fluxo de trabalho hospedado no <xref:System.ServiceModel.WorkflowServiceHost> , você pode adicionar o <xref:System.Activities.Tracking.EtwTrackingParticipant> usando o `behavior` elemento <> em um arquivo de configuração, conforme mostrado no exemplo a seguir.

```xml
<behaviors>
   <serviceBehaviors>
        <behavior>
          <etwTracking profileName="Sample Tracking Profile" />
        </behavior>
   </serviceBehaviors>
</behaviors>
```

Como alternativa, para um serviço de fluxo de trabalho hospedado em <xref:System.ServiceModel.WorkflowServiceHost>, você pode adicionar a extensão do comportamento de <xref:System.Activities.Tracking.EtwTrackingParticipant> com o código. Para adicionar um participante personalizado de rastreamento, criar uma nova extensão do comportamento e adicioná-lo a <xref:System.ServiceModel.ServiceHost> conforme mostrado no código de exemplo a seguir.

> [!NOTE]
> Se você quiser exibir o código de exemplo que mostra como criar um elemento de comportamento personalizado que adiciona um participante de acompanhamento personalizado, consulte os exemplos de [acompanhamento](./samples/tracking.md) .

```csharp
ServiceHost svcHost = new ServiceHost(typeof(WorkflowService), new
                                 Uri("http://localhost:8001/Sample"));
EtwTrackingBehavior trackingBehavior =
    new EtwTrackingBehavior
    {
        ProfileName = "Sample Tracking Profile"
    };
svcHost.Description.Behaviors.Add(trackingBehavior);
svcHost.Open();
```

O participante de rastreamento é adicionado ao host serviço de fluxo de trabalho como uma extensão para o comportamento.

Este exemplo de código abaixo mostra como ler um perfil de rastreamento do arquivo de configuração.

```csharp
TrackingProfile GetProfile(string profileName, string displayName)
        {
            TrackingProfile trackingProfile = null;
            TrackingSection trackingSection = (TrackingSection)WebConfigurationManager.GetSection("system.serviceModel/tracking");
            if (trackingSection == null)
            {
                return null;
            }

            profileName ??= "";

            //Find the profile with the specified profile name in the list of profile found in config
            var match = from p in new List<TrackingProfile>(trackingSection.TrackingProfiles)
                        where (p.Name == profileName) && ((p.ActivityDefinitionId == displayName) || (p.ActivityDefinitionId == "*"))
                        select p;

            if (match.Count() == 0)
            {
                //return an empty profile
                trackingProfile = new TrackingProfile()
                {
                    ActivityDefinitionId = displayName
                };

            }
            else
            {
                trackingProfile = match.First();
            }

            return trackingProfile;
```

Este exemplo de código mostra como adicionar um perfil de rastreamento a um host de fluxo de trabalho.

```csharp
WorkflowServiceHost workflowServiceHost = serviceHostBase as WorkflowServiceHost;
if (null != workflowServiceHost)
{
    string workflowDisplayName = workflowServiceHost.Activity.DisplayName;
    TrackingProfile trackingProfile = GetProfile(this.profileName, workflowDisplayName);
    workflowServiceHost.WorkflowExtensions.Add(()  => new EtwTrackingParticipant {
        TrackingProfile = trackingProfile
    });
 }
```

> [!NOTE]
> Para obter mais informações sobre perfis de rastreamento, consulte [perfis de rastreamento](tracking-profiles.md).

### <a name="configuring-tracking-using-workflowinvoker"></a>Configurando o rastreamento usando WorkflowInvoker

Para configurar o rastreamento para um fluxo de trabalho foi executado usando <xref:System.Activities.WorkflowInvoker>, adicione o provedor de rastreamento como uma extensão para uma instância de <xref:System.Activities.WorkflowInvoker> . O exemplo de código a seguir é do exemplo de [rastreamento personalizado](./samples/custom-tracking.md) .

```csharp
WorkflowInvoker invoker = new WorkflowInvoker(BuildSampleWorkflow());
invoker.Extensions.Add(customTrackingParticipant);
invoker.Invoke();
```

### <a name="viewing-tracking-records-in-event-viewer"></a>Registros de exibição de rastreamento no visualizador de eventos

Há dois logs do visualizador de eventos de interesse específico exibir quando controlando a execução de WF - o log analítico e depuração de log. Ambos residem no nó Microsoft&#124;Windows&#124;aplicativo Server-Applications. Os logs dentro desta seção contêm eventos de um único aplicativo em vez de eventos que têm um impacto no sistema inteiro.

Os eventos de rastreamento de depuração são gravados no log de depuração. Para coletar eventos de rastreamento de depuração de WF no visualizador de eventos, ative o log de depuração.

1. Para abrir Visualizador de Eventos, clique em **Iniciar** e em **executar.** Na caixa de diálogo Executar, digite `eventvwr` .

2. Na caixa de diálogo Visualizador de Eventos, expanda o nó **logs de aplicativos e serviços** .

3. Expanda os nós **Microsoft**, **Windows** e **Application Server – Applications** .

4. Clique com o botão direito do mouse no nó de **depuração** no nó **servidor de aplicativos – aplicativos** e selecione **habilitar log**.

5. Execute o aplicativo rastreamento ativado gerar eventos de rastreamento.

6. Clique com o botão direito do mouse no nó de **depuração** e selecione **Atualizar.** Os eventos de rastreamento devem ser no centro painel visível.

WF 4 fornece um participante de rastreamento que grava registros de rastreamento a uma sessão de rastreamento (ETW de evento para o Windows). O participante de rastreamento de ETW é configurado com um perfil de rastreamento para assinar a acompanhar registros. Quando você estiver ativado, os erros que acompanham registros são emitidas a ETW. Eventos de controle de (ETW entre o intervalo de 100-113) que correspondem aos eventos de rastreamento emissores por participante de rastreamento de ETW são gravados no log analítico.

Para exibir registros de rastreamento, siga estas etapas.

1. Para abrir Visualizador de Eventos, clique em **Iniciar** e em **executar.** Na caixa de diálogo Executar, digite `eventvwr` .

2. Na caixa de diálogo Visualizador de Eventos, expanda o nó **logs de aplicativos e serviços** .

3. Expanda os nós **Microsoft**, **Windows** e **Application Server – Applications** .

4. Clique com o botão direito do mouse no nó **analítico** no nó **servidor de aplicativos – aplicativos** e selecione **habilitar log**.

5. Executar o aplicativo acompanhamento- ativado gerar registros de rastreamento.

6. Clique com o botão direito do mouse no nó **analítico** e selecione **Atualizar.** Controlar registros deve ser no centro painel visível.

A imagem a seguir mostra eventos de rastreamento no Visualizador de eventos:

![Captura de tela da Visualizador de Eventos mostrando registros de rastreamento.](./media/configuring-tracking-for-a-workflow/tracking-event-viewer.png)

### <a name="registering-an-application-specific-provider-id"></a>Registrando um ID específico do aplicativo provedor

Se os eventos precisam ser gravados em um log do aplicativo específico, siga estas etapas para registrar o novo manifesto do provedor.

1. Declare a identificação do provedor no arquivo de configuração do aplicativo.

    ```xml
    <system.serviceModel>
        <diagnostics etwProviderId="2720e974-9fe9-477a-bb60-81fe3bf91eec"/>
    </system.serviceModel>
    ```

2. Copie o arquivo de manifesto de%windir%\Microsoft.NET\Framework \\ \<latest version of [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]> \Microsoft.Windows.ApplicationServer.Applications.Man para um local temporário e renomeie-o para Microsoft.Windows.ApplicationServer.Applications_Provider1. Man

3. Altere o GUID no arquivo de manifesto a nova GUID.

    ```xml
    <provider name="Microsoft-Windows-Application Server-Applications" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}" />
    ```

4. Altere o nome do provedor se você não desejar desinstalar o provedor padrão.

    ```xml
    <provider name="Microsoft-Windows-Application Server-Applications" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}" />
    ```

5. Se você alterou o nome do provedor na etapa anterior, altere os nomes de canal no arquivo de manifesto para o novo nome do provedor.

    ```xml
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Admin" chid="ADMIN_CHANNEL" symbol="ADMIN_CHANNEL" type="Admin" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ADMIN_CHANNEL.message)" />
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Operational" chid="OPERATIONAL_CHANNEL" symbol="OPERATIONAL_CHANNEL" type="Operational" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.OPERATIONAL_CHANNEL.message)" />
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Analytic" chid="ANALYTIC_CHANNEL" symbol="ANALYTIC_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ANALYTIC_CHANNEL.message)" />
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Debug" chid="DEBUG_CHANNEL" symbol="DEBUG_CHANNEL" type="Debug" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.DEBUG_CHANNEL.message)" />
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Perf" chid="PERF_CHANNEL" symbol="PERF_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.PERF_CHANNEL.message)" />
    ```

6. Gerencia o DLL de recurso seguindo estas etapas.

    1. Instalar o Windows SDK. A SDK do Windows inclui o compilador de mensagem ([mc.exe](/windows/win32/wes/message-compiler--mc-exe-)) e o compilador de recurso ([rc.exe](/windows/win32/menurc/using-rc-the-rc-command-line-)).

    2. Em um prompt de comando do Windows SDK, execução mc.exe no novo arquivo de manifesto.

        ```console
        mc.exe Microsoft.Windows.ApplicationServer.Applications_Provider1.man
        ```

    3. Executar rc.exe no arquivo de recurso gerado na etapa anterior.

        ```console
        rc.exe  Microsoft.Windows.ApplicationServer.Applications_Provider1.rc
        ```

    4. Crie um arquivo vazio de Cs chamado NewProviderReg.cs.

    5. Criar uma DLL de recurso usando o compilador C#.

        ```console
        csc /target:library /win32res:Microsoft.Windows.ApplicationServer.Applications_Provider1.res NewProviderReg.cs /out:Microsoft.Windows.ApplicationServer.Applications_Provider1.dll
        ```

    6. Altere o recurso e o nome da DLL de mensagem no arquivo de manifesto de `Microsoft.Windows.ApplicationServer.Applications.Provider1.man` para o novo nome de dll.

        ```xml
        <provider name="Microsoft-Windows-Application Server-Applications_Provider1" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}" symbol="Microsoft_Windows_ApplicationServer_ApplicationEvents" resourceFileName="<dll directory>\Microsoft.Windows.ApplicationServer.Applications_Provider1.dll" messageFileName="<dll directory>\Microsoft.Windows.ApplicationServer.Applications_Provider1.dll" />
        ```

    7. Use [wevtutil](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732848(v=ws.10)) para registrar o manifesto.

        ```console
        wevtutil im Microsoft.Windows.ApplicationServer.Applications_Provider1.man
        ```

## <a name="see-also"></a>Consulte também

- [Monitoramento do Windows Server app Fabric](/previous-versions/appfabric/ee677251(v=azure.10))
- [Monitorando aplicativos com o app Fabric](/previous-versions/appfabric/ee677276(v=azure.10))
