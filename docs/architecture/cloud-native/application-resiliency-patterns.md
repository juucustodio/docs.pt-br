---
title: Padrões de resiliência de aplicativo
description: Arquitetando aplicativos .NET nativos da nuvem para o Azure | Padrões de resiliência do aplicativo
author: robvet
ms.date: 01/19/2021
ms.openlocfilehash: 655df16ef58f1deb2d2f4d0487c47658499f2108
ms.sourcegitcommit: 4df8e005c074ceb1f978f007b222fe253be2baf3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/04/2021
ms.locfileid: "99547714"
---
# <a name="application-resiliency-patterns"></a>Padrões de resiliência de aplicativo

A primeira linha de defesa é a resiliência do aplicativo.

Embora você possa investir um tempo considerável escrevendo sua própria estrutura de resiliência, esses produtos já existem. O [Polly](https://dotnetfoundation.org/projects/polly) é uma biblioteca abrangente de resiliência do .net e tratamento transitório de falhas que permite aos desenvolvedores expressar políticas de resiliência de uma maneira fluente e thread-safe. O Polly tem como alvo aplicativos criados com o .NET Framework ou o .NET 5. A tabela a seguir descreve os recursos de resiliência, chamados `policies` , disponíveis na biblioteca Polly. Eles podem ser aplicados individualmente ou agrupados juntos.

| Política | Experiência |
| :-------- | :-------- |
| Tentar novamente | Configura operações de repetição em operações designadas. |
| Disjuntor | Bloqueia as operações solicitadas por um período predefinido quando as falhas excedem um limite configurado |
| Tempo limite | Limita o limite da duração para a qual um chamador pode aguardar uma resposta. |
| Bulkhead | Restringe ações ao pool de recursos de tamanho fixo para evitar chamadas com falha de um recurso congestionamento. |
| Cache | Armazena respostas automaticamente. |
| Fallback | Define o comportamento estruturado após uma falha. |

Observe como, na figura anterior, as políticas de resiliência se aplicam a mensagens de solicitação, sejam provenientes de um cliente externo ou serviço de back-end. O objetivo é compensar a solicitação de um serviço que pode estar momentaneamente indisponível. Essas interrupções de curta duração normalmente se manifestam com os códigos de status HTTP mostrados na tabela a seguir.

| Código de status HTTP| Causa |
| :-------- | :-------- |
| 404 | Não encontrado |
| 408 | Tempo limite da solicitação |
| 429 | Muitas solicitações (você provavelmente foi limitado) |
| 502 | Gateway inválido |
| 503 | Serviço indisponível |
| 504 | Tempo limite do gateway |

Pergunta: você tentaria novamente um código de status HTTP de 403-Proibido? Não. Aqui, o sistema está funcionando corretamente, mas informando ao chamador que eles não estão autorizados a executar a operação solicitada. Deve-se ter cuidado para repetir apenas as operações causadas por falhas.

Como recomendado no capítulo 1, os desenvolvedores da Microsoft que constroem aplicativos nativos de nuvem devem visar a plataforma .NET. A versão 2,1 introduziu a biblioteca [HTTPClientFactory](https://www.stevejgordon.co.uk/introduction-to-httpclientfactory-aspnetcore) para criar instâncias de cliente http para interagir com recursos baseados em URL. Substituindo a classe HTTPClient original, a classe Factory dá suporte a muitos recursos avançados, um dos quais é uma [integração total](../microservices/implement-resilient-applications/implement-http-call-retries-exponential-backoff-polly.md) com a biblioteca de resiliência Polly. Com ele, você pode definir facilmente políticas de resiliência na classe de inicialização do aplicativo para lidar com falhas parciais e problemas de conectividade.

Em seguida, vamos expandir em padrões de repetição e de disjuntor.

### <a name="retry-pattern"></a>Padrão de repetição

Em um ambiente de nuvem nativa distribuída, as chamadas para serviços e recursos de nuvem podem falhar devido a falhas transitórias (de curta duração), que normalmente se corrigem após um breve período de tempo. A implementação de uma estratégia de repetição ajuda um serviço nativo de nuvem a mitigar esses cenários.

O [padrão de repetição](/azure/architecture/patterns/retry) permite que um serviço Repita uma operação de solicitação com falha a um número (configurável) de vezes com um tempo de espera crescente exponencialmente. A Figura 6-2 mostra uma nova tentativa em ação.

![Padrão de repetição em ação](./media/retry-pattern.png)

**Figura 6-2**. Padrão de repetição em ação

Na figura anterior, um padrão de repetição foi implementado para uma operação de solicitação. Ele está configurado para permitir até quatro repetições antes de falhar com um intervalo de retirada (tempo de espera) a partir de dois segundos, o que exponencialmente dobra para cada tentativa subsequente.

- A primeira invocação falha e retorna um código de status HTTP de 500. O aplicativo aguarda dois segundos e tenta novamente a chamada.
- A segunda invocação também falha e retorna um código de status HTTP de 500. O aplicativo agora dobra o intervalo de retirada para quatro segundos e tenta novamente a chamada.
- Por fim, a terceira chamada é realizada com sucesso.
- Nesse cenário, a operação de repetição teria tentado até quatro repetições enquanto dobra a duração da retirada antes de falhar a chamada.
- Houve falha na quarta tentativa de repetição, uma política de fallback seria invocada para lidar normalmente com o problema.

É importante aumentar o período de retirada antes de tentar novamente a chamada para permitir que o tempo do serviço seja autocorrigido. É uma prática recomendada implementar uma retirada exponencialmente crescente (duplicando o período em cada repetição) para permitir o tempo de correção adequado.

## <a name="circuit-breaker-pattern"></a>Padrão de disjuntor

Embora o padrão de repetição possa ajudar a recuperar uma solicitação confusas em uma falha parcial, há situações em que as falhas podem ser causadas por eventos inesperados que exigirão períodos de tempo mais longos para resolver. Essas falhas podem variar de gravidade de uma perda parcial de conectividade até a falha completa de um serviço. Nessas situações, é inútil que um aplicativo repita continuamente uma operação que provavelmente não terá sucesso.

Para piorar as coisas, a execução de operações contínuas de repetição em um serviço não responsivo pode movê-lo para um cenário de negação de serviço autoimposto, no qual você inunda o serviço com chamadas contínuas esgotando recursos como memória, threads e conexões de banco de dados, causando falhas em partes não relacionadas do sistema que usam os mesmos recursos.

Nessas situações, seria preferível para a operação falhar imediatamente e tentar invocar o serviço apenas se for provável que tenha êxito.

O [padrão de disjuntor](/azure/architecture/patterns/circuit-breaker) pode impedir que um aplicativo tente executar repetidamente uma operação que provavelmente falhará. Após um número predefinido de chamadas com falha, ele bloqueia todo o tráfego para o serviço. Periodicamente, ele permitirá uma chamada de avaliação para determinar se a falha foi resolvida. A Figura 6-3 mostra o padrão de disjuntor em ação.

![Padrão de disjuntor em ação](./media/circuit-breaker-pattern.png)

**Figura 6-3**. Padrão de disjuntor em ação

Na figura anterior, um padrão de disjuntor foi adicionado ao padrão de nova tentativa original. Observe como após 100 solicitações com falha, os separadores de circuito são abertos e não permite mais chamadas para o serviço. O valor CheckCircuit, definido como 30 segundos, especifica a frequência com que a biblioteca permite que uma solicitação prossiga para o serviço. Se essa chamada for realizada com sucesso, o circuito será fechado e o serviço estará novamente disponível para o tráfego.

Tenha em mente que a intenção do padrão de disjuntor é *diferente* daquela do padrão de repetição. O padrão de repetição permite que um aplicativo Repita uma operação na expectativa de que ele terá sucesso. O padrão de disjuntor impede que um aplicativo faça uma operação que provavelmente falhará. Normalmente, um aplicativo irá *combinar* esses dois padrões usando o padrão de repetição para invocar uma operação por meio de um disjuntor.

## <a name="testing-for-resiliency"></a>Teste de resiliência

O teste de resiliência nem sempre pode ser feito da mesma maneira que você testa a funcionalidade do aplicativo (executando testes de unidade, testes de integração e assim por diante). Em vez disso, você deve testar como a carga de trabalho de ponta a ponta é executada sob condições de falha, o que ocorre apenas intermitentemente. Por exemplo: injetar falhas ao travar processos, certificados expirados, tornar os serviços dependentes indisponíveis etc. Estruturas como o [caos – o macaco](https://github.com/Netflix/chaosmonkey) pode ser usado para esses testes de caos.

A resiliência do aplicativo é necessária para lidar com operações solicitadas problemáticas. Mas, é apenas metade da história. Em seguida, abordamos os recursos de resiliência disponíveis na nuvem do Azure.

>[!div class="step-by-step"]
>[Anterior](resiliency.md) 
> [Avançar](infrastructure-resiliency-azure.md)
