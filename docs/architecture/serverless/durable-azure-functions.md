---
title: Aplicativos duráveis Azure Functions-sem servidor
description: Os Azure Functions duráveis estendem o tempo de execução Azure Functions para permitir fluxos de trabalho com estado no código.
author: cecilphillip
ms.author: cephilli
ms.date: 06/26/2018
ms.openlocfilehash: c3ee628b5c2239cd13395fda7714b38b06efa058
ms.sourcegitcommit: f99115e12a5eb75638abe45072e023a3ce3351ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2020
ms.locfileid: "94557149"
---
# <a name="durable-azure-functions"></a>Azure Functions durável

Ao criar aplicativos sem servidor com o Azure Functions, suas operações normalmente serão projetadas para serem executadas de maneira sem monitoração de estado. A razão para essa escolha de design é porque, à medida que a plataforma é dimensionada, fica difícil saber em quais servidores o código está sendo executado. Também se torna difícil saber quantas instâncias estão ativas em qualquer ponto determinado. No entanto, há classes de aplicativos que exigem que o estado atual de um processo seja conhecido. Considere o processo de envio de um pedido para uma loja online. A operação de check-out pode ser um fluxo de trabalho composto por várias operações que precisam saber o estado do processo. Essas informações podem incluir o inventário do produto, se o cliente tiver créditos de sua conta e também os resultados do processamento do cartão de crédito. Essas operações podem ser facilmente seus próprios fluxos de trabalho internos ou até mesmo serviços de sistemas de terceiros.

Existem vários padrões atualmente que ajudam na coordenação do estado do aplicativo entre sistemas internos e externos. É comum entrar em soluções que dependem de sistemas de enfileiramento centralizados, repositórios de chave-valor distribuído ou bancos de dados compartilhados para gerenciar esse estado. No entanto, esses são todos os recursos adicionais que agora precisam ser provisionados e gerenciados. Em um ambiente sem servidor, seu código pode se tornar complicado tentando coordenar esses recursos manualmente. Azure Functions oferece uma alternativa para a criação de funções com estado chamada Durable Functions.

Durable Functions é uma extensão para o tempo de execução Azure Functions que permite a definição de fluxos de trabalho com estado no código. Ao dividir os fluxos de trabalho em atividades, a extensão de Durable Functions pode gerenciar o estado, criar pontos de verificação de progresso e manipular a distribuição de chamadas de função entre servidores. Em segundo plano, ele faz uso de uma conta de armazenamento do Azure para manter o histórico de execução, agendar funções de atividade e recuperar respostas. O código sem servidor nunca deve interagir com informações persistentes nessa conta de armazenamento e normalmente não é algo com o qual os desenvolvedores precisam interagir.

## <a name="triggering-a-stateful-workflow"></a>Disparando um fluxo de trabalho com estado

Fluxos de trabalho com estado no Durable Functions podem ser divididos em dois componentes intrínsecos; gatilhos de orquestração e de atividade. Gatilhos e associações são componentes principais usados pelo Azure Functions para permitir que suas funções sem servidor sejam notificadas quando iniciar, receber entrada e retornar resultados.

### <a name="working-with-the-orchestration-client"></a>Trabalhando com o cliente de orquestração

As orquestrações são exclusivas em comparação com outros estilos de operações disparadas no Azure Functions. Durable Functions permite a execução de funções que podem levar horas ou até mesmo dias para serem concluídas. Esse tipo de comportamento vem com a necessidade de verificar o status de uma orquestração em execução, encerrar preempção ou enviar notificações de eventos externos.

Para esses casos, a extensão Durable Functions fornece a `DurableOrchestrationClient` classe que permite que você interaja com funções orquestradas. Você obtém acesso ao cliente de orquestração usando a `OrchestrationClientAttribute` associação. Em geral, você incluiria esse atributo com outro tipo de gatilho, como um `HttpTrigger` ou `ServiceBusTrigger` . Depois que a função de origem tiver sido disparada, o cliente de orquestração poderá ser usado para iniciar uma função de orquestrador.

