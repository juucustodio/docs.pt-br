---
title: Projetando um microsserviço orientado a DDD
description: Arquitetura de Microsserviços .NET para aplicativos .NET em contêineres | Entenda o design do microsserviço de pedidos orientado a DDD e suas camadas de aplicativo.
ms.date: 01/13/2021
ms.openlocfilehash: 1d17f0842bb371ce65e96f33d25b2d6e94493396
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188329"
---
# <a name="design-a-ddd-oriented-microservice"></a>Projetar um microsserviço orientado a DDD

O DDD (design orientado a domínio) defende modelagem com base na realidade dos negócios conforme relevante para os seus casos de uso. No contexto da criação de aplicativos, o DDD fala sobre problemas como domínios. Ele descreve as áreas de problema independentes como Contextos Limitados (cada Contexto Limitado se correlaciona a um microsserviço) e enfatiza uma linguagem comum para falar sobre esses problemas. Ele também sugere muitos padrões e conceitos técnicos, como entidades de domínio com modelos avançados (sem [modelo de anêmico de domínio](https://martinfowler.com/bliki/AnemicDomainModel.html)), objetos de valor, agregações e regras raiz de agregação (ou entidade raiz) para dar suporte à implementação interna. Esta seção apresenta o design e a implementação desses padrões internos.

Às vezes, esses padrões e regras técnicas de DDD são considerados obstáculos que têm uma curva de aprendizado acentuada para implementar abordagens de DDD. Mas a parte importante não são os padrões em si, mas organizar o código para que ele fique alinhado aos problemas de negócios e usar os mesmos termos de negócios (linguagem ubíqua). Além disso, as abordagens DDD deverão ser aplicadas somente se você estiver implementando microsserviços complexos com regras de negócio significativas. Responsabilidades mais simples, como um serviço CRUD, podem ser gerenciadas com abordagens mais simples.

Onde traçar os limites é a tarefa principal ao criar e definir um microsserviço. Padrões DDD ajudam você a compreender a complexidade no domínio. Para o modelo de domínio para cada Contexto Limitado, você pode identificar e definir as entidades, os objetos de valor e agregações que modelem seu domínio. Você cria e refina um modelo de domínio contido dentro de um limite que define o seu contexto. E isso é explícito na forma de um Microservice. Os componentes dentro desses limites acabam sendo seus microsserviços, embora, em alguns casos, uma continuidade de negócios ou microsserviços de negócios possam ser compostos por vários serviços físicos. DDD é sobre limites, assim como os microsserviços.

## <a name="keep-the-microservice-context-boundaries-relatively-small"></a>Mantenha os limites de contexto do microsserviço relativamente pequenos

Determinar onde colocar os limites entre Contextos Limitados equilibra dois objetivos concorrentes. Primeiro, você deseja criar inicialmente os menores microsserviços possíveis, embora isso não deva ser a meta principal; você deve criar um limite em torno de itens que precisam de coesão. Segundo, você deseja evitar comunicações verborrágica entre microsserviços. Essas metas podem contradizer umas às outras. Você deve equilibrá-las decompondo o sistema em tantos microsserviços quanto puder até ver esses limites de comunicação crescendo rapidamente a cada tentativa adicional de separar um novo contexto limitado. Coesão é essencial em um único contexto limitado.

É semelhante ao [cheiro de código de Intimidade Inadequada](https://sourcemaking.com/refactoring/smells/inappropriate-intimacy) ao implementar classes. Se dois microsserviços precisarem colaborar muito entre si, eles deverão provavelmente ser o mesmo microsserviço.

Outra maneira de examinar esse aspecto é a autonomia. Se um microsserviço precisar confiar em outro serviço para atender diretamente a uma solicitação, ele não será realmente autônomo.

## <a name="layers-in-ddd-microservices"></a>Camadas em microsserviços de DDD

A maioria dos aplicativos empresariais com complexidade de negócios e técnica significativa é definida por várias camadas. As camadas são um artefato lógico e não estão relacionadas à implantação do serviço. Elas existem para ajudar os desenvolvedores a gerenciar a complexidade no código. Camadas diferentes (como a camada de modelo de domínio versus a camada de apresentação, etc.) podem ter tipos diferentes, que exigem traduções entre esses tipos.

Por exemplo, uma entidade pode ser carregada do banco de dados. Em seguida, parte dessas informações ou uma agregação de informações, incluindo dados adicionais de outras entidades, podem ser enviadas para uma interface do usuário do cliente por meio de uma API da Web REST. O ponto aqui é que a entidade de domínio está contida na camada de modelo de domínio e não deve ser propagada para outras áreas às quais ela não pertence, como a camada de apresentação.

Além disso, você precisa ter entidades sempre válidas (consulte a seção [Criar validações na camada de modelo de domínio](domain-model-layer-validations.md)) controlada por raízes agregadas (entidades raiz). Portanto, as entidades não devem ser associadas aos modos de exibição do cliente pois, no nível da interface do usuário, alguns dados podem ainda não ter sido validados. Esse motivo é o que o ViewModel é para. O ViewModel é um modelo de dados exclusivamente para necessidades de camada de apresentação. As entidades de domínio não pertencem diretamente ao ViewModel. Em vez disso, você precisa converter entre entidades de domínio e ViewModels e vice-versa.

Ao lidar com complexidade, é importante ter um modelo de domínio controlado por raízes agregadas que garantam que todas as invariáveis e regras relacionadas àquele grupo de entidades (agregação) sejam executadas por meio de um único ponto de entrada ou porta, a raiz de agregação.

A Figura 7-5 mostra como um design em camadas é implementado no aplicativo eShopOnContainers.

![Diagrama mostrando as camadas em um microserviço de design controlado por domínio.](./media/ddd-oriented-microservice/domain-driven-design-microservice.png)

**Figura 7-5**. Camadas DDD no microsserviço de ordenação em eShopOnContainers

As três camadas em um microsserviço de DDD como o de pedidos. Cada camada é um projeto do VS: a camada de aplicativo é Ordering.API, a camada de domínio é Ordering.Domain e a camada de infraestrutura é Ordering.Infrastructure. Você deseja criar o sistema de modo que cada camada se comunique apenas com determinadas outras camadas. Essa abordagem pode ser mais fácil de ser imposta se as camadas são implementadas como bibliotecas de classes diferentes, pois você pode identificar claramente quais dependências são definidas entre as bibliotecas. Por exemplo, a camada de modelo de domínio não deve receber uma dependência de nenhuma outra camada (as classes de modelo de domínio devem ser [POCO](https://en.wikipedia.org/wiki/Plain_Old_CLR_Object) ou Plain Old CLR Objects). Como mostra a Figura 7-6, a biblioteca de camadas **Order. Domain** tem dependências somente nas bibliotecas .net ou nos pacotes NuGet, mas não em nenhuma outra biblioteca personalizada, como biblioteca de dados ou biblioteca de persistência.

![Captura de tela de ordenação de dependências. domain.](./media/ddd-oriented-microservice/ordering-domain-dependencies.png)

**Figura 7-6**. Camadas implementadas como bibliotecas permitem melhor controle de dependências entre as camadas

### <a name="the-domain-model-layer"></a>A camada de modelo de domínio

O excelente livro de Eric Evans, [Domain Driven Design](https://domainlanguage.com/ddd/) (Projeto Orientado a Domínio) diz o seguinte sobre a camada de modelo de domínio e a camada de aplicativo.

**Camada de modelo de domínio**: responsável por representar conceitos de negócios, informações sobre a situação de negócios e as regras de negócio. O estado que reflete a situação de negócios é controlado e usado aqui, embora os detalhes técnicos de armazená-lo sejam delegados à infraestrutura. Essa camada é a essência do software de negócios.

A camada de modelo de domínio é onde os negócios é expresso. Quando você implementa uma camada de modelo de domínio de microsserviço em .NET, essa camada é codificada como uma biblioteca de classes com as entidades de domínio que capturam dados mais comportamento (métodos com lógica).

Seguindo os princípios de [Ignorância da Persistência](https://deviq.com/persistence-ignorance/) e a [Ignorância da Infraestrutura](https://ayende.com/blog/3137/infrastructure-ignorance), essa camada deve ignorar totalmente os detalhes de persistência de dados. Essas tarefas de persistência devem ser executadas pela camada de infraestrutura. Portanto, essa camada não deveria receber dependências diretas da infraestrutura, o que significa que uma regra importante é que suas classes de entidade do modelo de domínio devem ser [POCO](https://en.wikipedia.org/wiki/Plain_Old_CLR_Object)s.

Entidades de domínio não devem ter nenhuma dependência direta (como derivar de uma classe base) em nenhuma estrutura de infraestrutura de acesso a dados, como Entity Framework ou NHibernate. Idealmente, suas entidades de domínio não devem derivar nem implementar nenhum tipo definido em nenhuma estrutura de infraestrutura.

As estruturas ORM mais modernas, como Entity Framework Core, permitem essa abordagem, de modo que suas classes de modelo de domínio não estejam ligadas à infraestrutura. No entanto, ter entidades POCO nem sempre é possível ao usar determinados bancos de dados NoSQL e estruturas, como Atores e Coleções Confiáveis no Azure Service Fabric.

Mesmo quando é importante seguir o princípio de Ignorância de Persistência para o modelo de Domínio, você não deve ignorar preocupações de persistência. Ainda é importante entender o modelo de dados físicos e como ele é mapeado para o modelo de objeto de entidade. Caso contrário, você pode criar designs impossíveis.

Além disso, esse aspecto não significa que você pode usar um modelo projetado para um banco de dados relacional e movê-lo diretamente para um banco de dados NoSQL ou orientado a documentos. Em alguns modelos de entidade, o modelo pode se ajustar, mas geralmente não se ajusta. Ainda há restrições que o modelo de entidade deve cumprir, com base tanto na tecnologia de armazenamento quanto na tecnologia ORM.

### <a name="the-application-layer"></a>A camada de aplicativo

Passando para a camada de aplicativo, novamente podemos citar o livro de Eric Evans [Domain Driven Design](https://domainlanguage.com/ddd/) (Projeto Orientado a Domínio):

**Camada de aplicativo:** define os trabalhos que o software deve fazer e direciona os objetos de domínio expressivos para resolver problemas. As tarefas pelas quais esta camada é responsável são significativas para os negócios ou necessárias para a interação com as camadas do aplicativo de outros sistemas. Essa camada é mantida fina. Ele não contém regras de negócio nem conhecimento, mas apenas coordena o trabalho de tarefas e delegados para colaborações de objetos de domínio na próxima camada abaixo. Ele não tem um estado refletindo a situação de negócios, mas pode ter um estado que reflita o progresso de uma tarefa para o usuário ou o programa.

A camada de aplicativo de um microserviço no .NET normalmente é codificada como um projeto de API da Web ASP.NET Core. O projeto implementa a interação do microserviço, o acesso remoto à rede e as APIs da Web externas usadas na interface do usuário ou nos aplicativos cliente. Ele incluirá consultas se estiver usando uma abordagem CQRS, comandos aceitos pelo microsserviço e até mesmo a comunicação controlada por evento entre microsserviços (eventos de integração). A API Web do ASP.NET Core que representa a camada de aplicativo não deve conter as regras de negócio nem o conhecimento do domínio (especialmente regras de domínio para transações ou atualizações); isso deve ser de propriedade da biblioteca de classes de modelo de domínio. A camada do aplicativo deve apenas coordenar tarefas e não deve reter nem definir qualquer estado de domínio (modelo de domínio). Ela delega a execução de regras de negócio para as classes de modelo de domínio em si (raízes agregadas e entidades de domínio), que, por fim, atualizarão os dados dentro dessas entidades de domínio.

Basicamente, a “lógica de aplicativo” é onde você implementa todos os casos de uso que dependem de um determinado front-end. Por exemplo, a implementação relacionada a um serviço de API da Web.

A meta é que a lógica do domínio na camada de modelo de domínio, suas invariáveis, o modelo de dados e as regras de negócio relacionadas sejam completamente independentes das camadas de apresentação e do aplicativo. Principalmente, a camada de modelo de domínio deve não deve depender diretamente de nenhuma estrutura de infraestrutura.

### <a name="the-infrastructure-layer"></a>A camada de infraestrutura

A camada de infraestrutura é como os dados inicialmente mantidos em entidades de domínio (em memória) são mantidos em bancos de dados ou outro repositório persistente. Um exemplo é usar o código do Entity Framework Core para implementar as classes padrão do repositório que usam um DBContext para manter os dados em um banco de dados relacional.

De acordo com os princípios de [ignorância de persistência](https://deviq.com/persistence-ignorance/) e [ignorância de infraestrutura](https://ayende.com/blog/3137/infrastructure-ignorance) mencionados anteriormente, a camada de infraestrutura não deve "contaminate" a camada de modelo de domínio. Você deve manter as classes de entidade de modelo de domínio independentes da infraestrutura que você usa para manter os dados (EF ou qualquer outra estrutura) não obtendo dependências rígidas de estruturas. Sua biblioteca de classes de camada de modelo de domínio deve ter somente o código de domínio, apenas classes de entidade [POCO](https://en.wikipedia.org/wiki/Plain_Old_CLR_Object) implementando a essência do seu software e completamente separadas de tecnologias de infraestrutura.

Assim, suas camadas ou bibliotecas e projetos de classes devem, por fim, depender da sua camada de modelo de domínio (biblioteca), não vice-versa, conforme mostra a Figura 7-7.

![Diagrama mostrando dependências que existem entre as camadas de serviço do DDD.](./media/ddd-oriented-microservice/ddd-service-layer-dependencies.png)

**Figura 7-7**. Dependências entre camadas em DDD

Dependências em um serviço de DDD, a camada de aplicativo depende do domínio e da infraestrutura e a infraestrutura depende do domínio, mas o domínio não depende de nenhuma camada. Esse design de camada deve ser independente de cada microsserviço. Conforme observado anteriormente, você pode implementar os microsserviços mais complexos seguindo padrões DDD ao mesmo tempo em que implementa microsserviços conduzidos por dados mais simples (CRUD simples em uma única camada) de maneira mais simples.

#### <a name="additional-resources"></a>Recursos adicionais

- **DevIQ. Princípio de ignorância de persistência** \
  <https://deviq.com/persistence-ignorance/>

- **Oren Eini. Ignorância de infraestrutura** \
  <https://ayende.com/blog/3137/infrastructure-ignorance>

- **Anjo Lopez. Arquitetura em camadas no design de Domain-Driven** \
  <https://ajlopez.wordpress.com/2008/09/12/layered-architecture-in-domain-driven-design/>

>[!div class="step-by-step"]
>[Anterior](cqrs-microservice-reads.md) 
> [Avançar](microservice-domain-model.md)
