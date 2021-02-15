---
title: Considerações de arquitetura sem servidor-aplicativos sem servidor
description: Entenda os desafios da arquitetura de aplicativos sem servidor, desde o gerenciamento de estado e o armazenamento persistente até o dimensionamento, o registro em log, o rastreamento e o diagnóstico.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 04/06/2020
ms.openlocfilehash: fbbb0c38cea58902124743fb99f9ab31b3d09be9
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91171644"
---
# <a name="serverless-architecture-considerations"></a>Considerações sobre a arquitetura sem servidor

A adoção de uma arquitetura sem servidor vem com determinados desafios. Esta seção explora algumas das considerações mais comuns a serem consideradas. Todos esses desafios têm soluções. Assim como acontece com todas as opções de arquitetura, a decisão de ir sem servidor deve ser feita somente após considerar atentamente os prós e contras. Dependendo das necessidades do seu aplicativo, você pode decidir que uma implementação sem servidor não é a solução certa para determinados componentes.

## <a name="managing-state"></a>Gerenciar estado

As funções sem servidor, assim como com os microservices em geral, não têm estado por padrão. Evitar o estado permite que sem servidor seja efêmero, para escalar horizontalmente e para fornecer resiliência sem um ponto central de falha. Em algumas circunstâncias, os processos de negócios exigem o estado. Se o processo exigir um estado, você terá duas opções. Você pode adotar um modelo que não seja sem servidor ou interagir com um serviço separado que forneça o estado. Adicionar o estado pode complicar a solução e torná-la mais difícil de dimensionar e, potencialmente, criar um ponto único de falha. Considere cuidadosamente se a função absolutamente exige estado. Se a resposta for "Sim", determine se ainda faz sentido implementá-la com servidor.

Há várias soluções para adotar o estado sem comprometer os benefícios do servidor. Algumas das soluções mais populares incluem:

- Use um armazenamento de dados temporário ou um cache distribuído, como Redis
- Armazene o estado em um banco de dados, como SQL ou CosmosDB
- Tratar o estado por meio de um mecanismo de fluxo de trabalho como [funções duráveis](/azure/azure-functions/durable/durable-functions-overview)

O resultado final é que você deve estar ciente da necessidade de qualquer gerenciamento de estado dentro dos processos que está pensando em implementar sem servidor.

## <a name="long-running-processes"></a>Processos de execução longa

Muitos benefícios do inserver sem servidor dependem dos processos que estão sendo efêmeros. Tempos de execução curtos facilitam para o provedor sem servidor liberar recursos à medida que as funções terminam e compartilham funções entre os hosts. A maioria dos provedores de nuvem limita o tempo total que sua função pode executar em cerca de 10 minutos. Se o processo puder levar mais tempo, você poderá considerar uma implementação alternativa.

Há algumas exceções e soluções. Uma solução pode ser dividir o processo em componentes menores que, individualmente, levam menos tempo para serem executados. Se o processo for executado por tempo devido a dependências, você também poderá considerar um fluxo de trabalho assíncrono usando uma solução como funções duráveis. As funções duráveis pausam e mantêm o estado do processo enquanto ele está aguardando a conclusão de um processo externo. A manipulação assíncrona reduz o tempo de execução do processo real.

## <a name="startup-time"></a>Tempo de inicialização

Uma preocupação potencial com implementações sem servidor é o tempo de inicialização. Para conservar recursos, muitos provedores sem servidor criam infraestrutura "sob demanda". Quando uma função sem servidor é disparada após um período de tempo, os recursos para hospedar a função podem precisar ser criados ou reiniciados. Em algumas situações, inícios frios podem resultar em atrasos de vários segundos. O tempo de inicialização varia entre provedores e níveis de serviço. Há algumas abordagens para abordar o tempo de inicialização se for importante minimizar para o sucesso do aplicativo.

- Alguns provedores permitem que os usuários paguem por níveis de serviço que garantem que a infraestrutura está "sempre ativa".
- Implemente um mecanismo Keep-Alive (execute ping no ponto de extremidade para mantê-lo "ativo").
- Use orquestração como kubernetes com uma abordagem de função em contêiner (o host já está em execução, portanto, a rotação de novas instâncias é extremamente rápida).

## <a name="database-updates-and-migrations"></a>Atualizações e migrações de banco de dados

Uma vantagem de um código sem servidor é que você pode liberar novas funções não precisar reimplantar todo o aplicativo. Essa vantagem pode se tornar uma desvantagem quando há um banco de dados relacional envolvido. As alterações nos esquemas de banco de dados são difíceis de sincronizar com atualizações sem servidor. Desafios adicionais são apresentados quando as coisas dão errado e as alterações devem ser revertidas. A integridade dos dados é um motivo pelo qual uma prática recomendada para microserviços e funções sem servidor é que eles possuem seus próprios dados. É possível implantar alterações como uma única unidade de computação e dados. A realidade é que muitos sistemas herdados apresentam um grande banco de dados de back-end que deve ser reconciliado com a arquitetura sem servidor.

Uma abordagem popular para resolver o controle de versão de esquema é nunca modificar as propriedades e colunas existentes, mas, em vez disso, adicionar novas informações. Por exemplo, considere uma alteração para mover de um sinalizador booliano "concluído" para uma lista de tarefas pendentes para uma "data de conclusão". Em vez de remover o campo antigo, a alteração do banco de dados irá:

1. Adicione um novo campo "data de conclusão".
1. Transforme o campo booliano "concluído" em uma função computada que avalia se a data de conclusão é posterior à data atual.
1. Adicione um gatilho para definir a data de conclusão como a data atual quando o booliano concluído for definido como true.