```csharp
[FunctionName("KickOff")]
public static async Task<HttpResponseMessage> Run(
    [HttpTrigger(AuthorizationLevel.Function, "POST")]HttpRequestMessage req,
    [OrchestrationClient ] DurableOrchestrationClient<orchestrationClient>)
{
    OrderRequestData data = await req.Content.ReadAsAsync<OrderRequestData>();

    string instanceId = await orchestrationClient.StartNewAsync("PlaceOrder", data);

    return orchestrationClient.CreateCheckStatusResponse(req, instanceId);
}
```

### <a name="the-orchestrator-function"></a>A função de orquestrador

Anotar uma função com o OrchestrationTriggerAttribute em Azure Functions marca que funciona como uma função de orquestrador. É responsável por gerenciar as várias atividades que compõem seu fluxo de trabalho com estado.

As funções de orquestrador não podem fazer uso de associações diferentes de OrchestrationTriggerAttribute. Esse atributo só pode ser usado com um tipo de parâmetro de DurableOrchestrationContext. Nenhuma outra entrada pode ser usada, pois a desserialização de entradas na assinatura de função não tem suporte. Para obter as entradas fornecidas pelo cliente de orquestração, o método getinput \<T\> deve ser usado.

Além disso, os tipos de retorno das funções de orquestração devem ser void, Task ou um valor serializável JSON.

> *O código de tratamento de erros foi deixado para fins de brevidade*

```csharp
[FunctionName("PlaceOrder")]
public static async Task<string> PlaceOrder([OrchestrationTrigger] DurableOrchestrationContext context)
{
    OrderRequestData orderData = context.GetInput<OrderRequestData>();

    await context.CallActivityAsync<bool>("CheckAndReserveInventory", orderData);
    await context.CallActivityAsync<string>("ProcessPayment", orderData);

    string trackingNumber = await context.CallActivityAsync<string>("ScheduleShipping", orderData);
    await context.CallActivityAsync<string>("EmailCustomer", trackingNumber);

    return trackingNumber;
}
```

Várias instâncias de uma orquestração podem ser iniciadas e executadas ao mesmo tempo. Chamar o `StartNewAsync` método no `DurableOrchestrationClient` inicia uma nova instância da orquestração. O método retorna um `Task<string>` que é concluído quando a orquestração é iniciada. Uma exceção do tipo `TimeoutException` é gerada se a orquestração não tiver começado dentro de 30 segundos.

O `Task<string>` from concluído `StartNewAsync` deve conter a ID exclusiva da instância de orquestração. Essa ID de instância pode ser usada para invocar operações nessa orquestração específica. A orquestração pode ser consultada para o status ou notificações de eventos enviadas.

### <a name="the-activity-functions"></a>As funções de atividade

Funções de atividade são operações discretas que são compostas em uma função de orquestração para criar o fluxo de trabalho. Aqui está o local em que a maior parte do trabalho real ocorre. Eles representam a lógica de negócios, os processos de longa duração e as peças de quebra-cabeça para uma solução maior.

O `ActivityTriggerAttribute` é usado para anotar um parâmetro de função do tipo `DurableActivityContext` . O uso da anotação informa ao tempo de execução que a função destina-se a ser usada como uma função de atividade. Os valores de entrada para as funções de atividade são recuperados usando o `GetInput<T>` método do `DurableActivityContext` parâmetro.

Semelhante às funções de orquestração, os tipos de retorno das funções de atividade devem ser void, Task ou um valor serializável JSON.

Todas as exceções sem tratamento que são lançadas em funções de atividade serão enviadas para a função de orquestrador de chamada e apresentadas como um `TaskFailedException` . Neste ponto, o erro pode ser capturado e registrado no orquestrador, e a atividade pode ser repetida.

```csharp
[FunctionName("CheckAndReserveInventory")]
public static bool CheckAndReserveInventory([ActivityTrigger] DurableActivityContext context)
{
    OrderRequestData orderData = context.GetInput<OrderRequestData>();

    // Connect to inventory system and try to reserve items
    return true;
}
```

## <a name="recommended-resources"></a>Recursos recomendados

- [Durable Functions](/azure/azure-functions/durable-functions-overview)
- [Associações para Durable Functions](/azure/azure-functions/durable-functions-bindings)
- [Gerenciar instâncias no Durable Functions](/azure/azure-functions/durable-functions-instance-management)

>[!div class="step-by-step"]
>[Anterior](event-grid.md) 
> [Avançar](orchestration-patterns.md)
