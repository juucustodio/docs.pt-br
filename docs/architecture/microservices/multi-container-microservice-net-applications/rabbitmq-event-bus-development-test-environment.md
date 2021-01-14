---
title: Implementando um barramento de eventos com o RabbitMQ para o ambiente de desenvolvimento ou de teste
description: Arquitetura de microsserviços do .NET para aplicativos .NET em contêineres | Use o RabbitMQ para implementar mensagens de barramento de eventos para eventos de integração para os ambientes de desenvolvimento ou de teste.
ms.date: 01/13/2021
ms.openlocfilehash: a1e7d11e376080a03269f202fa6ae24ffeb0f4d2
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188075"
---
# <a name="implementing-an-event-bus-with-rabbitmq-for-the-development-or-test-environment"></a>Implementando um barramento de eventos com o RabbitMQ para o ambiente de desenvolvimento ou de teste

Devemos começar dizendo que, se você criar seu barramento de eventos personalizado com base no RabbitMQ em execução em um contêiner, como o aplicativo eShopOnContainers faz, ele deverá ser usado apenas para seus ambientes de desenvolvimento e teste. Não use-o para seu ambiente de produção, a menos que esteja criando-o como parte de um barramento de serviço pronto para produção. Um barramento de eventos personalizado simples talvez não tenha muitos recursos críticos prontos para produção que um barramento de serviço comercial tem.

Uma das implementações personalizadas do barramento de evento no eShopOnContainers é basicamente uma biblioteca que usa a API RabbitMQ. (Há outra implementação baseada no barramento de serviço do Azure.)

A implementação do barramento de eventos com RabbitMQ permite que os microsserviços assinem, publiquem e recebam eventos, conforme mostrado na Figura 6-21.

![Diagrama mostrando RabbitMQ entre remetente de mensagem e receptor de mensagem.](./media/rabbitmq-event-bus-development-test-environment/rabbitmq-implementation.png)

**Figura 6-21.** Implementação de um barramento de eventos do RabbitMQ

O RabbitMQ é um intermediário entre o publicador da mensagem e os assinantes, para tratar da distribuição. No código, a classe EventBusRabbitMQ implementa a interface IEventBus genérica. Essa implementação se baseia na injeção de dependência para que você possa alternar desta versão de desenvolvimento/teste para uma versão de produção.

```csharp
public class EventBusRabbitMQ : IEventBus, IDisposable
{
    // Implementation using RabbitMQ API
    //...
}
```

A implementação do RabbitMQ de um barramento de eventos de Desenvolvimento/Teste de exemplo é um código clichê. Ele precisa lidar com a conexão com o servidor do RabbitMQ e fornecer o código para a publicação de um evento de mensagem nas filas. Ele também precisa implementar um dicionário de coleções de manipuladores de eventos de integração para cada tipo de evento; esses tipos de evento podem ter uma instanciação diferente e diferentes assinaturas para cada microsserviço receptor, conforme mostrado na Figura 6-21.

## <a name="implementing-a-simple-publish-method-with-rabbitmq"></a>Implementando um método de publicação simples com RabbitMQ

O código a seguir é uma versão **_simplificada_* de uma implementação de barramento de evento para RabbitMQ, para demonstrar todo o cenário. Na prática, a conexão não é tratada dessa maneira. Para ver a implementação completa, confira o código real no repositório [dotnet-architecture/eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/BuildingBlocks/EventBus/EventBusRabbitMQ/EventBusRabbitMQ.cs).

```csharp
public class EventBusRabbitMQ : IEventBus, IDisposable
{
    // Member objects and other methods ...
    // ...

    public void Publish(IntegrationEvent @event)
    {
        var eventName = @event.GetType().Name;
        var factory = new ConnectionFactory() { HostName = _connectionString };
        using (var connection = factory.CreateConnection())
        using (var channel = connection.CreateModel())
        {
            channel.ExchangeDeclare(exchange: _brokerName,
                type: "direct");
            string message = JsonConvert.SerializeObject(@event);
            var body = Encoding.UTF8.GetBytes(message);
            channel.BasicPublish(exchange: _brokerName,
                routingKey: eventName,
                basicProperties: null,
                body: body);
       }
    }
}
```

O [código real](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/BuildingBlocks/EventBus/EventBusRabbitMQ/EventBusRabbitMQ.cs) do método publish no aplicativo eShopOnContainers é melhorado usando uma política de repetição [Polly](https://github.com/App-vNext/Polly) , que repete a tarefa algumas vezes, caso o contêiner RabbitMQ não esteja pronto. Esse cenário pode ocorrer quando o Docker-Compose está iniciando os contêineres; por exemplo, o contêiner RabbitMQ pode ser iniciado mais lentamente do que os outros contêineres.

Conforme mencionado anteriormente, há muitas configurações possíveis no RabbitMQ. Portanto, esse código deve ser usado apenas para ambientes de Desenvolvimento/Teste.

## <a name="implementing-the-subscription-code-with-the-rabbitmq-api"></a>Implementando o código de assinatura com a API do RabbitMQ

Como acontece com o código de publicação, o código a seguir é uma simplificação de parte da implementação do barramento de eventos para RabbitMQ. Mais uma vez, geralmente não é necessário alterá-lo, a menos que você o esteja aprimorando.

```csharp
public class EventBusRabbitMQ : IEventBus, IDisposable
{
    // Member objects and other methods ...
    // ...

    public void Subscribe<T, TH>()
        where T : IntegrationEvent
        where TH : IIntegrationEventHandler<T>
    {
        var eventName = _subsManager.GetEventKey<T>();

        var containsKey = _subsManager.HasSubscriptionsForEvent(eventName);
        if (!containsKey)
        {
            if (!_persistentConnection.IsConnected)
            {
                _persistentConnection.TryConnect();
            }

            using (var channel = _persistentConnection.CreateModel())
            {
                channel.QueueBind(queue: _queueName,
                                    exchange: BROKER_NAME,
                                    routingKey: eventName);
            }
        }

        _subsManager.AddSubscription<T, TH>();
    }
}
```

Cada tipo de evento tem um canal relacionado para obter eventos do RabbitMQ. Em seguida, é possível ter tantos manipuladores de eventos por tipo de evento e de canal conforme necessário.

O método Subscribe aceita um objeto IIntegrationEventHandler, que é como um método de retorno de chamada no microsserviço atual, além de seu objeto IntegrationEvent relacionado. O código, então, adiciona o manipulador de eventos à lista de manipuladores de eventos que cada tipo de evento de integração pode ter por microsserviço do cliente. Se o código do cliente ainda não tiver assinado o evento, o código criará um canal para o tipo de evento para que ele possa receber eventos em um estilo de push do RabbitMQ quando esse evento for publicado de qualquer outro serviço.

Conforme mencionado acima, o barramento de evento implementado em eShopOnContainers tem apenas e finalidade Education, já que trata apenas dos principais cenários, portanto, ele não está pronto para produção.

Para cenários de produção, verifique os recursos adicionais abaixo, específicos para RabbitMQ e a seção [implementando a comunicação baseada em evento entre os microserviços](./integration-event-based-microservice-communications.md#additional-resources) .

## <a name="additional-resources"></a>Recursos adicionais

Uma solução pronta para produção com suporte para RabbitMQ.

- _ *EasyNetQ**-cliente de API .net de código aberto para RabbitMQ \
  <https://easynetq.com/>

- **MassTransit** \
  <https://masstransit-project.com/>
  
> [!div class="step-by-step"]
> [Anterior](integration-event-based-microservice-communications.md) 
>  [Avançar](subscribe-events.md)
