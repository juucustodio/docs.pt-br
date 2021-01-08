---
title: Implantar aplicativos .NET existentes como contêineres do Windows
description: Modernizar aplicativos .NET existentes com contêineres de nuvem e Windows do Azure | Implantar aplicativos .NET existentes como contêineres do Windows
ms.date: 12/21/2020
ms.openlocfilehash: f3f164ca0578d5358f2c5365fd5a1d2e8e22d8c5
ms.sourcegitcommit: 5d9cee27d9ffe8f5670e5f663434511e81b8ac38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98025337"
---
# <a name="deploy-existing-net-apps-as-windows-containers"></a>Implantar aplicativos .NET existentes como contêineres do Windows

As implantações baseadas em contêineres do Windows são aplicáveis a aplicativos Cloud-Optimized e Cloud-Native aplicativos.

No entanto, neste guia e especialmente nas seções a seguir, ele se concentra principalmente no uso de contêineres do Windows para aplicativos *otimizados para a nuvem* , nos quais você não precisa rearquitetar seu aplicativo.

## <a name="what-are-containers-linux-or-windows"></a>O que são contêineres? (Linux ou Windows)

Os contêineres são uma maneira de encapsular um aplicativo em seu próprio pacote isolado. Em seu contêiner, o aplicativo não é afetado por aplicativos ou processos que existem fora do contêiner. Tudo o que o aplicativo depende para ser executado com êxito como um processo está dentro do contêiner. Sempre que o contêiner puder ser movido, os requisitos do aplicativo serão sempre atendidos, em termos de dependências diretas, porque são agrupados com tudo o que precisa ser executado (dependências de biblioteca, tempos de execução e assim por diante).

A principal característica de um contêiner é que ele torna o ambiente o mesmo em implantações diferentes porque o próprio contêiner vem com todas as dependências necessárias. Você pode depurar o aplicativo em seu computador e implantá-lo em outra máquina, com o mesmo ambiente garantido.

Um contêiner é uma instância de uma imagem de contêiner. Uma imagem de contêiner é uma maneira de empacotar um aplicativo ou serviço (como um instantâneo) e, em seguida, implantá-lo de forma confiável e reproduzível. Você poderia dizer que o Docker não é apenas uma tecnologia – ele também é uma filosofia e um processo.

Como os contêineres diariamente se tornam mais comuns, eles estão se tornando uma "unidade de implantação" de todo o setor.

## <a name="benefits-of-containers-docker-engine-on-linux-or-windows"></a>Benefícios dos contêineres (mecanismo do Docker no Linux ou Windows)

Criando aplicativos usando contêineres – que também podem ser definidos como blocos de construção leves – oferece um aumento significativo na agilidade para a criação, o envio e a execução de qualquer aplicativo, em qualquer infraestrutura.

Com contêineres, você pode levar qualquer aplicativo de desenvolvimento para produção com pouca ou nenhuma alteração de código, graças à integração do Docker entre as ferramentas de desenvolvedor da Microsoft, os sistemas operacionais e a nuvem.

Quando você implanta em VMs simples, provavelmente já tem um método em vigor para implantar aplicativos ASP.NET em suas VMs. No entanto, é provável que seu método envolva várias etapas manuais ou processos automatizados complexos usando uma ferramenta de implantação como Puppet ou uma ferramenta semelhante. Talvez seja necessário executar tarefas como modificar itens de configuração, copiar o conteúdo do aplicativo entre servidores e executar programas de instalação interativa com base em configurações. msi, seguidos de testes. Todas essas etapas na implantação adicionam tempo e risco às implantações. Você receberá falhas sempre que uma dependência não estiver presente no ambiente de destino.

Em contêineres do Windows, o processo de empacotamento de aplicativos é totalmente automatizado. Os contêineres do Windows baseiam-se na plataforma do Docker, que oferece atualizações automáticas e reversões para implantações de contêiner. A melhoria principal obtida com o uso do mecanismo do Docker é que você cria imagens, que são como instantâneos do seu aplicativo, com todas as suas dependências. As imagens são imagens do Docker (uma imagem de contêiner do Windows, neste caso). As imagens executam aplicativos ASP.NET em contêineres, sem voltar ao código-fonte. O instantâneo do contêiner se torna a unidade de implantação.

Muitas organizações estão disparando aplicativos monolíticos existentes pelos seguintes motivos:

