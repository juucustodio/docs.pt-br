---
title: Considerações sobre migração
description: O que uma equipe precisa saber para tomar a decisão certa sobre se e como migrar do ASP.NET MVC para o .NET Core?
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 4ae64b928b5fef75fcb16c33fb1a3a42013480cf
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488483"
---
# <a name="migration-considerations"></a>Considerações sobre migração

As equipes de perguntas mais básicas devem responder quando se trata de portar seus aplicativos para o .NET Core, elas devem ser portadas? Em alguns casos, o melhor caminho para avançar é permanecer em .NET Framework usando o MVC e/ou a API da Web do ASP.NET. Este capítulo considera os motivos pelos quais a mudança para o .NET Core faz sentido. O capítulo também considera cenários e pontos de extremidade para permanecer em .NET Framework.

## <a name="is-migration-to-net-core-appropriate"></a>A migração para o .NET Core é apropriada?

Vamos começar com alguns dos motivos pelos quais você talvez queira migrar para o .NET Core. Há alguns, portanto, não considere esta lista exaustiva.

### <a name="cross-platform-support"></a>Suporte de multiplaforma

Os aplicativos criados no .NET Core são verdadeiramente entre plataformas e podem ser executados no Windows, no Linux e no macOS. Os desenvolvedores não só podem usar qualquer hardware que desejarem, mas você também pode hospedar seu aplicativo em qualquer lugar. Os exemplos variam de IIS local para o Azure na nuvem ou de contêineres do Docker do Linux para dispositivos IoT.

### <a name="performance-and-scalability"></a>Desempenho e escala

