---
description: 'Saiba mais sobre: imperativo'
title: Obrigatório
ms.date: 03/30/2017
ms.assetid: 4f7ce807-c0e4-407a-92a6-22abafb40b51
ms.openlocfilehash: ceaaf6d2bb196a50c0a9a096e39f9b6f78d63a11
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631834"
---
# <a name="imperative"></a>Obrigatório

Este exemplo demonstra como definir um <xref:System.ServiceModel.WSHttpBinding> para um serviço usando código, em vez de definir a `wsHttpBinding` associação na configuração. Este exemplo é baseado no [introdução](getting-started-sample.md) que implementa um serviço de calculadora.

> [!NOTE]
> O procedimento de instalação e as instruções de Build para este exemplo estão localizados no final deste tópico.

O código a seguir demonstra como definir uma associação imperativa no código.

```csharp
public static void Main()
{
    WSHttpBinding binding = new WSHttpBinding();
    binding.Name = "binding1";
    binding.HostNameComparisonMode =
        HostNameComparisonMode.StrongWildcard;
    binding.Security.Mode = SecurityMode.Message;
    binding.ReliableSession.Enabled = false;
    binding.TransactionFlow = false;

    Uri baseAddress =
        new Uri("http://localhost:8000/servicemodelsamples/service");

    // Create a ServiceHost for the CalculatorService type and provide the base address.
    using(ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress))
    {
        serviceHost.AddServiceEndpoint(typeof(ICalculator),
                                       binding, baseAddress);
        // Open the ServiceHostBase to create listeners and start listening for messages.
        serviceHost.Open();

        // The service can now be accessed.
        Console.WriteLine("The service is ready.");
        Console.WriteLine("Press <ENTER> to terminate service.");
        Console.WriteLine();
        Console.ReadLine();
        // Close the ServiceHostBase to shutdown the service.
        serviceHost.Close();
    }
}
```

 O cliente cria um canal para se comunicar com o serviço, conforme mostrado no código de exemplo a seguir.

```csharp
WSHttpBinding binding = new WSHttpBinding();
binding.Name = "binding1";
binding.HostNameComparisonMode = HostNameComparisonMode.StrongWildcard;
binding.Security.Mode = SecurityMode.Message;
binding.ReliableSession.Enabled = false;
binding.TransactionFlow = false;

String url = "http://localhost:8000/servicemodelsamples/service";
EndpointAddress address = new EndpointAddress(url);
ChannelFactory<ICalculator> channelFactory = new ChannelFactory<ICalculator>(binding,address);
ICalculator channel = channelFactory.CreateChannel();
```

 Quando você executa o exemplo, as solicitações de operação e as respostas são exibidas na janela do console do cliente. Pressione ENTER na janela do cliente para desligar o cliente.

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714

Press <ENTER> to terminate client.
```

## <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo

1. Certifique-se de ter executado o [procedimento de configuração única para os exemplos de Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).

2. Para criar a edição C# ou Visual Basic .NET da solução, siga as instruções em [criando os exemplos de Windows Communication Foundation](building-the-samples.md).

3. Para executar o exemplo em uma configuração de computador único ou cruzado, siga as instruções em [executando os exemplos de Windows Communication Foundation](running-the-samples.md).

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Imperative`
