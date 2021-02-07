---
description: 'Saiba mais sobre: alterando os níveis de compartilhamento de cache para atividades de envio'
title: Alterando os níveis de compartilhamento de cache para enviar atividades
ms.date: 03/30/2017
ms.assetid: 03926a64-753d-460e-ac06-2a4ff8e1bbf5
ms.openlocfilehash: 7ced6a8a18779a0c0d5914e63fde658b6d0130ac
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99705207"
---
# <a name="changing-the-cache-sharing-levels-for-send-activities"></a>Alterando os níveis de compartilhamento de cache para enviar atividades

A <xref:System.ServiceModel.Activities.SendMessageChannelCache> extensão permite que você personalize os níveis de compartilhamento de cache, as configurações do cache da fábrica de canais e as configurações do cache do canal para fluxos de trabalho que enviam mensagens para pontos de extremidade de serviço usando <xref:System.ServiceModel.Activities.Send> atividades de mensagens. Esses fluxos de trabalho normalmente são fluxos de trabalho do cliente, mas também pode ser o serviços de fluxo de trabalho que são hospedados em um <xref:System.ServiceModel.WorkflowServiceHost>. O cache da fábrica de canais contém objetos armazenados em cache <xref:System.ServiceModel.ChannelFactory%601> . O cache do canal contém canais armazenados em cache.  
  
> [!NOTE]
> Os fluxos de trabalho podem usar <xref:System.ServiceModel.Activities.Send> atividades de mensagens para enviar mensagens ou parâmetros. O tempo de execução do fluxo de trabalho adiciona fábricas de canal ao cache que cria canais do tipo <xref:System.ServiceModel.Channels.IRequestChannel> quando você usa uma <xref:System.ServiceModel.Activities.ReceiveReply> atividade com uma <xref:System.ServiceModel.Activities.Send> atividade e um <xref:System.ServiceModel.Channels.IOutputChannel> ao usar apenas uma <xref:System.ServiceModel.Activities.Send> atividade (não <xref:System.ServiceModel.Activities.ReceiveReply> ).  
  
## <a name="the-cache-sharing-levels"></a>Os níveis de compartilhamento de cache  

 Por padrão, em um fluxo de trabalho hospedado por um <xref:System.ServiceModel.WorkflowServiceHost> cache usado pelas <xref:System.ServiceModel.Activities.Send> atividades de mensagens é compartilhado entre todas as instâncias de fluxo de trabalho no <xref:System.ServiceModel.WorkflowServiceHost> (cache de nível de host). Um fluxo de trabalho de cliente não é hospedado por um <xref:System.ServiceModel.WorkflowServiceHost>, o cache está disponível somente para a instância de fluxo de trabalho (cache de nível de instância). O cache só está disponível para <xref:System.ServiceModel.Activities.Send> atividades que não usam pontos de extremidade definidos na configuração, a menos que o cache não seguro esteja habilitado.  
  
 A seguir estão os diferentes níveis de compartilhamento de cache disponíveis para <xref:System.ServiceModel.Activities.Send> atividades em um fluxo de trabalho e seu uso recomendado:  
  
- **Nível de host**: no nível de compartilhamento de host, o cache está disponível somente para as instâncias de fluxo de trabalho hospedadas no host do serviço de fluxo de trabalho. Um cache também pode ser compartilhado entre hosts do serviço de fluxo de trabalho em um cache de todo o processo.  
  
- **Nível de instância**: no nível de compartilhamento da instância, o cache está disponível para uma instância de fluxo de trabalho específica durante seu tempo de vida, mas o cache não está disponível para outras instâncias de fluxo de trabalho.  
  
- **Sem cache**: o cache será desativado por padrão se você tiver um fluxo de trabalho que usa pontos de extremidade definidos na configuração. Também é recomendável manter o cache desativado nesse caso porque ativá-lo pode não ser seguro. Por exemplo, se uma identidade diferente (credenciais diferentes ou o uso da representação) for necessária para cada envio.  
  
## <a name="changing-the-cache-sharing-level-for-a-client-workflow"></a>Alterando o nível de compartilhamento do cache para um fluxo de trabalho do cliente  

 Para definir o compartilhamento de cache em um fluxo de trabalho de cliente, adicione uma instância da <xref:System.ServiceModel.Activities.SendMessageChannelCache> classe como uma extensão para o conjunto desejado de instâncias de fluxo de trabalho. Isso resulta no compartilhamento do cache em todas as instâncias de fluxo de trabalho. Os exemplos de código a seguir mostram como executar essas etapas.  
  
 Primeiro, declare uma instância do tipo <xref:System.ServiceModel.Activities.SendMessageChannelCache> .  
  
