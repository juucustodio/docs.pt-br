---
description: 'Saiba mais sobre: tempo de vida personalizado'
title: Tempo de vida personalizado
ms.date: 08/20/2018
ms.assetid: 52806c07-b91c-48fe-b992-88a41924f51f
ms.openlocfilehash: 24845aaa20e60f92e2add568c81ab3d6502ebedf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99732469"
---
# <a name="custom-lifetime"></a>Tempo de vida personalizado

Este exemplo demonstra como gravar uma extensão de Windows Communication Foundation (WCF) para fornecer serviços de tempo de vida personalizados para instâncias de serviço WCF compartilhadas.

> [!NOTE]
> O procedimento de instalação e as instruções de Build para este exemplo estão localizados no final deste artigo.

## <a name="shared-instancing"></a>Instanciação compartilhada

O WCF oferece vários modos de instanciação para suas instâncias de serviço. O modo de instanciação compartilhado abordado neste artigo fornece uma maneira de compartilhar uma instância de serviço entre vários canais. Os clientes podem contatar um método de fábrica no serviço e criar um novo canal para iniciar a comunicação. O trecho de código a seguir mostra como um aplicativo cliente cria um novo canal para uma instância de serviço existente:

```csharp
// Create a header for the shared instance id
MessageHeader shareableInstanceContextHeader = MessageHeader.CreateHeader(
        CustomHeader.HeaderName,
        CustomHeader.HeaderNamespace,
        Guid.NewGuid().ToString());

// Create the channel factory
ChannelFactory<IEchoService> channelFactory =
    new ChannelFactory<IEchoService>("echoservice");

// Create the first channel
IEchoService proxy = channelFactory.CreateChannel();

// Call an operation to create shared service instance
using (new OperationContextScope((IClientChannel)proxy))
{
    OperationContext.Current.OutgoingMessageHeaders.Add(shareableInstanceContextHeader);
    Console.WriteLine("Service returned: " + proxy.Echo("Apple"));
}

((IChannel)proxy).Close();

// Create the second channel
IEchoService proxy2 = channelFactory.CreateChannel();

// Call an operation using the same header that will reuse the shared service instance
using (new OperationContextScope((IClientChannel)proxy2))
{
    OperationContext.Current.OutgoingMessageHeaders.Add(shareableInstanceContextHeader);
    Console.WriteLine("Service returned: " + proxy2.Echo("Apple"));
}
```

Ao contrário de outros modos de instanciação, o modo de instanciação compartilhado tem uma maneira exclusiva de liberar as instâncias de serviço. Por padrão, quando todos os canais são fechados para um <xref:System.ServiceModel.InstanceContext> , o tempo de execução do serviço WCF verifica se o serviço <xref:System.ServiceModel.InstanceContextMode> está configurado para <xref:System.ServiceModel.InstanceContextMode.PerCall> ou <xref:System.ServiceModel.InstanceContextMode.PerSession> e, em caso afirmativo, libera a instância e declara os recursos. Se um personalizado <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> estiver sendo usado, o WCF invocará o <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> método da implementação do provedor antes de liberar a instância. Se o <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> retornar `true` , a instância será liberada, caso contrário, a <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> implementação será responsável por notificar o `Dispatcher` estado ocioso usando um método de retorno de chamada. Isso é feito chamando o <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.NotifyIdle%2A> método do provedor.

Este exemplo demonstra como você pode atrasar a liberação do <xref:System.ServiceModel.InstanceContext> com um tempo limite de ociosidade de 20 segundos.

## <a name="extending-the-instancecontext"></a>Estendendo o InstanceContext

No WCF, <xref:System.ServiceModel.InstanceContext> é o vínculo entre a instância do serviço e o `Dispatcher` . O WCF permite que você estenda esse componente de tempo de execução adicionando um novo estado ou comportamento usando seu padrão de objeto extensível. O padrão de objeto extensível é usado no WCF para estender as classes de tempo de execução existentes com a nova funcionalidade ou para adicionar novos recursos de estado a um objeto. Há três interfaces no padrão de objeto extensível: <xref:System.ServiceModel.IExtensibleObject%601> , <xref:System.ServiceModel.IExtension%601> e <xref:System.ServiceModel.IExtensionCollection%601> .

A <xref:System.ServiceModel.IExtensibleObject%601> interface é implementada por objetos para permitir extensões que personalizam sua funcionalidade.