Os aplicativos criados com o .NET Core estão sendo executados em [uma das pilhas Tech mais rápidas disponíveis em qualquer lugar](https://www.techempower.com/benchmarks/#hw=ph&test=plaintext). Os aplicativos ASP.NET MVC geralmente veem melhorias de desempenho no ASP.NET Core, especialmente se eles forem atualizados para aproveitar alguns novos recursos disponíveis no .NET Core.

### <a name="cloud-native"></a>Nativo da nuvem

Pelas razões acima e outras, os aplicativos .NET Core são adequados para a execução em ambientes de Hospedagem de nuvem. Aplicativos .NET Core simples e leves podem ser implantados em Azure App serviços ou contêineres e dimensionados horizontalmente conforme necessário para atender à demanda imediata do sistema.

### <a name="maintainable"></a>Passível

Para muitos aplicativos, enquanto eles continuaram atendendo às necessidades de clientes e negócios, a dívida técnica se acumulou e a manutenção do aplicativo cresceu caro. ASP.NET Core aplicativos são mais facilmente testados do que os aplicativos ASP.NET MVC, tornando-os mais fáceis de Refatorar e estender com confiança.

### <a name="modular"></a>Modular

ASP.NET Core é modular, usando pacotes NuGet como uma parte de primeira classe da estrutura. Os aplicativos criados para o .NET Core oferecem suporte à injeção de dependência, facilitando a composição de soluções de quaisquer implementações necessárias para um determinado ambiente. A criação de microserviços com o .NET Core é mais fácil do que com o ASP.NET MVC com sua dependência no IIS, que abre opções adicionais para dividir aplicativos grandes em módulos menores.

### <a name="modern"></a>Moderna

Permanecer em uma pilha de tecnologia moderna e ativamente desenvolvida tem uma série de vantagens. Novos recursos e recursos da linguagem C# serão adicionados somente ao .NET Core. A .NET Framework teve sua última versão com a versão 4,8, e versões do C# além de 8 não serão direcionadas .NET Framework. Embora o ASP.NET MVC permaneça compatível com a Microsoft por muitos anos, os melhores e mais brilhantes desenvolvedores de software .NET provavelmente estão procurando usar o .NET Core Framework mais moderno, com todas as vantagens oferecidas (apenas algumas das quais são resumidas acima). Encontrar desenvolvedores com as habilidades para manter um aplicativo ASP.NET MVC começará a se tornar um desafio em algum momento, assim como encontrará assistência online sobre treinamento e solução de problemas. Provavelmente, não há muitas novas postagens de blog sendo escritas sobre o ASP.NET MVC 5, enquanto há muitas escritas para o .NET 5,0, por exemplo.

Há muitos motivos convincentes a serem considerados na migração para o .NET Core, o que supostamente é por isso que você está lendo este livro! Mas vamos considerar algumas desvantagens e motivos pelos quais é possível fazer mais sentido permanecer no .NET Framework.

## <a name="when-is-net-framework-appropriate"></a>Quando o é .NET Framework apropriado?

O maior motivo para permanecer em .NET Framework é quando um aplicativo não está em desenvolvimento ativo e não se beneficia substancialmente das vantagens listadas acima. Nesse caso, provavelmente não há um bom caso de negócios para incorrer no custo de portar o aplicativo. Se seu aplicativo puder se beneficiar das vantagens das ofertas do .NET Core, talvez você ainda precise permanecer em .NET Framework se precisar de determinadas tecnologias que não estejam disponíveis no .NET Core. Há algumas [tecnologias .NET que não estão disponíveis no .NET Core](https://docs.microsoft.com/dotnet/core/porting/net-framework-tech-unavailable), incluindo AppDomains, comunicação remota, CAS (segurança de acesso a código), transparência de segurança e `System.EnterpriseServices` . Um breve resumo dessas tecnologias e suas alternativas estão incluídas aqui. Para obter diretrizes mais detalhadas, consulte a documentação.

### <a name="application-domains"></a>Domínios de aplicativo

Os domínios do aplicativo (AppDomains) isolam os aplicativos uns dos outros. Os AppDomains exigem suporte a tempo de execução e podem ser caros. Não há suporte para a criação de domínios de aplicativo adicionais, e não há planos para adicionar esse recurso ao .NET Core no futuro. Para o isolamento de código, use processos ou contêineres separados como alternativa.

### <a name="wcf"></a>WCF

O WCF do lado do servidor não tem suporte no .NET Core. O .NET Core dá suporte a clientes WCF, mas não a hosts WCF. Os aplicativos que exigem essa funcionalidade precisarão atualizar para uma tecnologia de comunicação diferente (como gRPC ou REST) como parte de uma migração.

Há uma [porta de cliente WCF disponível no .net Foundation](https://docs.microsoft.com/dotnet/core/dotnet-five#windows-communication-foundation). Ele é totalmente de software livre, de plataforma cruzada e tem suporte da Microsoft. Há também um [projeto CoreWCF](https://github.com/CoreWCF/CoreWCF) com suporte da Comunidade que *não* é oficialmente suportado pela Microsoft.

### <a name="remoting"></a>Comunicação remota

A Comunicação Remota do .NET foi identificada como uma arquitetura problemática. Ela é usada para comunicação entre AppDomains, o que não tem mais suporte. Além disso, a Comunicação Remota exige suporte de runtime, o que é caro para manter. Por esses motivos, o .NET Remoting não tem suporte no .NET Core e a equipe de produto não planeja adicionar suporte para ele no futuro. Há várias estratégias alternativas de mensagens e implementações que você pode usar para substituir a comunicação remota em seus aplicativos .NET Core.

### <a name="code-access-security-cas-and-security-transparency"></a>Segurança de acesso a código (CAS) e transparência de segurança

Nenhuma dessas tecnologias tem suporte do .NET Core. Em vez disso, a recomendação é usar limites de segurança fornecidos pelo sistema operacional. Por exemplo, virtualização, contêineres ou contas de usuário. Execute processos com o conjunto mínimo de privilégios necessário.

## <a name="references"></a>Referências

[.NET Framework tecnologias não disponíveis no .NET Core](https://docs.microsoft.com/dotnet/core/porting/net-framework-tech-unavailable)

>[!div class="step-by-step"]
>[Anterior](introduction.md) 
> [Avançar](migrate-aspnet-core-2-1.md)
