---
title: Comunicação front-end de cliente
description: Saiba como os clientes front-end se comunicam com sistemas nativos de nuvem
author: robvet
ms.date: 01/19/2021
ms.openlocfilehash: 089f55f8f6b9320fe552602eb40bb83be28f119b
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506234"
---
# <a name="front-end-client-communication"></a>Comunicação front-end de cliente

Em um sistema nativo de nuvem, os clientes front-end (aplicativos móveis, Web e de área de trabalho) exigem um canal de comunicação para interagir com microserviços de back-end independentes.  

Quais são as opções?

Para simplificar as coisas, um cliente front-end poderia *se comunicar diretamente* com os microserviços de back-end, mostrados na Figura 4-2.

![Comunicação direta entre cliente e serviço](./media/direct-client-to-service-communication.png)

**Figura 4-2.** Comunicação direta entre cliente e serviço

Com essa abordagem, cada microserviço tem um ponto de extremidade público acessível por clientes front-end. Em um ambiente de produção, você colocaria um balanceador de carga na frente dos microserviços, roteando o tráfego proporcionalmente.

Embora seja simples de implementar, a comunicação direta do cliente seria aceitável apenas para aplicativos de microatendimento simples. Esse padrão acopla rigidamente clientes front-end a serviços de back-end principais, abrindo a porta para vários problemas, incluindo:

- Cliente susceptibilidade para refatoração de serviço de back-end.
- Uma superfície de ataque mais ampla como serviços de back-end principais são expostos diretamente.
- Duplicação de preocupações abrangentes em cada microserviço.
- Código de cliente excessivamente complexo – os clientes devem controlar vários pontos de extremidade e lidar com falhas de maneira resiliente.

Em vez disso, um padrão de design de nuvem amplamente aceito é implementar um [serviço de gateway de API](../microservices/architect-microservice-container-applications/direct-client-to-microservice-communication-versus-the-api-gateway-pattern.md) entre os aplicativos de front-end e serviços de back-end. O padrão é mostrado na Figura 4-3.

![Padrão de gateway de API](./media/api-gateway-pattern.png)

**Figura 4-3.** Padrão de gateway de API

Na figura anterior, observe como o serviço de gateway de API abstrai os microserviços de núcleo de back-end. Implementada como uma API da Web, ela atua como um *proxy reverso*, roteando o tráfego de entrada para os microserviços internos.

O gateway isola o cliente do particionamento e refatoração de serviço interno. Se você alterar um serviço de back-end, você poderá acomodá-lo no gateway sem interromper o cliente. Também é sua primeira linha de defesa para preocupações abrangentes, como identidade, Caching, resiliência, medição e limitação. Muitas dessas preocupações abrangentes podem ser descarregadas dos serviços principais de back-end para o gateway, simplificando os serviços de back-end.

É necessário tomar cuidado para manter o gateway de API simples e rápido. Normalmente, a lógica de negócios é mantida fora do gateway. Os riscos complexos de gateway se tornam um afunilamento e, eventualmente, um próprio monolítico. Os sistemas maiores geralmente expõem vários gateways de API segmentados por tipo de cliente (móvel, Web, área de trabalho) ou funcionalidade de back-end. O padrão [back-end para front-ends](/azure/architecture/patterns/backends-for-frontends) fornece a direção para implementar vários gateways. O padrão é mostrado na Figura 4-4.

![Padrão de gateway de API](./media/backend-for-frontend-pattern.png)

**Figura 4-4.** Back-end para padrão de front-end

Observação na figura anterior como o tráfego de entrada é enviado para um gateway de API específico com base no tipo de cliente: aplicativo Web, móvel ou de área de trabalho. Essa abordagem faz sentido, pois os recursos de cada dispositivo diferem significativamente em limitações de fator forma, desempenho e exibição. Normalmente, os aplicativos móveis expõem menos funcionalidade do que um navegador ou aplicativos de área de trabalho. Cada gateway pode ser otimizado para corresponder aos recursos e à funcionalidade do dispositivo correspondente.

Para começar, você pode criar seu próprio serviço de gateway de API. Uma pesquisa rápida do GitHub fornecerá muitos exemplos. No entanto, há várias estruturas e produtos de gateway comercial disponíveis.

## <a name="ocelot-gateway"></a>Gateway Ocelot