- **Libere a agilidade por meio da implantação aprimorada**. Os contêineres oferecem um contrato de implantação consistente entre desenvolvimento e operações. Ao usar contêineres, você não ouvirá os desenvolvedores a dizer, "ele funciona no meu computador, por que não em produção?" Eles podem dizer, "ele é executado como um contêiner, portanto, ele será executado na produção". O aplicativo empacotado, com todas as suas dependências, pode ser executado em qualquer ambiente baseado em contêiner com suporte. Ele será executado da maneira como se destina a ser executado em todos os destinos de implantação (dev, QA, preparo, produção). Os contêineres eliminam a maioria dos conflitos quando passam de um estágio para o outro, o que melhora muito a implantação e você pode enviar mais rapidamente.

- **Reduções de custo**. Os contêineres levam a custos reduzidos, seja pela consolidação e remoção de hardware existente ou pela execução de aplicativos em uma densidade maior por unidade de hardware.

- **Portabilidade**. Os contêineres são modulares e portáteis. Os contêineres do Docker têm suporte em qualquer sistema operacional de servidor (Linux e Windows), em qualquer nuvem pública principal (Microsoft Azure, Amazon AWS, Google, IBM) e em ambientes de nuvem local e privada ou híbrida.

- **Controle**. Os contêineres oferecem um ambiente seguro e flexível que é controlado no nível de contêiner. Um contêiner pode ser protegido, isolado e até mesmo limitado definindo políticas de restrição de execução no contêiner. Conforme detalhado na seção sobre contêineres do Windows, os contêineres do Windows Server 2016 e do Hyper-V oferecem opções adicionais de suporte empresarial.

Melhorias significativas na agilidade, portabilidade e controle, por fim, levam a reduções de custo significativas quando você usa contêineres para desenvolver e manter aplicativos.

## <a name="what-is-docker"></a>O que é o Docker?

