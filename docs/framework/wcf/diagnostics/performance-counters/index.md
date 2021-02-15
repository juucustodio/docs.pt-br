---
description: 'Saiba mais sobre: contadores de desempenho do WCF'
title: Contadores de desempenho do WCF
ms.date: 03/30/2017
helpviewer_keywords:
- performance counters [WCF]
ms.assetid: f559b2bd-ed83-4988-97a1-e88f06646609
ms.openlocfilehash: c6572ece289fb550dd4974a8f8e957f7d3ef51b5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99655338"
---
# <a name="wcf-performance-counters"></a>Contadores de desempenho do WCF

O Windows Communication Foundation (WCF) inclui um grande conjunto de contadores de desempenho para ajudá-lo a medir o desempenho do seu aplicativo.  
  
## <a name="enabling-performance-counters"></a>Habilitando contadores de desempenho  

 Você pode habilitar contadores de desempenho para um serviço WCF por meio do arquivo de configuração app.config do serviço WCF da seguinte maneira:  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <diagnostics performanceCounters="All" />  
    </system.serviceModel>  
</configuration>  
```  
  
 O `performanceCounters` atributo pode ser definido para habilitar um tipo específico de contadores de desempenho. Os valores válidos são  
  
- Todos: todos os contadores de categoria (ServiceModelService, ServiceModelEndpoint e ServiceModelOperation) estão habilitados.  
  
- Somente: os contadores de categoria ServiceModelService estão habilitados. Esse é o valor padrão.  
  
- Desativada: os contadores de desempenho ServiceModel * estão desabilitados.  
  
 Se você quiser habilitar contadores de desempenho para todos os aplicativos WCF, poderá posicionar as definições de configuração no arquivo Machine.config.  Consulte a seção **aumentar tamanho da memória para contadores de desempenho** abaixo para obter mais informações sobre como configurar memória suficiente para contadores de desempenho em seu computador.  
  
 Se você usar pontos de extensibilidade do WCF, como chamadores de operação personalizados, também deverá emitir seus próprios contadores de desempenho. Isso ocorre porque, se você implementar um ponto de extensibilidade, o WCF poderá não emitir mais os dados do contador de desempenho padrão no caminho padrão. Se você não implementar o suporte de contador de desempenho manual, talvez não veja os dados do contador de desempenho que espera.  
  
 Você também pode habilitar contadores de desempenho em seu código da seguinte maneira:  
  
```csharp
using System.Configuration;  
using System.ServiceModel.Configuration;  
using System.ServiceModel.Diagnostics;  
Configuration config = ConfigurationManager.OpenExeConfiguration(  
    ConfigurationUserLevel.None);  
