---
title: Introdução aos aplicativos nativos de nuvem
description: Saiba mais sobre a computação nativa na nuvem
author: robvet
ms.date: 01/19/2021
ms.openlocfilehash: 852eed27d4cfcaefdfa89a73c54414a6306ed28d
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506091"
---
# <a name="introduction-to-cloud-native-applications"></a>Introdução aos aplicativos nativos de nuvem

Outro dia, no escritório, trabalhando em "a próxima grande coisa".

Seus anéis de celular. É seu recrutador amigável-aquele que chama você duas vezes por dia sobre novos trabalhos.

Mas, desta vez, ele é diferente: inicialização, patrimônio e muita contribuição.

A menção da tecnologia de nuvem e de ponta leva você pela borda.

Avance algumas semanas e agora você é um novo funcionário em uma sessão de design que arquiteta um aplicativo de comércio eletrônico principal. Você vai competir com os principais sites de comércio eletrônico.

Como você vai compilá-lo?

Se você seguir as diretrizes dos últimos 15 anos, provavelmente criará o sistema mostrado na Figura 1,1.

![Design monolítico tradicional](./media/monolithic-design.png)

**Figura 1-1**. Design monolítico tradicional

Você constrói um aplicativo de núcleo grande que contém toda a lógica do seu domínio. Ele inclui módulos como identidade, catálogo, ordenação e muito mais. O aplicativo principal se comunica com um grande banco de dados relacional. O núcleo expõe a funcionalidade por meio de uma interface HTML.

Parabéns!  Você acabou de criar um aplicativo monolítico.

Nem todos são ruins. Os monolíticos oferecem algumas vantagens distintas. Por exemplo, eles são diretos para...

- compilar
- test
- deploy
- solucionar problemas
- scale

Muitos aplicativos bem-sucedidos que existem hoje foram criados como monolíticos. O aplicativo é um problema e continua a evoluir, iteração após a iteração, adicionando mais funcionalidade.

Em algum momento, no entanto, você começa a se sentir desconfortável. Você se encontra perdendo o controle do aplicativo. Com o passar do tempo, a sensação se torna mais intensa e, eventualmente, você insere um estado conhecido como `Fear Cycle` .

- O aplicativo tornou-se tão complicado que nenhuma pessoa a entende.
- Você teme fazer alterações – cada alteração tem efeitos colaterais indesejados e dispendiosos.
- Novos recursos/correções se tornam complicados, demorados e caros de implementar.
- Cada versão é a menor possível e requer uma implantação completa de todo o aplicativo.
- Um componente instável pode travar todo o sistema.
- Novas tecnologias e estruturas não são uma opção.
- É difícil implementar metodologias de entrega ágil.
- A arquitetura erosion define como a base de código deteriora-se com "casos especiais" que não terminam.
- Os consultores informam que você deve reescrevê-lo.

Muitas organizações solucionaram o ciclo de medo monolítico adotando uma abordagem nativa de nuvem para a criação de sistemas. A Figura 1-2 mostra o mesmo sistema criado para aplicar técnicas e práticas nativas de nuvem.

![Design de Cloud-Native](./media/cloud-native-design.png)

**Figura 1-2**. Design nativo de nuvem

Observe como o aplicativo é decomposto em um conjunto de microserviços isolados pequenos. Cada serviço é independente e encapsula seu próprio código, dados e dependências. Cada um é implantado em um contêiner de software e gerenciado por um orquestrador de contêiner. Em vez de um banco de dados relacional grande, cada serviço possui o próprio armazenamento de dados, o tipo que varia de acordo com as necessidades de data. Observe como alguns serviços dependem de um banco de dados relacional, mas outros em bancos de dados NoSQL. Um serviço armazena seu estado em um cache distribuído. Observe como todo o tráfego é encaminhado por meio de um serviço de gateway de API que é responsável por direcionar o tráfego para os serviços de back-end principais e impor muitas preocupações abrangentes. O mais importante é que o aplicativo aproveita totalmente os recursos de escalabilidade, disponibilidade e resiliência encontrados nas plataformas de nuvem modernas.

### <a name="cloud-native-computing"></a>Computação nativa de nuvem

Hmm... Acabamos de usar o termo _nativo da nuvem_. Seu primeiro pensamento pode ser "o que significa exatamente isso?" Outro setor efeito criado por fornecedores de software para comercializar mais coisas? "

Felizmente, é muito diferente e, felizmente, esse livro ajudará a convencê-lo.

Dentro de pouco tempo, a nuvem nativa tornou-se uma tendência de condução no setor de software. É uma nova maneira de pensar na criação de sistemas grandes e complexos, uma abordagem que aproveita ao máximo as práticas modernas de desenvolvimento de software, tecnologias e infraestrutura de nuvem. A abordagem altera a maneira como você projeta, implementa, implanta e operacionalize os sistemas.

Ao contrário da atenção contínua que impulsiona nosso setor, a nuvem nativa é _para o-real_. Considere a CNCF ( [nuvem Native Computing Foundation](https://www.cncf.io/) ), um consórcio de mais de 300 grandes corporações com um compromisso de tornar a computação nativa em nuvem onipresente em várias pilhas de nuvem e tecnologia. Como um dos grupos de código-fonte aberto mais influentes, ele hospeda muitos dos projetos de software livre que mais crescem no GitHub. Eles incluem projetos como [kubernetes](https://kubernetes.io/), [Prometheus](https://prometheus.io/), [Helm](https://helm.sh/), [Envoy](https://www.envoyproxy.io/)e [gRPC](https://grpc.io/).

O CNCF promove um ecossistema de software livre e neutralidade de fornecedor. Após esse cliente potencial, este livro apresenta princípios nativos de nuvem, padrões e práticas recomendadas que são independentes de tecnologia. Ao mesmo tempo, discutiremos os serviços e a infraestrutura disponíveis no Microsoft Azure Cloud para construir sistemas nativos de nuvem.

Então, o que é exatamente a nuvem nativa? Volte, relaxe e deixe-nos ajudá-lo a explorar esse novo mundo.

>[!div class="step-by-step"]
>[Anterior](index.md) 
> [Avançar](definition.md)