Para aplicativos nativos .NET de nuvem simples, você pode considerar o [Gateway Ocelot](https://github.com/ThreeMammals/Ocelot). Ocelot é um gateway de API de software livre criado para os microserviços .NET que exigem um ponto de entrada unificado em seu sistema. É leve, rápido e escalonável.

Como qualquer gateway de API, sua principal funcionalidade é encaminhar solicitações HTTP de entrada para serviços downstream. Além disso, ele dá suporte a uma ampla variedade de recursos que podem ser configurados em um pipeline de middleware do .NET. Seu conjunto de recursos é apresentado na tabela a seguir.

|Recursos do Ocelot  | |
| :-------- | :-------- |
| Roteamento | Autenticação |
| Agregação de solicitação | Autorização |
| Descoberta de serviço (com Consul e Eureka) | Limitação |
| Balanceamento de carga | Registro em log, rastreamento |
| Cache | Cabeçalhos/transformação de cadeia de consulta |
| Pass-Through de correlação | Middleware personalizado |
| Qualidade de Serviço | Políticas de repetição |

Cada gateway Ocelot especifica os endereços upstream e downstream e os recursos configuráveis em um arquivo de configuração JSON. O cliente envia uma solicitação HTTP para o gateway Ocelot. Depois de recebido, Ocelot passa o objeto HttpRequest por meio de seu pipeline manipulando-o para o estado especificado por sua configuração. No final do pipeline, o Ocelot cria um novo HTTPResponseobject e o passa para o serviço downstream. Para a resposta, o Ocelot reverte o pipeline, enviando a resposta de volta para o cliente.

Ocelot está disponível como um pacote NuGet. Ele se destina ao NET Standard 2,0, tornando-o compatível com o .NET Core 2.0 + e .NET Framework 4.6.1 + Runtimes. O Ocelot integra-se com qualquer coisa que fala HTTP e é executado nas plataformas às quais o .NET Core dá suporte: Linux, macOS e Windows. O Ocelot é extensível e dá suporte a muitas plataformas modernas, incluindo contêineres do Docker, serviços Kubernetess do Azure ou outras nuvens públicas.  O Ocelot integra-se com pacotes de software livre como [Consul](https://www.consul.io), [GraphQL](https://graphql.org)e [Eureka](https://github.com/Netflix/eureka)da Netflix.

Considere o Ocelot para aplicativos nativos de nuvem simples que não exigem o rico conjunto de recursos de um gateway de API comercial.

## <a name="azure-application-gateway"></a>Gateway de Aplicativo do Azure

Para obter os requisitos de gateway simples, você pode considerar [aplicativo Azure gateway](/azure/application-gateway/overview). Disponível como um [serviço de PaaS](https://azure.microsoft.com/overview/what-is-paas/)do Azure, ele inclui recursos básicos de gateway, como roteamento de URL, terminação de SSL e um firewall do aplicativo Web. O serviço oferece suporte a recursos [de balanceamento de carga de camada 7](https://www.nginx.com/resources/glossary/layer-7-load-balancing/) . Com a camada 7, você pode rotear solicitações com base no conteúdo real de uma mensagem HTTP, não apenas em pacotes de rede TCP de nível baixo.

Ao longo deste livro, evangelizarmos a hospedagem de sistemas nativos de nuvem no [kubernetes](https://www.infoworld.com/article/3268073/what-is-kubernetes-your-next-application-platform.html). Um orquestrador de contêineres, o kubernetes automatiza a implantação, o dimensionamento e as preocupações operacionais de cargas de trabalho em contêineres. Aplicativo Azure gateway pode ser configurado como um gateway de API para o cluster do [serviço kubernetes do Azure](https://azure.microsoft.com/services/kubernetes-service/) .

O [controlador de entrada do gateway de aplicativo](https://azure.github.io/application-gateway-kubernetes-ingress/) permite que aplicativo Azure gateway funcione diretamente com o [serviço kubernetes do Azure](https://azure.microsoft.com/services/kubernetes-service/). A Figura 4,5 mostra a arquitetura.

![Controlador de Entrada do Gateway de Aplicativo](./media/application-gateway-ingress-controller.png)

**Figura 4-5.** Controlador de Entrada do Gateway de Aplicativo

O kubernetes inclui um recurso interno que dá suporte ao balanceamento de carga HTTP (nível 7), chamado [entrada](https://kubernetes.io/docs/concepts/services-networking/ingress/). A entrada define um conjunto de regras para o modo como as instâncias de microserviço dentro de AKS podem ser expostas para o mundo exterior. Na imagem anterior, o controlador de entrada interpreta as regras de entrada configuradas para o cluster e configura automaticamente o gateway de Aplicativo Azure. Com base nessas regras, o gateway de aplicativo roteia o tráfego para os microserviços em execução no AKS. O controlador de entrada escuta as alterações nas regras de entrada e faz as alterações apropriadas no gateway de Aplicativo Azure.

## <a name="azure-api-management"></a>Gerenciamento de API do Azure

Para sistemas nativos de nuvem de médio a grande escala, você pode considerar o [Gerenciamento de API do Azure](https://azure.microsoft.com/services/api-management/). É um serviço baseado em nuvem que não só resolve suas necessidades de gateway de API, mas fornece uma experiência de desenvolvedor e administrativa completa. O gerenciamento de API é mostrado na Figura 4-6.

![Gerenciamento de API do Azure](./media/azure-api-management.png)

**Figura 4-6.** Gerenciamento de API do Azure

Para começar, o gerenciamento de API expõe um servidor gateway que permite o acesso controlado a serviços de back-end com base nas regras e políticas configuráveis. Esses serviços podem estar na nuvem do Azure, no local data center ou em outras nuvens públicas. As chaves de API e os tokens JWT determinam quem pode fazer o quê. Todo o tráfego é registrado para fins analíticos.

Para desenvolvedores, o gerenciamento de API oferece um portal do desenvolvedor que fornece acesso a serviços, documentação e código de exemplo para chamá-los. Os desenvolvedores podem usar o Swagger/Open API para inspecionar pontos de extremidade de serviço e analisar seu uso. O serviço funciona nas principais plataformas de desenvolvimento: .NET, Java, Golang e muito mais.

O portal do editor expõe um painel de gerenciamento em que os administradores expõem APIs e gerenciam seu comportamento. O acesso ao serviço pode ser concedido, integridade do serviço monitorado e telemetria de serviço coletada. Os administradores aplicam *políticas* a cada ponto de extremidade para afetar o comportamento. [As políticas](/azure/api-management/api-management-howto-policies) são instruções predefinidas que são executadas em sequência para cada chamada de serviço.  As políticas são configuradas para uma chamada de entrada, chamada de saída ou chamadas após um erro. As políticas podem ser aplicadas em diferentes escopos de serviço como para habilitar a ordenação determinística ao combinar políticas. O produto é fornecido com um grande número de [políticas](/azure/api-management/api-management-policies)predefinidas.

Aqui estão exemplos de como as políticas podem afetar o comportamento de seus serviços nativos de nuvem:  

- Restringir o acesso ao serviço.
- Impor autenticação.  
- Limite as chamadas de uma única fonte, se necessário.
- Habilitar caching.
- Bloquear chamadas de endereços IP específicos.
- Controle o fluxo do serviço.
- Converta solicitações de SOAP em REST ou entre diferentes formatos de dados, como de XML para JSON.

O gerenciamento de API do Azure pode expor serviços de back-end hospedados em qualquer lugar – na nuvem ou em seu data center. Para serviços herdados que você pode expor em seus sistemas nativos de nuvem, ele dá suporte a APIs REST e SOAP. Até outros serviços do Azure podem ser expostos por meio do gerenciamento de API. Você pode fazer uma API gerenciada sobre um serviço de backup do Azure, como o [barramento de serviço](https://azure.microsoft.com/services/service-bus/) do Azure ou [aplicativos lógicos do Azure](https://azure.microsoft.com/services/logic-apps/). O gerenciamento de API do Azure não inclui suporte interno ao balanceamento de carga e deve ser usado em conjunto com um serviço de balanceamento de carga.

O gerenciamento de API do Azure está disponível em [quatro camadas diferentes](https://azure.microsoft.com/pricing/details/api-management/):

- Desenvolvedor
- Basic
- Standard
- Premium

A camada de desenvolvedor destina-se a cargas de trabalho e avaliação de não produção. As outras camadas oferecem progressivamente mais energia, recursos e SLAs (contratos de nível de serviço) mais altos. A camada Premium fornece [suporte a várias regiões e à](/azure/api-management/api-management-howto-deploy-multi-region) [rede virtual do Azure](/azure/virtual-network/virtual-networks-overview) . Todas as camadas têm um preço fixo por hora.

A nuvem do Azure também oferece uma [camada sem servidor](https://azure.microsoft.com/blog/announcing-azure-api-management-for-serverless-architectures/) para o gerenciamento de API do Azure. Referido como o *tipo de preço de consumo*, o serviço é uma variante do gerenciamento de API projetado em relação ao modelo de computação sem servidor. Ao contrário dos tipos de preço "pré-alocados" mostrados anteriormente, o nível de consumo fornece provisionamento instantâneo e preços de pagamento por ação.

Ele habilita recursos de gateway de API para os seguintes casos de uso:

- Os microserviços implementados usando tecnologias sem servidor, como [Azure Functions](/azure/azure-functions/functions-overview) e [aplicativos lógicos do Azure](https://azure.microsoft.com/services/logic-apps/).
- Recursos de serviço de backup do Azure, como filas e tópicos do barramento de serviço, armazenamento do Azure e outros.
- Microserviços em que o tráfego tem picos ocasionais grandes, mas permanece o mais baixo possível.

O nível de consumo usa os mesmos componentes subjacentes de gerenciamento de API de serviço, mas emprega uma arquitetura totalmente diferente com base em recursos alocados dinamicamente. Ele se alinha perfeitamente com o modelo de computação sem servidor:

- Nenhuma infraestrutura para gerenciar.
- Sem capacidade ociosa.
- Alta disponibilidade.
- Dimensionamento automático.
- O custo é baseado no uso real.
  
A nova camada de consumo é uma ótima opção para sistemas nativos de nuvem que expõem recursos sem servidor como APIs.

## <a name="real-time-communication"></a>Comunicação em tempo real

A comunicação em tempo real ou por push é outra opção para aplicativos de front-end que se comunicam com sistemas nativos de nuvem de back-end por HTTP. Os aplicativos, como os Tick-Financials, educação online, jogos e atualizações de andamento do trabalho, exigem respostas instantâneas e em tempo real do back-end. Com a comunicação HTTP normal, não há como o cliente saber quando novos dados estão disponíveis. O cliente deve *sondar* ou enviar continuamente solicitações para o servidor. Com a comunicação em *tempo real* , o servidor pode enviar novos dados para o cliente a qualquer momento.

Os sistemas em tempo real geralmente são caracterizados por fluxos de dados de alta frequência e por um grande número de conexões de cliente simultâneas. A implementação manual da conectividade em tempo real pode rapidamente se tornar complexa, exigindo uma infraestrutura não trivial para garantir a escalabilidade e o sistema de mensagens confiável aos clientes conectados. Você pode se encontrar gerenciando uma instância do cache Redis do Azure e um conjunto de balanceadores de carga configurados com sessões adesivas para afinidade de cliente.

O [serviço de signaler do Azure](https://azure.microsoft.com/services/signalr-service/) é um serviço do Azure totalmente gerenciado que simplifica a comunicação em tempo real para seus aplicativos nativos de nuvem. Detalhes de implementação técnica, como provisionamento de capacidade, dimensionamento e conexões persistentes, são dissociados. Eles são tratados para você com um contrato de nível de serviço de 99,9%. Você se concentra nos recursos do aplicativo, não no direcionamento da infraestrutura.

Uma vez habilitado, um serviço HTTP baseado em nuvem pode enviar atualizações de conteúdo diretamente a clientes conectados, incluindo aplicativos de navegador, móveis e de área de trabalho. Os clientes são atualizados sem a necessidade de sondar o servidor. O Azure Signalr abstrai as tecnologias de transporte que criam conectividade em tempo real, incluindo WebSockets, Server-Side eventos e sondagem longa. Os desenvolvedores se concentram em enviar mensagens para todos ou subconjuntos específicos de clientes conectados.

A Figura 4-7 mostra um conjunto de clientes HTTP que se conectam a um aplicativo nativo de nuvem com o Signaler do Azure habilitado.

![Azure SignalR](./media/azure-signalr-service.png)

**Figura 4-7.** Azure SignalR

Outra vantagem do serviço Signalr do Azure é a implementação de serviços nativos de nuvem sem servidor. Talvez seu código seja executado sob demanda com Azure Functions gatilhos. Esse cenário pode ser complicado porque seu código não mantém conexões longas com clientes. O Serviço Azure SignalR pode lidar com essa situação, uma vez que o serviço já gerencia conexões para você.

O serviço de sinalizador do Azure integra-se perfeitamente a outros serviços do Azure, como o banco de dados SQL do Azure, o barramento de serviço ou o cache Redis, abrindo muitas possibilidades para seus aplicativos nativos de nuvem.

>[!div class="step-by-step"]
>[Anterior](communication-patterns.md) 
> [Avançar](service-to-service-communication.md)