ServiceModelSectionGroup sg = ServiceModelSectionGroup.GetSectionGroup(config);  
sg.Diagnostic.PerformanceCounters = PerformanceCounterScope.All;  
config.Save();  
```  
  
## <a name="viewing-performance-data"></a>Exibindo dados de desempenho  

 Para exibir os dados capturados pelos contadores de desempenho, você pode usar o monitor de desempenho (Perfmon.exe) fornecido com o Windows. Você pode iniciar essa ferramenta acessando **Iniciar** e, em seguida, clique em **executar** e digite `perfmon.exe` na caixa de diálogo.  
  
> [!NOTE]
> As instâncias do contador de desempenho podem ser liberadas antes que as últimas mensagens sejam processadas pelo dispatcher do ponto de extremidade. Isso pode fazer com que os dados de desempenho não sejam capturados para algumas mensagens.  
  
## <a name="increasing-memory-size-for-performance-counters"></a>Aumentando o tamanho da memória para contadores de desempenho  

 O WCF usa memória compartilhada separada para suas categorias de contador de desempenho.  
  
 Por padrão, a memória compartilhada separada é definida como um trimestre do tamanho da memória do contador de desempenho global. A memória padrão do contador de desempenho global é de 524.288 bytes. Portanto, as três categorias de contador de desempenho do WCF têm um tamanho padrão de aproximadamente 128KB cada. Dependendo das características de tempo de execução dos aplicativos WCF em um computador, a memória do contador de desempenho pode ser esgotada. Quando isso acontece, o WCF grava um erro no log de eventos do aplicativo. O conteúdo do erro informa que um contador de desempenho não foi carregado e a entrada contém a exceção "System. InvalidOperationException: a exibição do arquivo de contadores personalizados está sem memória". Se o rastreamento estiver habilitado no nível de erro, essa falha também será rastreada. Se a memória do contador de desempenho estiver esgotada, continuar a executar seus aplicativos WCF com os contadores de desempenho habilitado pode resultar em degradação do desempenho. Se você for um administrador do computador, deverá configurá-lo para alocar memória suficiente para dar suporte ao número máximo de contadores de desempenho que podem existir a qualquer momento.  
  
 Você pode alterar a quantidade de memória do contador de desempenho para categorias do WCF no registro. Para fazer isso, você precisa adicionar um novo valor DWORD chamado `FileMappingSize` aos três locais a seguir e defini-lo como o valor desejado em bytes. Reinicialize o computador para que essas alterações sejam levadas em vigor.  
  
- HKLM\System\CurrentControlSet\Services\ServiceModelEndpoint 4.0.0.0 \ desempenho  
  
- HKLM\System\CurrentControlSet\Services\ServiceModelOperation 4.0.0.0 \ desempenho  
  
- HKLM\System\CurrentControlSet\Services\ServiceModelService 4.0.0.0 \ desempenho  
  
 Quando um grande número de objetos (por exemplo, ServiceHost) é Descartado, mas aguardando para ser coletado pelo lixo, o `PrivateBytes` contador de desempenho registrará um número excepcionalmente alto. Para resolver esse problema, você pode adicionar seus próprios contadores específicos do aplicativo ou usar o `performanceCounters` atributo para habilitar somente contadores de nível de serviço.  
  
## <a name="types-of-performance-counters"></a>Tipos de contadores de desempenho  

 Os contadores de desempenho têm como escopo três níveis diferentes: serviço, ponto de extremidade e operação.  
  
 Você pode usar o WMI para recuperar o nome de uma instância do contador de desempenho. Por exemplo,  
  
- O nome da instância do contador de serviço pode ser obtido por meio da propriedade "referendaname" da instância do [serviço](../wmi/service.md) WMI.  
  
- O nome da instância do contador de ponto de extremidade pode ser obtido por meio da propriedade "referendaname" da instância do [ponto de extremidade](../wmi/endpoint.md) do WMI.  
  
- O nome da instância do contador de operações pode ser obtido por meio do método "GetOperationCounterInstanceName" da instância do [ponto de extremidade](../wmi/endpoint.md) do WMI.  
  
 Para obter mais informações sobre o WMI, consulte [usando instrumentação de gerenciamento do Windows para diagnóstico](../wmi/index.md).  
  
### <a name="service-performance-counters"></a>Contadores de desempenho de serviço  

 Os contadores de desempenho de serviço medem o comportamento do serviço como um todo e podem ser usados para diagnosticar o desempenho do serviço inteiro. Eles podem ser encontrados no `ServiceModelService 4.0.0.0` objeto de desempenho ao exibir com o monitor de desempenho. As instâncias são nomeadas usando o seguinte padrão:  
  
`ServiceName@ServiceBaseAddress`
  
 Um contador em um escopo de serviço é agregado do contador em uma coleção de pontos de extremidade.  
  
 Os contadores de desempenho para a criação da instância de serviço são incrementados quando um novo InstanceContext é criado. Observe que um novo InstanceContext é criado mesmo quando você recebe uma mensagem que não está sendo ativada (com um serviço existente) ou quando você se conecta a uma instância de uma sessão, encerra a sessão e, em seguida, reconecta a partir de outra sessão.  
  
### <a name="endpoint-performance-counters"></a>Contadores de desempenho de ponto de extremidade  

 Os contadores de desempenho do ponto de extremidade permitem que você examine os dados que refletem como um ponto de extremidade está aceitando mensagens. Eles podem ser encontrados no `ServiceModelEndpoint 4.0.0.0` objeto de desempenho ao exibir usando o monitor de desempenho. As instâncias são nomeadas usando o seguinte padrão:  
  
`(ServiceName).(ContractName)@(endpoint listener address)`
  
 Os dados são semelhantes ao que é coletado para operações individuais, mas é agregado somente no ponto de extremidade.  
  
 Um contador em um escopo de ponto de extremidade é agregado dos contadores em uma coleção de operações.  
  
> [!NOTE]
> Se dois pontos de extremidade tiverem nomes de contrato e endereços idênticos, eles serão mapeados para a mesma instância do contador.  
  
### <a name="operation-performance-counters"></a>Contadores de desempenho de operação  

 Os contadores de desempenho de operação são encontrados no `ServiceModelOperation 4.0.0.0` objeto de desempenho ao exibir com o monitor de desempenho. Cada operação tem uma instância individual. Ou seja, se um determinado contrato tiver 10 operações, 10 instâncias do contador de operações serão associadas a esse contrato. As instâncias de objeto são nomeadas usando o seguinte padrão:  
  
`(ServiceName).(ContractName).(OperationName)@(first endpoint listener address)`
  
 Esse contador permite que você meça como a chamada está sendo usada e o quão bem a operação está sendo executada.  
  
 Quando os contadores são visíveis em vários escopos, os dados coletados de um escopo superior são agregados com dados de escopos inferiores. Por exemplo, `Calls` em um ponto de extremidade representa a soma de todas as chamadas de operação dentro do ponto de extremidade; `Calls` em um serviço representa a soma de todas as chamadas para todos os pontos de extremidades no serviço.  
  
> [!NOTE]
> Se você tiver nomes de operação duplicados em um contrato, você só obterá uma instância de contador para ambas as operações.  
  
## <a name="programming-the-wcf-performance-counters"></a>Programando os contadores de desempenho do WCF  

Vários arquivos são instalados na pasta de instalação do SDK para que você possa acessar os contadores de desempenho do WCF programaticamente. Esses arquivos são listados da seguinte maneira:
  
- *\_ServiceModelEndpointPerfCounters.vrg*
- *\_ServiceModelOperationPerfCounters.vrg*
- *\_ServiceModelServicePerfCounters.vrg*  
- *\_SMSvcHostPerfCounters.vrg*
- *\_TransactionBridgePerfCounters.vrg*
  
Para obter mais informações sobre como acessar os contadores programaticamente, consulte [arquitetura de programação de contador de desempenho](/previous-versions/visualstudio/visual-studio-2008/5f9bkxzf(v=vs.90)).
  
## <a name="see-also"></a>Consulte também

- [Administração e diagnósticos](../index.md)
