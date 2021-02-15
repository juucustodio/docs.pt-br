---
title: Resiliência da plataforma Azure
description: Arquitetando aplicativos .NET nativos da nuvem para o Azure | Resiliência de infraestrutura de nuvem com o Azure
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: 88634bc60df15cc93b1769a85879795ae383757a
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91163759"
---
# <a name="azure-platform-resiliency"></a>Resiliência da plataforma Azure

Criar um aplicativo confiável na nuvem é diferente do desenvolvimento de aplicativos local tradicional. Embora historicamente você adquiriu um hardware de extremidade superior para escalar verticalmente, em um ambiente de nuvem, você escala horizontalmente. Em vez de tentar evitar falhas, o objetivo é minimizar seus efeitos e manter o sistema estável.

Dito isso, os aplicativos de nuvem confiáveis exibem características distintas:

- Eles são resilientes, recuperam-se normalmente de problemas e continuam a funcionar.
- Eles são altamente disponíveis (HA) e são executados conforme projetados em um estado íntegro sem tempo de inatividade significativo.

Entender como essas características funcionam em conjunto e como elas afetam o custo-é essencial para a criação de um aplicativo de nuvem confiável. Em seguida, veremos como você pode criar resiliência e disponibilidade em seus aplicativos nativos de nuvem aproveitando os recursos da nuvem do Azure.

## <a name="design-with-resiliency"></a>Design com resiliência

