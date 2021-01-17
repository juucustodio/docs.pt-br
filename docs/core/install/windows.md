---
title: Instalar o .NET no Windows
description: Saiba mais sobre quais versões do Windows você pode instalar no .NET.
author: adegeo
ms.author: adegeo
ms.date: 01/06/2021
ms.openlocfilehash: 57cebc562949627be70aabe24e75ad4567d072fd
ms.sourcegitcommit: 3a8f1979a98c6c19217a1930e0af5908988eb8ba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98536119"
---
# <a name="install-net-on-windows"></a>Instalar o .NET no Windows

> [!div class="op_single_selector"]
>
> - [Instalar no Windows](windows.md)
> - [Instalar no macOS](macos.md)
> - [Instalar no Linux](linux.md)

Neste artigo, você aprenderá a instalar o .NET no Windows. O .NET é constituído do tempo de execução e do SDK. O tempo de execução é usado para executar um aplicativo .NET e pode ou não ser incluído com o aplicativo. O SDK é usado para criar aplicativos e bibliotecas .NET. O tempo de execução do .NET é sempre instalado com o SDK.

A versão mais recente do .NET é 5,0.

> [!div class="button"]
> [Baixar o .NET](https://dotnet.microsoft.com/download/dotnet-core)

## <a name="supported-releases"></a>Versões com suporte

A tabela a seguir é uma lista de versões do .NET com suporte no momento e as versões do Windows nas quais elas têm suporte. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do [Windows alcance o fim da vida útil](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

As datas de fim de serviço das versões do Windows 10 são segmentadas por edição. Somente as edições **Home**, **pro**, **pro Education** e **Pro for Workstations** são consideradas na tabela a seguir. Verifique a [folha de fatos do ciclo de vida do Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) para obter detalhes específicos.

> [!TIP]
> Um `+` símbolo representa a versão mínima.

| Sistema operacional            | .NET Core 2.1 | .NET Core 3.1 | .NET 5 |
|-----------------------------|---------------|---------------|--------|
| Windows 10, versão 20H2    | ✔️           | ✔️            | ✔️    |
| Windows 10, versão 2004    | ✔️           | ✔️            | ✔️    |
| Windows 10, versão 1909    | ✔️           | ✔️            | ✔️    |
| Windows 10, versão 1903    | ✔️           | ✔️            | ✔️    |
| Windows 10, versão 1809    | ✔️           | ✔️            | ✔️    |
| Windows 10, versão 1803    | ✔️           | ✔️            | ✔️    |
| Windows 10, versão 1709    | ✔️           | ✔️            | ✔️    |
| Windows 10, versão 1607    | ✔️           | ✔️            | ✔️    |
| Windows 8.1                 | ✔️           | ✔️            | ✔️    |
| [ESU][esu] do Windows 7 SP1    | ✔️           | ✔️            | ✔️    |
| Windows 10, versão 1607    | ✔️           | ✔️            | ✔️    |
| Windows 10, versão 1607    | ✔️           | ✔️            | ✔️    |
| Windows Server 2012 R2      | ✔️           | ✔️            | ✔️    |
| Windows Server Core 2012 R2 | ✔️           | ✔️            | ✔️    |
| Nano Server, versão 1809 +  | ✔️           | ✔️            | ✔️    |
| Nano Server, versão 1803   | ✔️           | ✔️            | ❌    |

## <a name="unsupported-releases"></a>Versões sem suporte

Não há mais suporte para as seguintes versões do .NET ❌ . Os downloads para eles ainda permanecem publicados:

- 3.0
- 2.2
- 2,0

## <a name="runtime-information"></a>Informações de tempo de execução

O tempo de execução é usado para executar aplicativos criados com o .NET. Quando um autor de aplicativo publica um aplicativo, ele pode incluir o tempo de execução com seu aplicativo. Se eles não incluírem o tempo de execução, cabe ao usuário instalar o tempo de execução.

Há três tempos de execução diferentes que você pode instalar no Windows:

*Tempo de execução ASP.NET Core*\
Executa ASP.NET Core aplicativos. Inclui o tempo de execução do .NET.

*Tempo de execução do desktop*\
Executa o .NET WPF e Windows Forms aplicativos de área de trabalho para Windows. Inclui o tempo de execução do .NET.

*Tempo de execução do .NET*\
Esse tempo de execução é o tempo de execução mais simples e não inclui nenhum outro tempo de execução. É altamente recomendável que você instale o *tempo de execução do ASP.NET Core* e o *tempo de execução da área de trabalho* para obter a melhor compatibilidade com aplicativos .net.

> [!div class="button"]
> [Baixar o tempo de execução do .NET](https://dotnet.microsoft.com/download/dotnet-core)

## <a name="sdk-information"></a>Informações do SDK

O SDK é usado para compilar e publicar aplicativos e bibliotecas .NET. A instalação do SDK inclui todos os três [tempos de execução](#runtime-information): ASP.NET Core, desktop e .net.

## <a name="dependencies"></a>Dependências

<!-- markdownlint-disable MD025 -->
<!-- markdownlint-disable MD024 -->

# <a name="net-50"></a>[.NET 5.0](#tab/net50)

As seguintes versões do Windows têm suporte com o .NET 5,0:

> [!NOTE]
> Um `+` símbolo representa a versão mínima.

| Sistema operacional                  | Versão       | Arquiteturas   |
|---------------------|---------------|-----------------|
| Cliente do Windows 10   | Versão 1607+ | x64, x86, ARM64 |
| Windows Client      | 7 SP1 +, 8,1   | x64, x86        |
| Windows Server      | 2012 R2 +      | x64, x86        |
| Núcleo do Windows Server | 2012 R2 +      | x64, x86        |
| Nano Server         | Versão 1809 + | x64             |

Para obter mais informações sobre OS sistemas operacionais, as distribuições e a política de ciclo de vida com suporte do .NET 5,0, consulte [versões do sistema operacional .net 5,0 com suporte](https://github.com/dotnet/core/blob/master/release-notes/5.0/5.0-supported-os.md).

# <a name="net-core-31"></a>[.NET Core 3.1](#tab/netcore31)

As seguintes versões do Windows têm suporte com o .NET Core 3,1:

> [!NOTE]
> Um `+` símbolo representa a versão mínima.

| Sistema operacional                            | Versão                        | Arquiteturas   |
| ----------------------------- | ------------------------------ | --------------- |
| Windows Client                | 7 SP1 +, 8,1                    | x64, x86        |
| Cliente do Windows 10             | Versão 1607+                  | x64, x86        |
| Windows Server                | 2012 R2 +                       | x64, x86        |
| Nano Server                   | Versão 1803+                  | x64, ARM32      |

Para obter mais informações sobre OS sistemas operacionais, as distribuições e a política de ciclo de vida com suporte do .NET Core 3,1, consulte [versões do sistema operacional .net core 3,1 com suporte](https://github.com/dotnet/core/blob/master/release-notes/3.1/3.1-supported-os.md).

# <a name="net-core-30"></a>[.NET Core 3.0](#tab/netcore30)

*O .NET Core 3,0 está atualmente ❌ sem suporte. Para obter mais informações, consulte a [política de suporte do .NET Core](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).*

As seguintes versões do Windows têm suporte com o .NET Core 3,0:

> [!NOTE]
> Um `+` símbolo representa a versão mínima.

| Sistema operacional                            | Versão                        | Arquiteturas   |
| ----------------------------- | ------------------------------ | --------------- |
| Windows Client                | 7 SP1 +, 8,1                    | x64, x86        |
| Cliente do Windows 10             | Versão 1607+                  | x64, x86        |
| Windows Server                | 2012 R2 +                       | x64, x86        |
| Nano Server                   | Versão 1803+                  | x64, ARM32      |

Para obter mais informações sobre OS sistemas operacionais, as distribuições e a política de ciclo de vida com suporte do .NET Core 3,0, consulte [versões do sistema operacional .net core 3,0 com suporte](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md).

# <a name="net-core-22"></a>[.NET Core 2.2](#tab/netcore22)

*O .NET Core 2,2 está atualmente ❌ sem suporte. Para obter mais informações, consulte a [política de suporte do .NET Core](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).*

As seguintes versões do Windows têm suporte com o .NET Core 2,2:

> [!NOTE]
> Um `+` símbolo representa a versão mínima.

| Sistema operacional                            | Versão                        | Arquiteturas   |
| ----------------------------- | ------------------------------ | --------------- |
| Windows Client                | 7 SP1 +, 8,1                    | x64, x86        |
| Cliente do Windows 10             | Versão 1607+                  | x64, x86        |
| Windows Server                | 2008 R2 SP1 +                   | x64, x86        |
| Nano Server                   | Versão 1803+                   | x64, ARM32      |

Para obter mais informações sobre OS sistemas operacionais, as distribuições e a política de ciclo de vida com suporte do .NET Core 2,2, consulte [versões do sistema operacional .net core 2,2 com suporte](https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-supported-os.md).

# <a name="net-core-21"></a>[.NET Core 2.1](#tab/netcore21)

As seguintes versões do Windows têm suporte com o .NET Core 2,1:

> [!NOTE]
> Um `+` símbolo representa a versão mínima.

| Sistema operacional                            | Versão                        | Arquiteturas   |
| ----------------------------- | ------------------------------ | --------------- |
| Windows Client                | 7 SP1 +, 8,1                    | x64, x86        |
| Cliente do Windows 10             | Versão 1607+                  | x64, x86        |
| Windows Server                | 2008 R2 SP1 +                   | x64, x86        |
| Nano Server                   | Versão 1803+                  | x86            |

Para obter mais informações sobre OS sistemas operacionais, as distribuições e a política de ciclo de vida com suporte do .NET Core 2,1, consulte [versões do sistema operacional .net core 2,1 com suporte](https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md).

---

<!-- markdownlint-disable MD001 -->

### <a name="windows-7--vista--81--server-2008-r2--server-2012-r2"></a><a name="additional-deps"></a> Windows 7/Vista/8,1/servidor 2008 R2/Server 2012 R2

Mais dependências serão necessárias se você estiver instalando o SDK do .NET ou o tempo de execução nas seguintes versões do Windows:

| Sistema operacional         | Pré-requisitos                                                                    |
|--------------------------|----------------------------------------------------------------------------------|
| [ESU][esu] do Windows 7 SP1 | -Microsoft Visual C++ 2015-2019 redistribuível [64-bit][vcc64]  /  [32-bit][vcc32] <br> -KB3063858 [64][kb64]bits  /  [32-bit][kb32] <br> - [MicrosoftRootCertificateAuthority2011. cer](https://go.microsoft.com/fwlink/?linkid=747875&clcid=0x409) (somente .net Core 2,1) |
| Windows Vista SP 2       | Microsoft Visual C++ 2015-2019 redistribuível [64-bit][vcc64]  /  [32-bit][vcc32] |
| Windows 8.1              | Microsoft Visual C++ 2015-2019 redistribuível [64-bit][vcc64]  /  [32-bit][vcc32] |
| Windows Server 2008 R2   | Microsoft Visual C++ 2015-2019 redistribuível [64-bit][vcc64]  /  [32-bit][vcc32] |
| Windows Server 2012 R2   | Microsoft Visual C++ 2015-2019 redistribuível [64-bit][vcc64]  /  [32-bit][vcc32] |

Os requisitos anteriores também serão necessários se você receber um erro relacionado a qualquer uma das seguintes DLLs:

- *api-ms-win-crt-runtime-l1-1-0.dll*
- *api-ms-win-cor-timezone-l1-1-0.dll*
- *hostfxr.dll*

## <a name="install-with-powershell-automation"></a>Instalar com a automação do PowerShell

Os [scripts dotnet-install](../tools/dotnet-install-script.md) são usados para a automação CI e para instalações não administrativas do tempo de execução. Você pode baixar o script na [página de referência de script dotnet-install](../tools/dotnet-install-script.md).

O script assume como padrão a instalação da versão mais recente do [LTS (suporte a longo prazo)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) , que é o .net Core 3,1. Você pode escolher uma versão específica especificando a `Channel` opção. Inclua a `Runtime` opção para instalar um tempo de execução. Caso contrário, o script instalará o SDK.

```powershell
dotnet-install.ps1 -Channel 5.0 -Runtime aspnetcore
```

Instale o SDK omitindo a `-Runtime` opção. A `-Channel` opção é definida neste exemplo como `Current` , que instala a versão mais recente com suporte.

```powershell
dotnet-install.ps1 -Channel Current
```

## <a name="install-with-visual-studio"></a>Instalar com o Visual Studio

Se você estiver usando o Visual Studio para desenvolver aplicativos .NET, a tabela a seguir descreve a versão mínima necessária do Visual Studio com base na versão do SDK do .NET de destino.

| Versão do SDK do .NET      | Versão do Visual Studio                      |
| --------------------- | ------------------------------------------ |
| 5.0                   | Visual Studio 2019 versão 16,8 ou superior. |
| 3.1                   | Visual Studio 2019 versão 16,4 ou superior. |
| 3.0                   | Visual Studio 2019 versão 16,3 ou superior. |
| 2.2                   | Visual Studio 2017 versão 15,9 ou superior. |
| 2.1                   | Visual Studio 2017 versão 15,7 ou superior. |

Se você já tiver o Visual Studio instalado, poderá verificar sua versão com as etapas a seguir.

01. Abra o Visual Studio.
01. Selecione **ajuda**  >  **sobre Microsoft Visual Studio**.
01. Leia o número de versão na caixa de diálogo **sobre** .

O Visual Studio pode instalar o SDK e o tempo de execução do .NET mais recentes.

> [!div class="button"]
> [Baixe o Visual Studio](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019).

### <a name="select-a-workload"></a>Selecionar uma carga de trabalho

Ao instalar ou modificar o Visual Studio, selecione uma ou mais das cargas de trabalho a seguir, dependendo do tipo de aplicativo que você está criando:

- A carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** na seção **outros conjuntos de ferramentas** .
- A carga de trabalho de **desenvolvimento da Web e ASP.net** na seção **Web & nuvem** .
- A carga de trabalho de **desenvolvimento do Azure** na seção **Web & nuvem** .
- A carga de trabalho **.net desktop Development** na seção **Desktop & Mobile** .

[![Carga de trabalho do Windows Visual Studio 2019 com .NET Core](media/install-sdk/windows-install-visual-studio-2019.png)](media/install-sdk/windows-install-visual-studio-2019.png#lightbox)

## <a name="install-alongside-visual-studio-code"></a>Instalar junto com Visual Studio Code

Visual Studio Code é um editor de código-fonte leve e avançado que é executado em sua área de trabalho. Visual Studio Code está disponível para Windows, macOS e Linux.

Embora Visual Studio Code não venha com um instalador .NET Core automatizado como o Visual Studio, adicionar o suporte ao .NET Core é simples.

01. [Baixe e instale o Visual Studio Code](https://code.visualstudio.com/Download).
01. [Baixe e instale o SDK do .NET Core](https://dotnet.microsoft.com/download/dotnet-core).
01. [Instale a extensão C# do Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp).

## <a name="windows-installer"></a>Windows Installer

A [página de download](https://dotnet.microsoft.com/download/dotnet-core) do .net fornece Windows Installer executáveis.

Ao usar os instaladores do Windows para instalar o .NET, você pode personalizar o caminho de instalação definindo `DOTNETHOME_X64` os `DOTNETHOME_X86` parâmetros e:

```console
dotnet-sdk-3.1.301-win-x64.exe DOTNETHOME_X64="F:\dotnet\x64" DOTNETHOME_X86="F:\dotnet\x86"
```

Se você quiser instalar o .NET silenciosamente, como em um ambiente de produção ou para oferecer suporte à integração contínua, use as seguintes opções:

- `/install`\
Instala o .NET.

- `/quiet`\
Impede que qualquer interface do usuário e prompts sejam exibidos.

- `norestart`\
Suprime todas as tentativas de reinicialização.

```console
dotnet-sdk-3.1.301-win-x64.exe /install /quiet /norestart
```

Para obter mais informações, consulte [Opções do Command-Line do instalador padrão](/windows/win32/msi/standard-installer-command-line-options).

> [!TIP]
> O instalador retorna um código de saída 0 para êxito e um código de saída de 3010 para indicar que uma reinicialização é necessária. Qualquer outro valor é geralmente um código de erro.

## <a name="download-and-manually-install"></a>Baixar e instalar manualmente

Como alternativa para os instaladores do Windows para .NET, você pode baixar e instalar manualmente o SDK ou o tempo de execução. A instalação manual geralmente é executada como parte do teste de integração contínua. Para um desenvolvedor ou usuário, geralmente é melhor usar um [instalador](https://dotnet.microsoft.com/download/dotnet-core).

Tanto o SDK do .NET quanto o tempo de execução do .NET podem ser instalados manualmente após terem sido baixados. Se você instalar o SDK do .NET, não precisará instalar o tempo de execução correspondente. Primeiro, Baixe uma versão binária para o SDK ou o tempo de execução de um dos seguintes sites:

- [Downloads do .NET 5,0](https://dotnet.microsoft.com/download/dotnet/5.0)
- [Downloads do .NET Core 3,1](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- [Downloads do .NET Core 2,1](https://dotnet.microsoft.com/download/dotnet-core/2.1)
- [Todos os downloads do .NET Core](https://dotnet.microsoft.com/download/dotnet-core)

Crie um diretório para extrair o .NET, por exemplo `%USERPROFILE%\dotnet` . Em seguida, extraia o arquivo zip baixado para esse diretório.

Por padrão, os comandos e aplicativos da CLI do .NET não usarão o .NET instalado dessa forma e você deverá optar por usá-lo explicitamente. Para fazer isso, altere as variáveis de ambiente com as quais um aplicativo é iniciado:

```console
set DOTNET_ROOT=%USERPROFILE%\dotnet
set PATH=%USERPROFILE%\dotnet;%PATH%
set DOTNET_MULTILEVEL_LOOKUP=0
```

Essa abordagem permite que você instale várias versões em locais separados e escolha explicitamente qual local de instalação um aplicativo deve usar executando o aplicativo com variáveis de ambiente apontando para esse local.

Quando `DOTNET_MULTILEVEL_LOOKUP` é definido como `0` , o .net ignora qualquer versão do .net instalada globalmente. Remova essa configuração de ambiente para permitir que o .NET considere o local de instalação global padrão ao selecionar a melhor estrutura para executar o aplicativo. O padrão é normalmente `C:\Program Files\dotnet` , que é onde os instaladores instalam o .net.

## <a name="docker"></a>Docker

Os contêineres fornecem uma maneira leve de isolar seu aplicativo do restante do sistema host. Os contêineres no mesmo computador compartilham apenas o kernel e usam os recursos fornecidos ao seu aplicativo.

O .NET pode ser executado em um contêiner do Docker. As imagens oficiais do Docker do .NET são publicadas no MCR (registro de contêiner da Microsoft) e podem ser descobertas no [repositório do Microsoft .net Docker Hub](https://hub.docker.com/_/microsoft-dotnet). Cada repositório contém imagens para diferentes combinações do .NET (SDK ou Runtime) e do sistema operacional que você pode usar.

A Microsoft fornece imagens personalizadas para cenários específicos. Por exemplo, o [repositório do ASP.NET Core](https://hub.docker.com/_/microsoft-dotnet-aspnet) fornece imagens que são criadas para a execução de aplicativos ASP.NET Core na produção.

Para obter mais informações sobre como usar o .NET em um contêiner do Docker, consulte [introdução ao .net e ao Docker](../docker/introduction.md) e [amostras](https://github.com/dotnet/dotnet-docker/blob/master/samples/README.md).

## <a name="next-steps"></a>Próximas etapas

- [Como verificar se o .net já está instalado](how-to-detect-installed-versions.md?pivots=os-windows).
- [Tutorial: tutorial de Olá, mundo](../tutorials/with-visual-studio.md).
- [Tutorial: criar um novo aplicativo com Visual Studio Code](../tutorials/with-visual-studio-code.md).
- [Tutorial: colocar em contêiner um aplicativo .NET Core](../docker/build-container.md).

[esu]: /troubleshoot/windows-client/windows-7-eos-faq/windows-7-extended-security-updates-faq
[vcc64]: https://aka.ms/vs/16/release/vc_redist.x64.exe
[vcc32]: https://aka.ms/vs/16/release/vc_redist.x86.exe
[kb64]: https://www.microsoft.com/en-us/download/details.aspx?id=47442
[kb32]: https://www.microsoft.com/en-us/download/details.aspx?id=47409