O [Docker](https://www.docker.com/) é um [projeto de código-fonte aberto](https://github.com/docker/docker) que automatiza a implantação de aplicativos como contêineres portáteis e autônomos que podem ser executados na nuvem ou localmente. O Docker é também um [empresa](https://www.docker.com/) que promove e evolui essa tecnologia. A empresa trabalha em colaboração com fornecedores de nuvem, Linux e Windows, incluindo a Microsoft.

![Diagrama mostrando como o Docker implanta contêineres na nuvem híbrida.](./media/deploy-existing-net-apps-as-windows-containers/docker-deploys-containers-all-layers.png)

**Figura 4-6.** O Docker implanta contêineres em todas as camadas da nuvem híbrida

Para alguém familiarizado com máquinas virtuais, os contêineres podem parecer ser notavelmente semelhantes. Um contêiner executa um sistema operacional, tem um sistema de arquivos e pode ser acessado através de uma rede, assim como um sistema de computador físico ou virtual. No entanto, a tecnologia e os conceitos por trás dos contêineres são muito diferentes das máquinas virtuais. Do ponto de vista de um desenvolvedor, um contêiner deve ser tratado mais como um único processo. Na verdade, um contêiner tem um único ponto de entrada para um processo.

Os contêineres do Docker (para simplificar, *contêineres*) podem ser executados nativamente no Linux e no Windows. Ao executar contêineres regulares, os contêineres do Windows podem ser executados somente em hosts do Windows (um servidor host ou uma VM) e os contêineres do Linux podem ser executados somente em hosts Linux. No entanto, em versões recentes do Windows Server e contêineres do Hyper-V, um contêiner do Linux também pode ser executado nativamente no Windows Server usando a tecnologia de isolamento do Hyper-V que atualmente está disponível somente em contêineres do Windows Server.

Em breve, ambientes mistos que têm contêineres Linux e Windows serão possíveis e até mesmo comuns.

## <a name="benefits-of-windows-containers-for-your-existing-net-applications"></a>Benefícios dos contêineres do Windows para seus aplicativos .NET existentes

Os benefícios de usar contêineres do Windows são fundamentalmente os mesmos benefícios obtidos de contêineres em geral. O uso de contêineres do Windows é a melhoria significativa da agilidade, da portabilidade e do controle.

Os aplicativos .NET existentes referem-se aos aplicativos que foram criados usando o .NET Framework. Por exemplo, eles podem ser aplicativos Web ASP.NETs tradicionais-eles não usam .NET Core ou .NET 5,0, que é mais recente e executa a plataforma cruzada em Linux, Windows e MacOS.

A principal dependência na .NET Framework é o Windows. Ele também tem dependências secundárias, como IIS e System. Web no ASP.NET tradicional.

Um aplicativo .NET Framework deve ser executado no Windows, período. Se você quiser colocar os aplicativos .NET Framework em contêineres existentes e não desejar ou não quer investir em uma migração para o .NET Core ou posterior ("se ele funcionar corretamente, não migrá-lo"), a única opção que você tem para contêineres é usar contêineres do Windows.

Portanto, um dos principais benefícios dos contêineres do Windows é que eles oferecem uma maneira de modernizar seus aplicativos .NET Framework existentes que estão sendo executados no Windows por meio de contêinerização. Por fim, os contêineres do Windows obtêm os benefícios que você está procurando usando os contêineres – agilidade, portabilidade e melhor controle.

## <a name="choose-an-os-to-target-with-net-based-containers"></a>Escolha um sistema operacional com o qual se destina. Contêineres baseados em rede

Considerando a diversidade de sistemas operacionais com suporte pelo Docker, bem como as diferenças entre o .NET Framework e o .NET Core, você deve direcionar um sistema operacional específico e versões específicas com base na estrutura que você está usando.

Para o Windows, é possível usar o Windows Server Core ou o Windows Nano Server. Essas versões do Windows fornecem características diferentes (como o IIS versus um servidor Web autohospedado, como Kestrel), que podem ser necessárias para aplicativos .NET Framework ou .NET.

Para Linux, várias distribuições estão disponíveis e há compatibilidade com elas nas imagens oficiais do .NET Docker (como Debian).

A Figura 4-7 mostra as versões do sistema operacional que você pode direcionar, dependendo da versão do aplicativo do .NET Framework.

![Diagrama que mostra o sistema operacional a ser direcionado com base na versão .NET Framework.](./media/deploy-existing-net-apps-as-windows-containers/dotnet-framework-operating-systems.png)

**Figura 4-7.** Sistemas operacionais a serem direcionados com base na versão .NET Framework

Em cenários de migração para aplicativos existentes ou herdados baseados em aplicativos .NET Framework, as principais dependências estão no Windows e no IIS. Sua única opção é usar imagens do Docker com base no Windows Server Core e no .NET Framework.

Ao adicionar o nome da imagem ao arquivo Dockerfile, você pode selecionar o sistema operacional e a versão usando uma marca, como nos exemplos a seguir para as imagens de contêiner do Windows baseadas em .NET Framework:

> | **Tag** | **Sistema e versão** |
> |---|---|
> | **mcr.microsoft.com/dotnet/framework/runtime:4.x-windowsservercore-20H2** | .NET Framework 4. x no Windows Server Core |
> | **mcr.microsoft.com/dotnet/framework/aspnet:4.x-windowsservercore-20H2** | .NET Framework 4. x com personalização ASP.NET adicional, no Windows Server Core |

Para .NET (multiplataforma para Linux e Windows), as marcas se parecerão com o seguinte:

> | **Tag** | **Sistema e versão**
> |---|---|
> | **mcr.microsoft.com/dotnet/runtime:5.0** | Tempo de execução do .NET somente no Linux |
> | **mcr.microsoft.com/dotnet/runtime:5.0-nanoserver-20H2** | Tempo de execução do .NET somente no Windows nano Server |

### <a name="multi-arch-images"></a>Imagens de vários arcos

A partir de meados de 2017, você também pode usar um novo recurso no Docker chamado imagens de [vários arcos](https://github.com/moby/moby/issues/15866) . As imagens do Docker .NET podem usar marcas de várias arcos. Os arquivos Dockerfile não precisam mais definir o sistema operacional que você está direcionando. O recurso de vários arcos permite que uma única marca seja usada em várias configurações de computador. Por exemplo, com vários arcos, você pode usar uma marca comum: **MCR.Microsoft.com/dotnet/Runtime:5.0**. Se você efetuar pull dessa marca de um ambiente de contêiner do Linux, obterá a imagem baseada em Debian. Se você efetuar pull dessa marca de um ambiente de contêiner do Windows, obterá a imagem baseada no nano Server.

Para .NET Framework imagens, como o .NET Framework tradicional dá suporte apenas ao Windows, você não pode usar o recurso de várias arcos.

## <a name="windows-container-types"></a>Tipos de contêiner do Windows

Assim como os contêineres do Linux, os contêineres do Windows Server são gerenciados usando o mecanismo do Docker. Ao contrário dos contêineres do Linux, os contêineres do Windows incluem dois tipos diferentes de contêineres ou tempos de execução – contêineres do Windows Server e isolamento do Hyper-V.

**Contêineres do Windows Server**: fornece isolamento de aplicativo por meio da tecnologia de isolamento de processo e namespace. Um contêiner do Windows Server compartilha um kernel com o host do contêiner e todos os contêineres que estão em execução no host. Esses contêineres não fornecem um limite de segurança hostil e não devem ser usados para isolar código não confiável. Devido ao espaço de kernel compartilhado, esses contêineres exigem a mesma versão e configuração de kernel.

**Isolamento do Hyper-V**: expande o isolamento fornecido pelos contêineres do Windows Server executando cada contêiner em uma VM altamente otimizada. Nessa configuração, o kernel do host do contêiner não é compartilhado com outros contêineres no mesmo host. Esses contêineres são projetados para hospedagem multilocatário hostil, com as mesmas garantias de segurança de uma VM. Como esses contêineres não compartilham o kernel com o host ou outros contêineres no host, eles podem executar kernels com diferentes versões e configurações (com versões com suporte). Por exemplo, todos os contêineres do Windows no Windows 10 usam o isolamento do Hyper-V para utilizar a versão e a configuração do kernel do Windows Server.

Executar um contêiner no Windows com ou sem o isolamento do Hyper-V é uma decisão em tempo de execução. Você pode optar por criar o contêiner com o isolamento do Hyper-V inicialmente e, em tempo de execução, optar por executá-lo como um contêiner do Windows Server em vez disso.

### <a name="additional-resources"></a>Recursos adicionais

- **Documentação de contêineres do Windows**

    <https://docs.microsoft.com/virtualization/windowscontainers/>

- **Conceitos básicos de contêineres do Windows**

    <https://docs.microsoft.com/virtualization/windowscontainers/about/>

- **Infográfico: Microsoft e contêineres**

    <https://info.microsoft.com/rs/157-GQE-382/images/Container%20infographic%201.4.17.pdf>

## <a name="the-container-ecosystem-in-azure"></a>O ecossistema do contêiner no Azure

Nas seções anteriores, foi explicado quais são os benefícios dos contêineres do Docker, bem como detalhes sobre as imagens de contêiner específicas para aplicativos .NET. Todas essas informações genéricas são fundamentais para desenvolver ou colocar um aplicativo em contêiner.
No entanto, ao pensar no ambiente de implantação de produção ou até mesmo em ambientes de QA e desenvolvimento/teste, Microsoft Azure fornece uma ampla variedade de opções, um ecossistema de contêiner completo na nuvem (mostrado no diagrama abaixo). Dependendo das necessidades específicas do seu aplicativo, você deve escolher um ou outro produto do Azure.

![Diagrama do ecossistema do contêiner no Azure.](./media/deploy-existing-net-apps-as-windows-containers/azure-container-ecosystem.png)

**Figura 4-7.5.** O ecossistema do contêiner no Azure

No ecossistema do contêiner no Azure, os seguintes produtos dão suporte a contêineres que são considerados infraestrutura:

- **ACI (Instâncias de Contêiner do Azure)**
- **Máquinas virtuais do Azure** (com suporte do contêiner)
- **Conjuntos de dimensionamento de máquinas virtuais do Azure** (com suporte do contêiner)

Dentre essas três, o ACI fornece um grande benefício, que é o fato de que você não precisa manter o sistema operacional subjacente, sem necessidade de atualização/patch, etc., mas o ACI ainda está posicionado no nível de infraestrutura, conforme melhor explicado nas próximas seções deste livro.

Os produtos nos contêineres de suporte do Azure que estão ao mesmo tempo posicionados mais no nível de PaaS (plataforma como serviço) são:

- **Serviço de Aplicativo do Azure**
- **Serviço kubernetes do Azure (AKS e ACS)**
- **Lote do Azure**

Em seguida, o registro de contêiner do Azure é um registro de contêiner altamente escalonável hospedado no Azure que você pode usar de todos os produtos anteriores ao registrar e implantar suas imagens de contêiner personalizadas.

Além disso, de seus contêineres, você pode consumir outros serviços gerenciados no Azure, como o banco de dados SQL do Azure, o cache Redis do Azure, o Azure Cosmos DB, etc. Além disso, há soluções/plataformas de terceiros disponíveis no Azure Marketplace, como Cloud Foundry e OpenShift, em que você também pode usar contêineres no Azure.

Nas próximas seções, você pode explorar as recomendações da Microsoft sobre quando usar cada um desses produtos e soluções do Azure especificamente ao direcionar contêineres do Windows.

>[!div class="step-by-step"]
>[Anterior](what-about-cloud-native-applications.md) 
> [Avançar](when-not-to-deploy-to-windows-containers.md)