Dissemos que a resiliência permite que seu aplicativo reaja a uma falha e ainda permaneça funcional. O White Paper, [resiliência no Azure White Paper](https://azure.microsoft.com/mediahandler/files/resourcefiles/resilience-in-azure-whitepaper/Resilience%20in%20Azure.pdf), fornece orientação para obter resiliência na plataforma Azure. Aqui estão algumas recomendações importantes:

- *Falha de hardware.* Crie redundância no aplicativo implantando componentes em diferentes domínios de falha. Por exemplo, verifique se as VMs do Azure são colocadas em diferentes racks usando conjuntos de disponibilidade.

- *Falha no datacenter.* Crie redundância no aplicativo com zonas de isolamento de falhas em data centers. Por exemplo, verifique se as VMs do Azure são colocadas em diferentes data centers isolados de falhas usando Zonas de Disponibilidade do Azure.

- *Falha regional.* Replique os dados e componentes em outra região para que os aplicativos possam ser recuperados rapidamente. Por exemplo, use Azure Site Recovery para replicar VMs do Azure para outra região do Azure.

- *Carga pesada.* Balancear a carga entre instâncias para lidar com picos de uso. Por exemplo, coloque duas ou mais VMs do Azure atrás de um balanceador de carga para distribuir o tráfego para todas as VMs.

- *Exclusão ou corrupção acidental de dados.* Faça backup dos dados para que eles possam ser restaurados se houver alguma exclusão ou corrupção. Por exemplo, use o backup do Azure para fazer backup de suas VMs do Azure periodicamente.

## <a name="design-with-redundancy"></a>Design com redundância

As falhas variam no escopo do impacto. Uma falha de hardware, como um disco com falha, pode afetar um único nó em um cluster. Um comutador de rede com falha pode afetar um rack de servidor inteiro. Falhas menos comuns, como perda de energia, podem interromper um datacenter inteiro. Raramente, uma região inteira fica indisponível.

A [redundância](/azure/architecture/guide/design-principles/redundancy) é uma maneira de fornecer resiliência do aplicativo. O nível exato de redundância necessário depende de seus requisitos de negócios e afetará o custo e a complexidade do seu sistema. Por exemplo, uma implantação de várias regiões é mais cara e mais complexa para ser gerenciada do que uma implantação de região única. Você precisará de procedimentos operacionais para gerenciar failover e failback. O custo adicional e a complexidade podem ser justificados para alguns cenários de negócios, mas não para outros.

Para arquitetar a redundância, você precisa identificar os caminhos críticos em seu aplicativo e, em seguida, determinar se há redundância em cada ponto do caminho? Se um subsistema falhar, o aplicativo fará failover para outra coisa? Por fim, você precisa de uma compreensão clara desses recursos incorporados à plataforma de nuvem do Azure que você pode aproveitar para atender aos seus requisitos de redundância. Aqui estão as recomendações para a arquitetura da redundância:

- *Implante várias instâncias de serviços.* Se seu aplicativo depender de uma única instância de um serviço, ele criará um único ponto de falha. O provisionamento de várias instâncias melhora a resiliência e a escalabilidade. Ao hospedar no serviço kubernetes do Azure, você pode configurar declarativamente instâncias redundantes (conjuntos de réplicas) no arquivo de manifesto kubernetes. O valor da contagem de réplicas pode ser gerenciado programaticamente, no portal ou por meio de recursos de dimensionamento automático.

- *Aproveitando um balanceador de carga.* O balanceamento de carga distribui as solicitações do aplicativo para instâncias de serviço íntegra e remove automaticamente instâncias não íntegras da rotação. Ao implantar no kubernetes, o balanceamento de carga pode ser especificado no arquivo de manifesto kubernetes na seção serviços.

- *Planejar a implantação em multiregião.* Se você implantar seu aplicativo em uma única região e essa região ficar indisponível, seu aplicativo também ficará indisponível. Isso pode ser inaceitável nos termos dos contratos de nível de serviço de seu aplicativo. Em vez disso, considere implantar seu aplicativo e seus serviços em várias regiões. Por exemplo, um cluster AKS (serviço de kubernetes do Azure) é implantado em uma única região. Para proteger seu sistema de uma falha regional, você pode implantar seu aplicativo em vários clusters AKS em regiões diferentes e usar o recurso de [regiões emparelhadas](https://buildazure.com/2017/01/06/azure-region-pairs-explained/) para coordenar as atualizações da plataforma e priorizar os esforços de recuperação.

- *Habilite [a replicação geográfica](/azure/sql-database/sql-database-active-geo-replication).* A replicação geográfica para serviços, como o banco de dados SQL do Azure e o Cosmos DB criará réplicas secundárias de sua data em várias regiões. Embora os dois serviços repliquem automaticamente os dados na mesma região, a replicação geográfica protege você contra uma interrupção regional, permitindo o failover para uma região secundária. Outra prática recomendada para os centros de replicação geográfica em relação ao armazenamento de imagens de contêiner. Para implantar um serviço no AKS, você precisa armazenar e efetuar pull da imagem de um repositório. O registro de contêiner do Azure integra-se com o AKS e pode armazenar imagens de contêiner com segurança. Para melhorar o desempenho e a disponibilidade, considere a replicação geográfica de suas imagens para um registro em cada região em que você tenha um cluster AKS. Cada cluster AKS, em seguida, efetua pull das imagens de contêiner do registro de contêiner local em sua região, conforme mostrado na Figura 6-4:

![Recursos replicados entre regiões](./media/replicated-resources.png)

**Figura 6-4**. Recursos replicados entre regiões

- *Implemente um balanceador de carga de tráfego DNS.* O [Gerenciador de tráfego do Azure](/azure/traffic-manager/traffic-manager-overview) fornece alta disponibilidade para aplicativos críticos pelo balanceamento de carga no nível do DNS. Ele pode rotear o tráfego para diferentes regiões com base na geografia, no tempo de resposta do cluster e até mesmo na integridade do ponto de extremidade do aplicativo. Por exemplo, o Gerenciador de tráfego do Azure pode direcionar os clientes para a instância de aplicativo e cluster AKS mais próxima. Se você tiver vários clusters AKS em regiões diferentes, use o Gerenciador de tráfego para controlar como o tráfego flui para os aplicativos que são executados em cada cluster. A Figura 6-5 mostra esse cenário.

![AKS e Gerenciador de tráfego do Azure](./media/aks-traffic-manager.png)

**Figura 6-5**. AKS e Gerenciador de tráfego do Azure

## <a name="design-for-scalability"></a>Design para escalabilidade

A nuvem prospera no dimensionamento. A capacidade de aumentar/diminuir os recursos do sistema para lidar com a carga crescente/decrescente do sistema é um princípio fundamental da nuvem do Azure. Mas, para dimensionar um aplicativo com eficiência, você precisa compreender os recursos de dimensionamento de cada serviço do Azure que você inclui em seu aplicativo.  Aqui estão recomendações para implementar efetivamente o dimensionamento em seu sistema.

- *Design para dimensionamento.* Um aplicativo deve ser projetado para dimensionamento. Para iniciar, os serviços devem ser sem estado para que as solicitações possam ser roteadas para qualquer instância. Ter serviços sem estado também significa que a adição ou remoção de uma instância não afeta negativamente os usuários atuais.

- *Cargas de trabalho de partição*. A decomposição de domínios em microserviços independentes e autônomos permite que cada serviço seja dimensionado de forma independente dos outros. Normalmente, os serviços terão necessidades e requisitos de escalabilidade diferentes. O particionamento permite que você dimensione apenas o que precisa ser dimensionado sem o custo desnecessário de dimensionamento de um aplicativo inteiro.

- *Favorecer a expansão.* Os aplicativos baseados em nuvem favorecem a expansão dos recursos em oposição ao dimensionamento. A expansão (também conhecida como escala horizontal) envolve a adição de mais recursos de serviço a um sistema existente para atender e compartilhar um nível de desempenho desejado. O dimensionamento (também conhecido como dimensionamento vertical) envolve a substituição de recursos existentes por hardware mais potente (mais núcleos de disco, memória e processamento). A expansão pode ser invocada automaticamente com os recursos de dimensionamento automático disponíveis em alguns recursos de nuvem do Azure. Escalar horizontalmente em vários recursos também adiciona redundância ao sistema geral. Por fim, a expansão de um único recurso é normalmente mais cara do que escalar horizontalmente em muitos recursos menores. A Figura 6-6 mostra as duas abordagens:

![Escalar verticalmente versus escalar horizontalmente](./media/scale-up-scale-out.png)

**Figura 6-6.** Escalar verticalmente versus escalar horizontalmente

- *Dimensionar proporcionalmente.* Ao dimensionar um serviço, considere em termos de *conjuntos de recursos*. Se você fosse expandir drasticamente um serviço específico, que impacto teria em armazenamentos de dados de back-end, em caches e serviços dependentes? Alguns recursos, como Cosmos DB, podem ser expandidos proporcionalmente, enquanto muitos outros não podem. Você deseja garantir que não expanda um recurso para um ponto em que ele esgotará outros recursos associados.

- *Evite a afinidade.* Uma prática recomendada é garantir que um nó não exija afinidade local, geralmente chamado de *sessão adesiva*. Uma solicitação deve ser capaz de rotear para qualquer instância. Se você precisar manter o estado, ele deve ser salvo em um cache distribuído, como o [cache Redis do Azure](https://azure.microsoft.com/services/cache/).

- *Aproveite os recursos de dimensionamento automático da plataforma.* Use recursos internos de dimensionamento automático sempre que possível, em vez de mecanismos personalizados ou de terceiros. Sempre que possível, use regras de dimensionamento agendadas para garantir que os recursos estejam disponíveis sem um atraso de inicialização, mas adicione o dimensionamento automático reativo às regras conforme apropriado, para lidar com alterações inesperadas na demanda. Para obter mais informações, consulte [diretrizes de dimensionamento](/azure/architecture/best-practices/auto-scaling)automático.

- *Expanda agressivamente.* Uma prática final seria escalar horizontalmente de forma agressiva para que você possa atender rapidamente a picos imediatos de tráfego sem perder negócios. E, em seguida, reduzir (ou seja, remover instâncias desnecessárias) de forma conservadora para manter o sistema estável. Uma maneira simples de implementar isso é definir o período de resfriamento, que é o tempo de espera entre as operações de dimensionamento, cinco minutos para adicionar recursos e até 15 minutos para remover instâncias.

## <a name="built-in-retry-in-services"></a>Repetição interna em serviços

Incentivamos a prática recomendada de implementar operações de repetição programáticas em uma seção anterior. Tenha em mente que muitos serviços do Azure e seus SDKs de cliente correspondentes também incluem mecanismos de repetição. A lista a seguir resume os recursos de repetição nos muitos dos serviços do Azure que são discutidos neste livro:

- *Azure Cosmos DB.* A <xref:Microsoft.Azure.Documents.Client.DocumentClient> classe da API do cliente desativa automaticamente as tentativas com falha. O número de repetições e o tempo de espera máximo são configuráveis. As exceções geradas pela API do cliente são solicitações que excedem a política de repetição ou erros não transitórios.

- *Cache Redis do Azure.* O cliente Redis StackExchange usa uma classe de Gerenciador de conexões que inclui novas tentativas em tentativas com falha. O número de repetições, a política de repetição específica e o tempo de espera são todos configuráveis.

- *Barramento de serviço do Azure.* O cliente do barramento de serviço expõe uma [classe RetryPolicy](xref:Microsoft.ServiceBus.RetryPolicy) que pode ser configurada com um intervalo de retirada, contagem de repetição e <xref:Microsoft.ServiceBus.RetryExponential.TerminationTimeBuffer%2A> , que especifica o tempo máximo que uma operação pode tomar. A política padrão é de nove tentativas de repetição máximas com um período de retirada de 30 segundos entre as tentativas.

- *Banco de Dados SQL do Azure.* O suporte de repetição é fornecido ao usar a biblioteca de [Entity Framework Core](/ef/core/miscellaneous/connection-resiliency) .

- *Armazenamento do Azure.* A biblioteca de cliente de armazenamento dá suporte a operações de repetição. As estratégias variam em tabelas de armazenamento do Azure, BLOBs e filas. Assim, as repetições alternativas alternam entre locais de serviços de armazenamento primários e secundários quando o recurso de redundância geográfica está habilitado.

- *Hubs de eventos do Azure.* A biblioteca de cliente do hub de eventos apresenta uma propriedade RetryPolicy, que inclui um recurso de retirada exponencial configurável.

>[!div class="step-by-step"]
>[Anterior](application-resiliency-patterns.md) 
> [Avançar](resilient-communications.md)
