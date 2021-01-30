---
title: Ferramentas adicionais
description: Uma visão geral das ferramentas adicionais que você pode instalar que dão suporte e estendem a funcionalidade do .NET.
author: mlacouture
ms.date: 02/13/2020
ms.custom: mvc
ms.openlocfilehash: 243f2da1c6f7809ac710c9700ea4cbde6f289295
ms.sourcegitcommit: 68c9d9d9a97aab3b59d388914004b5474cf1dbd7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2021
ms.locfileid: "99216389"
---
# <a name="net-additional-tools-overview"></a>Visão geral das ferramentas adicionais do .NET

Esta seção compila uma lista de ferramentas que dão suporte e ampliam a funcionalidade do .NET, além da CLI do .NET.

## <a name="net-uninstall-tool"></a>Ferramenta de desinstalação do .NET

A [ferramenta de desinstalação do .net](https://github.com/dotnet/cli-lab/releases) ( `dotnet-core-uninstall` ) permite que você limpe SDKs e tempos de execução do .net em um sistema, de modo que apenas as versões especificadas permaneçam. Uma coleção de opções está disponível para especificar quais versões são desinstaladas.

## <a name="net-diagnostic-tools"></a>Ferramentas de diagnóstico do .NET

[dotnet-os contadores](../diagnostics/dotnet-counters.md) são uma ferramenta de monitoramento de desempenho para a investigação de desempenho e monitoramento de integridade de primeiro nível.

[dotnet-o despejo](../diagnostics/dotnet-dump.md) fornece uma maneira de coletar e analisar despejos do Windows e do Linux Core sem um depurador nativo.

[dotnet-gcdump](../diagnostics/dotnet-gcdump.md) fornece uma maneira de coletar despejos de GC (coletor de lixo) de processos do .net em tempo real.

[dotnet-Trace](../diagnostics/dotnet-trace.md) coleta dados de criação de perfil de seu aplicativo que podem ajudar em cenários em que você precisa descobrir o que faz com que um aplicativo seja executado lentamente.

## <a name="net-install-tool-for-extension-authors"></a>Ferramenta de instalação do .NET para autores de extensão

A [ferramenta de instalação do .net para autores de extensão](https://github.com/dotnet/vscode-dotnet-runtime) é uma extensão Visual Studio Code que permite a aquisição do tempo de execução do .net especificamente para autores de extensão vs Code. Essa ferramenta deve ser utilizada em extensões que são escritas em .NET e exigem que o .NET inicialize as partes da extensão (por exemplo, um servidor de idioma). A extensão não deve ser usada diretamente pelos usuários para instalar o .NET para desenvolvimento.

## <a name="wcf-web-service-reference-tool"></a>Ferramenta de referência do serviço Web WCF

A ferramenta de referência do [serviço Web](wcf-web-service-reference-guide.md) WCF (Windows Communication Foundation) é um provedor de serviço conectado do Visual Studio que fez sua estréia no [Visual Studio 2017 versão 15,5](/visualstudio/releasenotes/vs2017-relnotes-v15.5#WCFTools). Essa ferramenta recupera metadados de um serviço Web na solução atual, em um local de rede ou em um arquivo WSDL. Ele gera um arquivo de origem compatível com o .NET, definindo uma classe proxy WCF com métodos que você pode usar para acessar as operações do serviço Web.

## <a name="wcf-dotnet-svcutil-tool"></a>Ferramenta dotnet-svcutil do WCF

A ferramenta do WCF [dotnet-SvcUtil](dotnet-svcutil-guide.md) é uma ferramenta .NET que recupera metadados de um serviço Web em um local de rede ou em um arquivo WSDL. Ele gera um arquivo de origem compatível com o .NET, definindo uma classe proxy WCF com métodos que você pode usar para acessar as operações do serviço Web.

A ferramenta **dotnet-SvcUtil** é uma alternativa para o provedor de serviços conectados do [**WCF Web Service Reference**](wcf-web-service-reference-guide.md) do Visual Studio, que foi enviado pela primeira vez com o Visual Studio 2017 versão 15,5. A ferramenta **dotnet-SvcUtil** , como uma ferramenta .net, está disponível no Linux, no MacOS e no Windows.

## <a name="wcf-dotnet-svcutilxmlserializer-tool"></a>Ferramenta dotnet-svcutil.xmlserializer da WCF

No .NET Framework, é possível gerar previamente um assembly de serialização usando a ferramenta svcutil. A [ ferramenta do serializadordotnet-svcutil.xml](dotnet-svcutil.xmlserializer-guide.md) do WCF fornece funcionalidade semelhante no .NET 5 (e no .NET Core) e versões posteriores. Ele gera previamente o código de serialização C# para os tipos no aplicativo cliente, que são usados pelo Contrato de Serviço da WCF e podem ser serializados pelo <xref:System.Xml.Serialization.XmlSerializer>. Isso melhora o desempenho de inicialização da serialização de XML ao serializar ou desserializar objetos desses tipos.

## <a name="xml-serializer-generator"></a>Gerador de serializador de XML

Assim como o [gerador de serializador XML (sgen.exe)](../../standard/serialization/xml-serializer-generator-tool-sgen-exe.md) para o .NET Framework, o [ pacote NuGet do serializadorMicrosoft.Xml. Generator](https://www.nuget.org/packages/Microsoft.XmlSerializer.Generator) é a solução para bibliotecas direcionadas ao .NET 5 (e ao .NET Core) e versões posteriores. Ele cria um assembly de serialização de XML para tipos contidos em um assembly a fim de melhorar o desempenho de inicialização da serialização de XML ao serializar ou desserializar objetos desses tipos usando <xref:System.Xml.Serialization.XmlSerializer>.

## <a name="generating-self-signed-certificates"></a>Gerando certificados Self-Signed

Você pode usar o [dotnet dev-certs](self-signed-certificates-guide.md) para criar certificados autoassinados para cenários de desenvolvimento e teste.
