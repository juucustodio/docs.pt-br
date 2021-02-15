---
title: Migrar seus bancos de dados relacionais para o Azure
description: Modernizar aplicativos .NET existentes com contêineres de nuvem e Windows do Azure | migrar seus bancos de dados relacionais para o Azure
ms.date: 12/21/2020
ms.openlocfilehash: c8dc92e1c5c5fb36a68bcad000c10e47c946ca0c
ms.sourcegitcommit: 5d9cee27d9ffe8f5670e5f663434511e81b8ac38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98025375"
---
# <a name="migrate-your-relational-databases-to-azure"></a>Migrar seus bancos de dados relacionais para o Azure

Visão: o Azure oferece a migração de banco de dados mais abrangente.

No Azure, você pode migrar seus servidores de banco de dados diretamente para VMs de IaaS (extração e deslocamento puro) ou pode migrar para o banco de dados SQL do Azure para obter benefícios adicionais. O banco de dados SQL do Azure oferece a instância gerenciada e opções completas de DBaaS (banco de dados como serviço). A Figura 3-1 mostra os vários caminhos de migração de banco de dados relacional disponíveis no Azure.

![Caminhos de migração de banco de dados no Azure](./media/image3-1.png)

**Figura 3-1.** Caminhos de migração de banco de dados no Azure

## <a name="when-to-migrate-to-azure-sql-database-managed-instance"></a>Quando migrar para o Instância Gerenciada do Banco de Dados SQL do Azure

Na maioria dos casos, Instância Gerenciada do Banco de Dados SQL do Azure será a melhor opção a ser considerada quando você migrar seus dados para o Azure. Se você estiver migrando bancos de dados SQL Server e precisar de quase 100% de garantia de que não precisará rearquitetar seu aplicativo ou fazer alterações em seu código de dados ou de acesso a dados, escolha o recurso Instância Gerenciada do Azure SQL Database.

Instância Gerenciada do Banco de Dados SQL do Azure é a melhor opção se você tiver requisitos adicionais para SQL Server funcionalidade em nível de instância ou requisitos de isolamento além dos recursos fornecidos em um banco de dados SQL do Azure padrão (modelo de banco de dados único). Essa última é a opção mais orientada a PaaS, mas não oferece os mesmos recursos que os de um SQL Server tradicional. A migração pode trazer os conflitos.

Por exemplo, uma organização que tenha feito investimentos profundos em recursos de SQL Server em nível de instância se beneficiaria da migração para o SQL Instância Gerenciada. Exemplos de recursos de SQL Server no nível de instância incluem integração do SQL Common Language Runtime (CLR), SQL Server Agent e consulta entre bancos de dados. O suporte para esses recursos não está disponível no banco de dados SQL do Azure padrão (um modelo de banco de dados único).

Uma organização que opera em um setor altamente regulamentado e que precisa manter o isolamento para fins de segurança também pode se beneficiar da escolha do modelo de Instância Gerenciada do SQL.

Instância Gerenciada no banco de dados SQL do Azure tem as seguintes características:

- Isolamento de segurança por meio da rede virtual do Azure

- Compatibilidade de superfície de aplicativo, com estes recursos:

  - SQL Server Agent e SQL Server Profiler

  - Referências e consultas entre bancos de dados, SQL CLR, replicação, captura de dados de alterações (CDC) e Service Broker

- Tamanhos de banco de dados de até 35 TB

- Migração de tempo de inatividade mínimo, com estes recursos:

  - Serviço de Migração de Banco de Dados do Azure

  - Backup e restauração nativos e envio de logs

Com esses recursos, quando você migra bancos de dados de aplicativos existentes para o banco de dados SQL do Azure, o modelo de Instância Gerenciada oferece quase 100% dos benefícios do PaaS para SQL Server. Instância Gerenciada é um ambiente de SQL Server em que você continua usando recursos em nível de instância sem alterar o design do aplicativo.

