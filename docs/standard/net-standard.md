---
title: .NET Standard
description: Saiba mais sobre .NET Standard, suas versões e as implementações do .NET que dão suporte a ela.
ms.date: 10/05/2020
ms.prod: dotnet
ms.technology: dotnet-standard
ms.custom: updateeachrelease
ms.assetid: c044882c-af15-45f2-96d1-534557a5ee9b
ms.openlocfilehash: 93fb10538441d939e95bb48dcdd0e61d9267dde0
ms.sourcegitcommit: c0b803bffaf101e12f071faf94ca21b46d04ff30
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/24/2020
ms.locfileid: "97765027"
---
# <a name="net-standard"></a>.NET Standard

[.Net Standard](https://github.com/dotnet/standard) é uma especificação formal das APIs do .NET que estão disponíveis em várias implementações do .net. A motivação por trás da .NET Standard era estabelecer uma maior uniformidade no ecossistema do .NET. No entanto, o .NET 5 adota uma abordagem diferente para estabelecer a uniformidade, e essa nova abordagem elimina a necessidade de .NET Standard em muitos cenários. Para obter mais informações, consulte [.NET 5 e .net Standard](#net-5-and-net-standard) mais adiante neste artigo.

## <a name="net-implementation-support"></a>Suporte à implementação do .NET

As diversas implementações do .NET se destinam a versões específicas do .NET Standard. Cada versão de implementação do .NET anuncia a versão mais alta do .NET Standard a qual ela dá suporte, uma afirmação que significa que também há suporte para versões anteriores. Por exemplo, .NET Framework 4,6 implementa .NET Standard 1,3, o que significa que ele expõe todas as APIs definidas em .NET Standard versões 1,0 a 1,3. Da mesma forma, .NET Framework 4.6.1 implementa .NET Standard 1,4, enquanto o .NET 5,0 implementa .NET Standard 2,1.

A tabela a seguir lista as versões **mínimas** de implementação que oferecem suporte a cada versão de .net Standard. Isso significa que as versões posteriores de uma implementação listada também oferecem suporte à versão de .NET Standard correspondente. Por exemplo, o .NET Core 2,1 e versões posteriores dão suporte a .NET Standard 2,0 e versões anteriores.

[!INCLUDE [net-standard-table](../../includes/net-standard-table.md)]

Para localizar a versão mais recente do .NET Standard para a qual você pode direcionar, siga estas etapas:

1. Localize a linha que indica a implementação do .NET na qual você deseja executar.
1. Localize a coluna nessa linha que indica sua versão, da direita para a esquerda.
1. O cabeçalho da coluna indica a versão do .NET Standard compatível com o destino. Você também pode ter como destino qualquer versão inferior do .NET Standard. Versões superiores do .NET Standard também darão suporte à implementação.
1. Repita esse processo para cada plataforma de destino. Se você tiver mais de uma plataforma de destino, escolha a versão menos recente entre elas. Por exemplo, se você deseja executar o .NET Framework 4,8 e o .NET 5,0, a versão mais alta .NET Standard que você pode usar é .NET Standard 2,0.

### <a name="which-net-standard-version-to-target"></a>Para qual versão do .NET Standard direcionar

Ao escolher uma versão de .NET Standard para o destino, considere essa compensação:

- Quanto mais alta a versão, mais APIs estarão disponíveis para o código da biblioteca.
- Quanto menor a versão, mais aplicativos e bibliotecas podem usar sua biblioteca.

Recomendamos que você direcione a versão *mais baixa* do .net Standard possível. Portanto, depois de localizar a versão mais recente do .NET Standard para a qual você pode direcionar, execute estas etapas:

1. Direcione para a próxima versão menos recente do .NET Standard e compile seu projeto.
2. Se seu projeto for compilado com êxito, repita a etapa 1. Caso contrário, redirecione para a próxima versão mais recente, e essa será a versão que você deve usar.

No entanto, ter como destino versões do .NET Standard inferiores introduz diversas dependências de suporte. Se o projeto for destinado ao .NET Standard 1.x, recomendamos que você *também* tenha como destino o .NET Standard 2.0. Isso simplifica o grafo de dependência para os usuários da sua biblioteca que são executados em implementações compatíveis com .NET Standard 2,0 e reduz o número de pacotes que precisam ser baixados.

### <a name="net-standard-versioning-rules"></a>Regras de controle de versão do .NET Standard

Há duas regras principais de controle de versão:

- Aditivo: as versões do .NET Standard são círculos logicamente concêntricos: versões mais recentes incorporam todas as APIs das versões anteriores. Não há alterações interruptivas entre as versões.
- Imutável: após o envio, as versões do .NET Standard serão congeladas.

Não haverá nenhuma nova versão do .NET Standard após 2,1. Para obter mais informações, consulte [.NET 5 e .net Standard](#net-5-and-net-standard) mais adiante neste artigo.

## <a name="specification"></a>Especificação

A especificação do .NET Standard é um conjunto padronizado de APIs. A especificação é mantida por implementadores do .NET, especificamente a Microsoft (inclui .NET Framework, .NET Core e mono) e o Unity.

### <a name="official-artifacts"></a>Artefatos oficiais

A especificação oficial é um conjunto de arquivos *. cs* que definem as APIs que fazem parte do padrão. O [diretório ref](https://github.com/dotnet/standard/tree/master/src/netstandard/ref) em [dotnet/standard repository](https://github.com/dotnet/standard) define as APIs do .NET Standard.

O metapacote [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library) ([de origem](https://github.com/dotnet/standard/blob/master/src/netstandard/pkg/NETStandard.Library.dependencies.props)) descreve o conjunto de bibliotecas que define (parcialmente) uma ou mais versões do .NET Standard.

Um componente específico, como o `System.Runtime`, descreve:

- Parte do .NET Standard (apenas seu escopo).
- Várias versões do .NET Standard, para esse escopo.

Artefatos derivados são fornecidos para habilitar leitura mais conveniente e permitir determinados cenários do desenvolvedor (por exemplo, usando um compilador).

- [Lista de APIs em markdown](https://github.com/dotnet/standard/tree/master/docs/versions)
- Assemblies de referência, distribuídos como pacotes NuGet e referenciados pelo metapacote [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library/).

### <a name="package-representation"></a>Representação de pacote

O meio de distribuição principal dos assemblies de referência do .NET Standard são os pacotes NuGet. As implementações são entregues de várias formas, apropriadas para cada implementação do .NET.

Pacotes NuGet são direcionados a uma ou mais [estruturas](frameworks.md). .NET Standard pacotes visam a estrutura ".NET Standard". Você pode direcionar a estrutura de .NET Standard usando o `netstandard` [Compact TFM](frameworks.md) (por exemplo, `netstandard1.4` ). As bibliotecas que se destinam a serem executadas em várias implementações do .NET devem ter como destino essa estrutura. Para obter o mais amplo conjunto de APIs, direcione `netstandard2.0`, pois o número de APIs disponíveis mais do que dobrou entre o .NET Standard 1.6 e 2.0.

O [`NETStandard.Library`](https://www.nuget.org/packages/NETStandard.Library/) metapacote faz referência ao conjunto completo de pacotes NuGet que definem .net Standard.  A maneira mais comum de direcionar para `netstandard` é fazer referência a esse metapacote. Ele descreve e fornece acesso às ~40 bibliotecas .NET e APIs associadas, que definem a .NET Standard. Você pode referenciar pacotes adicionais destinados a `netstandard` para obter acesso a APIs adicionais.

### <a name="versioning"></a>Controle de versão

A especificação não é singular, mas um conjunto de APIs com controle de versão linear. A primeira versão do padrão estabelece um conjunto de linhas de base de APIs. As versões subsequentes adicionam APIs e herdam APIs definidas por versões anteriores. Não há nenhum provisionamento estabelecido para remover APIs do padrão.

.NET Standard não é específico de uma implementação .NET, nem corresponde ao esquema de controle de versão de qualquer uma dessas implementações.

Conforme observado anteriormente, não haverá novas versões de .NET Standard após 2,1.

## <a name="target-net-standard"></a>.NET Standard de destino

Você pode [criar bibliotecas de .net Standard](../core/tutorials/libraries.md) usando uma combinação da `netstandard` estrutura e do `NETStandard.Library` metapacote.

## <a name="net-framework-compatibility-mode"></a>Modo de compatibilidade do .NET framework

O modo de compatibilidade do .NET Framework foi introduzido a partir do .NET Standard 2.0. Esse modo de compatibilidade permite que os projetos do .NET Standard referenciem as bibliotecas do .NET Framework como se elas fossem compiladas para o .NET Standard. Fazer referência a bibliotecas do .NET Framework não funciona para todos os projetos, como as bibliotecas que usam APIs do WPF (Windows Presentation Foundation).

Para obter mais informações, veja [.NET Framework compatibility mode](../core/porting/third-party-deps.md#net-framework-compatibility-mode) (Modo de compatibilidade do .NET Framework).

## <a name="net-standard-libraries-and-visual-studio"></a>Bibliotecas do .NET standard e Visual Studio

Para criar bibliotecas de .NET Standard no Visual Studio, verifique se você tem o [visual studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) ou o visual Studio 2017 versão 15,3 ou posterior instalado no Windows ou [Visual Studio para Mac a versão 7,1](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) ou posterior instalada no MacOS.

Se você precisar apenas consumir as bibliotecas do .NET Standard 2.0 em seus projetos, também será possível fazer isso no Visual Studio 2015. No entanto, é necessário ter o NuGet cliente 3.6 ou posterior instalado. É possível baixar o cliente do NuGet para Visual Studio 2015 na página [downloads do NuGet](https://www.nuget.org/downloads).

## <a name="net-5-and-net-standard"></a>.NET 5 e .NET Standard

O .NET 5 é a implementação do .NET que a Microsoft está desenvolvendo ativamente. É um único produto com um conjunto uniforme de recursos e APIs que podem ser usados para aplicativos de área de trabalho do Windows e aplicativos de console entre plataformas, serviços de nuvem e sites. Os [TFMs](frameworks.md) .NET 5,0 refletem essa ampla variedade de cenários:

* `net5.0`

  Esse TFM é para o código que é executado em todos os lugares. Com algumas exceções, ele inclui apenas tecnologias que funcionam entre plataformas. Para o código do .NET 5, `net5.0` substitui `netcoreapp` e `netstandard` TFMs.

* `net5.0-windows`

  Este é um exemplo de [TFMs específicas do sistema operacional](frameworks.md#net-5-os-specific-tfms) que adicionam funcionalidade específica do sistema operacional a tudo o que `net5.0` se refere.

### <a name="when-to-target-net50-vs-netstandard"></a>Quando direcionar para NET 5.0 versus netstandard

Para o código existente que tem `netstandard` como alvo, não há necessidade de alterar o TFM para `net5.0` . O .NET 5,0 implementa .NET Standard 2,1 e anteriores. O único motivo para redirecionar de .NET Standard para o .NET 5,0 seria obter acesso a mais recursos de tempo de execução, recursos de linguagem ou APIs. Por exemplo, para usar o C# 9, você precisa direcionar ao .NET 5,0. Você pode multidirecionar o .NET 5,0 e .NET Standard para obter acesso aos recursos mais recentes e ainda ter sua biblioteca disponível para outras implementações do .NET.

Aqui estão algumas diretrizes para o novo código para o .NET 5:

* Componentes do aplicativo

  Se você estiver usando bibliotecas para dividir um aplicativo em vários componentes, recomendamos que você direcione `net5.x` onde `5.x` é a versão mais antiga do .NET 5 que seu aplicativo pode atingir. Para simplificar, é melhor manter todos os projetos que compõem seu aplicativo na mesma versão do .NET. Em seguida, você pode assumir os mesmos recursos da BCL em todos os lugares.

* Bibliotecas reutilizáveis

  Se você estiver criando bibliotecas reutilizáveis que planeja enviar no NuGet, considere o compensador entre o alcance e o conjunto de recursos disponíveis. .NET Standard 2,0 é a versão mais recente com suporte do .NET Framework, portanto, ele fornece um bom alcance com um conjunto de recursos muito grande. Não é recomendável direcionar .NET Standard 1. x, pois você limitaria o conjunto de recursos disponíveis para um aumento mínimo no alcance.

  Se você não precisar dar suporte a .NET Framework, poderá ir .NET Standard 2,1 ou .NET 5. Recomendamos que você pule .NET Standard 2,1 e vá direto para o .NET 5. As bibliotecas mais amplamente usadas acabarão com vários destinos para .NET Standard 2,0 e para o .NET 5. O suporte ao .NET Standard 2,0 oferece o máximo de alcance, enquanto o suporte ao .NET 5 garante que você possa aproveitar os recursos mais recentes da plataforma para os clientes que já estão no .NET 5.

### <a name="net-standard-problems"></a>Problemas de .NET Standard

Aqui estão alguns problemas com .NET Standard que ajudam a explicar por que o .NET 5 é a melhor maneira de compartilhar código entre plataformas e cargas de trabalho:

- Lentidão para adicionar novas APIs

  .NET Standard foi criado como um conjunto de API que todas as implementações do .NET teriam de dar suporte, portanto, havia um processo de revisão para que as propostas adicionassem novas APIs. O objetivo era padronizar apenas as APIs que poderiam ser implementadas em todas as plataformas .NET atuais e futuras. O resultado foi que, se um recurso perdeu uma versão específica, talvez seja necessário aguardar alguns anos antes que ele tenha sido adicionado a uma versão do padrão. Em seguida, você esperaria mais tempo para que a nova versão do .NET Standard seja amplamente suportada.

  **Solução no .NET 5:** Quando um recurso é implementado, ele já está disponível para cada aplicativo e biblioteca do .NET 5, pois a base de código é compartilhada. E, como não há nenhuma diferença entre a especificação da API e sua implementação, você pode aproveitar os novos recursos muito mais rapidamente do que com .NET Standard.

- Controle de versão complexo

  A separação da especificação de API de suas implementações resulta em um mapeamento complexo entre versões de especificação de API e versões de implementação. Essa complexidade é evidente na tabela mostrada anteriormente neste artigo e as instruções sobre como interpretá-la.

  **Solução no .NET 5:** Não há nenhuma separação entre uma especificação de API do .NET 5. x e sua implementação. O resultado é um esquema TFM simplificado. Há um prefixo TFM para todas as cargas de trabalho: `net5.0` é usado para bibliotecas, aplicativos de console e aplicativos Web. A única variação é um [sufixo que especifica APIs específicas da plataforma](frameworks.md#net-5-os-specific-tfms) para uma plataforma específica, como `net5.0-windows` . Graças a essa Convenção de nomenclatura TFM, você pode facilmente dizer se um determinado aplicativo pode usar uma determinada biblioteca. Nenhuma tabela equivalente de número de versão como a de .NET Standard é necessária.

- Plataforma-exceções sem suporte em tempo de execução

  O .NET Standard expõe APIs específicas da plataforma. Seu código pode ser compilado sem erros e parece ser portável a qualquer plataforma, mesmo que não seja portátil. Quando ele é executado em uma plataforma que não tem uma implementação para uma determinada API, você obtém erros de tempo de execução.

  **Solução no .NET 5:** O SDK do .NET 5 inclui analisadores de código que são habilitados por padrão. O analisador de compatibilidade de plataforma detecta o uso não intencional de APIs que não têm suporte nas plataformas nas quais você pretende executar. Para obter mais informações, consulte [analisador de compatibilidade de plataforma](analyzers/platform-compat-analyzer.md).

### <a name="net-standard-not-deprecated"></a>.NET Standard não preterido

.NET Standard ainda é necessário para as bibliotecas que podem ser usadas por várias implementações do .NET. É recomendável que você direcione .NET Standard nos seguintes cenários:

* Use `netstandard2.0` para compartilhar código entre .NET Framework e todas as outras implementações do .net.
* Use `netstandard2.1` para compartilhar código entre o mono, o Xamarin e o .NET Core 3. x.

## <a name="see-also"></a>Confira também

- [.NET Standard versões (origem)](https://github.com/dotnet/standard/blob/master/docs/versions.md)
- [Versões do .NET Standard (interface do usuário interativa)](https://dotnet.microsoft.com/platform/dotnet-standard#versions)
- [Criar uma biblioteca de .NET Standard](../core/tutorials/library-with-visual-studio.md)
- [Direcionamento multiplataforma](./library-guidance/cross-platform-targeting.md)