```csharp  
// Create an instance of SendMessageChannelCache with default cache settings.  
static SendMessageChannelCache sharedChannelCacheExtension =  
    new SendMessageChannelCache();  
```  
  
 Em seguida, adicione a extensão de cache a cada instância de fluxo de trabalho do cliente.  
  
```csharp
WorkflowApplication clientInstance1 = new WorkflowApplication(new clientWorkflow1());  
WorkflowApplication clientInstance2 = new WorkflowApplication(new clientWorkflow2());  
  
// Share the cache extension object
  
clientInstance1.Extensions.Add(sharedChannelCacheExtension);  
clientInstance2.Extensions.Add(sharedChannelCacheExtension);  
```  
  
## <a name="changing-the-cache-sharing-level-for-a-hosted-workflow-service"></a>Alterando o nível de compartilhamento do cache para um serviço de fluxo de trabalho hospedado  

 Para definir o compartilhamento de cache em um serviço de fluxo de trabalho hospedado, adicione uma instância da <xref:System.ServiceModel.Activities.SendMessageChannelCache> classe como uma extensão a todos os hosts do serviço de fluxo de trabalho. Isso resulta no compartilhamento do cache em todos os hosts do serviço de fluxo de trabalho. Os exemplos de código a seguir mostram como executar essas etapas.  
  
 Primeiro, declare uma instância do tipo <xref:System.ServiceModel.Activities.SendMessageChannelCache> no nível de classe.  
  
```csharp  
// Create static instance of SendMessageChannelCache with default cache settings.  
static SendMessageChannelCache sharedChannelCacheExtension = new  
    SendMessageChannelCache();  
```  
  
 Em seguida, adicione a extensão de cache estático a cada host de serviço de fluxo de trabalho.  
  
```csharp  
WorkflowServiceHost host1 = new WorkflowServiceHost(new serviceWorkflow1(), new Uri(baseAddress1));  
WorkflowServiceHost host2 = new WorkflowServiceHost(new serviceWorkflow2(), new Uri(baseAddress2));  
  
// Share the static cache to get an AppDomain level cache.  
host1.WorkflowExtensions.Add(sharedChannelCacheExtension);  
host2.WorkflowExtensions.Add(sharedChannelCacheExtension);  
```  
  
 Para definir o compartilhamento de cache em um serviço de fluxo de trabalho hospedado para o nível de instância, adicione um `Func<SendMessageChannelCache>` delegado como uma extensão ao host do serviço de fluxo de trabalho e atribua esse delegado ao código que instancia uma nova instância da <xref:System.ServiceModel.Activities.SendMessageChannelCache> classe. Isso resulta em um cache diferente para cada instância de fluxo de trabalho individual, em vez de um único cache compartilhado por todas as instâncias de fluxo de trabalho no host do serviço de fluxo de trabalho. O exemplo de código a seguir mostra como conseguir isso usando uma expressão lambda para definir diretamente a <xref:System.ServiceModel.Activities.SendMessageChannelCache> extensão à qual o delegado aponta.  
  
```csharp
serviceHost.WorkflowExtensions.Add(() => new SendMessageChannelCache  
{  
    // Use FactorySettings property to add custom factory cache settings.  
    FactorySettings = new ChannelCacheSettings
    { MaxItemsInCache = 5, },  
    // Use ChannelSettings property to add custom channel cache settings.  
    ChannelSettings = new ChannelCacheSettings
    { MaxItemsInCache = 10 },  
});  
```  
  
## <a name="customizing-cache-settings"></a>Personalizando configurações de cache  

 Você pode personalizar as configurações de cache para o cache de fábrica do canal e o cache do canal. As configurações de cache são definidas na <xref:System.ServiceModel.Activities.ChannelCacheSettings> classe. A <xref:System.ServiceModel.Activities.SendMessageChannelCache> classe define as configurações de cache padrão para o cache de fábrica de canais e o cache de canal em seu construtor sem parâmetros. A tabela a seguir lista os valores padrão dessas configurações de cache para cada tipo de cache.  
  
|Settings|LeaseTimeout (min)|IdleTimeout (min)|MaxItemsInCache|  
|-|-|-|-|  
|Padrão de cache de fábrica|TimeSpan.MaxValue|2|16|  
|Padrão de cache do canal|5|2|16|  
  
 Para personalizar o cache de fábrica e as configurações de cache do canal, crie uma instância da <xref:System.ServiceModel.Activities.SendMessageChannelCache> classe usando o construtor <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> com parâmetros e passe uma nova instância do <xref:System.ServiceModel.Activities.ChannelCacheSettings> com valores personalizados para cada um dos `factorySettings` `channelSettings` parâmetros e. Em seguida, adicione a nova instância dessa classe como uma extensão a um host do serviço de fluxo de trabalho ou a uma instância de fluxo de trabalho. O exemplo de código a seguir mostra como executar essas etapas para uma instância de fluxo de trabalho.  
  