Instância Gerenciada é provavelmente a melhor opção para as empresas que estão usando SQL Server e que exigem flexibilidade em sua segurança de rede na nuvem. É como ter uma rede virtual privada para seus bancos de dados SQL.

## <a name="when-to-migrate-to-azure-sql-database"></a>Quando migrar para o banco de dados SQL do Azure

Conforme mencionado, o banco de dados SQL do Azure padrão é um DBaaS relacional totalmente gerenciado. No momento, o banco de dados SQL gerencia milhões de bancos de dados de produção em 38 data centers, em todo o mundo. Ele dá suporte a uma ampla variedade de aplicativos e cargas de trabalho, desde o gerenciamento de dados transacionais simples até a maioria dos aplicativos críticos de dados e de missão crítica que exigem processamento de dados avançado em escala global.

Devido a seus recursos completos de PaaS, melhor preço-e, por fim, custo mais baixo – você deve mudar para o banco de dados SQL do Azure padrão como sua "opção por padrão" se você tiver um aplicativo que usa bancos de dados SQL básicos, padrão e nenhum recurso de instância adicional. SQL Server recursos como integração do SQL CLR, SQL Server Agent e consultas entre bancos de dados não têm suporte no banco de dados SQL do Azure padrão. Esses recursos estão disponíveis apenas no modelo de Instância Gerenciada do Banco de Dados SQL do Azure.

O banco de dados SQL do Azure é o único serviço de banco de dados de nuvem inteligente criado para desenvolvedores de aplicativos. Ele também é o único serviço de banco de dados de nuvem que é dimensionado dinamicamente, sem tempo de inatividade, para ajudá-lo a fornecer aplicativos multilocatários com eficiência. Por fim, o banco de dados SQL do Azure deixa mais tempo para inovar e acelera seu tempo de colocação no mercado. Você pode criar aplicativos seguros e conectar-se ao banco de dados SQL usando os idiomas e as plataformas que preferir.

O banco de dados SQL do Azure oferece os seguintes benefícios:

- Inteligência interna (aprendizado de máquina) que aprende e se adapta ao seu aplicativo

- Provisionamento de banco de dados sob demanda

- Uma variedade de ofertas, para todas as cargas de trabalho

- 99,99% de SLA de disponibilidade, manutenção zero

- Replicação geográfica e serviços de restauração para proteção de dados

- Recurso de restauração pontual do banco de dados SQL do Azure

- Compatibilidade com o SQL Server 2016, incluindo híbrido e migração

O banco de dados SQL do Azure padrão está mais próximo de PaaS do que Instância Gerenciada do Banco de Dados SQL do Azure. Prefira o banco de dados SQL do Azure padrão, pois você obterá mais benefícios de uma nuvem gerenciada. No entanto, o banco de dados SQL do Azure tem algumas diferenças importantes de instâncias de SQL Server normais e locais. Dependendo dos requisitos de banco de dados do aplicativo existente e de suas políticas e requisitos empresariais, talvez não seja a melhor opção quando você estiver planejando a migração para a nuvem.

## <a name="when-to-move-your-original-rdbms-to-a-vm-iaas"></a>Quando mover seu RDBMS original para uma VM (IaaS)

Uma das suas opções de migração é mover seu RDBMS (sistema de gerenciamento de banco de dados relacional) original, incluindo Oracle, IBM DB2, MySQL, PostgreSQL ou SQL Server, para um servidor semelhante em execução em uma VM do Azure. Se você tiver aplicativos existentes que exigem a migração mais rápida para a nuvem com alterações mínimas ou nenhuma alteração, uma migração direta para IaaS na nuvem pode ser uma opção justa. Talvez não seja a melhor maneira de aproveitar todos os benefícios da nuvem, mas é provavelmente o caminho inicial mais rápido.

