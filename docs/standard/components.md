---
title: Componentes de arquitetura do .NET
description: Descreve os componentes de arquitetura do .NET, como .NET Standard, implementações .NET, tempos de execução .NET e ferramentas.
author: cartermp
ms.date: 10/05/2020
ms.openlocfilehash: c5f174034ce0cd0e1cf0b799c7b3f4bff99447a2
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100423129"
---
# <a name="net-architectural-components"></a>Componentes de arquitetura do .NET

Um aplicativo .NET é desenvolvido para e é executado em uma ou mais *implementações do .NET*. As implementações do .NET incluem o .NET Framework, o .NET 5 (e o .NET Core) e o mono. Há uma especificação de API comum a várias implementações do .NET que é chamada .NET Standard. Este artigo fornece uma breve introdução a cada um desses conceitos.

## <a name="net-standard"></a>.NET Standard

.NET Standard é um conjunto de APIs que são implementadas pela biblioteca de classes base de uma implementação do .NET. De maneira mais formal, é uma especificação das APIs do .NET que compõem um conjunto uniforme de contratos nos quais você compila seu código. Esses contratos são implementados em várias implementações do .NET.

.NET Standard é uma [estrutura de destino](glossary.md#target-framework). Se seu código tiver como alvo uma versão do .NET Standard, ele poderá ser executado em qualquer implementação do .NET que dê suporte a essa versão do .NET Standard.

.NET Standard foi criado para permitir a portabilidade entre diferentes implementações do .NET, mas agora o .NET 5 oferece uma maneira melhor de compartilhar código em várias plataformas e cargas de trabalho. Para obter mais informações, consulte [.NET 5 e .net Standard](net-standard.md#net-5-and-net-standard).

## <a name="net-implementations"></a>Implementações do .NET

Cada implementação do .NET inclui os seguintes componentes:

- Um ou mais runtimes. Exemplos: .NET Framework CLR, .NET 5 CLR.
- Uma biblioteca de classes. Exemplos: .NET Framework biblioteca de classes base, biblioteca de classes base do .NET 5.
- Opcionalmente, uma ou mais estruturas de aplicativo. Exemplos: [ASP.net](https://www.asp.net/), [Windows Forms](/dotnet/desktop/winforms/windows-forms-overview)e [Windows Presentation Foundation (WPF)](/dotnet/desktop/wpf/) estão incluídos no .NET Framework e no .NET 5.
- Opcionalmente, ferramentas de desenvolvimento. Algumas ferramentas de desenvolvimento são compartilhadas entre várias implementações.

Há quatro implementações do .NET às quais a Microsoft dá suporte:

- .NET 5 (e .NET Core) e versões posteriores
- .NET Framework
- Mono
- UWP

O .NET 5 agora é a principal implementação, aquela que é o foco do desenvolvimento em andamento. O .NET 5 foi criado em uma única base de código que dá suporte a várias plataformas e várias cargas de trabalho, como aplicativos de desktop do Windows e aplicativos de console entre plataformas, serviços de nuvem e sites.

### <a name="net-5"></a>.NET 5

O .NET 5 é uma implementação de plataforma cruzada do .NET que foi projetada para lidar com cargas de trabalho de servidor e nuvem em escala. Ele também dá suporte a outras cargas de trabalho, incluindo aplicativos de desktop. Ele é executado no Windows, no macOS e no Linux. Ele implementa .NET Standard, portanto, o código que tem como alvo .NET Standard pode ser executado no .NET 5. [ASP.NET Core](https://dotnet.microsoft.com/learn/aspnet/what-is-aspnet-core), [Windows Forms](/dotnet/desktop/winforms/windows-forms-overview)e [Windows Presentation Foundation (WPF)](/dotnet/desktop/wpf/) são executados no .NET 5.

Para obter mais informações, consulte os seguintes recursos:

- [Introdução ao .NET](../core/introduction.md)
- [Escolhendo entre o .NET 5 e o .NET Framework para aplicativos de servidor](choosing-core-framework-server.md)
- [.NET 5 e .NET Standard](net-standard.md#net-5-and-net-standard)

### <a name="net-framework"></a>.NET Framework

.NET Framework é a implementação original do .NET que existia desde 2002. As versões 4,5 e posteriores implementam .NET Standard, portanto, o código que tem como destino .NET Standard pode ser executado nessas versões do .NET Framework. Ele contém APIs adicionais específicas do Windows, como APIs para desenvolvimento de área de trabalho do Windows com o Windows Forms e o WPF. O .NET Framework é otimizado para a compilação de aplicativos da área de trabalho do Windows.

Para obter mais informações, consulte o [Guia de .NET Framework](../framework/index.yml).

### <a name="mono"></a>Mono

O Mono é uma implementação do .NET que é usada principalmente quando um pequeno runtime é necessário. É o tempo de execução que capacita aplicativos Xamarin no Android, macOS, iOS, tvOS e watchOS e concentra-se principalmente em uma pequena superfície. O Mono também é plataforma para jogos criados com o mecanismo Unity.

Ele dá suporte a todas as versões do .NET Standard publicadas atualmente.

Historicamente, o Mono implementava a maior API do .NET Framework e emulava alguns dos recursos mais populares do Unix. Às vezes, ele é usado para executar aplicativos .NET que dependem desses recursos no Unix.

O Mono normalmente é usado com um compilador Just-In-Time, mas ele também apresenta um compilador estático completo (compilação Ahead Of Time) que é usado em plataformas como iOS.

Para obter mais informações, consulte a [documentação do mono](https://www.mono-project.com/docs/).

### <a name="universal-windows-platform-uwp"></a>Plataforma Universal do Windows (UWP)

A UWP é uma implementação do .NET que é usada para criar aplicativos do Windows modernos e sensíveis ao toque, bem como software para a IoT (Internet das Coisas). Ele foi projetado para unificar os diferentes tipos de dispositivos que você talvez queira direcionar, incluindo PCs, tablets, telefones e até mesmo o Xbox. A UWP fornece muitos serviços, como um repositório centralizado de aplicativos, um ambiente de execução (AppContainer) e um conjunto de APIs do Windows para usar em vez das APIS do Win32 (WinRT). Os aplicativos podem ser escritos em C++, C#, Visual Basic e JavaScript.

Para obter mais informações, consulte [introdução ao plataforma universal do Windows](/windows/uwp/get-started/universal-application-platform-guide).

## <a name="net-runtimes"></a>Runtimes do .NET

Um runtime é o ambiente de execução de um programa gerenciado. O SO faz parte do ambiente do runtime, mas não faz parte do runtime do .NET. Aqui estão alguns exemplos de runtimes do .NET:

- CLR (Common Language Runtime) para .NET Framework
- CLR (Common Language Runtime) para .NET 5
- .NET Native para a Plataforma Universal do Windows
- O runtime Mono para Xamarin.iOS, Xamarin.Android, Xamarin.Mac e a estrutura de área de trabalho do Mono

## <a name="net-tooling-and-common-infrastructure"></a>Ferramentas do .NET e infraestrutura comum

Você tem acesso a um amplo conjunto de ferramentas e componentes de infraestrutura que funcionam com todas as implementações do .NET. Essas ferramentas e componentes incluem:

- As linguagens do .NET e seus compiladores
- O sistema de projetos do .NET (com base em arquivos *.csproj*, *.vbproj* e *.fsproj*)
- [MSBuild](/visualstudio/msbuild/msbuild), o mecanismo de compilação usado para criar projetos
- [NuGet](/nuget/), Gerenciador de pacotes da Microsoft para .net
- Ferramentas de orquestração de build em software livre, como [CAKE](https://cakebuild.net/) e [FAKE](https://fake.build/)

Para obter mais informações, consulte [ferramentas e produtividade](../core/introduction.md#tools-and-productivity).

## <a name="applicable-standards"></a>Padrões aplicáveis

A linguagem C# e as especificações de Common Language Infrastructure (CLI) são padronizadas por meio de [ECMA International &reg; ](https://www.ecma-international.org/). As primeiras edições desses padrões foram publicadas pela ECMA em dezembro de 2001.

As revisões subsequentes para os padrões foram desenvolvidas pelos grupos de tarefas TC49-TG2 (C#) e TC49-TG3 (CLI) no comitê técnico de linguagens de programação ([TC49](https://www.ecma-international.org/memento/tc49.htm)) e adotadas pelo assembly geral da ECMA e subsequentemente por ISO/IEC JTC 1 por meio do processo ISO Fast-Track.

### <a name="latest-standards"></a>Padrões mais recentes

Os documentos ECMA oficiais a seguir estão disponíveis para [C#](http://www.ecma-international.org/publications/standards/Ecma-334.htm) e a [CLI](http://www.ecma-international.org/publications/standards/Ecma-335.htm) ([TR-84](http://www.ecma-international.org/publications/techreports/E-TR-084.htm)):

- **O padrão de linguagem C# (versão 5,0)**: [ECMA-334.pdf](https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-334.pdf)
- **O Common Language Infrastructure**: [ECMA-335.pdf](https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-335.pdf).
- **Informações derivadas do arquivo XML da partição IV**: [ECMA-084.pdf](https://www.ecma-international.org/publications/files/ECMA-TR/ECMA%20TR-084.pdf) formato.

Os documentos ISO/IEC oficiais estão disponíveis na página de padrões do ISO/IEC [publicamente disponível](https://standards.iso.org/ittf/PubliclyAvailableStandards/) . Esses links são diretos dessa página:

- **Tecnologia da informação-linguagens de programação-C#**: [ISO/IEC 23270:2018](https://standards.iso.org/ittf/PubliclyAvailableStandards/c075178_ISO_IEC_23270_2018.zip)
- **Tecnologia da informação — partições de Common Language Infrastructure (CLI) I para vi**: [ISO/IEC 23271:2012](https://standards.iso.org/ittf/PubliclyAvailableStandards/c058046_ISO_IEC_23271_2012(E).zip)
- **Tecnologia da informação — Common Language Infrastructure (CLI) — relatório técnico sobre informações derivadas do arquivo XML da partição IV**: [ISO/IEC TR 23272:2011](https://standards.iso.org/ittf/PubliclyAvailableStandards/c057955_ISO_IEC_TR_23272_2011.zip)

## <a name="see-also"></a>Consulte também

- [Introdução ao .NET](../core/introduction.md)
- [Introdução .NET Standard](net-standard.md)
- [Escolhendo entre o .NET 5 e o .NET Framework para aplicativos de servidor](choosing-core-framework-server.md)
- [Guia do .NET Framework](../framework/index.yml)
- [Guia do C#](../csharp/index.yml)
- [Guia do F#](../fsharp/index.yml)
- [Guia do Visual Basic](../visual-basic/index.yml)
