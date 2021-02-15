---
title: Como aproveitar funções sem servidor
description: Aproveitamento e Azure Functions sem servidor em aplicativos nativos de nuvem
ms.date: 05/13/2020
ms.openlocfilehash: 8e5c60d29cd8d635f79f42c232b33f060949e2b5
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91155361"
---
# <a name="leveraging-serverless-functions"></a>Como aproveitar funções sem servidor

No espectro do gerenciamento de máquinas físicas para aproveitar os recursos de nuvem, as vidas sem servidor no final extremo. Sua única responsabilidade é seu código, e você só paga quando seu código é executado. Azure Functions fornece uma maneira de criar recursos sem servidor em seus aplicativos nativos de nuvem.

## <a name="what-is-serverless"></a>O que é sem servidor?

Sem servidor é um modelo de serviço relativamente novo de computação em nuvem. Isso não significa que os servidores são opcionais-seu código ainda é executado em um servidor em algum lugar. A diferença é que a equipe de aplicativos não se preocupa mais com o gerenciamento da infraestrutura de servidor. Em vez disso, o fornecedor de nuvem possui essa responsabilidade. A equipe de desenvolvimento aumenta sua produtividade fornecendo soluções de negócios para os clientes, não para o trabalho.

A computação sem servidor usa contêineres com estado disparados por eventos para hospedar seus serviços. Eles podem escalar horizontalmente e em para atender à demanda conforme necessário. Plataformas sem servidor como Azure Functions têm integração total com outros serviços do Azure, como filas, eventos e armazenamento.

## <a name="what-challenges-are-solved-by-serverless"></a>Quais desafios são resolvidos sem servidor?

As plataformas sem servidor abordam muitas preocupações demoradas e caras:

- Compra de computadores e licenças de software
- Hospedagem, proteção, configuração e manutenção de computadores e seus requisitos de rede, energia e/C
- Aplicação de patch e atualização de software e sistemas operacionais
- Configurando servidores Web ou serviços de máquina para hospedar software de aplicativo
- Configurando o software de aplicativo em sua plataforma

Muitas empresas alocam grandes orçamentos para dar suporte a questões de infraestrutura de hardware. A mudança para a nuvem pode ajudar a reduzir esses custos; a mudança de aplicativos para o sem servidor pode ajudar a eliminá-los.

## <a name="what-is-the-difference-between-a-microservice-and-a-serverless-function"></a>Qual é a diferença entre um microserviço e uma função sem servidor?

Normalmente, um microserviço encapsula um recurso de negócios, como um carrinho de compras para um site de comércio online. Ele expõe várias operações que permitem que um usuário gerencie sua experiência de compra. Uma função, no entanto, é um pequeno bloco leve de código que executa uma operação de finalidade única em resposta a um evento.
Os microserviços normalmente são construídos para responder a solicitações, geralmente de uma interface. As solicitações podem ser baseadas em HTTP REST ou gRPC. Serviços sem servidor respondem a eventos. Sua arquitetura orientada por eventos é ideal para o processamento de tarefas em segundo plano e de execução curta.

## <a name="what-scenarios-are-appropriate-for-serverless"></a>Quais cenários são apropriados para servidores sem servidor?

Serverless expõe funções de curta execução individuais que são invocadas em resposta a um gatilho. Isso os torna ideais para o processamento de tarefas em segundo plano.

Um aplicativo pode precisar enviar um email como uma etapa em um fluxo de trabalho. Em vez de enviar a notificação como parte de uma solicitação de microatendimento, coloque os detalhes da mensagem em uma fila. Uma função do Azure pode remover a mensagem da fila e enviar o email de forma assíncrona. Isso pode melhorar o desempenho e a escalabilidade do microserviço. O [nivelamento de carga baseado em fila](/azure/architecture/patterns/queue-based-load-leveling) pode ser implementado para evitar gargalos relacionados ao envio dos emails. Além disso, esse serviço autônomo pode ser reutilizado como um utilitário em vários aplicativos diferentes.