```csharp  
ChannelCacheSettings factorySettings = new ChannelCacheSettings{  
                        MaxItemsInCache = 5,
                        IdleTimeout = TimeSpan.FromMinutes(5),
                        LeaseTimeout = TimeSpan.FromMinutes(20)};  
  
ChannelCacheSettings channelSettings = new ChannelCacheSettings{  
                        MaxItemsInCache = 5,
                        IdleTimeout = TimeSpan.FromMinutes(2),  
                        LeaseTimeout = TimeSpan.FromMinutes(10) };  
  
SendMessageChannelCache customChannelCacheExtension =
    new SendMessageChannelCache(factorySettings, channelSettings);  
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 Para habilitar o Caching quando seu serviço de fluxo de trabalho tiver pontos de extremidade definidos na configuração, crie uma instância da <xref:System.ServiceModel.Activities.SendMessageChannelCache> classe usando o construtor <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> com parâmetros com o `allowUnsafeCaching` parâmetro definido como `true` . Em seguida, adicione a nova instância dessa classe como uma extensão a um host do serviço de fluxo de trabalho ou a uma instância de fluxo de trabalho. O exemplo de código a seguir mostra como habilitar o Caching para uma instância de fluxo de trabalho.  
  
```csharp  
SendMessageChannelCache customChannelCacheExtension =
    new SendMessageChannelCache{ AllowUnsafeCaching = true };  
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 Para desabilitar completamente o cache para as fábricas de canal e os canais, desabilite o cache da fábrica de canais. Fazer isso também desativa o cache do canal à medida que os canais são de propriedade de suas fábricas de canal correspondentes. Para desabilitar o cache da fábrica de canais, passe o `factorySettings` parâmetro para o <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> Construtor inicializado para uma <xref:System.ServiceModel.Activities.ChannelCacheSettings> instância com um <xref:System.ServiceModel.Activities.ChannelCacheSettings.MaxItemsInCache%2A> valor de 0. O exemplo de código a seguir mostra isso.  
  
```csharp  
// Disable the factory cache. This results in the channel cache to be turned off as well.  
ChannelCacheSettings factorySettings = new ChannelCacheSettings  
    { MaxItemsInCache = 0 };  
  
ChannelCacheSettings channelSettings = new ChannelCacheSettings();  
  
SendMessageChannelCache customChannelCacheExtension =
    new SendMessageChannelCache(factorySettings, channelSettings);
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 Você pode optar por usar apenas o cache da fábrica do canal e desabilitar o cache do canal passando o `channelSettings` parâmetro para o <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> Construtor inicializado para uma <xref:System.ServiceModel.Activities.ChannelCacheSettings> instância com um <xref:System.ServiceModel.Activities.ChannelCacheSettings.MaxItemsInCache%2A> valor de 0. O exemplo de código a seguir mostra isso.  
  
```csharp  
ChannelCacheSettings factorySettings = new ChannelCacheSettings();  
// Disable only the channel cache.  
ChannelCacheSettings channelSettings = new ChannelCacheSettings  
    { MaxItemsInCache = 0};  
  
SendMessageChannelCache customChannelCacheExtension =
    new SendMessageChannelCache(factorySettings, channelSettings);
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 Em um serviço hospedado de fluxo de trabalho, você pode especificar os cache e o canal cache configurações de fábrica no arquivo de configuração do aplicativo. Para fazer isso, adicionar um comportamento de serviço que contém as configurações de cache para cache de fábrica e o canal e adicionar esse comportamento de serviço ao seu serviço. O exemplo a seguir mostra o conteúdo de um arquivo de configuração que contém o `MyChannelCacheBehavior` comportamento do serviço com o cache de fábrica personalizado e as configurações de cache do canal. Esse comportamento de serviço é adicionado ao serviço por meio do `behaviorConfiguration` atributo.  
  
```xml  
<configuration>
  <system.serviceModel>  
    <!-- List of other config sections here -->
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="MyChannelCacheBehavior">  
          <sendMessageChannelCache allowUnsafeCaching ="false" >  
            <!-- Control only the host level settings -->
            <factorySettings maxItemsInCache = "8" idleTimeout = "00:05:00" leaseTimeout="10:00:00" />  
            <channelSettings maxItemsInCache = "32" idleTimeout = "00:05:00" leaseTimeout="00:06:00" />  
          </sendMessageChannelCache>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service name="MyService" behaviorConfiguration="MyChannelCacheBehavior" />  
    </services>  
  </system.serviceModel>  
</configuration>  
```
