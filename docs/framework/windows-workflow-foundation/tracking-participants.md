---
description: 'Saiba mais sobre: participantes de acompanhamento'
title: Participantes de rastreamento
ms.date: 03/30/2017
ms.assetid: f13e360c-eeb7-4a49-98a0-8f6a52d64f68
ms.openlocfilehash: 2fa4edd0f93e72bff0ee4c9a07ad6f6988f3e040
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755155"
---
# <a name="tracking-participants"></a>Participantes de rastreamento

Os participantes de rastreamento são os pontos de extensibilidade que permitem que um desenvolvedor de fluxo de trabalho acessar objetos de <xref:System.Activities.Tracking.InteropTrackingRecord.TrackingRecord%2A> e processe os. O [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] inclui um participante padrão de rastreamento que grava registros de rastreamento como eventos de Rastreamento de Eventos para Windows (ETW). Se isso não atender aos requisitos, você também poderá escrever um participante de rastreamento personalizado.  
  
## <a name="tracking-participants"></a>Participantes de rastreamento  

 A infraestrutura de rastreamento permite que o aplicativo de um filtro os registros de saída de rastreamento para que um participante pode assinar um subconjunto de registros. O mecanismo para aplicar um filtro é com um perfil de rastreamento.  
  
 Windows Workflow Foundation (WF) no [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] fornece um participante de rastreamento que grava os registros de controle em uma sessão de ETW. O participante é configurado em um serviço de fluxo de trabalho adicionando um comportamento acompanhamento- específico em um arquivo de configuração. Ativar um participante de rastreamento de ETW permite controlar os registros a serem exibidos no visualizador de eventos. O exemplo SDK para o rastreamento ETW- base é uma boa maneira para obter o familiarizado com rastreamento de WF usando o participante controlando ETW- base.  
  
## <a name="etw-tracking-participant"></a>Participante de rastreamento de ETW  

 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] inclui um participante de rastreamento de ETW que grava os registros de rastreamento a uma sessão de ETW. Isso é feito em uma maneira muito eficiente com um impacto mínimo o desempenho do aplicativo ou à produção de servidor. Uma vantagem de usar o participante de acompanhamento de ETW padrão é que os registros que o controle receba podem ser exibidos com o outro aplicativo e o sistema entra no visualizador de eventos do Windows.  
  
 O participante de rastreamento do padrão ETW é configurado no arquivo web.config conforme mostrado no exemplo o seguir.  
  
```xml  
<configuration>  
  <system.web>  
    <compilation debug="true" targetFramework="4.0" />  
  </system.web>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <etwTracking profileName="Sample Tracking Profile"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
   <tracking>  
      <profiles>  
        <trackingProfile name="Sample Tracking Profile">  
        ….  
       </trackingProfile>  
      </profiles>  
    </tracking>  
  </system.serviceModel>  
</configuration>  
```  
  
> [!NOTE]
> Se um nome de `trackingProfile` não for especificado, como apenas `<etwTracking/>` ou `<etwTracking profileName=""/>`, então o perfil padrão de rastreamento instalado com [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] no arquivo Machine.config é usado.  
  
 No arquivo Machine.config, o perfil padrão de rastreamento assina os registros e a falhas de instância de fluxo de trabalho.  
  
 Em ETW, os eventos são gravados para a sessão de ETW com uma identificação do provedor O provedor que o ID que o participante de rastreamento de ETW usa gravar o rastreamento registra a ETW é definido na seção de diagnóstico do arquivo web.config (em `<system.serviceModel><diagnostics>`). Por padrão, o participante de rastreamento de ETW usa um padrão de identificação do provedor quando se não foi especificado, conforme mostrado no exemplo o seguir.  
  
```xml  
<system.serviceModel>  
        <diagnostics etwProviderId="52A3165D-4AD9-405C-B1E8-7D9A257EAC9F" />  
```  
  
 A ilustração a seguir mostra o fluxo de dados de rastreamento através de participante de rastreamento de ETW. Uma vez que os dados de acompanhamento alcançam a sessão de ETW, podem ser acessados de várias maneiras. Uma das maneiras mais úteis de acessar esses eventos é através do visualizador de eventos, uma ferramenta do Windows comuns usada exibindo efetua logon e rastreamentos de aplicativos e serviços.  
  
 ![Fluxo de dados de rastreamento por meio do provedor de rastreamento ETW.](./media/tracking-participants/tracking-data-event-tracing-windows-provider.gif)  
  
## <a name="tracking-participant-event-data"></a>Dados do evento de participante de rastreamento  

 Um participante de rastreamento serializa dados controlados de evento a uma sessão de ETW no formato de um evento pelo registro de rastreamento.  Um evento é identificado usando um identificador dentro do intervalo de 100 a 199. Para obter definições dos registros de eventos de rastreamento emitidos por um participante de acompanhamento, consulte o tópico de [referência de eventos de rastreamento](tracking-events-reference.md) .  
  
 O tamanho de um evento de ETW é limitado pelo tamanho do buffer de ETW, ou pela carga útil máximo para um evento de ETW, qualquer valor é menor. Se o tamanho do evento excede qualquer um desses limites de ETW, o evento será truncado e seu conteúdo é removido de uma maneira arbitrária. Variáveis, os argumentos, anotações e os dados personalizado não são removidos seletivamente. No caso de truncamento, todos estes é truncada independentemente do valor que fez com que o tamanho do evento excede o limite de ETW.  Os dados são removidos substituídos por `<item>..<item>`.  
  
 Tipos complexos em variáveis, argumentos e itens de dados personalizados são serializados para o registro de evento do ETW usando a <xref:System.Runtime.Serialization.NetDataContractSerializer> classe. Essa classe inclui informações de CLR- tipo no vapor serializado XML.  
  
 Truncamento de dados de carregamento útil devido aos limites de ETW pode resultar em duplicado através dos registros que estão sendo enviados a uma sessão de ETW. Isso pode ocorrer se mais de uma sessão é escutando eventos e as sessões têm diferentes limites de carregamento útil para os eventos.  
  
 Para a sessão com o limite inferior o evento pode ser truncado. O participante de rastreamento de ETW não tem conhecimento do número de sessões que escutam por eventos; se um evento é truncado para uma sessão no participante de ETW tentar de volta para o evento uma vez. Nesse caso a sessão que está configurada para aceitar um tamanho maior de carregamento útil obterá o evento duas vezes (o evento não truncado e truncado). Duplicação pode ser impedida configurando todas as sessões de ETW com os mesmos limites de tamanho do buffer.  
  