Atualmente, Microsoft Azure dá suporte a até [331 servidores de banco de dados diferentes](https://azuremarketplace.microsoft.com/marketplace/apps/category/databases?page=1&subcategories=databases-all) implantados como VMs IaaS. Isso inclui RDBMS popular como SQL Server, Oracle, MySQL, PostgreSQL e IBM DB2 e muitos outros bancos de dados NoSQL, como MongoDB, Cassandra, DataStax, MariaDB e Cloudera.

> [!NOTE]
> Embora mover seu RDBMS para uma VM do Azure possa ser a maneira mais rápida de migrar seus dados para a nuvem (porque ele é IaaS), essa abordagem requer um investimento significativo em suas equipes de ti (administradores de banco de dados e profissionais de ti). As equipes empresariais precisam ser capazes de configurar e gerenciar alta disponibilidade, recuperação de desastre e aplicação de patches para SQL Server. Esse contexto também precisa de um ambiente personalizado, com direitos administrativos completos.

## <a name="when-to-migrate-to-sql-server-as-a-vm-iaas"></a>Quando migrar para SQL Server como uma VM (IaaS)

Pode haver alguns casos em que você ainda precisa migrar para SQL Server como uma VM regular. Um cenário de exemplo é se você precisar usar SQL Server Reporting Services. No entanto, na maioria dos casos, Instância Gerenciada do Banco de Dados SQL do Azure pode fornecer tudo o que você precisa para migrar de servidores SQL locais, de modo que a migração para uma VM SQL Server deve ser o último recurso a ser tentada.

## <a name="use-azure-database-migration-service-to-migrate-your-relational-databases-to-azure"></a>Usar o serviço de migração de banco de dados do Azure para migrar seus bancos dados relacionais para o Azure

Você pode usar o serviço de migração de banco de dados do Azure para migrar bancos de dados relacionais como SQL Server, Oracle e MySQL para o Azure, se o banco de dados de destino é um banco de dados SQL do Azure, Instância Gerenciada do Banco de Dados SQL do Azure ou SQL Server em uma VM do Azure.

O fluxo de trabalho automatizado, com o relatório de avaliação, orienta você pelas alterações que você precisa fazer antes de migrar o banco de dados. Quando você estiver pronto, o serviço migrará o banco de dados de origem para o Azure.

Sempre que você alterar um RDBMS original, talvez seja necessário testar novamente. Você também pode precisar alterar o código de Object-Relational de frases SQL ou de mapeamento (ORM) em seu aplicativo, dependendo dos resultados do teste.

Se você tiver qualquer outro banco de dados (por exemplo, IBM DB2) e optar por uma abordagem de comparação de precisão e deslocamento, convém continuar usando esses bancos de dados como VMs de IaaS no Azure, a menos que você esteja disposto a realizar uma migração mais complexa. Uma migração de dados mais complexa exigirá esforço adicional, pois você estaria migrando para um tipo de banco de dado diferente com o novo esquema e diferentes bibliotecas de programação.

Para saber como migrar bancos de dados usando o Azure Database Migration Service, consulte [obter a nuvem mais rápido com o instância gerenciada do banco de dados SQL do Azure e o serviço de migração de banco de dados do Azure](https://channel9.msdn.com/Events/Build/2017/P4008).

## <a name="additional-resources"></a>Recursos adicionais

- **Escolha uma opção de SQL Server de nuvem: banco de dados SQL do Azure (PaaS) ou SQL Server na VM do Azure (IaaS)**

    <https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas>

- **Acesse a nuvem mais rápido com o Azure SQL DB Instância Gerenciada e o serviço de migração de banco de dados**

    <https://channel9.msdn.com/Events/Build/2017/P4008>

- **Migração de banco de dados do SQL Server para o Banco de Dados SQL na nuvem**

    <https://docs.microsoft.com/azure/sql-database/sql-database-cloud-migrate>

- **Banco de Dados SQL do Azure**

    <https://azure.microsoft.com/services/sql-database/?v=16.50>

- **SQL Server em máquinas virtuais**

    <https://azure.microsoft.com/services/virtual-machines/sql-server/>

> [!div class="step-by-step"]
> [Anterior](lift-and-shift-existing-apps-azure-iaas.md) 
>  [Avançar](modernize-existing-apps-to-cloud-optimized/index.md) <!-- Next Chapter -->