Mensagens assíncronas de filas e tópicos é um padrão comum para disparar funções sem servidor. No entanto, Azure Functions pode ser disparado por outros eventos, como alterações no armazenamento de BLOBs do Azure. Um serviço que dá suporte a carregamentos de imagem pode ter uma função do Azure responsável por otimizar o tamanho da imagem. A função pode ser disparada diretamente por inserções no armazenamento de BLOBs do Azure, mantendo a complexidade das operações de microserviço.

Muitos serviços têm processos de execução longa como parte de seus fluxos de trabalho. Muitas vezes, essas tarefas são feitas como parte da interação do usuário com o aplicativo. Essas tarefas podem forçar o usuário a esperar, afetando negativamente sua experiência. A computação sem servidor fornece uma ótima maneira de mover tarefas mais lentas para fora do loop de interação do usuário. Essas tarefas podem ser dimensionadas com demanda sem a necessidade de dimensionar todo o aplicativo.

## <a name="when-should-you-avoid-serverless"></a>Quando você não deve evitar servidor?

Provisionamento e dimensionamento de soluções sem servidor sob demanda. Quando uma nova instância é chamada, o Cold Starts é um problema comum. Um início frio é o período de tempo necessário para provisionar essa instância. Normalmente, esse atraso pode ser de alguns segundos, mas pode ser mais demorado dependendo de vários fatores. Depois de provisionado, uma única instância é mantida ativa, desde que receba solicitações periódicas. Mas, se um serviço for chamado com menos frequência, o Azure poderá removê-lo da memória e exigir uma inicialização a frio quando for reinvocado. Inícios frios também são necessários quando uma função é dimensionada para uma nova instância.

A Figura 3-10 mostra um padrão de inicialização a frio. Observe as etapas adicionais necessárias quando o aplicativo está frio.

![Inativo versus a figura de início quente ](./media/cold-start-warm-start.png)
 **3-10**. Início frio versus início quente.

Para evitar que o frio seja totalmente iniciado, você pode mudar de um [plano de consumo para um plano dedicado](https://azure.microsoft.com/blog/understanding-serverless-cold-start/). Você também pode configurar uma ou mais [instâncias pré-configuradas](/azure/azure-functions/functions-premium-plan#pre-warmed-instances) com a atualização do plano Premium. Nesses casos, quando você precisa adicionar outra instância, ela já está ativa e pronta para uso. Essas opções podem ajudar a mitigar o problema de inicialização a frio associado à computação sem servidor.

Os provedores de nuvem cobram por servidor com base no tempo de execução de computação e na memória consumida. Operações de longa execução ou cargas de trabalho de alto consumo de memória nem sempre são os melhores candidatos para servidor. As funções sem servidor favorecem pequenas partes de trabalho que podem ser concluídas rapidamente. A maioria das plataformas sem servidor exige que as funções individuais sejam concluídas em alguns minutos. Azure Functions usa como padrão uma duração de tempo limite de 5 minutos, que pode ser configurada até 10 minutos. O plano do Azure Functions Premium também pode mitigar esse problema, padronizando os tempos limite para 30 minutos com um limite superior não associado que pode ser configurado. O tempo de computação não é o horário do calendário. Funções mais avançadas usando a [estrutura de durable Functions do Azure](/azure/azure-functions/durable/durable-functions-overview?tabs=csharp) podem pausar a execução por um curso de vários dias. A cobrança é baseada no tempo de execução real – quando a função é ativada e retoma o processamento.

Por fim, aproveitar Azure Functions para tarefas de aplicativo adiciona complexidade. É prudente primeiro arquitetar seu aplicativo com um design modular e menos rígido. Em seguida, identifique se há benefícios sem servidor que justifiquem a complexidade adicional.

>[!div class="step-by-step"]
>[Anterior](leverage-containers-orchestrators.md) 
> [Avançar](combine-containers-serverless-approaches.md)
