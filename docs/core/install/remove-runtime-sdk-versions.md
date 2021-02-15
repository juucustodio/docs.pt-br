---
title: Remover o tempo de execução e o SDK do .NET
description: Este artigo descreve como determinar quais versões do tempo de execução e SDK do .NET estão instaladas no momento e como removê-las no Windows, Mac e Linux.
author: adegeo
ms.author: adegeo
ms.date: 11/20/2020
zone_pivot_groups: operating-systems-set-one
ms.openlocfilehash: f07a9acdc5be310d38da18602dde2ebf678e9a1b
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96031716"
---
# <a name="how-to-remove-the-net-runtime-and-sdk"></a>Como remover o tempo de execução e o SDK do .NET

Ao longo do tempo, à medida que você instala versões atualizadas do tempo de execução e do SDK do .NET, talvez você queira remover versões desatualizadas do .NET do seu computador. A remoção de versões mais antigas do tempo de execução pode alterar o tempo de execução escolhido para executar aplicativos de estrutura compartilhados, conforme detalhado no artigo sobre a [seleção de versão do .net](../versions/selection.md).

## <a name="should-i-remove-a-version"></a>Devo remover uma versão?

Os comportamentos de [seleção de versão do .net](../versions/selection.md) e a compatibilidade de tempo de execução do .net em atualizações permitem a remoção segura de versões anteriores. As atualizações de tempo de execução do .NET são compatíveis em uma **banda** de versão principal, como 1. x e 2. x. Além disso, as versões mais recentes do SDK do .NET geralmente mantêm a capacidade de criar aplicativos destinados a versões anteriores do Runtime de maneira compatível.

Em geral, você precisa apenas do SDK mais recente e da versão de patch mais recente dos runtimes necessários para seu aplicativo. As instâncias em que você talvez queira manter versões mais antigas do SDK ou *do* Runtime incluem manterproject.jsaplicativos baseados em. A menos que seu aplicativo tenha motivos específicos para runtimes ou SDKs anteriores, você pode remover com segurança as versões mais antigas.

## <a name="determine-what-is-installed"></a>Determinar o que está instalado