A <xref:System.ServiceModel.IExtension%601> interface é implementada por objetos que podem ser extensões de classes do tipo `T` .

E, finalmente, a <xref:System.ServiceModel.IExtensionCollection%601> interface é uma coleção de <xref:System.ServiceModel.IExtension%601> implementações que permite recuperar uma implementação de <xref:System.ServiceModel.IExtension%601> por seu tipo.

Portanto, para estender o <xref:System.ServiceModel.InstanceContext> , você deve implementar a <xref:System.ServiceModel.IExtension%601> interface. Neste projeto de exemplo, a `CustomLeaseExtension` classe contém essa implementação.

```csharp
class CustomLeaseExtension : IExtension<InstanceContext>
{
}
```

A <xref:System.ServiceModel.IExtension%601> interface tem dois métodos <xref:System.ServiceModel.IExtension%601.Attach%2A> e <xref:System.ServiceModel.IExtension%601.Detach%2A> . Como seus nomes sugerem, esses dois métodos são chamados quando o tempo de execução anexa e desanexa a extensão a uma instância da <xref:System.ServiceModel.InstanceContext> classe. Neste exemplo, o `Attach` método é usado para controlar o <xref:System.ServiceModel.InstanceContext> objeto que pertence à instância atual da extensão.

```csharp
InstanceContext owner;

public void Attach(InstanceContext owner)
{
    this.owner = owner;
}
```

Além disso, você deve adicionar a implementação necessária à extensão para fornecer o suporte estendido ao tempo de vida. Portanto, a `ICustomLease` interface é declarada com os métodos desejados e é implementada na `CustomLeaseExtension` classe.

```csharp
interface ICustomLease
{
    bool IsIdle { get; }
    InstanceContextIdleCallback Callback { get; set; }
}

class CustomLeaseExtension : IExtension<InstanceContext>, ICustomLease
{
}
```

Quando o WCF invoca o <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> método na <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> implementação, essa chamada é roteada para o <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> método do `CustomLeaseExtension` . Em seguida, o `CustomLeaseExtension` verifica seu estado particular para ver se o <xref:System.ServiceModel.InstanceContext> está ocioso. Se estiver ocioso, ele retornará `true` . Caso contrário, ele iniciará um temporizador para uma quantidade especificada de tempo de vida estendido.

```csharp
public bool IsIdle
{
  get
  {
    lock (thisLock)
    {
      if (isIdle)
      {
        return true;
      }
      else
      {
        StartTimer();
        return false;
      }
    }
  }
}
```

No evento do temporizador `Elapsed` , a função de retorno de chamada no Dispatcher é chamada para iniciar outro ciclo de limpeza.

```csharp
void idleTimer_Elapsed(object sender, ElapsedEventArgs args)
{
    lock (thisLock)
    {
        StopTimer();
        isIdle = true;
        Utility.WriteMessageToConsole(
            ResourceHelper.GetString("MsgLeaseExpired"));
        callback(owner);
    }
}
```

Não há como renovar o temporizador em execução quando uma nova mensagem chega à instância que está sendo movida para o estado ocioso.

O exemplo implementa <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> para interceptar as chamadas para o <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> método e roteá-las para o `CustomLeaseExtension` . A <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> implementação está contida na `CustomLifetimeLease` classe. O <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> método é invocado quando o WCF está prestes a liberar a instância de serviço. No entanto, há apenas uma instância de uma `ISharedSessionInstance` implementação específica na coleção do imbehavior <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> . Isso significa que não há como saber se o <xref:System.ServiceModel.InstanceContext> está fechado no momento em que o WCF verifica o <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> método. Portanto, este exemplo usa o bloqueio de thread para serializar solicitações para o <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> método.

> [!IMPORTANT]
> Usar o bloqueio de thread não é uma abordagem recomendada porque a serialização pode afetar seriamente o desempenho do seu aplicativo.

Um campo de membro privado é usado na `CustomLifetimeLease` classe para acompanhar o estado ocioso e é retornado pelo <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> método. Cada vez que o <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> método é chamado, o `isIdle` campo é retornado e redefinido como `false` .  É essencial definir esse valor como para garantir que `false` o Dispatcher chame o <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.NotifyIdle%2A> método.

```csharp
public bool IsIdle(InstanceContext instanceContext)
{
    get
    {
        lock (thisLock)
        {
            //...
            bool idleCopy = isIdle;
            isIdle = false;
            return idleCopy;
        }
    }
}
```

