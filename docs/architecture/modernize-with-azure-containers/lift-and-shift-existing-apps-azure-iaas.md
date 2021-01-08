---
title: Migrar e deslocar aplicativos .NET existentes para IaaS do Azure (pronto para infraestrutura de nuvem)
description: Modernizar aplicativos .NET existentes com contêineres de nuvem e Windows do Azure.
ms.date: 12/21/2020
ms.openlocfilehash: fb875c38cac236826007bba217189238b7c00898
ms.sourcegitcommit: 5d9cee27d9ffe8f5670e5f663434511e81b8ac38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98025388"
---
# <a name="lift-and-shift-existing-net-apps-to-azure-iaas-cloud-infrastructure-ready"></a>Migrar e deslocar aplicativos .NET existentes para IaaS do Azure (pronto para infraestrutura de nuvem)

> Visão: como uma primeira etapa, para reduzir seu investimento local e o custo total de manutenção de hardware e rede, basta hospedar novamente os aplicativos existentes na nuvem.

Antes de entrar em *como* migrar seus aplicativos existentes para a plataforma IaaS (infraestrutura como serviço) do Azure, é importante analisar os motivos pelos *quais* você desejaria migrar diretamente para o IaaS no Azure. O cenário nesse nível de maturidade de modernização essencialmente é começar a usar VMs na nuvem, em vez de continuar a usar sua infraestrutura local atual.

Outro ponto a ser analisado é *por que* você pode desejar migrar para a nuvem de IaaS pura em vez de apenas adicionar serviços gerenciados avançados no Azure. Determine quais casos podem exigir IaaS em primeiro lugar.

A Figura 2-1 posiciona os aplicativos de Infrastructure-Ready de nuvem nos níveis de maturidade de modernização:

![Posicionando aplicativos Infrastructure-Ready de nuvem](./media/image2-1.png)

**Figura 2-1.** Posicionando aplicativos Infrastructure-Ready de nuvem

## <a name="why-migrate-existing-net-web-applications-to-azure-iaas"></a>Por que migrar aplicativos Web .NET existentes para IaaS do Azure

O principal motivo para migrar para a nuvem, mesmo em um nível de IaaS inicial, é obter reduções de custo. Com o uso de serviços de infraestrutura mais gerenciados, sua organização pode reduzir seu investimento em manutenção de hardware, provisionamento e implantação de servidor ou VM e gerenciamento de infraestrutura.

Depois de tomar a decisão de mover seus aplicativos para a nuvem, o principal motivo pelo qual você pode escolher IaaS em vez de opções mais avançadas, como PaaS, é simplesmente que o ambiente de IaaS será mais familiar. Mover para um ambiente semelhante ao seu ambiente local atual oferece uma curva de aprendizado mais baixa, o que o torna o caminho mais rápido para a nuvem.

No entanto, usar o caminho mais rápido para a nuvem não significa que você obterá mais benefícios em ter seus aplicativos em execução na nuvem. Qualquer organização obterá os benefícios mais significativos de uma migração de nuvem nos níveis de maturidade já introduzidos Cloud-Optimized e Cloud-Native.

Também se tornou evidente que os aplicativos são mais fáceis de modernizar e rearquitetar no futuro quando já estão em execução na nuvem, mesmo no IaaS. A migração de dados de aplicativos já foi atingida. Além disso, sua organização terá adquirido as habilidades necessárias para trabalhar na nuvem e fazer a mudança para operar em uma "cultura de nuvem".

## <a name="when-to-migrate-to-iaas-instead-of-to-paas"></a>Quando migrar para IaaS em vez de para PaaS

As próximas seções discutem Cloud-Optimized aplicativos que são basicamente baseados em plataformas e serviços de PaaS. Esses aplicativos oferecem a você a maior vantagem de migrar para a nuvem.

Se sua meta é simplesmente mover os aplicativos existentes para a nuvem, primeiro, identifique os aplicativos existentes que não exigem modificação substancial para serem executados no serviço de Azure App. Esses aplicativos devem ser os primeiros candidatos para a otimização da nuvem.

Em seguida, para os aplicativos que ainda não podem ser movidos para contêineres do Windows e PaaS, como serviço de aplicativo ou orquestradores, como o serviço kubernetes do Azure, migre esses aplicativos para IaaS (Simple simples VMs).

Mas lembre-se de que configurar, proteger e manter corretamente as VMs requer muito mais tempo e experiência de ti em comparação com o uso de serviços de PaaS no Azure. Se você estiver considerando as máquinas virtuais do Azure, certifique-se de levar em conta o esforço de manutenção em andamento necessário para corrigir, atualizar e gerenciar seu ambiente de VM. As máquinas virtuais do Azure são IaaS.

