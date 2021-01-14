---
title: Assinando eventos
description: Arquitetura de microsserviços .NET para aplicativos .NET em contêineres | Entenda os detalhes de publicação e assinatura de eventos de integração.
ms.date: 01/13/2021
ms.openlocfilehash: c9146ddbdfbf00e743108c07af1f74d7690a17a8
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188719"
---
# <a name="subscribing-to-events"></a>Assinando eventos

A primeira etapa para usar o barramento de eventos é fazer com que os microsserviços assinem os eventos que eles desejam receber. Essa funcionalidade deve ser feita nos microserviços do destinatário.

O código simples a seguir mostra o que cada destinatário de microsserviço precisa implementar ao iniciar o serviço (ou seja, a classe `Startup`) para assinar os eventos que precisa. Nesse caso, o microsserviço `basket-api` precisa assinar as mensagens `ProductPriceChangedIntegrationEvent` e `OrderStartedIntegrationEvent`.

Por exemplo, ao assinar o `ProductPriceChangedIntegrationEvent` evento, isso torna o microatendimento da cesta ciente de quaisquer alterações no preço do produto e permite que ele avise o usuário sobre a alteração se o produto estiver no carrinho do usuário.

```csharp
var eventBus = app.ApplicationServices.GetRequiredService<IEventBus>();

eventBus.Subscribe<ProductPriceChangedIntegrationEvent,
                   ProductPriceChangedIntegrationEventHandler>();

eventBus.Subscribe<OrderStartedIntegrationEvent,
                   OrderStartedIntegrationEventHandler>();

```

Depois que esse código for executado, o microsserviço assinante escutará por meio de canais RabbitMQ. Quando qualquer mensagem do tipo ProductPriceChangedIntegrationEvent chegar, o código invocará o manipulador de eventos, que será passado a ele e processará o evento.

## <a name="publishing-events-through-the-event-bus"></a>Publicando eventos por meio do barramento de eventos

Por fim, o remetente da mensagem (microsserviço de origem) publica os eventos de integração com um código semelhante ao exemplo a seguir. (Essa abordagem é um exemplo simplificado que não leva em conta a atomicidade.) Você implementaria um código semelhante sempre que um evento precisar ser propagado em vários microserviços, normalmente logo após a confirmação dos dados ou das transações do microserviço de origem.

Primeiro, o objeto de implementação do barramento de eventos (baseado no RabbitMQ ou em um barramento de serviço) seria injetado no construtor do controlador, como no código a seguir:

```csharp
[Route("api/v1/[controller]")]
public class CatalogController : ControllerBase
{
    private readonly CatalogContext _context;
    private readonly IOptionsSnapshot<Settings> _settings;
    private readonly IEventBus _eventBus;

    public CatalogController(CatalogContext context,
        IOptionsSnapshot<Settings> settings,
        IEventBus eventBus)
    {
        _context = context;
        _settings = settings;
        _eventBus = eventBus;
    }
    // ...
}
```

Em seguida, você o utiliza dos métodos do controlador, como no método UpdateProduct:

```csharp
[Route("items")]
[HttpPost]
public async Task<IActionResult> UpdateProduct([FromBody]CatalogItem product)
{
    var item = await _context.CatalogItems.SingleOrDefaultAsync(
        i => i.Id == product.Id);
    // ...
    if (item.Price != product.Price)
    {
        var oldPrice = item.Price;
        item.Price = product.Price;
        _context.CatalogItems.Update(item);
        var @event = new ProductPriceChangedIntegrationEvent(item.Id,
            item.Price,
            oldPrice);
        // Commit changes in original transaction
        await _context.SaveChangesAsync();
        // Publish integration event to the event bus
        // (RabbitMQ or a service bus underneath)
        _eventBus.Publish(@event);
        // ...
    }
    // ...
}
```

Nesse caso, como o microsserviço de origem é um microsserviço CRUD simples, o código é colocado diretamente em um controlador de API Web.

Em microsserviços mais avançados, como ao usar abordagens de CQRS, ele pode ser implementado na classe `CommandHandler`, dentro do método `Handle()`.

### <a name="designing-atomicity-and-resiliency-when-publishing-to-the-event-bus"></a>Criando atomicidade e resiliência ao publicar no barramento de eventos