Se o <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A?displayProperty=nameWithType> método retornar `false` , o Dispatcher registrará uma função de retorno de chamada usando o <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.NotifyIdle%2A> método. Esse método recebe uma referência para o <xref:System.ServiceModel.InstanceContext> que está sendo liberado. Portanto, o código de exemplo pode consultar a `ICustomLease` extensão de tipo e verificar a `ICustomLease.IsIdle` propriedade no estado estendido.

```csharp
public void NotifyIdle(InstanceContextIdleCallback callback,
            InstanceContext instanceContext)
{
    lock (thisLock)
    {
       ICustomLease customLease =
           instanceContext.Extensions.Find<ICustomLease>();
       customLease.Callback = callback;
       isIdle = customLease.IsIdle;
       if (isIdle)
       {
             callback(instanceContext);
       }
    }
}
```

Antes de a `ICustomLease.IsIdle` propriedade ser marcada, a propriedade de retorno de chamada precisa ser definida, pois é essencial para `CustomLeaseExtension` notificar o Dispatcher quando ele se tornar ocioso. Se `ICustomLease.IsIdle` retornar `true` , o `isIdle` membro privado será simplesmente definido `CustomLifetimeLease` como `true` e chamará o método de retorno de chamada. Como o código mantém um bloqueio, outros threads não podem alterar o valor desse membro privado. E, na próxima vez que o Dispatcher chamar o <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A?displayProperty=nameWithType> , ele retornará `true` e permitirá que o Dispatcher libere a instância.

Agora que a base para a extensão personalizada foi concluída, ela precisa ser conectada ao modelo de serviço. Para conectar a `CustomLeaseExtension` implementação ao, o <xref:System.ServiceModel.InstanceContext> WCF fornece a <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer> interface para executar a inicialização do <xref:System.ServiceModel.InstanceContext> . No exemplo, a `CustomLeaseInitializer` classe implementa essa interface e adiciona uma instância do `CustomLeaseExtension` à coleção a <xref:System.ServiceModel.InstanceContext.Extensions%2A> partir da única inicialização do método. Esse método é chamado pelo Dispatcher durante a inicialização do <xref:System.ServiceModel.InstanceContext> .

```csharp
public void InitializeInstanceContext(InstanceContext instanceContext,
    System.ServiceModel.Channels.Message message, IContextChannel channel)

    //...

    IExtension<InstanceContext> customLeaseExtension =
        new CustomLeaseExtension(timeout, headerId);
    instanceContext.Extensions.Add(customLeaseExtension);
}
```

 Por fim, a <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> implementação é conectada ao modelo de serviço usando a <xref:System.ServiceModel.Description.IServiceBehavior> implementação. Essa implementação é colocada na `CustomLeaseTimeAttribute` classe e também deriva da <xref:System.Attribute> classe base para expor esse comportamento como um atributo.

```csharp
public void ApplyDispatchBehavior(ServiceDescription description,
           ServiceHostBase serviceHostBase)
{
    CustomLifetimeLease customLease = new CustomLifetimeLease(timeout);

    foreach (ChannelDispatcherBase cdb in serviceHostBase.ChannelDispatchers)
    {
        ChannelDispatcher cd = cdb as ChannelDispatcher;

        if (cd != null)
        {
            foreach (EndpointDispatcher ed in cd.Endpoints)
            {
                ed.DispatchRuntime.InstanceContextProvider = customLease;
            }
        }
    }
}
```

Esse comportamento pode ser adicionado a uma classe de serviço de exemplo, anotando-o com o `CustomLeaseTime` atributo.

```csharp
[CustomLeaseTime(Timeout = 20000)]
public class EchoService : IEchoService
{
  //…
}
```

Quando você executa o exemplo, as solicitações e respostas da operação são exibidas nas janelas do console do cliente e do serviço. Pressione ENTER em cada janela do console para desligar o serviço e o cliente.

### <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo

1. Verifique se você executou o [procedimento de configuração única para os exemplos de Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).

2. Para criar a edição C# ou Visual Basic .NET da solução, siga as instruções em [criando os exemplos de Windows Communication Foundation](building-the-samples.md).

3. Para executar o exemplo em uma configuração de computador único ou cruzado, siga as instruções em [executando os exemplos de Windows Communication Foundation](running-the-samples.md).

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Lifetime`
