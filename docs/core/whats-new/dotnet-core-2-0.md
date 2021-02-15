---
title: Novidades do .NET Core 2.0
description: Conheça os novos recursos encontrados no .NET Core.
ms.date: 08/13/2017
ms.openlocfilehash: bdca38d1584107727fe8e20b80ab2337f4cb05f1
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223719"
---
# <a name="whats-new-in-net-core-20"></a>Novidades do .NET Core 2.0

O .NET Core 2.0 contém melhorias e novos recursos nas seguintes áreas:

- [Ferramentas](#tooling)
- [Suporte ao idioma](#language-support)
- [Aprimoramentos da plataforma](#platform-improvements)
- [Alterações de API](#api-changes-and-library-support)
- [integração com o Visual Studio](#visual-studio-integration)
- [Melhorias na documentação](#documentation-improvements)

## <a name="tooling"></a>Ferramentas

### <a name="dotnet-restore-runs-implicitly"></a>dotnet restore é executado implicitamente

Em versões anteriores do .NET Core, era preciso executar o comando [dotnet restore](../tools/dotnet-restore.md) para baixar dependências logo após a criação de um novo projeto com o comando [dotnet new](../tools/dotnet-new.md), bem como sempre que uma nova dependência era adicionada ao seu projeto.

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

Você também pode desabilitar a invocação automática do `dotnet restore` transmitindo a opção `--no-restore` para os comandos `new`, `run`, `build`, `publish`, `pack` e `test`.

### <a name="retargeting-to-net-core-20"></a>Redirecionar para o .NET Core 2.0

Se o SDK do .NET Core 2.0 estiver instalado, os projetos destinados ao .NET Core 1.x poderão ser redirecionados para o .NET Core 2.0.

Para redirecionar para o .NET Core 2.0, edite o arquivo do projeto alterando o valor do elemento `<TargetFramework>` (ou o elemento `<TargetFrameworks>` se você tiver mais de um destino no seu arquivo de projeto) de 1.x para 2.0:

```xml
<PropertyGroup>
    <TargetFramework>netcoreapp2.0</TargetFramework>
 </PropertyGroup>
```

Você também pode redirecionar bibliotecas do .NET Standard para o .NET Standard 2.0 da mesma maneira:

```xml
<PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
 </PropertyGroup>
```

Para mais informações sobre como migrar seu projeto para o .NET Core 2.0, confira [Migrar do ASP.NET Core 1.x para o ASP.NET Core 2.0](/aspnet/core/migration/1x-to-2x/index).

## <a name="language-support"></a>Suporte ao idioma

Além do suporte a C# e F#, o .NET Core 2.0 também suporta Visual Basic.

### <a name="visual-basic"></a>Visual Basic

Com a versão 2.0, o .NET Core agora oferece suporte para o Visual Basic 2017. Você pode usar o Visual Basic para criar os seguintes tipos de projeto:

- Aplicativo de console do .NET Core
- Bibliotecas de classe do .NET Core
- Bibliotecas de classe do .NET Standard
- Projetos de testes de unidade do .NET Core
- Projetos de testes de xUnit do .NET Core

Por exemplo, para criar um aplicativo "Olá, Mundo" do Visual Basic, siga as seguintes etapas da linha de comando:

1. Abra uma janela do console, crie um diretório para seu projeto e torne-o o diretório atual.

1. Digite o comando `dotnet new console -lang vb`.

   O comando cria um arquivo de projeto com uma extensão de arquivo `.vbproj`, junto com um arquivo de código-fonte do Visual Basic chamado *Program.vb*. Este arquivo contém o código-fonte para gravar a cadeia de caracteres "Olá, Mundo!" na janela do console.

1. Digite o comando `dotnet run`. A [CLI do .NET Core](../tools/index.md) compila e executa automaticamente o aplicativo, que exibe a mensagem "Olá, Mundo!" na janela do console.

### <a name="support-for-c-71"></a>Suporte para C# 7.1

O .NET Core 2.0 suporta C# 7.1, que adiciona uma série de novos recursos, incluindo:

- O método `Main`, o ponto de entrada do aplicativo, pode ser marcado com a palavra-chave [async](../../csharp/language-reference/keywords/async.md).
- Nomes de tuplas inferidos.
- Expressões padrão.

<!-- For more information see [link to C# what's new](url). -->

## <a name="platform-improvements"></a>Aprimoramentos da plataforma

O .NET Core 2.0 inclui uma série de recursos que facilitam a instalação do .NET Core e o uso dele em sistemas operacionais com suporte.

### <a name="net-core-for-linux-is-a-single-implementation"></a>O .NET Core para Linux é uma implementação única

O .NET Core 2.0 oferece uma implementação única do Linux que funciona em várias distribuições do Linux. O .NET Core 1.x requer que você baixe uma implementação do Linux específica para distribuição.

Você também pode desenvolver aplicativos destinados ao Linux como um sistema operacional único. O .NET Core 1.x requer que você direcione cada distribuição do Linux separadamente.

### <a name="support-for-the-apple-cryptographic-libraries"></a>Suporte para as bibliotecas criptográficas da Apple

O .NET Core 1.x no macOS exigia a biblioteca criptográfica do kit de ferramentas OpenSSL. O .NET Core 2.0 usa as bibliotecas criptográficas da Apple e não requer o OpenSSL, portanto, não é mais preciso instalá-lo.

## <a name="api-changes-and-library-support"></a>Alterações de API e suporte à biblioteca

### <a name="support-for-net-standard-20"></a>Suporte para .NET Standard 2.0

.NET Standard define um conjunto com controle de versão de APIs que deve estar disponível em implementações do .NET que estão em conformidade com essa versão do padrão. .NET Standard é destinada aos desenvolvedores de biblioteca. Ele visa garantir a funcionalidade disponível para uma biblioteca que se destina a uma versão do .NET Standard em cada implementação do .NET. O .NET Core 1. x suporta .NET Standard versão 1,6; o .NET Core 2,0 oferece suporte à versão mais recente, .NET Standard 2,0. Para obter mais informações, confira [.NET Standard](../../standard/net-standard.md).

.NET Standard 2,0 inclui mais de 20.000 mais APIs do que estavam disponíveis em .NET Standard 1,6. A maior parte dessa área de superfície expandida resulta da incorporação de APIs que são comuns ao .NET Framework e Xamarin no .NET Standard.

.NET Standard bibliotecas de classe 2,0 também podem referenciar .NET Framework bibliotecas de classes, desde que elas chamem as APIs que estão presentes no .NET Standard 2,0. Nenhuma recompilação das bibliotecas do .NET Framework é necessária.

Para obter uma lista das APIs que foram adicionadas ao .NET Standard desde sua última versão, .NET Standard 1,6, consulte [.NET Standard 2,0 vs. 1,6](https://raw.githubusercontent.com/dotnet/standard/master/docs/versions/netstandard2.0_diff.md).

### <a name="expanded-surface-area"></a>Área de superfície expandida

O número total de APIs disponíveis no .NET Core 2.0 mais que dobrou em comparação com o .NET Core 1.1.

E com o [Pacote de Compatibilidade do Windows](../porting/windows-compat-pack.md), a portabilidade do .NET Framework também se tornou muito mais simples.

### <a name="support-for-net-framework-libraries"></a>Suporte a bibliotecas do .NET Framework

O código .NET Core pode fazer referência a bibliotecas existentes do .NET Framework, incluindo pacotes do NuGet. Observe que as bibliotecas devem usar APIs que são encontradas no .NET Standard.

## <a name="visual-studio-integration"></a>integração com o Visual Studio

O Visual Studio 2017 versão 15.3 e, em alguns casos, o Visual Studio para Mac oferece vários aprimoramentos significativos para os desenvolvedores do .NET Core.

### <a name="retargeting-net-core-apps-and-net-standard-libraries"></a>Redirecionamento de aplicativos .NET Core e bibliotecas do .NET Standard

Se o SDK do .NET Core 2.0 estiver instalado, você poderá redirecionar projetos do .NET Core 1.x para o .NET Core 2.0 e bibliotecas do .NET Standard 1.x para o .NET Standard 2.0.

Para redirecionar seu projeto no Visual Studio, abra a guia **Aplicativo** da caixa de diálogo de propriedades do projeto e altere o valor **Estrutura de destino** para **.NET Core 2.0** ou **.NET Standard 2.0**. Você também pode alterar clicando com o botão direito do mouse no projeto e selecionando a opção **Editar \*arquivo .csproj**. Para obter mais informações, confira a seção [Ferramentas](#tooling) neste tópico.

### <a name="live-unit-testing-support-for-net-core"></a>Suporte a Live Unit Testing para .NET Core

Sempre que você modifica o código, o Live Unit Testing executa os testes de unidade afetados automaticamente em segundo plano e exibe os resultados e a cobertura de código de forma dinâmica no ambiente do Visual Studio. O .NET Core 2.0 agora oferece suporte ao Live Unit Testing. Anteriormente, o Live Unit Testing estava disponível somente para aplicativos do .NET Framework.

Para obter mais informações, consulte [Live Unit Testing com o Visual Studio](/visualstudio/test/live-unit-testing) e as [perguntas frequentes sobre Live Unit Testing](/visualstudio/test/live-unit-testing-faq).

### <a name="better-support-for-multiple-target-frameworks"></a>Melhor suporte a várias estruturas de destino

Se você estiver criando um projeto para várias estruturas de destino, selecione a plataforma de destino no menu de nível superior. Na imagem a seguir, um projeto chamado SCD1 é direcionado ao macOS X 10.11 (`osx.10.11-x64`) de 64 bits e ao Windows 10/Windows Server 2016 (`win10-x64`) de 64 bits. Selecione a estrutura de destino antes de selecionar o botão do projeto, neste caso para executar um build de depuração.

![Captura de tela mostrando a seleção da estrutura de destino durante a criação de um projeto.](./media/dotnet-core-2-0/target-framework-selection.png)

### <a name="side-by-side-support-for-net-core-sdks"></a>Suporte lado a lado para SDKs do .NET Core

Agora você pode instalar o SDK do .NET Core independentemente do Visual Studio. Isso possibilita que uma única versão do Visual Studio crie projetos destinados a diferentes versões do .NET Core. Anteriormente, o Visual Studio e o SDK do .NET Core foram acoplados; uma versão específica do SDK acompanhava uma versão específica do Visual Studio.

## <a name="documentation-improvements"></a>Melhorias na documentação

### <a name="net-application-architecture"></a>Arquitetura do Aplicativo .NET

A [Arquitetura do Aplicativo .NET](https://dotnet.microsoft.com/learn/dotnet/architecture-guides) proporciona o acesso a um conjunto de livros eletrônicos que oferecem diretrizes, práticas recomendadas e aplicativos de exemplo ao usar o .NET para compilar:

- [Microserviços e contêineres do Docker](../../architecture/microservices/index.md)
- [Aplicativos Web com ASP.NET](../../architecture/modern-web-apps-azure/index.md)
- [Aplicativos móveis com o Xamarin](/xamarin/xamarin-forms/enterprise-application-patterns/index)
- [Aplicativos que são implantados na nuvem com o Azure](/azure/architecture/reference-architectures/index)

## <a name="see-also"></a>Consulte também

- [Novidades do ASP.NET Core 2.0](/aspnet/core/aspnetcore-2.0)
