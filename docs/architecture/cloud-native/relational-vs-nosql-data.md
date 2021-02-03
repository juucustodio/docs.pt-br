---
title: Relacional versus Dados NoSQL
description: Saiba mais sobre dados relacionais e NoSQL em aplicativos nativos de nuvem
author: robvet
ms.date: 01/19/2021
ms.openlocfilehash: 1148778b68c90586187d927eccd9b733403ede44
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505505"
---
# <a name="relational-vs-nosql-data"></a>Relacional versus Dados NoSQL

Relacional e NoSQL são dois tipos de sistemas de banco de dados comumente implementados em aplicativos nativos de nuvem. Eles são criados de forma diferente, armazenam dados de maneira diferente e acessados de forma diferente. Nesta seção, veremos os dois. Mais adiante neste capítulo, veremos uma tecnologia de banco de dados emergente chamada *NewSQL*.

*Os bancos de dados relacionais* têm sido uma tecnologia predominante há décadas. Eles são maduros, comprovados e amplamente implementados. Produtos de banco de dados concorrentes, ferramentas e abound de experiência. Os bancos de dados relacionais fornecem um armazenamento de tabelas relacionadas. Essas tabelas têm um esquema fixo, usam o SQL (linguagem SQL) para gerenciar dados e dão suporte a garantias ACID.

*Os bancos de dados não-SQL* se referem a armazenamentos não relacionais de alto desempenho. Eles se destacam em suas características de facilidade de uso, escalabilidade, resiliência e disponibilidade. Em vez de unir tabelas de dados normalizados, o NoSQL armazena dados não estruturados ou semiestruturados, geralmente em pares chave-valor ou documentos JSON. Os bancos de dados não SQL normalmente não fornecem garantias de ACID além do escopo de uma única partição de banco de dados. Serviços de alto volume que exigem tempo de resposta de subsegundo favorecem armazenamentos de bancos de serviços NoSQL.

