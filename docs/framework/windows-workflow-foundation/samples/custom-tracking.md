---
description: 'Saiba mais sobre: acompanhamento personalizado'
title: Rastreamento personalizada
ms.date: 03/30/2017
ms.assetid: 2d191c9f-62f4-4c63-92dd-cda917fcf254
ms.openlocfilehash: a06faaaa50a06d613f7183ca018438a8f2b4460b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792551"
---
# <a name="custom-tracking"></a>Rastreamento personalizada

Este exemplo demonstra como criar um participante personalizado de rastreamento e gravar o conteúdo dos dados de acompanhamento no console. Além disso, o exemplo demonstra como emitir os objetos de <xref:System.Activities.Tracking.CustomTrackingRecord> preenchido com dados definidos pelo usuário. O participante controlando console- base filtra os objetos de <xref:System.Activities.Tracking.TrackingRecord> emissores pelo fluxo de trabalho usando um objeto de perfil de rastreamento criado em código.

## <a name="sample-details"></a>Detalhes de exemplo

 Windows Workflow Foundation (WF) fornece uma infraestrutura de controle para controlar a execução de uma instância de fluxo de trabalho. O runtime de rastreamento implementa uma instância de fluxo de trabalho para emitir os eventos relacionados ao ciclo de vida de fluxo de trabalho, os eventos de atividades de fluxo de trabalho e eventos personalizados de rastreamento. A tabela a seguir detalha os componentes principais de infraestrutura de rastreamento.

|Componente|Descrição|
|---------------|-----------------|
|runtime de rastreamento|Fornece a infraestrutura para emitir registros de rastreamento.|
|Participantes de rastreamento|Consome os registros de rastreamento. O .NET Framework 4 é fornecido com um participante de controle que grava registros de rastreamento como eventos de ETW (rastreamento de eventos para Windows).|
|Controlando o perfil|Um mecanismo de filtragem que permite que um participante de rastreamento assine para um subconjunto de registros de rastreamento emissores de uma instância de fluxo de trabalho.|

 A tabela a seguir detalha os registros de rastreamento que o runtime de fluxo de trabalho se emite.

|Registro de Rastreamento|Descrição|
|---------------------|-----------------|
|Registros de rastreamento de instância de fluxo de trabalho.|Descreve o ciclo de vida de instância de fluxo de trabalho. Por exemplo, um registro de instância é emitida quando o fluxo de trabalho inicia ou termina.|
|Estado da atividade que acompanha registros.|Detalha a execução da atividade. Esses registros indicam o estado de uma atividade de fluxo de trabalho como quando uma atividade é agendada ou quando a atividade completa ou quando uma falha é lançada.|
|Registro de ressunção do indexador.|Emitido sempre que um marcador em uma instância de fluxo de trabalho que é.|
|Registros personalizados de rastreamento.|Um autor de fluxo de trabalho pode criar registros personalizados de rastreamento e emitir os dentro da atividade personalizado.|

 O participante de rastreamento assinatura para um subconjunto dos objetos emissores de <xref:System.Activities.Tracking.TrackingRecord> usando perfis de rastreamento. Um perfil de rastreamento contém consultas de rastreamento que permitem assinar para um tipo de registro específico de rastreamento. Controlar perfis pode ser especificado no código ou na configuração.

### <a name="custom-tracking-participant"></a>Participante de rastreamento personalizada

 O participante API de rastreamento permite a extensão de rastreamento com um usuário fornecido pelo participante que pode incluir a lógica personalizada para manipular os objetos de <xref:System.Activities.Tracking.TrackingRecord> emissores em runtime de fluxo de trabalho.

 Para gravar um participante de rastreamento o usuário deve implementar <xref:System.Activities.Tracking.TrackingParticipant>. Especificamente, o método de <xref:System.Activities.Tracking.TrackingParticipant.Track%2A> precisa ser implementado por participante personalizado. Este método é chamado quando <xref:System.Activities.Tracking.TrackingRecord> é emitida em runtime de fluxo de trabalho.

