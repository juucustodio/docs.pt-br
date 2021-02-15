---
title: Escolher entre o .NET 5 e o .NET Framework para aplicativos de servidor
description: Um guia para ajudá-lo a decidir qual implementação do .NET usar ao criar um aplicativo de servidor.
author: cartermp
ms.date: 10/06/2020
ms.openlocfilehash: d9dce0343f9d37e976472b818e896a5b0a661e76
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160445"
---
# <a name="net-5-vs-net-framework-for-server-apps"></a>.NET 5 versus .NET Framework para aplicativos de servidor

Há duas implementações de .NET com suporte para a criação de aplicativos do lado do servidor: .NET Framework e .NET 5 (incluindo o .NET Core). Ambas compartilham muitos dos mesmos componentes e você pode compartilhar código entre as duas. No entanto, há diferenças fundamentais entre as duas e sua escolha depende do que você deseja realizar. Este artigo diretrizes sobre quando usar cada um.

Use o .NET 5 para o aplicativo de servidor quando:

- Você tiver necessidades de plataforma cruzada.
- Você está direcionando para os microserviços.
- Você está usando contêineres do Docker.
- Você precisar de alto desempenho e sistemas escalonáveis.
- Você precisar de versões do .NET correspondentes a cada aplicativo.

Use o .NET Framework para o aplicativo para servidores se:

- Seu aplicativo usar o .NET Framework atualmente (a recomendação é estender em vez de migrar).
- Seu aplicativo usa bibliotecas .NET de terceiros ou pacotes NuGet não disponíveis para o .NET 5.
- Seu aplicativo usa tecnologias .NET que não estão disponíveis para o .NET 5.
- Seu aplicativo usa uma plataforma que não dá suporte ao .NET 5.

## <a name="when-to-choose-net-5"></a>Quando escolher o .NET 5

As seções a seguir fornecem uma explicação mais detalhada dos motivos descritos anteriormente para escolher o .NET 5.

### <a name="cross-platform-needs"></a>Necessidades de plataforma cruzada

Se seu aplicativo (Web/serviço) precisar ser executado em várias plataformas (Windows, Linux e macOS), use o .NET 5.

