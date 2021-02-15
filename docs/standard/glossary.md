---
title: Glossário .NET
description: Descubra o significado de termos selecionados usados na documentação do .NET.
ms.date: 11/16/2020
ms.openlocfilehash: 77ed506fb1c5bd4018b5fe0c14cc0bf37cb08113
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96438192"
---
# <a name="net-glossary"></a>Glossário .NET

A principal meta deste glossário é esclarecer os significados de termos e acrônimos selecionados que aparecem com frequência na documentação do .NET sem definições.

## <a name="aot"></a>AOT

Compilador Ahead-of-Time.

Semelhante ao [JIT](#jit), esse compilador também converte [IL](#il) em código de máquina. Diferentemente da compilação JIT, a compilação AOT acontece antes que o aplicativo seja executado e normalmente é executada em um computador diferente. Como as cadeias de ferramentas da AOT não são compiladas em tempo de execução, elas não precisam minimizar o tempo gasto na compilação. Isso significa que elas podem gastar mais tempo em otimização. Como o contexto da AOT é o aplicativo inteiro, o compilador AOT também executa a vinculação de módulo cruzado e a análise de programa inteiro, o que significa que todas as referências são seguidas e um único executável é produzido.

Confira [CoreRT](#corert) e [.NET Native](#net-native).

## <a name="app-model"></a>modelo de aplicativo

Uma API específica da [carga de trabalho](#workload). Estes são alguns exemplos:

* ASP.NET
* ASP.NET Web API
* Entity Framework (EF)
* Windows Presentation Foundation (WPF)
* Windows Communication Foundation (WCF)
* Windows Workflow Foundation (WF)
* Windows Forms (WinForms)

## <a name="aspnet"></a>ASP.NET

A implementação do ASP.NET original que é fornecida com o .NET Framework.

Às vezes, o ASP.NET é um termo abrangente que se refere a ambas as implementações de ASP.NET, incluindo o ASP.NET Core. O significado que o termo carrega em uma determinada instância é determinado pelo contexto. Consulte ASP.NET 4. x quando quiser deixar claro que você não está usando o ASP.NET para significar ambas as implementações.

Confira [Documentação do ASP.NET](/aspnet/#pivot=aspnet).

## <a name="aspnet-core"></a>ASP.NET Core

Uma implementação de plataforma cruzada, de alto desempenho e de código aberto do ASP.NET.

Confira [Documentação do ASP.NET Core](/aspnet/#pivot=core).

## <a name="assembly"></a>assembly

Um arquivo *. dll* / *. exe* que pode conter uma coleção de APIs que podem ser chamadas por aplicativos ou outros assemblies.

Um assembly pode incluir tipos como interfaces, classes, estruturas, enumerações e delegados. Às vezes, os assemblies em uma pasta *bin* de projeto são chamados de *binários*. Consulte também [biblioteca](#library).

## <a name="bcl"></a>BCL

Biblioteca de classes base.

Um conjunto de bibliotecas que compõem o sistema. \* (e com uma extensão limitada da Microsoft. \* ) namespaces. A BCL é uma estrutura de nível inferior e de uso geral, base para a criação de estruturas de aplicativo de nível mais alto, como o ASP.NET Core.

O código-fonte da BCL para [.NET 5 (e .NET Core) e versões posteriores](#net-5-and-later-versions) está contido no [repositório do tempo de execução do .net](https://github.com/dotnet/runtime). A maioria dessas APIs de BCL também está disponível em .NET Framework, portanto, você pode considerar esse código-fonte como uma bifurcação do código-fonte da BCL .NET Framework.

Os termos a seguir geralmente se referem à mesma coleção de APIs às quais a BCL se refere:

- [principais bibliotecas do .NET](../core/compatibility/corefx.md)
- [bibliotecas do Framework](#framework-libraries)
- [bibliotecas de tempo de execução](#runtime)
- [estrutura compartilhada](#shared-framework)

## <a name="clr"></a>CLR

Common Language Runtime.

O significado exato depende do contexto. O Common Language Runtime geralmente se refere ao tempo de execução de [.NET Framework](#net-framework) ou ao tempo de execução do [.NET 5 (e do .NET Core) e versões posteriores](#net-5-and-later-versions).

Um CLR gerencia A alocação e o gerenciamento de memória. Um CLR também é uma máquina virtual que não só executa aplicativos, mas também gera e compila código imediatamente usando um compilador [JIT](#jit) .

A implementação do CLR para .NET Framework é somente Windows.

A implementação do CLR para o .NET 5 e versões posteriores (também conhecida como o principal CLR) é criada a partir da mesma base de código que o .NET Framework CLR. Originalmente, o CLR principal era o tempo de execução do Silverlight e foi projetado para ser executado em várias plataformas, especificamente Windows e OS X. Ele ainda é um tempo de execução de [plataforma cruzada](#cross-platform) , agora incluindo suporte para muitas distribuições do Linux.

Consulte também [tempo de execução](#runtime).

## <a name="core-clr"></a>CLR principal

O Common Language Runtime para [.NET 5 (e .NET Core) e versões posteriores](#net-5-and-later-versions).

Consulte [CLR](#clr)

## <a name="corert"></a>CoreRT

Ao contrário do [CLR](#clr), o CoreRT não é uma máquina virtual, o que significa que ele não inclui os recursos para gerar e executar código imediatamente porque ele não inclui um [JIT](#jit). No entanto, ele inclui o [GC](#gc) e a capacidade de RTTI (identificação de tipo de tempo de execução) e reflexão. Contudo, seu sistema de tipos é projetado para que os metadados para reflexão não sejam necessários. Não exigir metadados permite que uma cadeia de ferramentas [AOT](#aot) possa se vincular a metadados supérfluos e (o mais importante) identifique o código que o aplicativo não usa. O CoreRT está em desenvolvimento.

Consulte [introdução a .net Native e CoreRT](https://github.com/dotnet/corert/blob/master/Documentation/intro-to-corert.md).

## <a name="cross-platform"></a>várias plataformas

A capacidade de desenvolver e executar um aplicativo que pode ser usado em vários sistemas operacionais diferentes, como Linux, Windows e iOS, sem a necessidade de reescrever especificamente para cada um. Isso permite a reutilização de código e a consistência entre aplicativos em diferentes plataformas.

## <a name="ecosystem"></a>ecossistema

Todos os softwares de runtime, as ferramentas de desenvolvimento e os recursos da comunidade que são usados para compilar e executar aplicativos de uma determinada tecnologia.

O termo "Ecossistema do .NET" difere de termos semelhantes, como "Pilha do .NET", em relação à inclusão de bibliotecas e aplicativos de terceiros. Veja um exemplo em uma frase:

- "A motivação por trás do [.net Standard](#net-standard) é estabelecer uma maior uniformidade no ecossistema do .net."

## <a name="framework"></a>estrutura

Em geral, uma coleção abrangente de APIs que facilita o desenvolvimento e a implantação de aplicativos que são baseados em uma tecnologia específica. Nesse sentido geral, o ASP.NET Core e o Windows Forms são exemplos de estruturas de aplicativo. Consulte também [biblioteca](#library).

A palavra "estrutura" tem um significado diferente nos seguintes termos:

- [bibliotecas do Framework](#framework-libraries)
- [.NET Framework](#net-framework)
- [estrutura compartilhada](#shared-framework)
- [estrutura de destino](#target-framework)
- [TFM (Moniker de Estrutura de Destino)](#tfm)
- [aplicativo dependente de estrutura](../core/deploying/index.md#publish-framework-dependent)

Às vezes, "estrutura" refere-se a uma [implementação do .net](#implementation-of-net). Por exemplo, um artigo pode chamar o .NET 5 como uma estrutura.

## <a name="framework-libraries"></a>bibliotecas do Framework

O significado depende do contexto. Pode consultar as bibliotecas de estrutura para [.NET 5 (e .NET Core) e versões posteriores](#net-5-and-later-versions); nesse caso, ela se refere às mesmas bibliotecas às quais a [BCL](#bcl) se refere. Ele também pode se referir às bibliotecas do ASP.NET Core Framework, que se baseiam na BCL e fornecem APIs adicionais para aplicativos Web.

## <a name="gc"></a>GC

Coletor de lixo.

O coletor de lixo é uma implementação do gerenciamento automático de memória.  O GC libera a memória ocupada por objetos que não estejam mais em uso.

Consulte [Coleta de lixo](garbage-collection/index.md).

## <a name="il"></a>IL

Linguagem intermediária.

As linguagens .NET de nível mais alto , como C#, são compiladas em um conjunto de instruções independente de hardware, que é chamado de IL (linguagem intermediária). A IL às vezes é conhecida como MSIL (Microsoft Intermediate Language) ou CIL (Common Intermediate Language).

## <a name="jit"></a>JIT

Compilador Just-In-Time.

Semelhante ao [AOT](#aot), esse compilador converte a [IL](#il) em um código de máquina que o processador entenda. Ao contrário da AOT, a compilação JIT acontece sob demanda e é executada no mesmo computador em que o código precisa ser executado. Como a compilação JIT ocorre durante a execução do aplicativo, o tempo de compilação faz parte do tempo de execução. Assim, os compiladores JIT precisam equilibrar o tempo gasto com a otimização do código em relação à economia que o código resultante pode produzir. Mas um JIT reconhece o hardware e pode evitar que os desenvolvedores tenham que fornecer implementações diferentes.

## <a name="implementation-of-net"></a>implementação do .NET

Uma implementação do .NET inclui:

- Um ou mais runtimes. Exemplos: [CLR](#clr), [CoreRT](#corert).
- Uma biblioteca de classes que implementa uma versão do .NET Standard e pode incluir APIs adicionais. Exemplos: o [BCLs](#bcl) para [.NET Framework](#net-framework) e o [.NET 5 (e .NET Core) e versões posteriores](#net-5-and-later-versions).
- Opcionalmente, uma ou mais estruturas de aplicativo. Exemplos: [ASP.net](#aspnet), Windows Forms e WPF estão incluídos no .NET Framework e no .NET 5.
- Opcionalmente, ferramentas de desenvolvimento. Algumas ferramentas de desenvolvimento são compartilhadas entre várias implementações.

Exemplos de implementações do .NET:

- [.NET Framework](#net-framework)
- [.NET 5 e versões posteriores (incluindo o .NET Core 2.1-3.1)](#net-5-and-later-versions)
- [UWP (Plataforma Universal do Windows)](#uwp)
- [Mono](#mono)

## <a name="library"></a>biblioteca

Uma coleção de APIs que podem ser chamadas por aplicativos ou outras bibliotecas. Uma biblioteca do .NET é composta de um ou mais [assemblies](#assembly).

A biblioteca de palavras e a [estrutura](#framework) geralmente são usadas como sinônimos.

## <a name="mono"></a>Mono

Mono é uma implementação do .NET [multiplataforma](#cross-platform) de software livre usada principalmente quando é necessário um pequeno runtime. É o tempo de execução que capacita aplicativos Xamarin no Android, Mac, iOS, tvOS e watchOS e concentra-se principalmente em aplicativos que exigem uma pequena superfície.

Ele dá suporte a todas as versões do .NET Standard publicadas atualmente.

Historicamente, o Mono implementava a maior API do .NET Framework e emulava alguns dos recursos mais populares do Unix. Às vezes, ele é usado para executar aplicativos .NET que dependem desses recursos no Unix.

O mono normalmente é usado com um [compilador just-in-time](#jit), mas também apresenta um [compilador estático completo (compilação antecipada de tempo)](#aot) que é usado em plataformas como Ios.

Consulte a [documentação do mono](https://www.mono-project.com/docs/).

## <a name="net"></a>.NET

O termo coletivo para [.NET Standard](#net-standard) e todas as [implementações de .NET](#implementation-of-net), bem como as cargas de trabalho. Sempre totalmente em maiúsculas, nunca ".net".

Quando o [.NET 5](#net-5-and-later-versions) (atualmente em visualização) for lançado, será a implementação do .net recomendada para todo o novo desenvolvimento .net e, portanto, em alguns contextos ".net", significa ".NET 5 e versões posteriores".

Consulte os [conceitos básicos do .net](../fundamentals/index.yml)

## <a name="net-5-and-later-versions"></a>.NET 5 e versões posteriores

Uma implementação de software livre de várias plataformas, de alto desempenho e de software livre do .NET. Inclui um[CLR](#clr)(Common Language Runtime), um tempo de execução da [AOT](#aot) ([CoreRT](#corert), em desenvolvimento), uma[BCL](#bcl)(base Class Library) e o [SDK do .net](#net-sdk).

As versões anteriores desta implementação .NET são conhecidas como .NET Core. O .NET 5,0 é a próxima versão do .NET Core 3,1. A versão 4 foi ignorada para evitar confusão nesta implementação mais recente do .NET com a implementação mais antiga conhecida como [.NET Framework](#net-framework). A versão atual do .NET Framework é 4,8.

Consulte [conceitos básicos do .net](../fundamentals/index.yml).

## <a name="net-cli"></a>CLI do .NET

Um ferramentas de plataforma cruzada para o desenvolvimento de aplicativos e bibliotecas para [.NET 5 (e .NET Core) e versões posteriores](#net-5-and-later-versions). Também conhecido como o CLI do .NET Core.

Consulte [CLI do .net](../core/tools/index.md).

## <a name="net-core"></a>.NET Core

Consulte [.NET 5 e versões posteriores](#net-5-and-later-versions).

## <a name="net-framework"></a>.NET Framework

Uma implementação do .NET que é executado somente no Windows. Inclui o[CLR](#clr)(Common Language Runtime), a[BCL](#bcl)(base Class Library) e as bibliotecas de estrutura do aplicativo, como [ASP.net](#aspnet), Windows Forms e WPF.

Consulte o [Guia do .NET Framework](../framework/index.yml).

## <a name="net-native"></a>.NET Nativo

Uma cadeia de ferramentas de compilador que produz a[AOT](#aot)(vida útil antecipada de código), em oposição ao[JIT](#jit)(just-in-time).

A compilação acontece no computador do desenvolvedor, semelhante à maneira como um compilador e vinculador C++ funciona. Ela remove código não utilizado e gasta mais tempo otimizando-o. Ele extrai o código de bibliotecas e os mescla no executável. O resultado é um módulo único que representa o aplicativo inteiro.

A UWP foi a primeira estrutura de aplicativo com suporte pelo .NET Native. Agora, há suporte para criação de aplicativos de console nativo para macOS, Windows e Linux.

Consulte [Introdução ao .NET Native e ao CoreRT](https://github.com/dotnet/corert/blob/master/Documentation/intro-to-corert.md)

## <a name="net-sdk"></a>SDK .NET

Um conjunto de bibliotecas e ferramentas que permitem aos desenvolvedores criar aplicativos e bibliotecas .NET para o [.NET 5 (e o .NET Core) e versões posteriores](#net-5-and-later-versions). Também conhecido como o SDK do .NET Core.

Inclui a [CLI do .net](#net-cli) para compilar aplicativos, bibliotecas .net e tempo de execução para compilar e executar aplicativos e o executável dotnet (*dotnet.exe*) que executa comandos da CLI e executa aplicativos.

Consulte [visão geral do SDK do .net](../core/sdk.md).

## <a name="net-standard"></a>.NET Standard

Uma especificação formal das APIs do .NET que estão disponíveis em cada implementação do .NET.

Às vezes, a especificação do .NET Standard também é chamada de biblioteca na documentação. Como uma biblioteca inclui implementações de API e não apenas especificações (interfaces), é um equívoco chamar .NET Standard de "biblioteca".

Consulte [.NET Standard](net-standard.md).

## <a name="ngen"></a>NGEN

Geração (de imagem) nativa.

Você pode considerar essa tecnologia como um compilador [JIT](#jit) persistente. Ela geralmente compila o código no computador em que o código é executado, mas a compilação normalmente ocorre no momento da instalação.

## <a name="package"></a>pacote

Um pacote NuGet &mdash; ou apenas um pacote &mdash; é um arquivo *.zip* com um ou mais assemblies de mesmo nome, junto com metadados adicionais, como o nome do autor.

O arquivo *.zip* tem uma extensão *.nupkg* e pode conter ativos, como arquivos *.dll* e arquivos *.xml*, para uso com várias versões e estruturas de destino. Quando instalado em um aplicativo ou uma biblioteca, os ativos apropriados são selecionados com base na estrutura de destino especificada pelo aplicativo ou pela biblioteca. Os ativos que definem a interface estão na pasta *ref* e os ativos que definem a implementação estão na pasta *lib*.

## <a name="platform"></a>plataforma

Um sistema operacional e o hardware em que ele é executado, como macOS, Windows, Linux, iOS e Android.

Veja alguns exemplos de uso nessas frases:

- "O .NET Core é uma implementação multiplataforma do .NET."
- "Os perfis PCL representam plataformas da Microsoft, enquanto .NET Standard é independente da plataforma".

A documentação .NET herdada às vezes usa "plataforma .NET" para significar uma [implementação do .net](#implementation-of-net) ou da [pilha](#stack) do .net, incluindo todas as implementações. Ambos os usos tendem a ficar confusos com o significado principal (so/hardware); portanto, tentamos evitar esses usos.

"Plataforma" tem um significado diferente na frase "plataforma de desenvolvedor", que se refere a um software que fornece ferramentas e bibliotecas para compilar e executar aplicativos. O .NET é uma plataforma de desenvolvedor de software livre de plataforma cruzada para a criação de vários tipos diferentes de aplicativos.

## <a name="runtime"></a>runtime

Em geral, o ambiente de execução para um programa gerenciado. O SO faz parte do ambiente do runtime, mas não faz parte do runtime do .NET. Aqui estão alguns exemplos de tempos de execução do .NET neste sentido da palavra:

- [CLR](#clr)(Common Language Runtime)
- .NET Native (para UWP)
- runtime Mono

A palavra "tempo de execução" tem um significado diferente em alguns contextos:

* *Tempo de execução do .net* na [página de download do .NET 5,0](https://dotnet.microsoft.com/download/dotnet/5.0).

  Você pode baixar o *tempo* de execução do .net ou outros tempos de execução, como o *ASP.NET Core Runtime*. Um *tempo de execução* nesse uso é o conjunto de componentes que devem ser instalados em um computador para executar um aplicativo [dependente da estrutura](../core/deploying/index.md#publish-framework-dependent) no computador. O tempo de execução do .NET inclui o [CLR](#clr) e a [estrutura compartilhada](#shared-framework)do .net, que fornece a [BCL](#bcl).

* *Bibliotecas de tempo de execução .NET*

  Refere-se às mesmas bibliotecas às quais a [BCL](#bcl) se refere. No entanto, outros tempos de execução, como o ASP.NET Core Runtime, têm [estruturas compartilhadas](#shared-framework)diferentes, com bibliotecas adicionais que se baseiam na BCL.

* [RID (identificador de tempo de execução)](../core/rid-catalog.md).

  O *tempo de execução* aqui significa a plataforma do sistema operacional e a arquitetura de CPU em que um aplicativo .net é executado, por exemplo: `linux-x64` .

* Às vezes, o "tempo de execução" é usado no sentido de uma [implementação do .net](#implementation-of-net), como nos exemplos a seguir:

  - "Os diversos runtimes do .NET implementam versões específicas do .NET Standard. … Cada versão de runtime do .NET anuncia a última versão do .NET Standard à qual ele dá suporte..."
  - "Bibliotecas destinadas à execução em vários runtimes devem ter essa estrutura como destino." (referindo-se ao .NET Standard)

## <a name="shared-framework"></a>estrutura compartilhada

O significado depende do contexto. A *estrutura compartilhada do .net* refere-se às bibliotecas incluídas no [tempo de execução do .net](#runtime). Nesse caso, a *estrutura compartilhada* para [.NET 5 (e .NET Core) e versões posteriores](#net-5-and-later-versions) se refere às mesmas bibliotecas às quais a [BCL](#bcl) se refere.

Há outras estruturas compartilhadas. A *estrutura compartilhada ASP.NET Core* refere-se às bibliotecas incluídas no [tempo de execução de ASP.NET Core](#runtime), que inclui a BCL mais APIs adicionais para uso por aplicativos Web.

Para [aplicativos dependentes da estrutura](../core/deploying/index.md#publish-framework-dependent), a estrutura compartilhada consiste em bibliotecas que estão contidas em assemblies instalados em uma pasta no computador que executa o aplicativo. Para [aplicativos](../core/deploying/index.md#publish-self-contained)independentes, os assemblies de estrutura compartilhada são incluídos no aplicativo.

Para obter mais informações, consulte aprofundamento [em primitivos do .NET Core, parte 2: a estrutura compartilhada](https://natemcmaster.com/blog/2018/08/29/netcore-primitives-2/).

## <a name="stack"></a>stack

Um conjunto de tecnologias de programação que são usadas para compilar e executar aplicativos.

"A pilha do .NET" refere-se a .NET Standard e a todas as implementações do .NET. A frase "uma pilha do .NET" pode se referir a uma implementação do .NET.

## <a name="target-framework"></a>estrutura de destino

A coleção de APIs da qual um aplicativo ou biblioteca do .NET depende.

Um aplicativo ou uma biblioteca pode ter como destino uma versão do .NET Standard (por exemplo, .NET Standard 2,0), que é uma especificação para um conjunto padronizado de APIs em todas as implementações do .NET. Um aplicativo ou uma biblioteca também pode se destinar a uma versão de uma implementação específica do .NET, obtendo acesso a APIs específicas da implementação. Por exemplo, um aplicativo que tem como destino o Xamarin.iOS obtém acesso aos wrappers da API fornecidos para Xamarin iOS.

Para algumas estruturas de destino (por exemplo, o .NET Framework) as APIs disponíveis são definidas pelos assemblies que uma implementação do .NET instala em um sistema, que podem incluir as APIs de estrutura do aplicativo (por exemplo, ASP.NET, WinForms). Para estruturas de destino baseadas em pacote (como .NET Standard e .NET Core), a APIs de estrutura são definidas por pacotes instalados no aplicativo ou na biblioteca. Nesse caso, a estrutura de destino especifica implicitamente um pacote que faz referência a todos os pacotes que juntos compõem a estrutura.

Consulte [Estruturas de destino](frameworks.md).

## <a name="tfm"></a>TFM

Moniker da estrutura de destino.

Um formato de token padronizado para especificar a estrutura de destino de um aplicativo ou uma biblioteca do .NET. As estruturas de destino são geralmente referenciadas por um nome curto, como `net462`. Os TFMs de formato longo (como. .NETFramework,Version=4.6.2) existem, mas não são geralmente usados para especificar uma estrutura de destino.

Consulte [Estruturas de destino](frameworks.md).

## <a name="uwp"></a>UWP

Plataforma Universal do Windows.

Uma implementação do .NET que é usada para criar aplicativos do Windows modernos e sensíveis ao toque, bem como software para a IoT (Internet das Coisas). Ele foi projetado para unificar os diferentes tipos de dispositivos que você talvez queira direcionar, incluindo PCs, tablets, telefones e até mesmo o Xbox. A UWP fornece muitos serviços, como um repositório centralizado de aplicativos, um ambiente de execução (AppContainer) e um conjunto de APIs do Windows para usar em vez das APIS do Win32 (WinRT). Os aplicativos podem ser escritos em C++, C#, Visual Basic e JavaScript. Ao usar C# e Visual Basic, as APIs do .NET são fornecidas pelo .NET 5 (e .NET Core) e por versões posteriores.

## <a name="workload"></a>workload

Um tipo de aplicativo que alguém está criando. Mais genérico do que o [modelo de aplicativo](#app-model). Por exemplo, na parte superior de cada página de documentação do .NET, incluindo esta, é uma lista suspensa para **cargas** de trabalho, que permite que você alterne para a documentação de **\& dados** **Web**, **móveis**, de **nuvem**, de **área de trabalho** e de Machine Learning.

Em alguns contextos, a *carga de trabalho* refere-se a uma coleção de recursos do Visual Studio que você pode optar por instalar para dar suporte a um tipo específico de aplicativo. Para obter um exemplo, consulte [selecionar uma carga de trabalho](../core/install/windows.md#select-a-workload).

## <a name="see-also"></a>Confira também

- [Conceitos básicos do .NET](../fundamentals/index.yml)
- [Guia do .NET Framework](../framework/index.yml)
- [Visão geral do ASP.NET](/aspnet/index#pivot=aspnet)
- [Visão geral de ASP.NET Core](/aspnet/index#pivot=core)