A sequência de alterações garante que o código herdado continue a ser executado "como está", enquanto as funções sem servidor mais recentes podem aproveitar o novo campo.

Para obter mais informações sobre os dados em arquiteturas sem servidor, consulte [desafios e soluções para o gerenciamento de dados distribuídos](../microservices/architect-microservice-container-applications/distributed-data-management.md).

## <a name="scaling"></a>Dimensionamento

É um equívoco comum que significa sem servidor "nenhum servidor". É, na verdade, "menos servidor". O fato de que há uma infraestrutura de backup é importante entender quando se trata do dimensionamento. A maioria das plataformas sem servidor fornece um conjunto de controles para manipular como a infraestrutura deve ser dimensionada quando a densidade do evento aumenta. Você pode escolher entre uma variedade de opções, mas sua estratégia pode variar dependendo da função. Além disso, as funções normalmente são executadas em um host relacionado, para que as funções no mesmo host tenham as mesmas opções de escala. Portanto, é necessário organizar e planejar quais funções são hospedadas juntas com base nos requisitos de escala.

As regras geralmente especificam como escalar verticalmente (aumentar os recursos do host) e escalar horizontalmente (aumentar o número de instâncias de host) com base em parâmetros variáveis. Os gatilhos para escalas podem incluir agendamento, taxas de solicitação, utilização da CPU e uso de memória. O melhor desempenho geralmente traz um custo maior. As abordagens menos dispendiosas baseadas em consumo podem não ser dimensionadas rapidamente quando a taxa de solicitação aumenta repentinamente. Há uma compensação entre o pagamento antecipado do "custo de seguros" versus o pagamento estritamente "à medida que você vai" e o risco de respostas mais lentas devido a aumentos repentinos na demanda.

## <a name="monitoring-tracing-and-logging"></a>Monitoramento, rastreamento e registro em log

Um aspecto freqüentemente ignorado do DevOps é o monitoramento de aplicativos depois de implantado. É importante ter uma estratégia para monitorar funções sem servidor. O maior desafio é geralmente correlação ou reconhecimento quando um usuário chama várias funções como parte da mesma interação. A maioria das plataformas sem servidor permite o log de console que pode ser importado para ferramentas de terceiros. Também há opções para automatizar a coleta de telemetria, gerar e acompanhar IDs de correlação e monitorar ações específicas para fornecer informações detalhadas. O Azure fornece a [plataforma de Application insights](/azure/azure-functions/functions-monitoring) avançada para monitoramento e análise.

## <a name="inter-service-dependencies"></a>Dependências entre serviços

Uma arquitetura sem servidor pode incluir funções que dependem de outras funções. Na verdade, não é incomum que uma arquitetura sem servidor tenha vários serviços chamados entre si como parte de uma transação distribuída ou de interação. Para evitar um forte acoplamento, é recomendável que os serviços não referenciem uns aos outros diretamente. Quando o ponto de extremidade de um serviço precisa ser alterado, as referências diretas podem resultar em refatoração principal. Uma solução sugerida é fornecer um mecanismo de descoberta de serviço, como um registro, que fornece o ponto de extremidade apropriado para um tipo de solicitação. Outra solução é aproveitar os serviços de mensagens, como filas ou tópicos para comunicação entre serviços.

## <a name="managing-failure-and-providing-resiliency"></a>Gerenciamento de falhas e fornecimento de resiliência

Também é importante considerar o padrão de *separação de circuito*: se, por algum motivo, um serviço continuar a falhar, não é aconselhável chamar esse serviço repetidamente. Em vez disso, um serviço alternativo é chamado ou uma mensagem retornada até que a integridade do serviço dependente seja restabelecida. A arquitetura sem servidor precisa levar em conta a estratégia para resolver e gerenciar dependências entre serviços.

Para continuar o padrão de separação de circuito, os serviços precisam ser tolerantes a falhas e resilientes. Tolerância a falhas refere-se à capacidade do seu aplicativo de continuar em execução mesmo após exceções inesperadas ou Estados inválidos serem encontrados. A tolerância a falhas normalmente é uma função do próprio código e como ela é escrita para lidar com exceções. Resiliência refere-se à capacidade com que o aplicativo está em recuperação de falhas. A resiliência é geralmente gerenciada pela plataforma sem servidor. A plataforma deve ser capaz de criar uma nova instância de função sem servidor quando a existente falhar. A plataforma também deve ser inteligente o suficiente para interromper a rotação de novas instâncias quando cada nova instância falhar.

Para obter mais informações, consulte [Implementing the Circuit disjuntor Pattern](../microservices/implement-resilient-applications/implement-circuit-breaker-pattern.md).

## <a name="versioning-and-greenblue-deployments"></a>Implantações de controle de versão e verdes/azuis

Um dos principais benefícios do servidor é a capacidade de atualizar uma função específica sem precisar reimplantar o aplicativo inteiro. Para que as atualizações sejam bem-sucedidas, as funções devem ter controle de versão para que os serviços que as chamam sejam roteados para a versão correta do código. Uma estratégia para implantar novas versões também é importante. Uma abordagem comum é usar "implantações verdes/azuis". A implantação verde é a função atual. Uma nova versão "azul" é implantada para produção e testada. Quando o teste passa, as versões verde e azul são trocadas para que a nova versão venha ao vivo. Se forem encontrados problemas, eles poderão ser trocados novamente. O suporte à versão e às implantações verdes/azuis requer uma combinação de criação de funções para acomodar alterações de versão e trabalhar com a plataforma sem servidor para lidar com as implantações.

>[!div class="step-by-step"]
>[Anterior](serverless-architecture.md) 
> [Avançar](serverless-design-examples.md)