O .NET 5 dá suporte aos sistemas operacionais mencionados anteriormente como sua estação de trabalho de desenvolvimento. O Visual Studio fornece um IDE (ambiente de desenvolvimento integrado) para Windows e macOS. Você também pode usar o Visual Studio Code, que é executado no Windows, Linux e macOS. O Visual Studio Code dá suporte ao .NET 5, incluindo IntelliSense e depuração. A maioria dos editores de terceiros, como sublime, Emacs e VI, funciona com o .NET 5. Esses editores de terceiros obtém o IntelliSense do editor usando o [Omnisharp](https://www.omnisharp.net/). Você também pode evitar qualquer editor de código e usar diretamente o [CLI do .NET Core](../core/tools/index.md), disponível para todas as plataformas com suporte.

### <a name="microservices-architecture"></a>Arquitetura de microsserviços

Uma arquitetura de microsserviços possibilita uma combinação de tecnologias em um limite de serviço. Essa combinação de tecnologia permite uma adoção gradual do .NET 5 para novos microserviços que funcionam com outros microserviços ou serviços. Por exemplo, você pode combinar microsserviços ou serviços desenvolvidos com .NET Framework, Java, Ruby ou outras tecnologias monolíticas.

Há muitas plataformas de infraestrutura disponíveis. O [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) é criado para sistemas de microsserviço grandes e complexos. O [Serviço de Aplicativo do Azure](https://azure.microsoft.com/services/app-service/) é uma boa escolha para microsserviços sem monitoração de estado. Alternativas de microsserviços baseadas em Docker se adaptam a qualquer tipo de abordagem de microsserviços, conforme explicado na seção [Contêineres](#containers). Todas essas plataformas dão suporte ao .NET 5 e as tornam ideais para hospedar seus microserviços.

Para obter mais informações sobre a arquitetura de microserviços, consulte [microservices do .net. Arquitetura para aplicativos .NET em contêineres](../architecture/microservices/index.md).

### <a name="containers"></a>Contêineres

Os contêineres são frequentemente usados em conjunto com uma arquitetura de microsserviços. Os contêineres também podem ser usados para colocar em contêiner os aplicativos ou serviços Web que seguem qualquer padrão de arquitetura. .NET Framework pode ser usado em contêineres do Windows, mas a modularidade e a natureza leve do .NET 5 o tornam uma opção melhor para contêineres. Ao criar e implantar um contêiner, o tamanho de sua imagem é muito menor com o .NET 5 do que com .NET Framework. Como ele é multiplataforma, é possível implantar aplicativos para servidores em contêineres do Docker do Linux, por exemplo.

Os contêineres do Docker podem ser hospedados em sua própria infraestrutura do Windows ou do Linux ou em um serviço de nuvem, como o [Serviço de Kubernetes do Azure](https://azure.microsoft.com/services/kubernetes-service/). O Serviço de Kubernetes do Azure pode gerenciar, orquestrar e dimensionar aplicativos baseados em contêiner na nuvem.

### <a name="high-performance-and-scalable-systems"></a>Sistemas escalonáveis e de alto desempenho

Quando o sistema precisa do melhor desempenho e escalabilidade possíveis, o .NET 5 e o ASP.NET Core são as melhores opções. O runtime do servidor de alto desempenho para Windows Server e Linux tornam o .NET uma estrutura da Web de desempenho superior nas [avaliações da TechEmpower](https://www.techempower.com/benchmarks/#hw=ph&test=plaintext).

O desempenho e a escalabilidade são especialmente relevantes para arquiteturas de microsserviços, nas quais centenas de microsserviços podem estar em execução. Com o ASP.NET Core, os sistemas são executados com um número bem menor de servidores/VMs (Máquinas Virtuais). A redução em servidores/VMs gera economia em infraestrutura e hospedagem.

### <a name="side-by-side-net-versions-per-application-level"></a>Versões do .NET lado a lado por nível de aplicativo

Para instalar aplicativos com dependências em diferentes versões do .NET, recomendamos o .NET 5. O .NET 5 dá suporte à instalação lado a lado de versões diferentes do tempo de execução do .NET 5 no mesmo computador. Essa instalação lado a lado permite vários serviços no mesmo servidor, cada um deles em sua própria versão do .NET 5 (ou no .NET Core 2,1 ou 3,1). Ela também reduz os riscos e gera economia financeira nas operações de TI e atualizações de aplicativo.

A instalação lado a lado não é possível com .NET Framework. É um componente do Windows, e apenas uma versão pode existir em um computador de cada vez. Cada versão do .NET Framework substitui a versão anterior. Se você instalar um novo aplicativo direcionado a uma versão mais recente do .NET Framework, poderá interromper os aplicativos existentes que são executados no computador, pois a versão anterior foi substituída.

## <a name="when-to-choose-net-framework"></a>Quando escolher o .NET Framework

O .NET 5 oferece benefícios significativos para novos aplicativos e padrões de aplicativos. No entanto, .NET Framework continua sendo a escolha natural para muitos cenários existentes e, dessa forma, .NET Framework não é substituído pelo .NET 5 para todos os aplicativos de servidor.

### <a name="current-net-framework-applications"></a>Aplicativos .NET Framework atuais

Na maioria dos casos, você não precisa migrar seus aplicativos existentes para o .NET 5. Em vez disso, uma abordagem recomendada é usar o .NET 5 à medida que você estende um aplicativo existente, como escrever um novo serviço Web no ASP.NET Core.

### <a name="third-party-libraries-or-nuget-packages-not-available-for-net-5"></a>Bibliotecas de terceiros ou pacotes NuGet não disponíveis para o .NET 5

O .NET Standard permite o compartilhamento de código em todas as implementações do .NET, incluindo o .NET 5. Com o .NET Standard 2,0, um modo de compatibilidade permite que os projetos .NET Standard e .NET 5 façam referência a bibliotecas .NET Framework. Para obter mais informações, consulte [suporte para bibliotecas de .NET Framework](whats-new/whats-new-in-dotnet-standard.md#support-for-net-framework-libraries).

Você precisa usar .NET Framework apenas nos casos em que as bibliotecas ou os pacotes NuGet usam tecnologias que não estão disponíveis no .NET Standard ou no .NET 5.

### <a name="net-technologies-not-available-for-net-5"></a>Tecnologias .NET não disponíveis para o .NET 5

Algumas tecnologias .NET Framework não estão disponíveis no .NET 5. A lista a seguir mostra as tecnologias mais comuns não encontradas no .NET 5:

- ASP.NET Web Forms aplicativos: ASP.NET Web Forms estão disponíveis apenas no .NET Framework. O ASP.NET Core não pode ser usado para Web Forms do ASP.NET.

- Aplicativos de páginas da Web do ASP.NET: as páginas da Web do ASP.NET não estão incluídas no ASP.NET Core.

- Implementação de serviços do WCF. Mesmo quando há uma [biblioteca de cliente WCF](https://github.com/dotnet/wcf) para consumir serviços do WCF do .NET 5, a implementação do servidor WCF está disponível atualmente apenas no .NET Framework.

- Serviços relacionados a fluxo de trabalho: Windows Workflow Foundation (WF), serviços de fluxo de trabalho (WCF + WF em um único serviço) e WCF Data Services (anteriormente conhecidos como "serviços de dados ADO.NET") estão disponíveis somente no .NET Framework.

- Suporte a idiomas: atualmente, Visual Basic e F # têm suporte no .NET 5, mas não em todos os tipos de projeto. Para obter uma lista de modelos de projeto com suporte, consulte [Opções de modelo para o dotnet new](../core/tools/dotnet-new.md#arguments).

Para obter mais informações, consulte [.NET Framework Technologies indisponível no .NET 5](../core/porting/net-framework-tech-unavailable.md).

### <a name="platform-doesnt-support-net-5"></a>A plataforma não dá suporte ao .NET 5

Algumas plataformas da Microsoft ou de terceiros não oferecem suporte ao .NET 5. Alguns serviços do Azure fornecem um SDK que ainda não está disponível para consumo no .NET 5. Nesses casos, você pode usar a API REST equivalente em vez do SDK do cliente.

## <a name="see-also"></a>Veja também

- [Escolher entre o ASP.NET e o ASP.NET Core](/aspnet/core/choose-aspnet-framework)
- [ASP.NET Core direcionado para o .NET Framework](/aspnet/core/introduction-to-aspnet-core?view=aspnetcore-2.2&preserve-view=true#aspnet-core-targeting-net-framework)
- [Estruturas de destino](frameworks.md)
- [Introdução ao .NET](../core/introduction.md)
- [Portando de .NET Framework para o .NET 5](../core/porting/index.md)
- [Introdução ao .NET e ao Docker](../core/docker/introduction.md)
- [Visão Geral dos Componentes do .NET](components.md)
- [Microserviços .NET. Arquitetura para aplicativos .NET em contêineres](../architecture/microservices/index.md)