## <a name="use-azure-migrate-to-analyze-and-migrate-your-existing-applications-to-azure"></a>Usar as migrações para Azure para analisar e migrar seus aplicativos existentes para o Azure

A migração para a nuvem não precisa ser difícil. Mas muitas organizações lutam para começar-a obter uma visibilidade profunda do ambiente e as forte interdependências entre aplicativos, cargas de trabalho e dados. Sem essa visibilidade, pode ser difícil planejar o caminho para a frente. Sem informações detalhadas sobre o que é necessário para uma migração bem-sucedida, você não pode ter as conversas certas em sua organização. Você não sabe o suficiente sobre os benefícios de custo potencial ou se as cargas de trabalho poderiam apenas ser comparadas e trocadas ou exigiriam um retrabalho significativo para migrar com êxito. Não se perguntou que muitas organizações hesitam.

As [migrações para Azure](https://aka.ms/azuremigrate) são um novo serviço que fornece as diretrizes, as informações e os mecanismos necessários para ajudá-lo a migrar para o Azure. As Migrações para Azure fornecem:

- Descoberta e avaliação para máquinas virtuais locais

- Mapeamento de dependências embutidas para a descoberta de alta confiança de aplicativos de várias camadas

- Dimensionamento de direito inteligente para máquinas virtuais do Azure

- Relatórios de compatibilidade com diretrizes para correção de possíveis problemas

- Integração ao serviço de gerenciamento de banco de dados do Azure para migração e descoberta de banco de dados

As migrações para Azure dão a você confiança de que suas cargas de trabalho podem migrar com impacto mínimo sobre os negócios e são executados conforme o esperado no Azure. Com as ferramentas e as diretrizes certas, você pode obter o máximo de retorno sobre o investimento, garantindo que as necessidades críticas de desempenho e confiabilidade sejam atendidas.

A Figura 2-2 mostra o mapeamento de dependência interno para todas as conexões de servidor e aplicativo executadas pelas migrações para Azure.

![Posicionando aplicativos Infrastructure-Ready de nuvem](./media/image2-2.png)

**Figura 2-2.** Posicionando aplicativos Infrastructure-Ready de nuvem

## <a name="use-azure-site-recovery-to-migrate-your-existing-vms-to-azure-vms"></a>Usar Azure Site Recovery para migrar suas VMs existentes para VMs do Azure

Como parte da migração de ponta a ponta [do Azure](https://aka.ms/azuremigrate), [Azure site Recovery](/azure/site-recovery/site-recovery-overview) é uma ferramenta que você pode usar para migrar facilmente seus aplicativos Web para VMs no Azure. Você pode usar Site Recovery para replicar VMs locais e servidores físicos para o Azure ou para replicá-los para um local secundário localmente. Você pode até mesmo replicar uma carga de trabalho que está sendo executada em uma VM do Azure com suporte, em uma VM do *Hyper-V* local, em uma VM do *VMware* ou em um servidor físico Windows ou Linux. A replicação no Azure elimina o custo e a complexidade de manter um data center secundário.

O Site Recovery também é feito especificamente para ambientes híbridos que são parcialmente locais e parcialmente no Azure. Site Recovery ajuda a garantir a continuidade dos negócios, mantendo seus aplicativos em execução em VMs e servidores físicos locais disponíveis se um site ficar inativo. Ele Replica cargas de trabalho em execução em VMs e servidores físicos para que permaneçam disponíveis em um local secundário se o site primário não estiver disponível. Ele recupera as cargas de trabalho para o site primário quando ele está ativo e em execução novamente.

A Figura 2-3 mostra a execução de várias migrações de VM usando Azure Site Recovery.

![Posicionando aplicativos Infrastructure-Ready de nuvem](./media/image2-3.png)

**Figura 2-3.** Posicionando aplicativos Infrastructure-Ready de nuvem

### <a name="additional-resources"></a>Recursos adicionais

- **Folha de tabela de migrações para Azure**

    <https://aka.ms/azuremigration\_datasheet>

- **Migrações para Azure**

    <https://aka.ms/azuremigrate>

- **Central de migrações do Azure**

    <https://azure.microsoft.com/migration/>

- **Migrar para o Azure com Site Recovery**

    <https://docs.microsoft.com/azure/site-recovery/site-recovery-migrate-to-azure>

- **Visão geral do serviço de Azure Site Recovery**

    <https://docs.microsoft.com/azure/site-recovery/site-recovery-overview>

- **Migrando VMs no AWS para VMs do Azure**

    <https://docs.microsoft.com/azure/site-recovery/site-recovery-migrate-aws-to-azure>

>[!div class="step-by-step"]
>[Anterior](index.md) 
> [Avançar](migrate-your-relational-databases-to-azure.md) <!-- Next Chapter -->
