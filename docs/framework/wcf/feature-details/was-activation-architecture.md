---
description: 'Saiba mais sobre: arquitetura de ativação WAS'
title: Arquitetura de ativação do WAS
ms.date: 03/30/2017
ms.assetid: 58aeffb0-8f3f-4b40-80c8-15f3f1652fd3
ms.openlocfilehash: 616b3b404258356bcd5600c68b6f70aaf096e978
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99756013"
---
# <a name="was-activation-architecture"></a>Arquitetura de ativação do WAS

Este tópico relaciona e discute os componentes do serviço de ativação de processos do Windows (também conhecido como WAS).  
  
## <a name="activation-components"></a>Componentes de ativação  

 O foi composto por vários componentes de arquitetura:  
  
- Adaptadores de escuta. Os serviços do Windows que recebem mensagens em protocolos de rede específicos e se comunicam com o WAS para rotear mensagens de entrada para o processo de trabalho correto.  
  
- Deveria. O serviço do Windows que gerencia a criação e o tempo de vida de processos de trabalho.  
  
- O executável do processo de trabalho genérico (w3wp.exe).  
  
- Gerenciador de aplicativos. Gerencia a criação e o tempo de vida de domínios de aplicativo que hospedam aplicativos dentro do processo de trabalho.  
  
- Manipuladores de protocolo. Componentes específicos de protocolo que são executados no processo de trabalho e gerenciam a comunicação entre o processo de trabalho e os adaptadores de ouvinte individuais. Existem dois tipos de manipuladores de protocolo: manipuladores de protocolo de processo e manipuladores de protocolo AppDomain.  
  
 Quando o WAS ativa uma instância de processo de trabalho, ele carrega os manipuladores de protocolo de processo necessários para o processo de trabalho e usa o Gerenciador de aplicativos para criar um domínio de aplicativo para hospedar o aplicativo. O domínio do aplicativo carrega o código do aplicativo, bem como os manipuladores de protocolo AppDomain que os protocolos de rede usados pelo aplicativo exigem.  
  
 ![Captura de tela que mostra a arquitetura do WAS.](./media/was-activation-architecture/windows-process-application-service-architecture.gif)  
  
### <a name="listener-adapters"></a>Adaptadores de escuta  

 Os adaptadores de escuta são serviços individuais do Windows que implementam a lógica de comunicação de rede usada para receber mensagens usando o protocolo de rede no qual elas escutam. A tabela a seguir lista os adaptadores de ouvinte para protocolos Windows Communication Foundation (WCF).  
  
|Nome do serviço do adaptador de ouvinte|Protocolo|Observações|  
|-----------------------------------|--------------|-----------|  
|W3SVC|http|Componente comum que fornece ativação HTTP para o IIS 7,0 e o WCF.|  
|NetTcpActivator|net.tcp|Depende do serviço NetTcpPortSharing.|  
|NetPipeActivator|net.pipe||  
|NetMsmqActivator|net.msmq|Para uso com aplicativos baseados no serviço de enfileiramento de mensagens do WCF.|  
|NetMsmqActivator|msmq.formatname|Fornece compatibilidade com versões anteriores com aplicativos de enfileiramento de mensagens existentes.|  
  
 Os adaptadores de escuta para protocolos específicos são registrados durante a instalação no arquivo de applicationHost.config, conforme mostrado no exemplo de XML a seguir.  
  
```xml  
<system.applicationHost>  
    <listenerAdapters>  
        <add name="http" />  
        <add name="net.tcp"
          identity="S-1-5-80-3579033775-2824656752-1522793541-1960352512-462907086" />  
         <add name="net.pipe"
           identity="S-1-5-80-2943419899-937267781-4189664001-1229628381-3982115073" />  
          <add name="net.msmq"
            identity="S-1-5-80-89244771-1762554971-1007993102-348796144-2203111529" />  
           <add name="msmq.formatname"
             identity="S-1-5-80-89244771-1762554971-1007993102-348796144-2203111529" />  
    </listenerAdapters>  
</system.applicationHost>  
```  
  
### <a name="protocol-handlers"></a>Manipuladores de protocolo  

 Os manipuladores de protocolo de processo e AppDomain para protocolos específicos são registrados no arquivo de Web.config no nível da máquina.  
  
```xml  
<system.web>  
   <protocols>  
      <add name="net.tcp"
        processHandlerType=  
         "System.ServiceModel.WasHosting.TcpProcessProtocolHandler"  
        appDomainHandlerType=  
         "System.ServiceModel.WasHosting.TcpAppDomainProtocolHandler"  
        validate="false" />  
      <add name="net.pipe"
        processHandlerType=  
         "System.ServiceModel.WasHosting.NamedPipeProcessProtocolHandler"  
          appDomainHandlerType=  
           "System.ServiceModel.WasHosting.NamedPipeAppDomainProtocolHandler"/>  
      <add name="net.msmq"  
        processHandlerType=  
         "System.ServiceModel.WasHosting.MsmqProcessProtocolHandler"  
        appDomainHandlerType=  
         "System.ServiceModel.WasHosting.MsmqAppDomainProtocolHandler"  
        validate="false" />  
   </protocols>  
</system.web>  
```  
  
## <a name="see-also"></a>Consulte também

- [Configurar o WAS para uso com o WCF](configuring-the-wpa--service-for-use-with-wcf.md)
- [Recursos de hospedagem do Windows Server AppFabric](/previous-versions/appfabric/ee677189(v=azure.10))