```csharp
public abstract class TrackingParticipant
{
    protected TrackingParticipant();

    public virtual TrackingProfile TrackingProfile { get; set; }
    public abstract void Track(TrackingRecord record, TimeSpan timeout);
}
```

 O participante de acompanhamento completo é implementado no arquivo ConsoleTrackingParticipant.cs. O exemplo de código a seguir é o <xref:System.Activities.Tracking.TrackingParticipant.Track%2A> método para o participante de acompanhamento personalizado.

```csharp
protected override void Track(TrackingRecord record, TimeSpan timeout)
{
    ...
    WorkflowInstanceRecord workflowInstanceRecord = record as WorkflowInstanceRecord;
    if (workflowInstanceRecord != null)
    {
        Console.WriteLine(String.Format(CultureInfo.InvariantCulture,
            " Workflow InstanceID: {0} Workflow instance state: {1}",
            record.InstanceId, workflowInstanceRecord.State));
    }

    ActivityStateRecord activityStateRecord = record as ActivityStateRecord;
    if (activityStateRecord != null)
    {
        IDictionary<String, object> variables = activityStateRecord.Variables;
        StringBuilder vars = new StringBuilder();

        if (variables.Count > 0)
        {
            vars.AppendLine("\n\tVariables:");
            foreach (KeyValuePair<string, object> variable in variables)
            {
                vars.AppendLine(String.Format(
                    "\t\tName: {0} Value: {1}", variable.Key, variable.Value));
            }
        }
        Console.WriteLine(String.Format(CultureInfo.InvariantCulture,
            " :Activity DisplayName: {0} :ActivityInstanceState: {1} {2}",
                activityStateRecord.Activity.Name, activityStateRecord.State,
            ((variables.Count > 0) ? vars.ToString() : String.Empty)));
    }

    CustomTrackingRecord customTrackingRecord = record as CustomTrackingRecord;

    if ((customTrackingRecord != null) && (customTrackingRecord.Data.Count > 0))
    {
        ...
    }
    Console.WriteLine();

}
```

 O exemplo de código a seguir adiciona o participante de console para o solicitante de fluxo de trabalho.

```csharp
ConsoleTrackingParticipant customTrackingParticipant = new ConsoleTrackingParticipant()
{
    ...
    // The tracking profile is set here, refer to Program.CS
...
}

WorkflowInvoker invoker = new WorkflowInvoker(BuildSampleWorkflow());
invoker.Extensions.Add(customTrackingParticipant);
```

### <a name="emitting-custom-tracking-records"></a>Emitindo registros de rastreamento personalizadas

 Este exemplo também demonstra a capacidade de emitir objetos de <xref:System.Activities.Tracking.CustomTrackingRecord> de uma atividade personalizado de fluxo de trabalho:

- Os objetos de <xref:System.Activities.Tracking.CustomTrackingRecord> são criados e preenchido com dados definidos pelo usuário que são desejados ser emitidos com o registro.

- O <xref:System.Activities.Tracking.CustomTrackingRecord> é emitido chamando o método Track do <xref:System.Activities.ActivityContext> .

 O exemplo a seguir demonstra como emitir objetos de <xref:System.Activities.Tracking.CustomTrackingRecord> dentro de uma atividade personalizado.

```csharp
// Create the Custom Tracking Record
CustomTrackingRecord customRecord = new CustomTrackingRecord("OrderIn")
{
    Data =
    {
        {"OrderId", 200},
        {"OrderDate", "20 Aug 2001"}
    }
};

// Emit custom tracking record
context.Track(customRecord);
```

#### <a name="to-use-this-sample"></a>Para usar este exemplo

1. Usando o Visual Studio 2010, abra o arquivo de solução CustomTrackingSample. sln.

2. Para criar a solução, pressione CTRL+SHIFT+B.

3. Para executar a solução, pressione CTRL+F5.

> [!IMPORTANT]
> Os exemplos podem mais ser instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Tracking\CustomTracking`  
  
## <a name="see-also"></a>Consulte também

- [AppFabric que monitora Exemplos](/previous-versions/appfabric/ff383407(v=azure.10))