## <a name="accessing-tracking-data-from-an-etw-participant-in-the-event-viewer"></a>Acessando dados de acompanhamento de um participante de ETW no visualizador de eventos  

 Os eventos que são gravados em uma sessão de ETW por participante de rastreamento de ETW podem ser acessados através do visualizador de eventos (para usar o padrão de identificação do provedor). Isso permite rapidamente exibindo os registros de rastreamento que foram emitidos pelo fluxo de trabalho.  
  
> [!NOTE]
> Controlando o registro os eventos emissores a uma sessão de ETW usam IDs de evento no intervalo de 100 a 199.  
  
#### <a name="to-enable-viewing-the-tracking-records-in-event-viewer"></a>Para ativar exibir os registros de rastreamento no visualizador de eventos  
  
1. Ligue o visualizador de eventos (EVENTVWR.EXE)  
  
2. Selecione **Visualizador de eventos, logs de aplicativos e serviços, Microsoft, Windows, servidor de aplicativos-aplicativos**.  
  
3. Clique com o botão direito do mouse e verifique se **Exibir, Mostrar logs analíticos e de depuração** está selecionado. Se não, selecione-o para que a marca de seleção aparece próxima a ela. Isso exibe os logs **analíticos**, de **desempenho** e de **depuração** .  
  
4. Clique com o botão direito do mouse no log **analítico** e selecione **habilitar log**. O log existirá no diretório %SystemRoot% \ arquivo de Winevt System32 \ \ \ application logs Server-Applications%4Analytic.etl.  
  
## <a name="custom-tracking-participant"></a>Participante de rastreamento personalizada  

 O participante de rastreamento API permite a extensão de rastreamento usuário fornecido com o participante de rastreamento que pode incluir a lógica personalizada para manipular os registros de rastreamento emissores em runtime de fluxo de trabalho. Para gravar um participante personalizado de rastreamento, o desenvolvedor deve implementar o método `Track` na classe de <xref:System.Activities.Tracking.TrackingParticipant> . Este método é chamado quando um registro de rastreamento é emitida em runtime de fluxo de trabalho.  
  
 Os participantes de rastreamento derivam da classe de <xref:System.Activities.Tracking.TrackingParticipant> . Sistema forneceu <xref:System.Activities.Tracking.EtwTrackingParticipant> emite-se um rastreamento de evento para o evento do Windows (ETW) para cada registro de rastreamento que é recebido. Para criar um participante personalizado de rastreamento, uma classe é criada que deriva de <xref:System.Activities.Tracking.TrackingParticipant>. Para fornecer a funcionalidade básica de rastreamento, substitua o <xref:System.Activities.Tracking.TrackingParticipant.Track%2A>. o<xref:System.Activities.Tracking.TrackingParticipant.Track%2A> é chamado quando um registro de rastreamento é enviado em runtime e pode ser processado na forma desejada. No exemplo a seguir, uma classe personalizada de participante de rastreamento é definida que emite todos os registros de rastreamento para a janela do console. Você também pode implementar um objeto de <xref:System.Activities.Tracking.TrackingParticipant> que processa os registros de rastreamento que usam de forma assíncrona seus métodos de `BeginTrack` e de `EndTrack`  
  
```csharp  
class ConsoleTrackingParticipant : TrackingParticipant  
{  
    protected override void Track(TrackingRecord record, TimeSpan timeout)  
    {  
        if (record != null)  
        {  
            Console.WriteLine("=================================");  
            Console.WriteLine(record);  
        }  
    }  
}  
```  
  
 Para usar um participante específico de rastreamento, registrá-lo com a instância de fluxo de trabalho que você deseja controlar, conforme mostrado no exemplo o seguir.  
  
```csharp  
myInstance.Extensions.Add(new ConsoleTrackingParticipant());  
```  
  
 No exemplo a seguir, um fluxo de trabalho que consiste uma atividade de <xref:System.Activities.Statements.Sequence> que contém uma atividade de <xref:System.Activities.Statements.WriteLine> é criado. `ConsoleTrackingParticipant` é adicionado para extensões e fluxo de trabalho é chamado.  
  
```csharp  
Activity activity= new Sequence()  
{  
    Activities =  
    {  
        new WriteLine()  
        {  
            Text = "Hello World."  
        }  
    }  
};  
  
WorkflowApplication instance = new WorkflowApplication(activity);  
  
instance.Extensions.Add(new ConsoleTrackingParticipant());  
  instance.Completed = delegate(WorkflowApplicationCompletedEventArgs e)  
            {  
                Console.WriteLine("workflow instance completed, Id = " + instance.Id);  
                resetEvent.Set();  
            };  
            instance.Run();  
            Console.ReadLine();  
```  
  
## <a name="see-also"></a>Consulte também

- [Monitoramento do Windows Server app Fabric](/previous-versions/appfabric/ee677251(v=azure.10))
- [Monitorando aplicativos com o app Fabric](/previous-versions/appfabric/ee677276(v=azure.10))