O impacto das tecnologias [NoSQL](https://www.geeksforgeeks.org/introduction-to-nosql/) para sistemas nativos de nuvem distribuída não pode ser muito deEstado. A proliferação de novas tecnologias de dados neste espaço interrompeu as soluções que, uma vez, contavam exclusivamente com os bancos dados relacionais.

Os bancos de dados NoSQL incluem vários modelos diferentes para o acesso e o gerenciamento, cada um adequado para casos de uso específicos. A Figura 5-9 apresenta quatro modelos comuns.

![Modelos de dados NoSQL](./media/types-of-nosql-datastores.png)

**Figura 5-9**: modelos de dados para bancos de dados NoSQL

| Modelar | Características |
| :-------- | :-------- |
| Repositório de documentos | Os dados e os metadados são armazenados hierarquicamente em documentos baseados em JSON no banco de dados. |
| Repositório de valor de chave | A maneira mais simples dos bancos de dados NoSQL, que são representados como uma coleção de pares chave-valor. |
| Wide-Column Store | Os dados relacionados são armazenados como um conjunto de pares de chave/valor aninhados em uma única coluna. |
| Repositório de grafo | Os dados são armazenados em uma estrutura de gráfico como nó, borda e propriedades de dados. |

## <a name="the-cap-theorem"></a>Teorema CAP

Como uma maneira de entender as diferenças entre esses tipos de bancos de dados, considere o limite teorema, um conjunto de princípios aplicados a sistemas distribuídos que armazenam o estado. A Figura 5-10 mostra as três propriedades do CAP teorema.

![Teorema de CAP](./media/cap-theorem.png)

**Figura 5-10**. Teorema CAP

O teorema afirma que os sistemas de dados distribuídos oferecerão uma compensação entre consistência, disponibilidade e tolerância de partição. E, qualquer banco de dados pode garantir apenas *duas* das três propriedades:

- *Verificação.* Cada nó no cluster responde com os dados mais recentes, mesmo que o sistema deva bloquear a solicitação até que todas as réplicas sejam atualizadas. Se você consultar um "sistema consistente" para um item que está sendo atualizado no momento, você aguardará essa resposta até que todas as réplicas sejam atualizadas com êxito. No entanto, você receberá os dados mais atuais.

- *Ininterrupta.* Cada nó retorna uma resposta imediata, mesmo que essa resposta não seja os dados mais recentes. Se você consultar um "sistema disponível" para um item que está sendo atualizado, você obterá a melhor resposta possível que o serviço pode fornecer naquele momento.

- *Tolerância a partição.* Garante que o sistema continue a operar mesmo que um nó de dados replicado falhe ou perca a conectividade com outros nós de dados replicados.

Os bancos de dados relacionais normalmente fornecem consistência e disponibilidade, mas não a tolerância de partição. Normalmente, eles são provisionados para um único servidor e são dimensionados verticalmente adicionando mais recursos à máquina.

Muitos sistemas de banco de dados relacional dão suporte a recursos de replicação internos em que as cópias do banco de dados primário podem ser feitas em outras instâncias de servidor secundário. As operações de gravação são feitas na instância primária e replicadas para cada uma das secundárias. Após uma falha, a instância primária pode fazer failover para um secundário a fim de fornecer alta disponibilidade. Os secundários também podem ser usados para distribuir operações de leitura. Enquanto as operações de gravação sempre vão para a réplica primária, as operações de leitura podem ser roteadas para qualquer um dos secundários para reduzir a carga do sistema.

Os dados também podem ser particionados horizontalmente em vários nós, como com a [fragmentação](/azure/sql-database/sql-database-elastic-scale-introduction). Mas a fragmentação aumenta drasticamente a sobrecarga operacional por Spitting dados em muitas partes que não podem se comunicar facilmente. Ele pode ser dispendioso e demorado para gerenciar. Ele pode acabar afetando o desempenho, as junções de tabelas e a integridade referencial.

Se as réplicas de dados tiverem perdido a conectividade de rede em um cluster de banco de dados relacional "altamente consistente", você não poderá gravar no banco de dados. O sistema rejeitaria a operação de gravação, pois ela não pode replicar essa alteração para a outra réplica de dados. Cada réplica de dados precisa ser atualizada antes que a transação possa ser concluída.

Os bancos de dados NoSQL normalmente dão suporte à alta disponibilidade e à tolerância a partições. Eles são expandidos horizontalmente, geralmente em servidores de mercadoria. Essa abordagem fornece excelente disponibilidade, dentro e entre regiões geográficas a um custo reduzido. Você particiona e replica dados entre esses computadores, ou nós, fornecendo redundância e tolerância a falhas. A desvantagem é a consistência. Uma alteração nos dados em um nó NoSQL pode levar algum tempo para ser propagada para outros nós. Normalmente, um nó de banco de dados NoSQL fornecerá uma resposta imediata a uma consulta, mesmo que os dados apresentados estejam obsoletos e ainda não tenham sido atualizados.

Se as réplicas de dados tiverem de perder a conectividade em um cluster de banco de dado NoSQL "altamente disponível", você ainda poderá concluir uma operação de gravação no banco de dados. O cluster de banco de dados permitiria a operação de gravação e atualizaria cada réplica de dado à medida que ela se tornar disponível.

Esse tipo de resultado é conhecido como consistência eventual, uma característica de sistemas de dados distribuídos em que não há suporte para transações ACID. É um breve atraso entre a atualização de um item de dados e o tempo necessário para propagar essa atualização para cada um dos nós de réplica. Em condições normais, o retardo é normalmente curto, mas pode aumentar quando surgirem problemas. Por exemplo, o que aconteceria se você atualizasse um item de produto em um banco de dados NoSQL no Estados Unidos e consultasse o mesmo item de dado de um nó de réplica na Europa? Você receberia as informações anteriores do produto, até que o cluster atualize o nó Europeu com a alteração do produto. Retornando imediatamente um resultado de consulta e não aguardando a atualização de todos os nós de réplica, você obterá enorme escala e volume, mas com a possibilidade de apresentar dados mais antigos.

Alta disponibilidade e escalabilidade maciça geralmente são mais críticas para os negócios do que a consistência forte. Os desenvolvedores podem implementar técnicas e padrões como sagas, CQRS e mensagens assíncronas para adotar consistência eventual.

> Hoje em dia, deve-se ter cuidado ao considerar as restrições de teorema CAP. Um novo tipo de banco de dados, chamado NewSQL, surgiu, que estende o mecanismo de banco de dados relacional para dar suporte à escalabilidade horizontal e ao desempenho escalonável dos sistemas NoSQL.

## <a name="considerations-for-relational-vs-nosql-systems"></a>Considerações para sistemas relacionais versus NoSQL

Com base em requisitos de dados específicos, um microserviço baseado em nuvem é capaz de implementar um repositório de armazenamento de data de NoSQL e relacional ou ambos.

|  Considere um repositório de armazenamento NoSQL quando: | Considere um banco de dados relacional quando: |
| :-------- | :-------- |
| Você tem cargas de trabalho de alto volume que exigem grande escala | Seu volume de carga de trabalho é consistente e requer escala média para grande |
| Suas cargas de trabalho não exigem garantias ACID |  Garantias de ACID são necessárias |
| Seus dados são dinâmicos e frequentemente alterados | Seus dados são previsíveis e altamente estruturados |
| Os dados podem ser expressos sem relações | Os dados são expressos de maneira relacional |  
| Você precisa de gravações rápidas e a segurança de gravação não é crítica | A segurança de gravação é um requisito |  
| A recuperação de dados é simples e tende a ser simples | Você trabalha com consultas e relatórios complexos|
| Seus dados exigem uma ampla distribuição geográfica | Os usuários são mais centralizados |
| Seu aplicativo será implantado em um hardware de mercadoria, como com nuvens públicas | Seu aplicativo será implantado em hardware grande e high-end |

Nas próximas seções, exploraremos as opções disponíveis na nuvem do Azure para armazenar e gerenciar seus dados nativos de nuvem.

## <a name="database-as-a-service"></a>Banco de dados como serviço

Para começar, você pode provisionar uma máquina virtual do Azure e instalar o banco de dados de sua escolha para cada serviço. Embora você tenha controle total sobre o ambiente, abrem mão muitos recursos internos da plataforma de nuvem. Você também será responsável por gerenciar a máquina virtual e o banco de dados para cada serviço. Essa abordagem pode rapidamente tornar-se demorada e cara.

Em vez disso, os aplicativos nativos de nuvem favorecem os serviços de dados expostos como um [DBaaS (Database as Service como serviço)](https://www.stratoscale.com/blog/dbaas/what-is-database-as-a-service/). Totalmente gerenciado por um fornecedor de nuvem, esses serviços fornecem segurança, escalabilidade e monitoramento internos. Em vez de possuir o serviço, basta consumi-lo como um [serviço de backup](./definition.md#backing-services). O provedor opera o recurso em escala e tem a responsabilidade por desempenho e manutenção.

Eles podem ser configurados em regiões e zonas de disponibilidade de nuvem para obter alta disponibilidade. Todos eles dão suporte à capacidade just-in-time e a um modelo pago conforme o uso. O Azure apresenta diferentes tipos de opções de serviço de dados gerenciado, cada uma com benefícios específicos.

Primeiro, veremos os serviços DBaaS relacionais disponíveis no Azure. Você verá que o principal banco de dados de SQL Server da Microsoft está disponível junto com várias opções de código-fonte aberto. Em seguida, falaremos sobre os serviços de dados NoSQL no Azure.

## <a name="azure-relational-databases"></a>Bancos de dados relacionais do Azure

Para os microserviços nativos de nuvem que exigem dados relacionais, o Azure oferece quatro ofertas de DBaaS (bancos de dado relacionais como serviço) gerenciados, mostrados na Figura 5-11.

![Bancos de dados relacionais gerenciados no Azure](./media/azure-managed-databases.png)

**Figura 5-11**. Bancos de dados relacionais gerenciados disponíveis no Azure

Na figura anterior, observe como cada um se baseia em uma infraestrutura DBaaS comum que apresenta os principais recursos sem custo adicional.

Esses recursos são especialmente importantes para as organizações que provisionam grandes números de bancos de dados, mas têm recursos limitados para administrá-los.
Você pode provisionar um banco de dados do Azure em minutos selecionando a quantidade de núcleos de processamento, memória e armazenamento subjacente. Você pode dimensionar o banco de dados instantaneamente e ajustar dinamicamente os recursos com pouco ou nenhum tempo de inatividade.

## <a name="azure-sql-database"></a>Banco de Dados SQL do Azure

As equipes de desenvolvimento com experiência em Microsoft SQL Server devem considerar o [banco de dados SQL do Azure](/azure/sql-database/). É um DBaaS (banco de dados como serviço) relacional totalmente gerenciado com base na Mecanismo de Banco de Dados do Microsoft SQL Server. O serviço compartilha muitos recursos encontrados na versão local do SQL Server e executa a versão estável mais recente do Mecanismo de Banco de Dados de SQL Server.

Para uso com um microserviço nativo de nuvem, o banco de dados SQL do Azure está disponível com três opções de implantação:

- Uma Banco de Dados Individual representa um banco de dados SQL totalmente gerenciado em execução em um [servidor de banco de dados SQL do Azure](/azure/sql-database/sql-database-servers) na nuvem do Azure. O banco de dados é considerado [*contido*](/sql/relational-databases/databases/contained-databases) porque não tem nenhuma dependência de configuração no servidor de banco de dados subjacente.
  
- Uma [instância gerenciada](/azure/sql-database/sql-database-managed-instance) é uma instância totalmente gerenciada do mecanismo de banco de dados do Microsoft SQL Server que fornece compatibilidade quase 100% com uma SQL Server local. Essa opção dá suporte a bancos de dados maiores, até 35 TB e é colocada em uma [rede virtual do Azure](/azure/virtual-network/virtual-networks-overview) para um melhor isolamento.

- O [banco de dados SQL sem servidor do Azure](/azure/sql-database/sql-database-serverless) é uma camada de computação para um banco de dados individual que é dimensionado automaticamente com base na demanda de carga de trabalho Ele cobra apenas pela quantidade de computação usada por segundo. O serviço é adequado para cargas de trabalho com padrões de uso intermitentes e imprevisíveis, intercalados com períodos de inatividade. A camada de computação sem servidor também pausa automaticamente os bancos de dados durante períodos inativos para que somente os encargos de armazenamento sejam cobrados. Ela é retomada automaticamente quando a atividade retorna.

Além da pilha de Microsoft SQL Server tradicional, o Azure também apresenta versões gerenciadas de três bancos de dados de software livre populares.

## <a name="open-source-databases-in-azure"></a>Bancos de dados de código aberto no Azure

Os bancos de dados relacionais de código aberto se tornaram uma opção popular para aplicativos nativos de nuvem. Muitas empresas favorecem esses produtos de banco de dados comercial, especialmente para economia de custos. Muitas equipes de desenvolvimento aproveitam sua flexibilidade, desenvolvimento com suporte da Comunidade e ecossistema de ferramentas e extensões. Os bancos de dados de software livre podem ser implantados em vários provedores de nuvem, ajudando a minimizar a preocupação de "bloqueio de fornecedor".

Os desenvolvedores podem facilmente hospedar automaticamente qualquer banco de dados de código-fonte aberto em uma VM do Azure. Embora forneça controle total, essa abordagem o coloca no gancho do gerenciamento, do monitoramento e da manutenção do banco de dados e da VM.

No entanto, a Microsoft continua seu compromisso de manter o Azure uma "plataforma aberta" oferecendo vários bancos de dados de software livre populares como serviços DBaaS *totalmente gerenciados* .

### <a name="azure-database-for-mysql"></a>Banco de Dados do Azure para MySQL

O [MySQL](https://en.wikipedia.org/wiki/MySQL) é um banco de dados relacional de código aberto e um pilar para aplicativos criados na [pilha de software da lâmpada](https://en.wikipedia.org/wiki/LAMP_(software_bundle)). Amplamente escolhido para cargas de trabalho de *leitura pesada* , ela é usada por muitas organizações de grande porte, incluindo Facebook, Twitter e YouTube. A Community Edition está disponível gratuitamente, enquanto a Enterprise Edition exige uma compra de licença. Criado originalmente em 1995, o produto foi adquirido pela Sun Microsystems em 2008. A Oracle adquiriu Sun e MySQL em 2010.

O [banco de dados do Azure para MySQL](https://azure.microsoft.com/services/mysql/) é um serviço de banco de dados relacional gerenciado baseado no mecanismo de servidor MySQL de código-fonte aberto. Ele usa o MySQL Community Edition. O servidor MySQL do Azure é o ponto administrativo para o serviço. É o mesmo mecanismo de servidor MySQL usado para implantações locais. O mecanismo pode criar um único banco de dados por servidor ou vários bancos por servidor que compartilham recursos. Você pode continuar a gerenciar dados usando as mesmas ferramentas de código-fonte aberto sem ter que aprender novas habilidades ou gerenciar máquinas virtuais.

### <a name="azure-database-for-mariadb"></a>Banco de Dados do Azure para MariaDB

[MariaDB](https://mariadb.com/) O servidor é outro servidor de banco de dados de software livre popular. Ele foi criado como uma *bifurcação* do MySQL quando a Oracle comprou a Sun Microsystems, que era o MySQL. A intenção era garantir que MariaDB permanecia Open-Source. Como MariaDB é uma bifurcação do MySQL, as definições de tabela e de dados são compatíveis e os protocolos, estruturas e APIs do cliente são close-spojit.

O MariaDB tem uma comunidade forte e é usado por muitas empresas de grande porte. Embora a Oracle continue a manter, aprimorar e oferecer suporte ao MySQL, o MariaDB Foundation gerencia o MariaDB, permitindo contribuições públicas para o produto e a documentação.

O [banco de dados do Azure para MariaDB](https://azure.microsoft.com/services/mariadb/) é um banco de dados relacional totalmente gerenciado como um serviço na nuvem do Azure. O serviço é baseado no mecanismo de servidor do MariaDB Community Edition. Ele pode lidar com cargas de trabalho críticas com desempenho previsível e escalabilidade dinâmica.

### <a name="azure-database-for-postgresql"></a>Banco de Dados do Azure para PostgreSQL

O [PostgreSQL](https://www.postgresql.org/) é um banco de dados relacional de código aberto com mais de 30 anos de desenvolvimento ativo. O PostgresSQL tem uma reputação forte de confiabilidade e integridade de dados. É um recurso rico, compatível com SQL e considerado mais eficaz do que o MySQL, especialmente para cargas de trabalho com consultas complexas e gravações pesadas. Muitas empresas de grande porte, incluindo Apple, Red Hat e Fujitsu, têm produtos criados usando PostgreSQL.

O [banco de dados do Azure para PostgreSQL](https://azure.microsoft.com/services/postgresql/) é um serviço de banco de dados relacional totalmente gerenciado, baseado no mecanismo de banco de dados Postgres de código aberto. O serviço oferece suporte a várias plataformas de desenvolvimento, incluindo C++, Java, Python, Node, C \# e php. Você pode migrar bancos de dados do PostgreSQL para ele usando a ferramenta de [interface de linha de comando](https://datamigration.microsoft.com/scenario/postgresql-to-azurepostgresql?step=1) ou o serviço de migração do Azure Data.

O banco de dados do Azure para PostgreSQL está disponível com duas opções de implantação:

- A opção de implantação de [servidor único](/azure/postgresql/concepts-servers) é um ponto administrativo central para vários bancos de dados nos quais você pode implantar vários bancos de dados. O preço é estruturado por servidor com base nos núcleos e no armazenamento.

- A [opção de hiperescala (Citus)](https://azure.microsoft.com/blog/get-high-performance-scaling-for-your-azure-database-workloads-with-hyperscale/) é alimentada pela tecnologia de dados do Citus. Ele permite alto desempenho, *dimensionando horizontalmente* um único banco de dados em centenas de nós para fornecer desempenho e escala rápidos. Essa opção permite que o mecanismo caiba mais dados na memória, paraleliza consultas em centenas de nós e indexe dados mais rapidamente.

## <a name="nosql-data-in-azure"></a>Dados NoSQL no Azure

Cosmos DB é um serviço de banco de dados NoSQL totalmente gerenciado e distribuído globalmente na nuvem do Azure. Ele foi adotado por muitas grandes empresas em todo o mundo, incluindo Coca-Cola, Skype, ExxonMobil e Liberty mútuo.

Se seus serviços exigirem resposta rápida de qualquer lugar no mundo, alta disponibilidade ou escalabilidade elástica, Cosmos DB será uma ótima opção. A Figura 5-12 mostra Cosmos DB.

![Visão geral do Cosmos DB](./media/cosmos-db-overview.png)

**Figura 5-12**: visão geral do cosmos DB

A figura anterior apresenta muitos dos recursos nativos de nuvem internos disponíveis em Cosmos DB. Nesta seção, vamos examiná-las mais detalhadamente.

### <a name="global-support"></a>Suporte global

Os aplicativos nativos de nuvem geralmente têm um público global e exigem escala global.

Você pode distribuir bancos de dados do cosmos em regiões ou em todo o mundo, posicionando-os perto de seus usuários, melhorando o tempo de resposta e reduzindo a latência. Você pode adicionar ou remover um banco de dados de uma região sem pausar ou reimplantar seus serviços. Em segundo plano, Cosmos DB replica os dados de forma transparente para cada uma das regiões configuradas.

O Cosmos DB dá suporte ao clustering [ativo/ativo](https://kemptechnologies.com/white-papers/unfog-confusion-active-passive-activeactive-load-balancing/) no nível global, permitindo que você configure qualquer uma das suas regiões de banco de dados para dar suporte a *gravações e leituras*.

O protocolo de [vários mestres](/azure/cosmos-db/multi-master-benefits) é um recurso importante no cosmos DB que permite a seguinte funcionalidade:

- Gravação e escalabilidade de leitura elástica ilimitada.

- 99,999% de leitura e gravação de disponibilidade em todo o mundo.

- Garantia de leituras e gravações atendidas em menos de 10 milissegundos no percentil 99.

Com o Cosmos DB [APIs de hospedagem múltipla](/azure/cosmos-db/distribute-data-globally), seu microserviço reconhece automaticamente a região do Azure mais próxima e envia solicitações a ela. A região mais próxima é identificada por Cosmos DB sem nenhuma alteração de configuração. Se uma região ficar indisponível, o recurso de hospedagem múltipla roteará automaticamente as solicitações para a próxima região disponível mais próxima.

### <a name="multi-model-support"></a>Suporte a vários modelos

Ao refazer a plataforma de aplicativos monolíticos para uma arquitetura nativa de nuvem, as equipes de desenvolvimento às vezes precisam migrar armazenamentos de dados NoSQL de código aberto. Cosmos DB pode ajudá-lo a preservar seu investimento nesses armazenamentos de dados NoSQL com a plataforma de *vários modelos* . A tabela a seguir mostra as [APIs de compatibilidade](https://www.wikiwand.com/en/Cosmos_DB)NoSQL com suporte.

| Provedor | Descrição  |
| :-------- | :-------- |
| API do SQL | API proprietária que dá suporte a documentos JSON e consultas baseadas em SQL |
| API do BD do Mongo | Dá suporte a APIs do Mongo DB e a documentos JSON|
| API do Gremlin | Dá suporte à API Gremlin com nós baseados em grafo e representações de dados de borda |
| API Cassandra | Dá suporte à API Casandra para representações de dados de grande coluna |  
| API de Tabela  | Dá suporte ao armazenamento de tabelas do Azure com melhorias Premium |  
| API etcd | Habilita Cosmos DB como um repositório de backup para clusters do serviço kubernetes do Azure |

As equipes de desenvolvimento podem migrar os bancos de dados Mongo, Gremlin ou Cassandra existentes para o Cosmos DB com alterações mínimas no código ou em um dado. Para novos aplicativos, as equipes de desenvolvimento podem escolher entre as opções de código-fonte aberto ou o modelo de API do SQL interno.

> Internamente, o cosmos armazena os dados em um formato struct simples composto por tipos de dados primitivos. Para cada solicitação, o mecanismo de banco de dados converte os dados primitivos na representação de modelo que você selecionou.

Na tabela anterior, observe a opção [API de tabela](/azure/cosmos-db/table-introduction) . Essa API é uma evolução do armazenamento de tabelas do Azure. Ambos compartilham o mesmo modelo de tabela subjacente, mas o Cosmos DB API de Tabela adiciona aprimoramentos Premium não disponíveis na API de armazenamento do Azure. A tabela a seguir contrasta os recursos.

|  | Armazenamento de Tabelas do Azure  | Azure Cosmos DB  |
| :-------- | :-------- |:-------- |
| Latency | Rápido | Latência de milissegundo de dígito único para leituras e gravações em qualquer lugar do mundo |
| Produtividade | Limite de 20.000 operações por tabela | 10 milhões operações por tabela |
| Distribuição Global | Região única com uma única região de leitura secundária opcional | Distribuições completas para todas as regiões com failover automático |
| Indexação | Disponível somente para propriedades de chave de partição e de linha | Indexação automática de todas as propriedades |
| Preços | Com base no armazenamento | Com base na taxa de transferência |

Os microserviços que consomem o armazenamento de tabelas do Azure podem migrar facilmente para o API de Tabela de Cosmos DB. Nenhuma alteração de código é necessária.

### <a name="tunable-consistency"></a>Consistência ajustável

Anteriormente, na seção *relacional vs. NoSQL* , discutimos o assunto da *consistência de dados*. A consistência dos dados refere-se à *integridade* dos seus dados. Os serviços nativos de nuvem com dados distribuídos dependem da replicação e devem tomar uma compensação fundamental entre consistência de leitura, disponibilidade e latência.

A maioria dos bancos de dados distribuídos permite que os desenvolvedores escolham entre dois modelos de consistência: consistência forte e consistência eventual. A *consistência forte* é o padrão ouro de programação de dados. Ele garante que uma consulta sempre retornará os dados mais atuais, mesmo que o sistema deva incorrer em latência aguardando que uma atualização seja replicada em todas as cópias de banco de dados. Enquanto um banco de dados configurado para *consistência eventual* retornará dados imediatamente, mesmo que esses dados não sejam a cópia mais atual. A última opção permite maior disponibilidade, maior escala e melhor desempenho.

O Azure Cosmos DB oferece cinco modelos de [consistência](/azure/cosmos-db/consistency-levels) bem definidos mostrados na Figura 5-13.

![Cosmos DB grafo de consistência](./media/cosmos-consistency-level-graph.png)

**Figura 5-13**: níveis de consistência de Cosmos DB

 Essas opções permitem que você faça opções precisas e compensações granulares para consistência, disponibilidade e desempenho para seus dados. Os níveis são apresentados na tabela a seguir.

| Nível de coerência | Descrição  |
| :-------- | :-------- |
| Eventual | Nenhuma garantia de classificação para leituras. Eventualmente, as réplicas convergirão. |
| Prefixo de constante | As leituras ainda são eventuales, mas os dados são retornados na ordenação em que são gravadas. |
| Session | Garante que você possa ler todos os dados gravados durante a sessão atual. É o nível de consistência padrão. |
| Desatualização limitada | Lê as gravações de trilha por intervalo que você especificar. |  
| Forte  | As leituras são garantidas para retornar a versão confirmada mais recente de um item. Um cliente nunca vê uma leitura não confirmada ou parcial. |  

No artigo que está nos [deparando com o 9-Ball: Cosmos DB níveis de consistência explicados](https://blog.jeremylikness.com/blog/2018-03-23_getting-behind-the-9ball-cosmosdb-consistency-levels/), o gerente de programas da Microsoft Jeremy Likness fornece uma excelente explicação dos cinco modelos.

### <a name="partitioning"></a>Particionamento

O Azure Cosmos DB adota o [particionamento](/azure/cosmos-db/partitioning-overview) automático para dimensionar um banco de dados para atender às necessidades de desempenho de seus serviços nativos de nuvem.

Você gerencia os dados em Cosmos DB dados criando, contêineres e bancos de dado.

Os contêineres residem em um banco de dados Cosmos DB e representam um agrupamento independente de esquema de itens. Os itens são os dados que você adiciona ao contêiner. Eles são representados como documentos, linhas, nós ou bordas. Todos os itens adicionados a um contêiner são indexados automaticamente.

Para particionar o contêiner, os itens são divididos em subconjuntos distintos chamados partições lógicas. As partições lógicas são preenchidas com base no valor de uma chave de partição associada a cada item em um contêiner. A Figura 5-14 mostra dois contêineres cada um com uma partição lógica com base em um valor de chave de partição.

![Mecânica de particionamento de Cosmos DB](./media/cosmos-db-partitioning.png)

**Figura 5-14**: Cosmos dB a mecânica de particionamento

Observe na figura anterior como cada item inclui uma chave de partição de ' City ' ou ' Airport '. A chave determina a partição lógica do item. Os itens com um código de cidade são atribuídos ao contêiner à esquerda e os itens com um código de aeroporto, para o contêiner à direita. A combinação do valor da chave de partição com o valor de ID cria um índice de item, que identifica exclusivamente o item.

Internamente, Cosmos DB gerencia automaticamente o posicionamento de [partições lógicas](/azure/cosmos-db/partition-data) em partições físicas para atender às necessidades de escalabilidade e desempenho do contêiner. À medida que os requisitos de armazenamento e de taxa de transferência do aplicativo aumentam, Azure Cosmos DB redistribui partições lógicas em um número maior de servidores. As operações de redistribuição são gerenciadas pelo Cosmos DB e invocadas sem interrupção ou tempo de inatividade.

## <a name="newsql-databases"></a>Bancos de dados NewSQL

O *NewSQL* é uma tecnologia de banco de dados emergente que combina a escalabilidade distribuída do NoSQL com as garantias acid de um banco de dados relacional. Os bancos de dados NewSQL são importantes para sistemas de negócios que devem processar altos volumes de data, em ambientes distribuídos, com suporte total transacional e conformidade com ACID. Enquanto um banco de dados NoSQL pode fornecer grande escalabilidade, ele não garante a consistência dos dados. Problemas intermitentes de dados inconsistentes podem fazer uma sobrecarga na equipe de desenvolvimento. Os desenvolvedores devem construir proteções em seu código de microserviço para gerenciar problemas causados por dados inconsistentes.

A CNCF (nuvem Native Computing Foundation) apresenta vários projetos de banco de dados NewSQL.

| Project | Características |
| :-------- | :-------- |
| Cockroach DB |Um banco de dados relacional compatível com ACID que é dimensionado globalmente. Adicionar um novo nó a um cluster e o CockroachDB cuida do balanceamento dos dados entre instâncias e geografias. Ele cria, gerencia e distribui réplicas para garantir a confiabilidade. Ele é de código-fonte aberto e disponível gratuitamente.  |
| TiDB | Um banco de dados de software livre que dá suporte a cargas de trabalho de processamento analítico e transacional híbrido (HTAP). Ele é compatível com MySQL e apresenta escalabilidade horizontal, consistência forte e alta disponibilidade.  TiDB atua como um servidor MySQL. Você pode continuar a usar bibliotecas de cliente MySQL existentes, sem a necessidade de alterações de código abrangentes em seu aplicativo. |
| YugabyteDB | Um banco de dados SQL distribuído de código aberto, de alto desempenho. Ele dá suporte à baixa latência de consulta, resiliência contra falhas e distribuição de dados global. YugabyteDB é compatível com PostgressSQL e manipula as cargas de trabalho OLTP de expansão e dimensionamento da Internet. O produto também dá suporte a NoSQL e é compatível com Cassandra. |
|Vitess | Vitess é uma solução de banco de dados para implantação, dimensionamento e gerenciamento de clusters grandes de instâncias do MySQL. Ele pode ser executado em uma arquitetura de nuvem pública ou privada. O Vitess combina e estende vários recursos importantes do MySQL e recursos que dão suporte a fragmentação vertical e horizontal. Originado pelo YouTube, o Vitess tem disponibilizado todo o tráfego de banco de dados do YouTube desde 2011. |

Os projetos de código-fonte aberto na figura anterior estão disponíveis na base computação nativa de nuvem. Três das ofertas são produtos de banco de dados completos, que incluem o suporte do .NET. O outro, Vitess, é um sistema de clustering de banco de dados que dimensiona horizontalmente grandes clusters de instâncias do MySQL.

Um dos principais objetivos de design dos bancos de dados NewSQL é trabalhar nativamente no kubernetes, aproveitando a resiliência e a escalabilidade da plataforma.

Os bancos de dados NewSQL são projetados para prosperar em ambientes de nuvem efêmeras em que as máquinas virtuais subjacentes podem ser reiniciadas ou reagendadas no momento do aviso. Os bancos de dados são projetados para sobreviver a falhas de nó sem perda de dados nem tempo de inatividade. CockroachDB, por exemplo, é capaz de sobreviver a uma perda de máquina mantendo três réplicas consistentes de quaisquer dados em todos os nós em um cluster.

O kubernetes usa uma *construção de serviços* para permitir que um cliente resolva um grupo de processos de bancos de dados NewSQL idênticos de uma única entrada DNS. Ao desacoplar as instâncias de banco de dados do endereço do serviço ao qual ele está associado, podemos dimensionar sem interromper as instâncias existentes do aplicativo. O envio de uma solicitação para qualquer serviço em um determinado momento sempre produzirá o mesmo resultado.

Nesse cenário, todas as instâncias de banco de dados são iguais. Não há relações primárias ou secundárias. Técnicas como a *replicação de consenso* encontradas em CockroachDB permitem que qualquer nó de banco de dados manipule qualquer solicitação. Se o nó que recebe uma solicitação de balanceamento de carga tiver os dados necessários localmente, ele responderá imediatamente. Caso contrário, o nó se tornará um gateway e encaminhará a solicitação para os nós apropriados para obter a resposta correta. Da perspectiva do cliente, cada nó de banco de dados é o mesmo: eles aparecem como um único banco de dados *lógico* com garantias de consistência de um sistema de máquina única, apesar de ter dezenas ou até mesmo centenas de nós que estão trabalhando nos bastidores.

Para obter uma visão detalhada da mecânica por trás dos bancos de dados do NewSQL, consulte o artigo [Dash: quatro propriedades do Kubernetes-Native bancos de dados](https://thenewstack.io/dash-four-properties-of-kubernetes-native-databases/) .

## <a name="data-migration-to-the-cloud"></a>Migração de dados para a nuvem

Uma das tarefas mais demoradas é migrar dados de uma plataforma de dados para outra. O [serviço de migração de dados do Azure](https://azure.microsoft.com/services/database-migration/) pode ajudar a agilizar esses esforços. Ele pode migrar dados de várias fontes de banco de dados externas para as plataformas do Azure data com tempo de inatividade mínimo. As plataformas de destino incluem os seguintes serviços:

- Banco de Dados SQL do Azure
- Banco de Dados do Azure para MySQL
- Banco de Dados do Azure para MariaDB
- Banco de Dados do Azure para PostgreSQL
- CosmosDB
  
O serviço fornece recomendações para orientá-lo pelas alterações necessárias para executar uma migração, pequena ou grande.

>[!div class="step-by-step"]
>[Anterior](distributed-data.md) 
> [Avançar](azure-caching.md)