Ao publicar eventos de integração por meio de um sistema de mensagens distribuído como o barramento de eventos, surge o problema da atualização do banco de dados original e da publicação de um evento de forma atômica (ou seja, ambas as operações são concluídas ou nenhuma delas). Por exemplo, no exemplo simplificado mostrado anteriormente, o código confirma os dados no banco de dados quando o preço do produto é alterado e, em seguida, publica uma mensagem ProductPriceChangedIntegrationEvent. Inicialmente, pode parecer essencial que essas duas operações sejam executada atomicamente. No entanto, se você estiver usando uma transação distribuída envolvendo o banco de dados e o agente de mensagem, como você faz em sistemas mais antigos, como o [MSMQ (enfileiramento de mensagens da Microsoft)](/previous-versions/windows/desktop/legacy/ms711472(v=vs.85)), essa abordagem não é recomendada pelos motivos descritos pelo [teorema Cap](https://www.quora.com/What-Is-CAP-Theorem-1).

Basicamente, você usa microsserviços para criar sistemas escalonáveis e altamente disponíveis. Simplificando um pouco, o teorema de extremidade diz que você não pode criar um banco de dados (distribuído) (ou um microserviço que possui seu modelo) que está continuamente disponível, consistente *e* tolerante a qualquer partição. Você deve escolher duas dessas três propriedades.

Em arquiteturas baseadas em microserviços, você deve escolher disponibilidade e tolerância, além de realçar a consistência forte. Portanto, na maioria dos aplicativos modernos baseados em microsserviços, geralmente não é interessante usar transações distribuídas no sistema de mensagens, como ao implementar [transações distribuídas](/previous-versions/windows/desktop/ms681205(v=vs.85)) com base no DTC (Coordenador de Transações Distribuídas) do Windows com o [MSMQ](/previous-versions/windows/desktop/legacy/ms711472(v=vs.85)).

Vamos voltar para o problema inicial e seu exemplo. Se o serviço falhar depois que o banco de dados for atualizado (nesse caso, logo após a linha de código com `_context.SaveChangesAsync()` ), mas antes de o evento de integração ser publicado, o sistema geral poderá se tornar inconsistente. Essa abordagem pode ser crítica para os negócios, dependendo da operação de negócios específica com a qual você está lidando.

Como mencionado anteriormente na seção de arquitetura, você pode ter várias abordagens para lidar com esse problema:

- Usando o padrão [Event Sourcing](/azure/architecture/patterns/event-sourcing) completo.

- Usando mineração do log de transações.

- Usando o [padrão Outbox](https://www.kamilgrzybek.com/design/the-outbox-pattern/). Essa é uma tabela transacional para armazenar os eventos de integração (estendendo a transação local).

Neste cenário, o uso do padrão ES (Event Sourcing) completo é uma das melhores abordagens, se não for *a* melhor. No entanto, em muitos cenários de aplicativo, pode ser impossível implementar um sistema completo de ES. O ES significa o armazenamento somente dos eventos de domínio em seu banco de dados transacional, em vez de armazenar dados do estado atual. Armazenar apenas os eventos de domínio pode ter grandes benefícios, como ter o histórico do sistema disponível e poder determinar o estado do sistema em qualquer momento no passado. No entanto, implementar um sistema de ES completo exige que você refaça a arquitetura da maior parte do seu sistema e também pode apresentar muitas outras complexidades e requisitos. Por exemplo, vai ser interessante usar um banco de dados criado especificamente para fornecimento de eventos, como o [Event Store](https://eventstore.org/), ou um banco de dados orientado a documentos, como Azure Cosmos DB, MongoDB, Cassandra, CouchDB ou RavenDB. O ES é uma ótima abordagem para esse problema, mas não é a solução mais fácil, a menos que você já esteja familiarizado com fornecimento de eventos.

A opção de usar a mineração de logs de transações inicialmente parece transparente. No entanto, para usar essa abordagem, o microsserviço deverá ser acoplado ao seu log de transações do RDBMS, como o log de transações do SQL Server. Essa abordagem provavelmente não é desejável. Outra desvantagem é que as atualizações de baixo nível registradas no log de transações podem não estar no mesmo nível que seus eventos de integração de alto nível. Nesse caso, o processo de engenharia reversa dessas operações do log de transações poderá ser difícil.

Uma abordagem equilibrada é uma combinação de uma tabela de banco de dados transacional e um padrão de ES simplificado. Você pode usar um estado como "pronto para publicar o evento", que você definiu no evento original ao confirmá-lo na tabela de eventos de integração. Em seguida, você tenta publicar o evento no barramento de eventos. Se a ação de publicar evento for bem sucedido, você iniciará outra transação no serviço de origem e moverá o estado de "pronto para publicar o evento" para "evento já publicado".

Se a ação publicar evento no barramento de eventos falhar, os dados ainda não estarão inconsistentes no microserviço de origem — ele ainda estará marcado como "pronto para publicar o evento" e, em relação ao restante dos serviços, ele será eventualmente consistente. Você sempre fazer com que trabalhos em segundo plano verifiquem o estado das transações ou dos eventos de integração. Se o trabalho encontrar um evento no estado "pronto para publicar o evento", ele poderá tentar republicar esse evento no barramento de evento.

Observe que, com essa abordagem, você estará persistindo apenas os eventos de integração de cada microsserviço de origem e somente os eventos que você deseja comunicar para outros microsserviços ou sistemas externos. Por outro lado, em um sistema completo de ES, você também armazena todos os eventos de domínio.

Portanto, essa abordagem equilibrada é um sistema de ES simplificado. Você precisa de uma lista de eventos de integração com seu estado atual ("pronto para publicar" versus "publicado"). Mas você só precisa implementar esses estados para os eventos de integração. E, nessa abordagem, não é necessário armazenar todos os dados de domínio como eventos no banco de dados transacional, como você faria em um sistema completo de ES.

Se já está usando um banco de dados relacional, você pode usar uma tabela transacional para armazenar eventos de integração. Para obter a atomicidade em seu aplicativo, você usa um processo de duas etapas com base nas transações locais. Basicamente, você tem uma tabela IntegrationEvent no mesmo banco de dados em que estão as entidades de domínio. Essa tabela funciona como um seguro para a obtenção de atomicidade, para que você inclua eventos de integração persistidos nas mesmas transações que estão confirmando seus dados de domínio.

Passo a passo, o processo é o seguinte:

1. O aplicativo inicia uma transação de banco de dados local.

2. Em seguida, ele atualiza o estado das suas entidades de domínio e insere um evento na tabela de eventos de integração.

3. Por fim, ele confirma a transação, de modo que você obtenha a atomicidade desejada e

4. Você publica o evento de alguma forma (a seguir).

Ao implementar as etapas de publicação dos eventos, você tem estas opções:

- Publicar o evento de integração logo após a confirmação da transação e usar outra transação local para marcar os eventos na tabela como sendo publicados. Em seguida, usar a tabela apenas como um artefato para controlar os eventos de integração, em caso de problemas com os microsserviços remotos, e executar ações compensatórias com base nos eventos de integração armazenados.

- Usar a tabela como um tipo de fila. Um thread ou processo do aplicativo separado consulta a tabela de eventos de integração, publica os eventos no barramento de eventos e, em seguida, usa uma transação local para marcar os eventos como publicados.

A Figura 6-22 mostra a arquitetura da primeira dessas abordagens.

![Diagrama de atomicidade ao publicar sem um microserviço de trabalho.](./media/subscribe-events/atomicity-publish-event-bus.png)

**Figura 6-22**. Atomicidade ao publicar eventos no barramento de eventos

A abordagem ilustrada na Figura 6-22 não tem um microsserviço de trabalho adicional, que é responsável por verificar e confirmar o êxito dos eventos de integração publicados. Em caso de falha, esse microsserviço de trabalho verificador adicional pode ler os eventos na tabela e publicá-los novamente, ou seja, repetir a etapa 2.

Em relação à segunda abordagem: você usa a tabela EventLog como uma fila e sempre usa um microsserviço de trabalho para publicar as mensagens. Nesse caso, o processo é como o mostrado na Figura 6-23. Ela mostra um microsserviço adicional, e a tabela é a única fonte durante a publicação de eventos.

![Diagrama de atomicidade ao publicar com um microserviço de trabalho.](./media/subscribe-events/atomicity-publish-worker-microservice.png)

**Figura 6-23**. Atomicidade ao publicar eventos no barramento de eventos com um microsserviço de trabalho

Para simplificar, o exemplo eShopOnContainers usa a primeira abordagem (sem processos adicionais nem microsserviços verificadores) e o barramento de eventos. No entanto, o exemplo de eShopOnContainers não está tratando todos os casos de falha possíveis. Em um aplicativo real implantado na nuvem, você deve aceitar o fato de que os problemas surgirão eventualmente, e você deverá implementar essa lógica de verificação e reenvio. O uso da tabela como uma fila pode ser mais eficiente do que a primeira abordagem se você tem essa tabela como uma única fonte de eventos ao publicá-los (com o trabalho) por meio do barramento de eventos.

### <a name="implementing-atomicity-when-publishing-integration-events-through-the-event-bus"></a>Implementando atomicidade ao publicar eventos de integração por meio do barramento de eventos

O código a seguir mostra como criar uma única transação que envolva vários objetos DbContext: um contexto relacionados aos dados originais que estão sendo atualizados e o segundo contexto relacionado à tabela IntegrationEventLog.

A transação no código de exemplo abaixo não será resiliente se as conexões com o banco de dados tiverem algum problema no momento em que o código estiver em execução. Isso pode ocorrer em sistemas baseados em nuvem, como o BD SQL do Azure, que pode mover bancos de dados entre servidores. Para implementar transações resilientes em vários contextos, consulte a seção [Implementando conexões de SQL do Entity Framework Core resilientes](../implement-resilient-applications/implement-resilient-entity-framework-core-sql-connections.md) mais adiante, neste guia.

Para maior clareza, o exemplo a seguir mostra todo o processo em um único segmento de código. No entanto, a implementação de eShopOnContainers é Refatorada e divide essa lógica em várias classes para que seja mais fácil de manter.

```csharp
// Update Product from the Catalog microservice
//
public async Task<IActionResult> UpdateProduct([FromBody]CatalogItem productToUpdate)
{
  var catalogItem =
       await _catalogContext.CatalogItems.SingleOrDefaultAsync(i => i.Id ==
                                                               productToUpdate.Id);
  if (catalogItem == null) return NotFound();

  bool raiseProductPriceChangedEvent = false;
  IntegrationEvent priceChangedEvent = null;

  if (catalogItem.Price != productToUpdate.Price)
          raiseProductPriceChangedEvent = true;

  if (raiseProductPriceChangedEvent) // Create event if price has changed
  {
      var oldPrice = catalogItem.Price;
      priceChangedEvent = new ProductPriceChangedIntegrationEvent(catalogItem.Id,
                                                                  productToUpdate.Price,
                                                                  oldPrice);
  }
  // Update current product
  catalogItem = productToUpdate;

  // Just save the updated product if the Product's Price hasn't changed.
  if (!raiseProductPriceChangedEvent)
  {
      await _catalogContext.SaveChangesAsync();
  }
  else  // Publish to event bus only if product price changed
  {
        // Achieving atomicity between original DB and the IntegrationEventLog
        // with a local transaction
        using (var transaction = _catalogContext.Database.BeginTransaction())
        {
           _catalogContext.CatalogItems.Update(catalogItem);
           await _catalogContext.SaveChangesAsync();

           // Save to EventLog only if product price changed
           if(raiseProductPriceChangedEvent)
               await _integrationEventLogService.SaveEventAsync(priceChangedEvent);

           transaction.Commit();
        }

      // Publish the integration event through the event bus
      _eventBus.Publish(priceChangedEvent);

      _integrationEventLogService.MarkEventAsPublishedAsync(
                                                priceChangedEvent);
  }

  return Ok();
}

```

Depois que o evento de integração ProductPriceChangedIntegrationEvent é criado, a transação que armazena a operação de domínio original (atualizar o item de catálogo) também inclui a persistência do evento na tabela EventLog. Isso faz com que ele se torne uma única transação, e sempre será possível verificar se as mensagens de evento foram enviadas.

A tabela do log de eventos é atualizada atomicamente com a operação do banco de dados original, usando uma transação local no mesmo banco de dados. Se uma das operações falha, uma exceção é gerada e a transação reverte qualquer operação concluída, mantendo a consistência entre as operações de domínio e as mensagens de evento salvas na tabela.

### <a name="receiving-messages-from-subscriptions-event-handlers-in-receiver-microservices"></a>Recebendo mensagens de assinaturas: manipuladores de eventos em microsserviços destinatários

Além da lógica de assinatura de evento, você precisa implementar o código interno para os manipuladores de eventos de integração (como um método de retorno de chamada). O manipulador de eventos é o local em que você especifica o local em que as mensagens de eventos de um determinado tipo serão recebidas e processadas.

Primeiro, um manipulador de eventos recebe uma instância de evento do barramento de eventos. Em seguida, ele localiza o componente a ser processado, relacionado a esse evento de integração, propagando e persistindo o evento como uma alteração no estado no microsserviço destinatário. Por exemplo, se um evento ProductPriceChanged se origina no microsserviço catálogo, ele é tratado no microsserviço carrinho de compras e também altera o estado nesse microsserviço destinatário de carrinho de compras, conforme mostrado no código a seguir.

```csharp
namespace Microsoft.eShopOnContainers.Services.Basket.API.IntegrationEvents.EventHandling
{
    public class ProductPriceChangedIntegrationEventHandler :
        IIntegrationEventHandler<ProductPriceChangedIntegrationEvent>
    {
        private readonly IBasketRepository _repository;

        public ProductPriceChangedIntegrationEventHandler(
            IBasketRepository repository)
        {
            _repository = repository;
        }

        public async Task Handle(ProductPriceChangedIntegrationEvent @event)
        {
            var userIds = await _repository.GetUsers();
            foreach (var id in userIds)
            {
                var basket = await _repository.GetBasket(id);
                await UpdatePriceInBasketItems(@event.ProductId, @event.NewPrice, basket);
            }
        }

        private async Task UpdatePriceInBasketItems(int productId, decimal newPrice,
            CustomerBasket basket)
        {
            var itemsToUpdate = basket?.Items?.Where(x => int.Parse(x.ProductId) ==
                productId).ToList();
            if (itemsToUpdate != null)
            {
                foreach (var item in itemsToUpdate)
                {
                    if(item.UnitPrice != newPrice)
                    {
                        var originalPrice = item.UnitPrice;
                        item.UnitPrice = newPrice;
                        item.OldUnitPrice = originalPrice;
                    }
                }
                await _repository.UpdateBasket(basket);
            }
        }
    }
}
```

O manipulador de eventos deve verificar se o produto existe em qualquer uma das instâncias do carrinho de compras. Ele também atualiza o preço do item para cada item de linha relacionado ao carrinho. Por fim, ele cria um alerta sobre a alteração de preço, que será exibido para o usuário, conforme mostrado na Figura 6-24.

![Captura de tela de um navegador que mostra a notificação de alteração de preço no carrinho do usuário.](./media/subscribe-events/display-item-price-change.png)

**Figura 6-24**. Exibindo uma alteração de preço de item em um carrinho de compras, conforme comunicado pelos eventos de integração

## <a name="idempotency-in-update-message-events"></a>Idempotência em eventos de mensagem de atualização

Um aspecto importante dos eventos de mensagem de atualização é que uma falha em qualquer ponto da comunicação deverá fazer com que a mensagem seja repetida. Caso contrário, uma tarefa em segundo plano poderá tentar publicar um evento que já tenha sido publicado, criando uma condição de corrida. Verifique se as atualizações são idempotentes ou se elas fornecem informações suficientes para garantir que você possa detectar uma duplicata, descartá-la e enviar de volta apenas uma resposta.

Conforme observado anteriormente, a idempotência significa que uma operação poderá ser executada várias vezes sem alterar o resultado. Em um ambiente de sistema de mensagens, como ao comunicar eventos, um evento será idempotente se ele puder ser entregue várias vezes sem alterar o resultado para o microsserviço destinatário. Isso pode ser necessário devido à natureza do evento em si ou devido à maneira como o sistema manipula o evento. A idempotência de mensagem é importante em qualquer aplicativo que use o sistema de mensagens, e não apenas em aplicativos que implementam o padrão do barramento de eventos.

Um exemplo de uma operação idempotente é uma instrução SQL que insere dados em uma tabela somente se os dados ainda não estiverem na tabela. Não importa quantas vezes você executa essa instrução insert do SQL; o resultado será o mesmo: a tabela conterá esses dados. Essa idempotência também poderá ser necessária ao lidar com mensagens se houver chances de que elas sejam enviadas e processadas mais de uma vez. Por exemplo, se a lógica de repetição fizer com que um remetente envie exatamente a mesma mensagem mais de uma vez, você precisará verificar se ela é idempotente.

É possível projetar mensagens idempotentes. Por exemplo, crie um evento que indica "definir o preço do produto como US$ 25" em vez de "adicionar US$ 5 ao preço do produto". A primeira mensagem pode ser processada com segurança qualquer número de vezes e o resultado será o mesmo. Isso não é válido para a segunda mensagem. Mas, mesmo no primeiro caso, talvez não seja interessante processar o primeiro evento, porque o sistema também pode ter enviado um evento de alteração de preço mais recente, e o novo preço seria substituído.

Outro exemplo pode ser um evento de pedido concluído que é propagado para vários assinantes. O aplicativo precisa certificar-se de que as informações de pedidos sejam atualizadas em outros sistemas apenas uma vez, mesmo se houver eventos de mensagem duplicados para o mesmo evento de ordem concluída.

É conveniente ter algum tipo de identidade por evento, para que você possa criar uma lógica que imponha que cada evento seja processado apenas uma vez em cada destinatário.

Alguns processamentos de mensagens são inerentemente idempotentes. Por exemplo, se um sistema gerar miniaturas de imagem, não importará quantas vezes a mensagem sobre a miniatura gerada vai ser processada; o resultado será que as miniaturas foram geradas e elas serão sempre as mesmas. Por outro lado, operações como chamar um gateway de pagamento para cobrar um cartão de crédito jamais poderão ser idempotentes. Nesses casos, você precisa garantir que o processamento de uma mensagem várias vezes tenha o efeito que você espera.

### <a name="additional-resources"></a>Recursos adicionais

- **Honrando a mensagem Idempotência** \
  <https://docs.microsoft.com/previous-versions/msp-n-p/jj591565(v=pandp.10)#honoring-message-idempotency>

## <a name="deduplicating-integration-event-messages"></a>Eliminando a duplicação de mensagens de eventos de integração

Você pode garantir que os eventos de mensagem sejam enviados e processados apenas uma vez por assinante em diferentes níveis. Uma maneira é usar um recurso de eliminação de duplicação oferecido pela infraestrutura do sistema de mensagens que você está usando. Outra é implementar uma lógica personalizada no microsserviço de destino. A melhor opção é ter validações no nível de transporte e no nível do aplicativo.

### <a name="deduplicating-message-events-at-the-eventhandler-level"></a>Eliminando a duplicação de eventos de mensagem no nível do EventHandler

Uma maneira de garantir que um evento seja processado apenas uma vez por qualquer destinatário é implementando determinada lógica ao processar os eventos de mensagem em manipuladores de eventos. Por exemplo, essa é a abordagem usada no aplicativo eShopOnContainers, como você pode ver no [código-fonte da classe UserCheckoutAcceptedIntegrationEventHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Application/IntegrationEvents/EventHandling/UserCheckoutAcceptedIntegrationEventHandler.cs) quando ele recebe um evento de `UserCheckoutAcceptedIntegrationEvent` integração. (Nesse caso, o `CreateOrderCommand` é encapsulado com um `IdentifiedCommand` , usando o `eventMsg.RequestId` como um identificador, antes de enviá-lo ao manipulador de comandos).

### <a name="deduplicating-messages-when-using-rabbitmq"></a>Eliminando a duplicação de mensagens ao usar RabbitMQ

Quando ocorrem falhas intermitentes na rede, as mensagens podem ser duplicadas e o destinatário da mensagem deve estar preparado para lidar com essas mensagens duplicadas. Sempre que possível, os destinatários devem lidar com as mensagens de maneira idempotente, pois isso é melhor que tratá-las explicitamente com a eliminação de duplicação.

De acordo com a [documentação do RabbitMQ](https://www.rabbitmq.com/reliability.html#consumer), "se uma mensagem for entregue a um consumidor e, em seguida, colocada na fila novamente (porque ela não foi confirmada antes de a conexão do consumidor ser descartada, por exemplo), o RabbitMQ definirá o sinalizador reentregue nele quando ele for entregue novamente (seja para o mesmo consumidor ou outro).

Se o sinalizador "reentregue" for definido, o receptor deverá levar isso em conta, pois a mensagem talvez já tenha sido processada. Mas isso não é garantido; a mensagem pode nunca ter alcançado o destinatário depois de deixar o agente de mensagens, talvez por causa de problemas de rede. Por outro lado, se o sinalizador "reentregue" não for definido, será garantido que a mensagem não tenha sido enviada mais de uma vez. Portanto, o receptor precisa eliminar a duplicação de mensagens ou processar mensagens de forma idempotente somente se o sinalizador "reentregue" for definido na mensagem.

### <a name="additional-resources"></a>Recursos adicionais

- **EShopOnContainers bifurcados usando NServiceBus (software específico)** \
    <https://go.particular.net/eShopOnContainers>

- **Mensagens controladas por evento** \
    <https://patterns.arcitura.com/soa-patterns/design_patterns/event_driven_messaging>

- **Jimmy Bogard. Refatoração em relação à resiliência: avaliando o acoplamento** \
    <https://jimmybogard.com/refactoring-towards-resilience-evaluating-coupling/>

- **Canal de publicação/assinatura** \
    <https://www.enterpriseintegrationpatterns.com/patterns/messaging/PublishSubscribeChannel.html>

- **Comunicação entre contextos limitados** \
    <https://docs.microsoft.com/previous-versions/msp-n-p/jj591572(v=pandp.10)>

- **Consistência eventual** \
    <https://en.wikipedia.org/wiki/Eventual_consistency>

- **Philip Brown. Estratégias para a integração de contextos limitados** \
    <https://www.culttt.com/2014/11/26/strategies-integrating-bounded-contexts/>

- **Chris Richardson. Desenvolvendo microserviços transacionais usando agregações, fornecimento de eventos e CQRS-parte 2** \
    <https://www.infoq.com/articles/microservices-aggregates-events-cqrs-part-2-richardson>

- **Chris Richardson. Padrão de fornecimento do evento** \
    <https://microservices.io/patterns/data/event-sourcing.html>

- **Introdução ao fornecimento de eventos** \
    <https://docs.microsoft.com/previous-versions/msp-n-p/jj591559(v=pandp.10)>

- **Banco de dados Event Store**. Site oficial. \
    <https://geteventstore.com/>

- **Patrick Nommensen. Event-Driven Gerenciamento de Dados para os microserviços** \
    <https://dzone.com/articles/event-driven-data-management-for-microservices-1>

- **Teorema CAP** \
    <https://en.wikipedia.org/wiki/CAP_theorem>

- **O que é o Teorema de CAP?** \
    <https://www.quora.com/What-Is-CAP-Theorem-1>

- **Primer de consistência de dados** \
    <https://docs.microsoft.com/previous-versions/msp-n-p/dn589800(v=pandp.10)>

- **Rick saling. A CAP teorema: por que "tudo é diferente" com a nuvem e a Internet** \
    <https://docs.microsoft.com/archive/blogs/rickatmicrosoft/the-cap-theorem-why-everything-is-different-with-the-cloud-and-internet/>

- **Eric Brewer. LIMITE de doze anos mais tarde: como as "regras" foram alteradas** \
    <https://www.infoq.com/articles/cap-twelve-years-later-how-the-rules-have-changed>

- **Barramento de serviço do Azure. mensagens orientadas: detecção de duplicidades**  \
    <https://code.msdn.microsoft.com/Brokered-Messaging-c0acea25>

- **Guia de Confiabilidade** (documentação do RabbitMQ) \
    <https://www.rabbitmq.com/reliability.html#consumer>

> [!div class="step-by-step"]
> [Anterior](rabbitmq-event-bus-development-test-environment.md) 
>  [Avançar](test-aspnet-core-services-web-apps.md)
