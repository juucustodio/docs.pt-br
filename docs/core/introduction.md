---
title: Introdução e visão geral do .NET
description: Saiba mais sobre o .NET, uma plataforma de desenvolvimento de software livre gratuita para a criação de muitos tipos de aplicativos.
author: tdykstra
ms.date: 11/16/2020
ms.custom: updateeachrelease
ms.openlocfilehash: e0c86b377d4ea73bb275bc48c0f0cccb2db249dd
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189994"
---
# <a name="introduction-to-net"></a>Introdução ao .NET

O .NET é uma plataforma de desenvolvimento de software livre gratuita para a criação de vários tipos de aplicativos, como:

* [Aplicativos Web, APIs da Web e microservices](/aspnet/core/introduction-to-aspnet-core#recommended-learning-path)
* [Funções sem servidor na nuvem](/azure/azure-functions/functions-create-first-function-vs-code?pivots=programming-language-csharp)
* [Aplicativos nativos da nuvem](../architecture/cloud-native/index.md)
* [Aplicativos móveis](https://dotnet.microsoft.com/learn/xamarin/hello-world-tutorial/intro)
* Aplicativos da área de trabalho
  * [WPF do Windows](/dotnet/desktop/wpf/)
  * [Windows Forms](/dotnet/desktop/winforms/)
  * [UWP (Plataforma Universal do Windows)](/windows/uwp/get-started/create-a-hello-world-app-xaml-universal)
* [Jogos](https://dotnet.microsoft.com/apps/games)
* [Internet das coisas (IoT)](../iot/index.yml)
* [Aprendizado de máquina](../machine-learning/index.yml)
* [Aplicativos de console](tutorials/with-visual-studio-code.md)
* [Serviços Windows](/aspnet/core/host-and-deploy/windows-service)

Compartilhe a funcionalidade entre diferentes aplicativos e tipos de aplicativos usando [bibliotecas de classes](../standard/class-libraries.md).

Com o .NET, seus arquivos de código e de projeto parecem e sentem o mesmo, independentemente do tipo de aplicativo que você está criando. Você tem acesso aos mesmos recursos de tempo de execução, API e linguagem com cada aplicativo.

## <a name="cross-platform"></a>Plataforma cruzada

Você pode criar aplicativos .NET para muitos sistemas operacionais, incluindo:

* Windows
* macOS
* Linux
* Android
* iOS
* tvOS
* watchOS

As arquiteturas de processador com suporte incluem:

* x64
* x86
* ARM32
* ARM64

O .NET permite que você use recursos específicos da plataforma, como APIs do sistema operacional. Os exemplos são Windows Forms e WPF no Windows e as ligações nativas para cada plataforma móvel do Xamarin.

Para obter mais informações, consulte [política de ciclo de vida do so com suporte](https://github.com/dotnet/core/blob/master/os-lifecycle-policy.md) e [Catálogo de RID do .net](rid-catalog.md).

## <a name="open-source"></a>Software livre

O .NET é um software livre, usando as [licenças MIT e Apache 2](https://github.com/dotnet/runtime/blob/master/LICENSE.TXT). O .NET é um projeto do [.net Foundation](https://dotnetfoundation.org/).

Para obter mais informações, consulte a [lista de repositórios do projeto no github.com](https://github.com/dotnet/core/blob/master/Documentation/core-repos.md).

## <a name="support"></a>Suporte

O .NET tem suporte da Microsoft no Windows, macOS e Linux. Ele é atualizado regularmente para segurança e qualidade, na segunda terça-feira de cada mês.

As distribuições binárias do .NET da Microsoft são criadas e testadas em servidores mantidos pela Microsoft no Azure e seguem práticas de engenharia e segurança da Microsoft.

O [Red Hat dá suporte ao .net](https://developers.redhat.com/topics/dotnet/) em Red Hat Enterprise Linux (RHEL). Red Hat e Microsoft colaboram para garantir que o .NET Core funcione bem no RHEL.

O [tizen dá suporte ao .net](https://developer.tizen.org/development/training/.net-application) em plataformas tizen.

Para obter mais informações, consulte [versões e suporte para .NET Core e .NET 5](releases-and-support.md).

## <a name="tools-and-productivity"></a>Ferramentas e produtividade

O .NET oferece a você uma opção de linguagens, IDEs (ambientes de desenvolvimento integrados) e outras ferramentas.

### <a name="programming-languages"></a>Linguagens de programação

O .NET dá suporte a três linguagens de programação:

* [C#](../csharp/index.yml)

  O C# (pronuncia-se "Veja nítido") é uma linguagem de programação moderna, orientada a objeto e de tipo seguro. O C# tem suas raízes na família de linguagens C e os programadores em C, C++, Java e JavaScript a reconhecerão imediatamente.

* [F#](../fsharp/index.yml)

  A linguagem F # dá suporte a modelos de programação funcionais, orientados a objeto e imperativos.

* [Visual Basic](../visual-basic/index.yml)

  Entre as linguagens do .NET, a sintaxe do Visual Basic é mais próxima da linguagem humana comum, o que pode facilitar o aprendizado. Ao contrário do C# e F #, para os quais a Microsoft está desenvolvendo ativamente novos recursos, a linguagem Visual Basic é estável. Não há suporte para Visual Basic para aplicativos Web, mas há suporte para APIs Web.

Aqui estão alguns dos recursos com suporte nas linguagens .NET:

* [Segurança de tipos](../standard/base-types/common-type-system.md)
* Inferência de tipos- [C#](../csharp/programming-guide/types/index.md#specifying-types-in-variable-declarations), [F #](../fsharp/language-reference/type-inference.md), [Visual Basic](../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
* [Tipos genéricos](../standard/generics.md)
* [Representantes](../standard/delegates-lambdas.md)
* [Lambdas](../standard/delegates-lambdas.md)
* [Eventos](../standard/events/index.md)
* [Exceções](../standard/exceptions/index.md)
* [Atributos](../standard/attributes/index.md)
* [Código assíncrono](../standard/async.md)
* [Programação paralela](../standard/parallel-programming/index.md)
* [Analisadores de código](../fundamentals/code-analysis/overview.md)

### <a name="ides"></a>IDEs

Os ambientes de desenvolvimento integrados para .NET incluem:

* [Visual Studio](https://visualstudio.microsoft.com/vs/)

  Somente é executado no Windows. Tem ampla funcionalidade interna projetada para funcionar com o .NET. A Community Edition é gratuita para estudantes, colaboradores de software livre e indivíduos.

* [Visual Studio Code](https://code.visualstudio.com/)

  É executado no Windows, no macOS e no Linux. Gratuito e software livre. As extensões estão disponíveis para trabalhar com linguagens .NET.

* [Visual Studio para Mac](https://visualstudio.microsoft.com/vs/mac/)

  É executado somente no macOS. Para desenvolver aplicativos .NET e jogos para iOS, Android e Web.

* [Codespaces do GitHub](https://github.com/features/codespaces)

  Um ambiente de Visual Studio Code online, atualmente em beta.

### <a name="sdk-and-runtimes"></a>SDK e tempos de execução

O [SDK do .net](sdk.md) é um conjunto de bibliotecas e ferramentas para desenvolver e executar aplicativos .net.

Ao [baixar o .net](https://dotnet.microsoft.com/download/dotnet-core/), você pode escolher o SDK ou um *tempo de execução*, como o tempo de execução do .net ou o tempo de execução do ASP.NET Core. Instale um tempo de execução em um computador que você deseja preparar para executar aplicativos .NET. Instale o SDK em um computador que você deseja usar para desenvolvimento. Ao baixar o SDK, você obtém automaticamente os tempos de execução com ele.

O download do SDK inclui os seguintes componentes:

* A [CLI do .net](tools/index.md). Ferramentas de linha de comando que você pode usar para desenvolvimento local e scripts de integração contínua.
* O  [driver](tools/index.md#driver)`dotnet`. Um comando da CLI que executa aplicativos dependentes da estrutura.
* Os compiladores da linguagem de programação [Roslyn](https://github.com/dotnet/roslyn) e [F #](https://github.com/microsoft/visualfsharp) .
* O mecanismo de compilação do [MSBuild](/visualstudio/msbuild/msbuild) .
* O [tempo de execução do .net](#clr). Fornece um sistema de tipos, carregamento de assembly, coletor de lixo, interoperabilidade nativa e outros serviços básicos.
* [Bibliotecas de tempo de execução](#runtime-libraries). Fornece tipos de dados primitivos e utilitários fundamentais.
* O tempo de execução de ASP.NET Core. Fornece serviços básicos para aplicativos conectados à Internet, como aplicativos Web, aplicativos de IoT e back-ends móveis.
* O tempo de execução da área de trabalho. Fornece serviços básicos para aplicativos da área de trabalho do Windows, incluindo Windows Forms e WPF.

O download do tempo de execução inclui os seguintes componentes:

* Opcionalmente, o tempo de execução da área de trabalho ou ASP.NET Core.
* O [tempo de execução do .net](#clr). Fornece um sistema de tipos, carregamento de assembly, coletor de lixo, interoperabilidade nativa e outros serviços básicos.
* [Bibliotecas de tempo de execução](#runtime-libraries). Fornece tipos de dados primitivos e utilitários fundamentais.
* O  [driver](tools/index.md#driver)`dotnet`. Um comando da CLI que executa aplicativos dependentes da estrutura.

Para obter mais informações, consulte os seguintes recursos:

* [Visão geral do SDK do .NET](sdk.md)
* [Visão geral da CLI do .NET](tools/index.md)
* [Comando dotnet](tools/dotnet.md)

### <a name="project-system-and-msbuild"></a>Sistema de projeto e MSBuild

Um aplicativo .NET é criado a partir do código-fonte usando o [MSBuild](/visualstudio/msbuild/msbuild). Um arquivo de projeto (*. csproj*, *. fsproj* ou *. vbproj*) especifica [destinos](/visualstudio/msbuild/msbuild-targets) e [tarefas](/visualstudio/msbuild/msbuild-tasks) associadas que são responsáveis por compilar, empacotar e publicar código. Há identificadores do SDK que se referem a coleções padrão de destinos e tarefas. O uso desses identificadores ajuda a manter os arquivos de projeto pequenos e fáceis de trabalhar com o. Por exemplo, aqui está um arquivo de projeto para um aplicativo de console:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>
  </PropertyGroup>
</Project>
```

E aqui está um para um aplicativo Web:

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
  </PropertyGroup>
</Project>
```

Nesses exemplos, o `Sdk` atributo do `Project` elemento especifica um conjunto de destinos e tarefas do MSBuild que criam o projeto.  O `TargetFramework` elemento Especifica a versão do .NET da qual o aplicativo depende. Você pode editar o arquivo de projeto para adicionar outros destinos e tarefas específicos ao projeto.

Para obter mais informações, consulte [visão geral do SDK do projeto .net](project-sdk/overview.md) e [estruturas de destino](../standard/frameworks.md).

### <a name="cicd"></a>CI/CD

O MSBuild e a CLI do .NET podem ser usados com várias ferramentas de integração contínua e ambientes, como:

* [GitHub Actions](https://github.com/features/actions)
* [Azure DevOps](/azure/devops/user-guide/what-is-azure-devops)
* [BOLO](https://cakebuild.net/)
* [FALSA](https://fake.build/)

Para obter mais informações, consulte [usando o SDK e as ferramentas do .net na CI (integração contínua)](tools/using-ci-with-cli.md)

### <a name="nuget"></a>NuGet

O [NuGet](/nuget/what-is-nuget) é um Gerenciador de pacotes de código-fonte aberto projetado para .net. Um pacote NuGet é um arquivo *. zip* com a `.nupkg` extensão que contém código compilado (DLLs), outros arquivos relacionados a esse código e um manifesto descritivo que inclui informações como o número de versão do pacote. Desenvolvedores com código para compartilhar criar pacotes e publicá-los no [NuGet.org](https://nuget.org) ou em um host privado. Os desenvolvedores que desejam usar código compartilhado adicionam um pacote ao seu projeto e, em seguida, podem chamar a API exposta pelo pacote em seu código de projeto.

Para obter mais informações, consulte a [documentação do NuGet](/nuget/).

### <a name="net-interactive"></a>.NET Interativo

O .NET Interactive é um grupo de ferramentas de CLI e APIs que permitem aos usuários criar experiências interativas na Web, na redução e nos notebooks.

Para obter mais informações, consulte os seguintes recursos:

* [Tutorial do .NET In-Browser](https://dotnet.microsoft.com/learn/dotnet/in-browser-tutorial/1)
* [Usando blocos de anotações do .NET com o Jupyter em seu computador](https://github.com/dotnet/interactive/blob/main/docs/NotebooksLocalExperience.md)
* [Documentação interativa do .NET](https://github.com/dotnet/interactive/blob/main/docs/README.md)

## <a name="execution-models"></a>Modelos de execução

Os aplicativos .NET executam [código gerenciado](../standard/managed-code.md) em um ambiente de tempo de execução conhecido como CLR (Common Language Runtime).

### <a name="clr"></a>CLR

O .NET [CLR](../standard/clr.md) é um tempo de execução de plataforma cruzada que inclui suporte para Windows, MacOS e Linux. O CLR manipula a alocação e o gerenciamento de memória. O CLR também é uma máquina virtual que não só executa aplicativos, mas também gera e compila código usando um compilador JIT (just-in-time).

Para obter mais informações, consulte [visão geral do CLR (Common Language Runtime)](../standard/clr.md).

### <a name="jit-compiler-and-il"></a>Compilador JIT e IL

As linguagens .NET de nível mais alto , como C#, são compiladas em um conjunto de instruções independente de hardware, que é chamado de IL (linguagem intermediária). Quando um aplicativo é executado, o compilador JIT traduz o IL para o código do computador que o processador entende. A compilação JIT ocorre no mesmo computador em que o código vai ser executado.

Como a compilação JIT ocorre durante a execução do aplicativo, o tempo de compilação é parte do tempo de execução. Portanto, os compiladores JIT precisam balancear o tempo gasto otimizando o código contra as economias que o código resultante pode produzir. Mas um compilador JIT conhece o hardware real e pode liberar os desenvolvedores de ter que enviar diferentes implementações para diferentes plataformas.

O compilador JIT .NET pode fazer uma *compilação em camadas*, o que significa que ele pode recompilar métodos individuais em tempo de execução. Esse recurso permite que ele seja compilado rapidamente e ainda seja capaz de produzir uma versão altamente ajustada do código para métodos usados com frequência.

Para obter mais informações, consulte [processo de execução gerenciado](../standard/managed-execution-process.md) e [compilação em camadas](whats-new/dotnet-core-3-0.md#tiered-compilation).

### <a name="aot-compiler"></a>Compilador AOT

A experiência padrão para a maioria das cargas de trabalho do .NET é o compilador JIT, mas o .NET oferece duas formas de compilação de AOT (antecipação de tempo):

* Alguns cenários exigem a compilação da AOT de 100%. Um exemplo é [Ios](/xamarin/ios/).
* Em outros cenários, a maior parte do código de um aplicativo é compilada pela AOT, mas algumas são compiladas por JIT. Alguns padrões de código não são amigáveis para a AOT (como os genéricos). Um exemplo dessa forma de compilação AOT é a opção de publicação [pronta para execução](whats-new/dotnet-core-3-0.md#readytorun-images) . Essa forma de AOT oferece os benefícios da AOT sem suas desvantagens.

### <a name="automatic-memory-management"></a>Gerenciamento automático de memória

O GC ( *coletor de lixo* ) gerencia a alocação e a liberação de memória para aplicativos. Cada vez que seu código cria um novo objeto, o CLR aloca memória para o objeto a partir do [heap gerenciado](../standard/garbage-collection/fundamentals.md#the-managed-heap). Desde que exista espaço de endereço disponível no heap gerenciado, o runtime continua alocando espaço para novos objetos. Quando não houver espaço de endereço livre suficiente, o GC verificará se há objetos no heap gerenciado que não estão mais sendo usados pelo aplicativo. Em seguida, ele recupera essa memória.

O GC é um dos serviços CLR que ajuda a garantir a *segurança da memória*. Um programa é considerado de memória segura se ele acessa somente a memória alocada. Por exemplo, o runtime garante que um aplicativo não acesse memória não alocada além dos limites de uma matriz.

Para obter mais informações, consulte [gerenciamento automático de memória](../standard/automatic-memory-management.md) e [conceitos básicos da coleta de lixo](../standard/garbage-collection/fundamentals.md).

### <a name="working-with-unmanaged-resources"></a>Trabalhando com recursos não gerenciados

Às vezes, o código precisa fazer referência a *recursos não gerenciados*. Os recursos não gerenciados são recursos que não são mantidos automaticamente pelo runtime do .NET. Por exemplo, um identificador de arquivo é um recurso não gerenciado. Um objeto <xref:System.IO.FileStream> é um objeto gerenciado, mas ele faz referência a um identificador de arquivo, que não é gerenciado. Quando terminar de usar o <xref:System.IO.FileStream> , você precisará liberar explicitamente o identificador de arquivo.

No .NET, objetos que fazem referência a recursos não gerenciados implementam a interface <xref:System.IDisposable>. Quando você termina de usar o objeto, você chama o método <xref:System.IDisposable.Dispose> do objeto, responsável por liberar quaisquer recursos não gerenciados. As linguagens .NET fornecem uma `using` instrução conveniente ([C#](../csharp/language-reference/keywords/using.md), [F #](../fsharp/language-reference/resource-management-the-use-keyword.md), [VB](../visual-basic/language-reference/statements/using-statement.md)) que garante que o `Dispose` método seja chamado.

Para obter mais informações, consulte [limpando recursos não gerenciados](../standard/garbage-collection/unmanaged.md).

## <a name="deployment-models"></a>Modelos de implantação

Os aplicativos .NET podem ser publicados em dois modos diferentes:

* A *publicação de um aplicativo como independente* produz um arquivo executável que inclui o [tempo de execução](#sdk-and-runtimes) e as [bibliotecas](#runtime-libraries)do .net e o aplicativo e suas dependências. Os usuários do aplicativo podem executá-lo em um computador que não tem o tempo de execução do .NET instalado. Os aplicativos independentes são específicos da plataforma e, opcionalmente, podem ser publicados usando uma forma de [compilação AOT](#aot-compiler).

* A publicação de um aplicativo como *dependente da estrutura* produz um arquivo executável e arquivos binários (arquivos *. dll* ) que incluem apenas o próprio aplicativo e suas dependências. Os usuários do aplicativo precisam instalar o [tempo de execução](#sdk-and-runtimes)do .net separadamente. O arquivo executável é específico da plataforma, mas os arquivos *. dll* de aplicativos dependentes da estrutura são de plataforma cruzada.

  Você pode instalar várias versões do tempo de execução lado a lado para executar aplicativos dependentes da estrutura direcionados a diferentes versões do tempo de execução. Para obter mais informações, consulte [estruturas de destino](../standard/frameworks.md).

Os executáveis são produzidos para plataformas de destino específicas, que você especifica com um [RID (identificador de tempo de execução)](rid-catalog.md).

Para obter mais informações, consulte [visão geral da publicação de aplicativos .net](deploying/index.md) e [introdução ao .net e ao Docker](docker/introduction.md).

## <a name="runtime-libraries"></a>Bibliotecas de runtime

O .NET tem um conjunto padrão de bibliotecas de classes, conhecido como [bibliotecas de tempo de execução](../standard/glossary.md#runtime), bibliotecas de [estruturas](../standard/glossary.md#framework-libraries)ou a [BCL (biblioteca de classes base)](../standard/glossary.md#bcl). Essas bibliotecas fornecem implementações para muitos tipos específicos de carga de trabalho e de finalidade geral e funcionalidade de utilitário.

Aqui estão alguns exemplos de tipos definidos nas bibliotecas de tempo de execução do .NET:

* Tipos primitivos, como <xref:System.Boolean?displayProperty=nameWithType> e <xref:System.Int32?displayProperty=nameWithType> .
* Coleções, como <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> e <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType>.
* Tipos de dados, como <xref:System.Data.DataSet?displayProperty=nameWithType> e <xref:System.Data.DataTable?displayProperty=nameWithType> .
* Tipos de utilitário de rede, como <xref:System.Net.Http.HttpClient?displayProperty=nameWithType> .
* Tipos de utilitário de e [/s de arquivo e fluxo](../standard/io/index.md) , como <xref:System.IO.FileStream?displayProperty=nameWithType> e <xref:System.IO.TextWriter?displayProperty=nameWithType> .
* Tipos de utilitário de [serialização](../standard/serialization/index.md) , como <xref:System.Text.Json.JsonSerializer?displayProperty=nameWithType> e <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> .
* Tipos de alto desempenho, como <xref:System.Span%601?displayProperty=nameWithType> <xref:System.Numerics.Vector?displayProperty=nameWithType> [pipelines](../standard/io/pipelines.md), e.

Para obter mais informações, consulte [visão geral das bibliotecas de tempo de execução](../standard/runtime-libraries-overview.md). O código-fonte para as bibliotecas está no [repositório de dotnet/tempo de execução do GitHub](https://github.com/dotnet/runtime/tree/master/src/libraries).

### <a name="extensions-to-the-runtime-libraries"></a>Extensões para as bibliotecas de tempo de execução

As bibliotecas para algumas funcionalidades de aplicativos comumente usadas não estão incluídas nas bibliotecas de tempo de execução, mas são disponibilizadas em pacotes NuGet, como o seguinte:

| Pacote NuGet | Documentação |
|---------|---------|
| [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting) | [Gerenciamento de tempo de vida do aplicativo (host genérico)](extensions/generic-host.md) |
| [Microsoft. Extensions. DependencyInjection](https://www.nuget.org/packages/Microsoft.Extensions.DependencyInjection) | [DI (injeção de dependência)](extensions/dependency-injection.md)
| [Microsoft.Extensions.Configuração](https://www.nuget.org/packages/Microsoft.Extensions.Configuration) | [Configuration](extensions/configuration.md) |
| [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging) | [Registro em log](extensions/logging.md) |
| [Microsoft. Extensions. opções](https://www.nuget.org/packages/Microsoft.Extensions.Options) | [Padrão de opções](extensions/options.md) |

Para obter mais informações, consulte o [repositório dotnet/extensões no GitHub](https://github.com/dotnet/extensions).

## <a name="data-access"></a>Acesso de dados

O .NET fornece um ORM (objeto/mapeador relacional) e uma maneira de escrever consultas SQL no código.

### <a name="entity-framework-core"></a>Entity Framework Core

O Entity Framework (EF) Core é uma tecnologia de acesso a [dados de software](https://github.com/aspnet/EntityFrameworkCore) livre e entre plataformas que pode servir como um ORM. EF Core permite trabalhar com um banco de dados referindo-se a objetos .NET no código. Ele reduz a quantidade de código de acesso a dados que, de outra forma, você precisaria escrever e testar. O EF Core dá suporte a vários mecanismos de banco de dados.

Para obter mais informações, consulte [Entity Framework Core](/ef/core/) e [provedores de banco de dados](/ef/core/providers/).

### <a name="linq"></a>LINQ

A consulta integrada à linguagem (LINQ) permite que você escreva um código declarativo para operar em dados. Os dados podem ser de várias formas (como objetos na memória, um banco de dados SQL ou um documento XML), mas o código LINQ que você escreve não difere para cada fonte de dados.

Para obter mais informações, consulte [visão geral do LINQ (consulta integrada à linguagem)](../standard/linq/index.md).

## <a name="net-terminology"></a>Terminologia do .NET

Para entender a documentação do .NET, ele pode ajudar a saber como o uso de alguns termos mudou ao longo do tempo.

### <a name="net-core-and-net-5"></a>.NET Core e .NET 5

No 2002, a Microsoft lançou o [.NET Framework](../framework/get-started/overview.md), uma plataforma de desenvolvimento para a criação de aplicativos do Windows. Hoje .NET Framework está na versão 4,8 e ainda [tem suporte da Microsoft](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework).

Em 2014, a Microsoft começou a escrever um sucessor de software livre entre plataformas para .NET Framework. Essa nova implementação do .NET foi denominada .NET Core até atingir a versão 3,1. A próxima versão após o .NET Core 3,1 é o .NET 5,0, que está atualmente em versão prévia. O número de versão 4 foi ignorado para evitar confusão entre esta implementação do .NET e .NET Framework 4,8. O nome "Core" foi Descartado para tornar claro que essa é agora a principal implementação do .NET.

Este artigo é sobre o .NET 5, mas grande parte da documentação do .NET 5 ainda tem referências a ".NET Core" ou ".NET Framework". Além disso, "Core" permanece nos nomes [ASP.NET Core](/aspnet/core/) e [Entity Framework Core](/ef/core/).

A documentação também se refere a .NET Standard. [.Net Standard](../standard/net-standard.md) é uma especificação de API que permite desenvolver bibliotecas de classes para várias implementações do .net.

Para obter mais informações, consulte [componentes arquitetônicos .net](../standard/components.md).

### <a name="overloaded-terms"></a>Termos sobrecarregados

Algumas das terminologias do .NET podem ser confusas porque a mesma palavra é usada de maneiras diferentes em diferentes contextos. Aqui estão algumas das instâncias mais proeminentes:

* **appmodel**

  |Contexto  |"tempo de execução" significando |
  |---------|---------|
  | [CLR (Common Language Runtime)](#clr)| O ambiente de execução de um programa gerenciado. O sistema operacional faz parte do ambiente de tempo de execução, mas não faz parte do tempo de execução do .NET. |
  | [Tempo de execução do .NET na página de download do .NET](https://dotnet.microsoft.com/download/dotnet-core) | As bibliotecas [CLR](#clr) e [Runtime](#runtime-libraries), que juntas fornecem suporte para a execução de aplicativos [dependentes da estrutura](#deployment-models) . A página também oferece opções de tempo de execução para aplicativos do ASP.NET Core Server e aplicativos da área de trabalho do Windows. |
  | [Identificador de tempo de execução (RID)](rid-catalog.md) | A plataforma do sistema operacional e a arquitetura de CPU em que um aplicativo .NET é executado. Por exemplo: Windows x64, Linux x64. |

* **Framework**

  |Contexto  | "estrutura" significando |
  |---------|---------------------|
  | .NET Framework | A implementação original somente do Windows do .NET. "Framework" está em letras maiúsculas. |
  | estrutura de destino | A coleção de APIs da qual um aplicativo ou biblioteca do .NET depende. Exemplos: .NET Core 3,1, .NET Standard 2,0 |
  | TFM (Moniker de Estrutura de Destino)  | Um TFM é um formato de token padronizado para especificar a estrutura de destino de um aplicativo ou biblioteca .NET. Exemplo: `net462` para .NET Framework 4.6.2. |
  | aplicativo dependente de estrutura | Um aplicativo que só pode ser executado em um computador em que você instalou o tempo de execução da [página de download do .net](https://dotnet.microsoft.com/download/dotnet-core). "Estrutura" nesse uso é a mesma coisa que o "tempo de execução" que você baixa da página de download do .NET. |
  | bibliotecas do Framework | Às vezes, usado como sinônimo para [bibliotecas de tempo de execução](#runtime-libraries). |

* **SDK**

  |Contexto  | "SDK" significando |
  |---------|---------------|
  | [SDK na página de download do .NET](#sdk-and-runtimes)  | Uma coleção de ferramentas e bibliotecas que você baixa e instala para desenvolver e executar aplicativos .NET. Inclui a CLI, o MSBuild, o tempo de execução do .NET e outros componentes.|
  | [Projeto no estilo SDK](#project-system-and-msbuild) | Um conjunto de destinos e tarefas do MSBuild que especifica como criar um projeto para um tipo de aplicativo específico. O SDK, nesse sentido, é especificado usando o `Sdk` atributo do `Project` elemento em um arquivo de projeto. |

* **platform**

  |Contexto  | "plataforma" significa |
  |---------|--------------------|
  | plataforma cruzada | Neste termo, "plataforma" significa um sistema operacional e o hardware em que ele é executado, como Windows, macOS, Linux, iOS e Android. |
  | Plataforma .NET | O uso varia. A referência pode ser para uma implementação do .NET (como .NET Framework ou .NET 5) ou para um conceito abrangente de .NET, incluindo todas as implementações. |

Para obter mais informações sobre a terminologia do .NET, consulte o [Glossário do .net](../standard/glossary.md).

## <a name="advanced-scenarios"></a>Cenários avançados

As seções a seguir explicam alguns recursos do .NET que são úteis em cenários avançados.

### <a name="native-interop"></a>Interoperabilidade nativa

Todos os sistemas operacionais incluem uma API (interface de programação de aplicativo) que fornece serviços de sistema. O .NET fornece várias maneiras de chamar essas APIs.

A principal maneira de interoperar com APIs nativas é por meio de "invocação de plataforma" ou P/Invoke para curto. P/Invoke tem suporte em plataformas Linux e Windows. Uma maneira somente Windows de interoperação é conhecida como "interoperabilidade COM", que funciona com [componentes com](/cpp/atl/introduction-to-com) em código gerenciado. Ela foi desenvolvida com base na infraestrutura de P/Invoke, mas funciona de maneiras levemente diferentes.

Para obter mais informações, consulte [interoperabilidade nativa](../standard/native-interop/index.md).

### <a name="unsafe-code"></a>Código não seguro

Dependendo do suporte da linguagem, o CLR permite acessar a memória nativa e realizar aritmética de ponteiro por meio de código `unsafe`. Essas operações são necessárias para certos algoritmos e interoperabilidade do sistema. Embora seja eficiente, o uso de código não seguro é desencorajado, a menos que seja necessário interoperar com as APIs do sistema ou implementar o algoritmo mais eficiente. O código não seguro pode não ser executado da mesma maneira em ambientes diferentes e também perde os benefícios de um coletor de lixo e da segurança de tipos. Recomenda-se restringir e centralizar ao máximo o código não seguro, além de testar esse código detalhadamente.

Para obter mais informações, consulte [código e ponteiros sem segurança](../csharp/programming-guide/unsafe-code-pointers/index.md).

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Escolher um tutorial do .NET](tutorials/index.md)

> [!div class="nextstepaction"]
> [Experimente o .NET em seu navegador](../csharp/tutorials/intro-to-csharp/numbers-in-csharp.yml)

> [!div class="nextstepaction"]
> [Faça um tour de C #](../csharp/tour-of-csharp/index.md)

> [!div class="nextstepaction"]
> [Faça um tour de F #](../fsharp/tour.md)