A CLI do .NET tem opções que você pode usar para listar as versões do SDK e do tempo de execução que estão instalados em seu computador.  Use [`dotnet --list-sdks`](../tools/dotnet.md#options) para ver a lista de SDKs instalados em seu computador. Use [`dotnet --list-runtimes`](../tools/dotnet.md#options) para ver a lista de tempos de execução instalados em seu computador. Para obter mais informações, consulte [como verificar se o .net já está instalado](how-to-detect-installed-versions.md).

## <a name="uninstall-net"></a>Desinstalar o .NET

::: zone pivot="os-windows"

O .NET usa a caixa de diálogo de **recursos dos aplicativos** do Windows & para remover versões do tempo de execução e do SDK do .net. A figura a seguir mostra a caixa de diálogo **aplicativos & recursos** . Você pode pesquisar o **SDK do core** ou **SDK do .net** para filtrar e mostrar as versões instaladas do .net.

![Adicionar/remover programas para remover o .NET](./media/remove-runtime-sdk-versions/programs-and-features.png)

Selecione todas as versões que você deseja remover do seu computador e clique em **Desinstalar**.

::: zone-end

::: zone pivot="os-linux"

Há mais opções para desinstalar o .NET (SDK ou tempo de execução) no Linux. A melhor maneira de desinstalar o .NET é espelhar a ação usada para instalar o .NET. As especificações dependem de sua distribuição escolhida e do método de instalação.

> [!IMPORTANT]
> Para instalações do Red Hat, consulte a [documentação do produto Red Hat para .net](https://access.redhat.com/documentation/en-us/net/5.0/).

Não é necessário desinstalar o SDK do .NET ao atualizá-lo usando um Gerenciador de pacotes, a menos que você esteja atualizando de uma versão de visualização. Os comandos `update` ou `refresh` do gerenciador de pacotes removerão automaticamente a versão mais antiga após a instalação bem-sucedida de uma versão mais recente. Se você tiver uma versão de visualização instalada, desinstale-a.

Se você instalou o .NET usando um Gerenciador de pacotes, use esse mesmo Gerenciador de pacotes para desinstalar o SDK ou tempo de execução do .NET. As instalações do .NET oferecem suporte aos gerenciadores de pacotes mais populares. Consulte a documentação do Gerenciador de pacotes de distribuição para obter a sintaxe precisa em seu ambiente:

- [apt-get(8)](https://linux.die.net/man/8/apt-get) é usado por sistemas baseados em Debian, incluindo o Ubuntu.
- [yum(8)](https://linux.die.net/man/8/yum) é usado no Fedora, CentOS e Oracle Linux.
- [zypper(8)](https://en.opensuse.org/SDB:Zypper_manual_(plain)) é usado no openSUSE e no SLES (SUSE Linux Enterprise System).
- [dnf(8)](https://dnf.readthedocs.io/en/latest/command_ref.html) é usado no Fedora.

Em quase todos os casos, o comando para remover um pacote é `remove`.

O nome do pacote para a instalação do SDK do .NET para a maioria dos gerenciadores de pacotes é `dotnet-sdk` , seguido pelo número de versão. A partir da versão 2.1.300 do SDK do .NET e `2.1` da versão do tempo de execução, somente os números de versão principal e secundária são necessários: por exemplo, o SDK do .NET versão 2.1.300 pode ser referenciado como o pacote `dotnet-sdk-2.1` . As versões anteriores exigem toda a cadeia de caracteres da versão: por exemplo, `dotnet-sdk-2.1.200` seriam necessárias para a versão 2.1.200 do SDK do .net.

Para computadores que instalaram apenas o tempo de execução, e não o SDK, o nome do pacote é `dotnet-runtime-<version>` para o tempo de execução do .net e `aspnetcore-runtime-<version>` para toda a pilha de tempo de execução.

> [!TIP]
> As instalações do .NET Core anteriores a 2,0 não desinstalaram o aplicativo host quando o SDK foi desinstalado usando o Gerenciador de pacotes. Usando `apt-get`, o comando é:
>
> ```bash
> apt-get remove dotnet-host
> ```
>
> Não há nenhuma versão anexada a `dotnet-host` .

Se você instalou o usando um tarball, deverá remover o .NET usando o método manual.

No Linux, você deve remover os SDKs e tempos de execução separadamente, removendo os diretórios com controle de versão. Removê-los exclui o SDK e o tempo de execução do disco. Por exemplo, para remover o SDK 1.0.1 e o runtime, você usaria os seguintes comandos de bash:

```bash
version="1.0.1"
sudo rm -rf /usr/local/share/dotnet/sdk/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.NETCore.App/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.All/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.App/$version
sudo rm -rf /usr/local/share/dotnet/host/fxr/$version
```

Os diretórios pais para o SDK e o runtime são listados na saída dos comandos `dotnet --list-sdks` e `dotnet --list-runtimes`, conforme mostrado na tabela anterior.

::: zone-end

::: zone pivot="os-macos"

No Mac, você deve remover os SDKs e tempos de execução separadamente, removendo os diretórios com controle de versão. Removê-los exclui o SDK e o tempo de execução do disco. Por exemplo, para remover o SDK 1.0.1 e o runtime, você usaria os seguintes comandos de bash:

```bash
version="1.0.1"
sudo rm -rf /usr/local/share/dotnet/sdk/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.NETCore.App/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.All/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.App/$version
sudo rm -rf /usr/local/share/dotnet/host/fxr/$version
```

Os diretórios pais para o SDK e o runtime são listados na saída dos comandos `dotnet --list-sdks` e `dotnet --list-runtimes`, conforme mostrado na tabela anterior.

::: zone-end

## <a name="net-uninstall-tool"></a>Ferramenta de desinstalação do .NET

A [ferramenta de desinstalação do .net](../additional-tools/uninstall-tool.md) ( `dotnet-core-uninstall` ) permite remover SDKs e tempos de execução do .net de um sistema. Uma coleção de opções está disponível para especificar quais versões devem ser desinstaladas.

## <a name="visual-studio-dependency-on-net-core-sdk-versions"></a>Dependência do Visual Studio em versões de SDK do .NET Core

Antes do Visual Studio 2019 versão 16,3, os instaladores do Visual Studio chamaram o instalador de SDK do .NET Core autônomo. Como resultado, as versões do SDK são exibidas na caixa de diálogo **recursos de & de aplicativos** do Windows. Remover SDKs do .NET Core que foram instalados pelo Visual Studio usando o instalador autônomo pode interromper o Visual Studio. Se o Visual Studio tiver problemas depois de desinstalar os SDKs, execute o reparo nessa versão específica do Visual Studio. A tabela a seguir mostra algumas das dependências do Visual Studio em SDK do .NET Core versões:

| Versão do Visual Studio           | Versão do SDK do .NET Core          |
|---------------------------------|--------------------------------|
| Visual Studio 2019 versão 16.2 | SDK do .NET Core 2.2.4 XX, 2.1.8 XX |
| Visual Studio 2019 versão 16.1 | SDK do .NET Core 2.2.3 XX, 2.1.7 XX |
| Visual Studio 2019 versão 16,0 | SDK do .NET Core 2.2.2 XX, 2.1.6 XX |
| Visual Studio 2017 versão 15,9 | SDK do .NET Core 2.2.1 XX, 2.1.5 XX |
| Visual Studio 2017 versão 15.8 | SDK do .NET Core 2.1.4 XX          |

A partir do Visual Studio 2019 versão 16,3, o Visual Studio é responsável por sua própria cópia do SDK do .NET. Por esse motivo, você não vê mais essas versões do SDK na caixa de diálogo **aplicativos & recursos** .

## <a name="remove-the-nuget-fallback-folder"></a>Remover a pasta de fallback do NuGet

Antes do SDK do .NET Core 3,0, os instaladores de SDK do .NET Core usaram uma pasta chamada *NuGetFallbackFolder* para armazenar um cache de pacotes NuGet. Esse cache foi usado durante operações como `dotnet restore` ou `dotnet build /t:Restore` . O *NuGetFallbackFolder* está localizado em *C:\Program Files\dotnet\sdk* no Windows e em */usr/local/share/dotnet/SDK* no MacOS.

Talvez você queira remover essa pasta, se:

- Você está desenvolvendo apenas usando o SDK do .NET Core 3,0 ou o .NET 5,0 ou versões posteriores.
- Você está desenvolvendo usando versões SDK do .NET Core anteriores a 3,0, mas pode trabalhar online.

Se você quiser remover a pasta de fallback do NuGet, poderá excluí-la, mas precisará de privilégios de administrador para fazer isso.

Não é recomendável excluir a pasta *dotnet* . Isso removeria todas as ferramentas globais que você instalou anteriormente. Além disso, no Windows:

- Você interromperá o Visual Studio 2019 versão 16,3 e versões posteriores. Você pode executar o **reparo** para recuperar.
- Se houver SDK do .NET Core entradas na caixa de diálogo **aplicativos & recursos** , eles ficarão órfãos.
