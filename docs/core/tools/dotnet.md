---
title: Comando dotnet
description: Saiba mais sobre o comando dotNet (o Driver genérico para a CLI do .NET) e seu uso.
ms.date: 11/11/2020
ms.openlocfilehash: 7a0c8f2eb7ab407bd725db56cbf31da4689970e4
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634019"
---
# <a name="dotnet-command"></a>Comando dotnet

**Este artigo aplica-se a:** ✔️ SDK do .net Core 2,1 e versões posteriores

## <a name="name"></a>Name

`dotnet` -O Driver genérico para a CLI do .NET.

## <a name="synopsis"></a>Sinopse

Para obter informações sobre os comandos disponíveis e o ambiente:

```dotnetcli
dotnet [--version] [--info] [--list-runtimes] [--list-sdks]

dotnet -h|--help
```

Para executar um comando (requer a instalação do SDK):

```dotnetcli
dotnet <COMMAND> [-d|--diagnostics] [-h|--help] [--verbosity <LEVEL>]
    [command-options] [arguments]
```

Para executar um aplicativo:

```dotnetcli
dotnet [--additionalprobingpath <PATH>] [--additional-deps <PATH>]
    [--fx-version <VERSION>]  [--roll-forward <SETTING>]
    <PATH_TO_APPLICATION> [arguments]

dotnet exec [--additionalprobingpath] [--additional-deps <PATH>]
    [--fx-version <VERSION>]  [--roll-forward <SETTING>]
    <PATH_TO_APPLICATION> [arguments]
```

`--roll-forward` está disponível desde o .NET Core 3. x. Use o `--roll-forward-on-no-candidate-fx` para .NET Core 2. x.

## <a name="description"></a>Description

O `dotnet` comando tem duas funções:

- Ele fornece comandos para trabalhar com projetos .NET.

  Por exemplo, [`dotnet build`](dotnet-build.md) compila um projeto. Cada comando define suas próprias opções e argumentos. Todos os comandos dão suporte à `--help` opção de impressão de breve documentação sobre como usar o comando.

- Ele executa aplicativos .NET.

  Especifique o caminho para um arquivo de aplicativo `.dll` para executar o aplicativo.  Executar o aplicativo significa localizar e executar o ponto de entrada, que, no caso de aplicativos de console, é o `Main` método. Por exemplo, `dotnet myapp.dll` executa o `myapp` aplicativo. Consulte [implantação de aplicativos .net](../deploying/index.md) para saber mais sobre as opções de implantação.

## <a name="options"></a>Opções

Diferentes opções estão disponíveis por `dotnet` si só, para executar um comando e para executar um aplicativo.

### <a name="options-for-dotnet-by-itself"></a>Opções para dotnet por si só

As opções a seguir são por `dotnet` si só. Por exemplo, `dotnet --info`. Eles imprimem informações sobre o ambiente.

- **`--info`**

  Imprime informações detalhadas sobre uma instalação do .NET e o ambiente do computador, como o sistema operacional atual, e confirme o SHA da versão do .NET.

- **`--version`**

  Imprime a versão do SDK do .NET em uso.

- **`--list-runtimes`**

  Imprime uma lista de tempos de execução .NET instalados. Uma versão x86 do SDK lista apenas os tempos de execução x86 e uma versão x64 do SDK lista somente os tempos de execução do x64.

- **`--list-sdks`**

  Imprime uma lista dos SDKs .NET instalados.

- **`-h|--help`**

  Imprime uma lista de comandos disponíveis.

### <a name="sdk-options-for-running-a-command"></a>Opções do SDK para executar um comando

As opções a seguir são para `dotnet` com um comando. Por exemplo, `dotnet build --help`.

- **`-d|--diagnostics`**

  Habilita a saída de diagnóstico.

- **`-v|--verbosity <LEVEL>`**

  Define o nível de detalhes do comando. Os valores permitidos são `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`. Sem suporte em todos os comandos. Consulte a página de comando específica para determinar se essa opção está disponível.

- **`-h|--help`**

  Imprime a documentação para um determinado comando, como `dotnet build --help`.

- **`command options`**

  Cada comando define opções específicas para esse comando. Consulte a página de comando específica para obter uma lista de opções disponíveis.

### <a name="runtime-options"></a>Opções de tempo de execução

As opções a seguir estão disponíveis quando o `dotnet` executa um aplicativo. Por exemplo, `dotnet myapp.dll --roll-forward Major`.

- **`--additionalprobingpath <PATH>`**

  Caminho que contém a política de investigação e os assemblies a serem investigados.

- **`--additional-deps <PATH>`**

  Caminho para um arquivo *.deps.json* adicional. Um *deps.jsno* arquivo contém uma lista de dependências, dependências de compilação e informações de versão usadas para resolver conflitos de assembly. Para obter mais informações, confira [Arquivos de configuração de runtime](https://github.com/dotnet/cli/blob/master/Documentation/specs/runtime-configuration-file.md) no GitHub.

- **`--depsfile <PATH_TO_DEPSFILE>`**

  Caminho para o *deps.jsno* arquivo. Um *deps.jsno* arquivo é um arquivo de configuração que contém informações sobre as dependências necessárias para executar o aplicativo. Esse arquivo é gerado pelo SDK do .NET.

- **`--runtimeconfig`**

  Caminho para um arquivo *runtimeconfig.json*. Um *runtimeconfig.jsno* arquivo é um arquivo de configuração que contém as configurações de tempo de execução. Para obter mais informações, consulte [definições de configuração de tempo de execução do .net](../run-time-config/index.md#runtimeconfigjson).

- **`--roll-forward <SETTING>`****Disponível a partir do SDK do .NET Core 3,0.**

  Controla como o roll forward é aplicado ao aplicativo. O `SETTING` pode ser um dos valores a seguir. Se não for especificado, `Minor` será o padrão.

  - `LatestPatch` -Rolar para a versão mais alta do patch. Isso desabilita o roll forward da versão secundária.
  - `Minor` – Rolar para a versão secundária mais baixa, se a versão secundária solicitada estiver ausente. Se a versão secundária solicitada estiver presente, a política LatestPatch será usada.
  - `Major` – Role para frente até a versão principal mais baixa e a versão secundária mais baixa, se a versão principal solicitada estiver ausente. Se a versão principal solicitada está presente, a política Secundária é usada.
  - `LatestMinor` – Role para frente até a versão secundária mais alta, mesmo que a versão secundária solicitada esteja presente. Destinado a cenários de hospedagem de componente.
  - `LatestMajor` – Role para frente até a versão secundária mais alta e a mais alta, mesmo que a principal solicitada esteja presente. Destinado a cenários de hospedagem de componente.
  - `Disable` -Não rolar para frente. Associar somente à versão especificada. Essa política não é recomendada para uso geral, pois ela desabilita a capacidade de efetuar roll forward para os patches mais recentes. Esse valor só é recomendado para teste.

  Com exceção de `Disable` , todas as configurações usarão a versão de patch mais alta disponível.

  O comportamento de roll forward também pode ser configurado em uma propriedade de arquivo de projeto, uma propriedade de arquivo de configuração de tempo de execução e uma variável de ambiente. Para obter mais informações, consulte [roll forward de tempo de execução de versão principal](../whats-new/dotnet-core-3-0.md#major-version-runtime-roll-forward).

- **`--roll-forward-on-no-candidate-fx <N>`****Disponível no SDK do .NET Core 2. x.**

  Define o comportamento quando a estrutura compartilhada necessária não está disponível. `N` pode ser:

  - `0` – Desabilitar até mesmo o roll forward da versão secundária.
  - `1` – Efetuar roll forward da versão secundária, mas não da versão principal. Esse é o comportamento padrão.
  - `2` – Efetuar roll forward das versões secundária e principal.

  Para saber mais, confira [Efetuar roll forward](../whats-new/dotnet-core-2-1.md#roll-forward).

  A partir do .NET Core 3,0, essa opção é substituída pelo `--roll-forward` , e essa opção deve ser usada em vez disso.

- **`--fx-version <VERSION>`**

  Versão do tempo de execução do .NET a ser usada para executar o aplicativo.

  Essa opção substitui a versão da primeira referência de estrutura no arquivo do aplicativo `.runtimeconfig.json` . Isso significa que ele funcionará apenas conforme o esperado se houver apenas uma referência de estrutura. Se o aplicativo tiver mais de uma referência de estrutura, usar essa opção poderá causar erros.

## <a name="dotnet-commands"></a>Comandos dotnet

### <a name="general"></a>Geral

| Comando                                       | Função                                                            |
| --------------------------------------------- | ------------------------------------------------------------------- |
| [dotnet build](dotnet-build.md)               | Compila um aplicativo .NET.                                     |
| [dotnet build-server](dotnet-build-server.md) | Interage com servidores iniciados por um build.                          |
| [dotnet clean](dotnet-clean.md)               | Limpa saídas de build.                                                |
| [dotnet help](dotnet-help.md)                 | Mostra uma documentação mais detalhada online para o comando.           |
| [dotnet migrate](dotnet-migrate.md)           | Migra um projeto válido da Visualização 2 para um projeto do SDK 1.0 do .NET Core.  |
| [dotnet msbuild](dotnet-msbuild.md)           | Oferece acesso à linha de comando do MSBuild.                        |
| [dotnet new](dotnet-new.md)                   | Inicializa um projeto do C# ou F# de um modelo especificado.                |
| [dotnet pack](dotnet-pack.md)                 | Cria um pacote NuGet do seu código.                               |
| [dotnet publish](dotnet-publish.md)           | Publica um aplicativo dependente do .NET Framework ou autocontido. |
| [dotnet restore](dotnet-restore.md)           | Restaura as dependências para um determinado aplicativo.                  |
| [dotnet run](dotnet-run.md)                   | Executa o aplicativo na origem.                                   |
| [dotnet sln](dotnet-sln.md)                   | Opções para adicionar, remover e listar projetos em um arquivo de solução.       |
| [dotnet store](dotnet-store.md)               | Armazena os assemblies no repositório de pacotes de runtime.                     |
| [dotnet test](dotnet-test.md)                 | Executa testes usando um executor de teste.                                     |

### <a name="project-references"></a>Referências de projeto

Comando | Função
--- | ---
[dotnet add reference](dotnet-add-reference.md) | Adiciona uma referência ao projeto.
[dotnet list reference](dotnet-list-reference.md) | Lista referências ao projeto.
[dotnet remove reference](dotnet-remove-reference.md) | Remove uma referência ao projeto.

### <a name="nuget-packages"></a>Pacotes NuGet

Comando | Função
--- | ---
[dotnet add package](dotnet-add-package.md) | Adiciona um pacote NuGet.
[dotnet remove package](dotnet-remove-package.md) | Remove um pacote NuGet.

### <a name="nuget-commands"></a>Comandos NuGet

Comando | Função
--- | ---
[dotnet nuget delete](dotnet-nuget-delete.md) | Exclui ou retira da lista um pacote do servidor.
[dotnet nuget push](dotnet-nuget-push.md) | Envia um pacote ao servidor e os publica.
[dotnet nuget locals](dotnet-nuget-locals.md) | Limpa ou lista os recursos locais do NuGet, como cache de solicitação http, cache temporário ou pasta de pacotes globais em todo o computador.
[dotnet nuget add source](dotnet-nuget-add-source.md) | Adiciona uma origem do NuGet.
[dotnet nuget disable source](dotnet-nuget-disable-source.md) | Desabilita uma origem do NuGet.
[dotnet nuget enable source](dotnet-nuget-enable-source.md) | Habilita uma origem do NuGet.
[dotnet nuget list source](dotnet-nuget-list-source.md) | Lista todas as fontes do NuGet configuradas.
[dotnet nuget remove source](dotnet-nuget-remove-source.md) | Remove uma origem do NuGet.
[dotnet nuget update source](dotnet-nuget-update-source.md) | Atualiza uma origem do NuGet.

### <a name="global-tool-path-and-local-tools-commands"></a>Comandos globais, de caminho de ferramenta e de ferramentas locais

Ferramentas são aplicativos de console que são instalados a partir de pacotes NuGet e são invocados no prompt de comando. Você pode escrever ferramentas por conta própria ou instalar ferramentas escritas por terceiros. As ferramentas também são conhecidas como ferramentas globais, ferramentas de caminho de ferramenta e ferramentas locais. Para obter mais informações, consulte [visão geral das ferramentas .net](global-tools.md). As ferramentas globais e de caminho de ferramenta estão disponíveis a partir do SDK do .NET Core 2,1. As ferramentas locais estão disponíveis a partir do SDK do .NET Core 3,0.

Comando | Função
--- | ---
[dotnet tool install](dotnet-tool-install.md) | Instala uma ferramenta em seu computador.
[dotnet tool list](dotnet-tool-list.md) | Lista todas as ferramentas globais, ferramentas-caminho ou locais atualmente instaladas no seu computador.
[dotnet tool search](dotnet-tool-list.md) | Pesquisa NuGet.org para ferramentas que têm o termo de pesquisa especificado em seu nome ou metadados.
[dotnet tool uninstall](dotnet-tool-uninstall.md) | Desinstala uma ferramenta do seu computador.
[dotnet tool update](dotnet-tool-update.md) | Atualiza uma ferramenta instalada em seu computador.

### <a name="additional-tools"></a>Ferramentas adicionais

A partir do SDK do .NET Core 2.1.300, várias ferramentas que estavam disponíveis apenas em uma base por projeto usando `DotnetCliToolReference` agora estão disponíveis como parte do SDK do .net. Essas ferramentas estão listadas na tabela a seguir:

| Ferramenta                                              | Função                                                     |
| ------------------------------------------------- | ------------------------------------------------------------ |
| dev-certs                                         | Cria e gerencia certificados de desenvolvimento.                |
| [salva](/ef/core/miscellaneous/cli/dotnet)           | Ferramentas de linha de comando do Entity Framework Core.                    |
| sql-cache                                         | Ferramentas de linha de comando de cache do SQL Server.                         |
| [user-secrets](/aspnet/core/security/app-secrets) | Gerencia os segredos do usuário de desenvolvimento.                            |
| [variáveis](/aspnet/core/tutorials/dotnet-watch)      | Inicia um observador de arquivo que executa um comando quando os arquivos são alterados. |

Para obter mais informações sobre cada ferramenta, digite `dotnet <tool-name> --help`.

## <a name="examples"></a>Exemplos

Crie um novo aplicativo de console .NET:

```dotnetcli
dotnet new console
```

Compile um projeto e suas dependências em um determinado diretório:

```dotnetcli
dotnet build
```

Executar um aplicativo:

```dotnetcli
dotnet myapp.dll
```

## <a name="environment-variables"></a>Variáveis de ambiente

- `DOTNET_ROOT`, `DOTNET_ROOT(x86)`

  Especifica o local dos tempos de execução do .NET, se eles não estiverem instalados no local padrão. O local padrão no Windows é `C:\Program Files\dotnet` . O local padrão no Linux e no macOS é `/usr/share/dotnet` . Essa variável de ambiente é usada somente ao executar aplicativos por meio de executáveis gerados (apphosts). `DOTNET_ROOT(x86)` é usado em vez disso, ao executar um executável de 32 bits em um sistema operacional de 64 bits.

- `NUGET_PACKAGES`

  A pasta de pacotes globais. Se não estiver definido, o padrão será `~/.nuget/packages` em Unix ou `%userprofile%\.nuget\packages` no Windows.

- `DOTNET_SERVICING`

  Especifica o local do índice de manutenção a ser usado pelo host compartilhado ao carregar o runtime.

- `DOTNET_NOLOGO`

  Especifica se as mensagens de boas-vindas e telemetria do .NET são exibidas na primeira execução. Defina como `true` ativar mudo dessas mensagens (valores `true` , `1` ou `yes` aceitas) ou defina como `false` para permitir (valores `false` , `0` ou `no` aceito). Se não estiver definido, o padrão será `false` e as mensagens serão exibidas na primeira execução. Esse sinalizador não tem nenhum efeito na telemetria (consulte `DOTNET_CLI_TELEMETRY_OPTOUT` para recusar o envio de telemetria).

- `DOTNET_CLI_TELEMETRY_OPTOUT`

  Especifica se os dados sobre o uso das ferramentas .NET são coletados e enviados à Microsoft. Definido como `true` para recusar o recurso de telemetria (os valores `true`, `1` ou `yes` são aceitos). Caso contrário, definido como `false` para aceitar os recursos de telemetria (os valores `false`, `0` ou `no` são aceitos). Se não estiver definido, o padrão será `false`, e o recurso de telemetria estará ativo.

- `DOTNET_MULTILEVEL_LOOKUP`

  Especifica se o tempo de execução do .NET, a estrutura compartilhada ou o SDK são resolvidos a partir do local global. Se não estiver definido, o padrão será 1 (lógico `true` ). Defina como 0 (lógico `false` ) para não resolver a partir do local global e ter instalações isoladas do .net. Para obter mais informações sobre a pesquisa de vários níveis, consulte [Pesquisa SharedFX de vários níveis](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/multilevel-sharedfx-lookup.md).

- `DOTNET_ROLL_FORWARD`**Disponível a partir do .NET Core 3. x.**

  Determina o comportamento de roll-forward. Para obter mais informações, consulte a `--roll-forward` opção anterior neste artigo.

- `DOTNET_ROLL_FORWARD_TO_PRERELEASE`**Disponível a partir do .NET Core 3. x.**

  Se definido como `1` (habilitado), permite a rolagem posterior para uma versão de pré-lançamento de uma versão de lançamento. Por padrão ( `0` -Disabled), quando uma versão de lançamento do tempo de execução do .net é solicitada, o roll forward só considerará as versões de lançamento instaladas.

  Para saber mais, confira [Efetuar roll forward](../whats-new/dotnet-core-3-0.md#major-version-runtime-roll-forward).

- `DOTNET_ROLL_FORWARD_ON_NO_CANDIDATE_FX`**Disponível no .NET Core 2. x.**

  Desabilita o roll forward da versão secundária, se definido como `0`. Para saber mais, confira [Efetuar roll forward](../whats-new/dotnet-core-2-1.md#roll-forward).

  Essa configuração é substituída no .NET Core 3,0 pelo `DOTNET_ROLL_FORWARD` . Em vez disso, as novas configurações devem ser usadas.

- `DOTNET_CLI_UI_LANGUAGE`

  Define o idioma da interface do usuário da CLI usando um valor de localidade, como `en-us` . Os valores com suporte são os mesmos para o Visual Studio. Para obter mais informações, consulte a seção sobre como alterar o idioma do instalador na [documentação de instalação do Visual Studio](/visualstudio/install/install-visual-studio). As regras do Gerenciador de recursos do .NET se aplicam, portanto, você não precisa escolher uma correspondência exata &mdash; que também pode escolher os descendentes na `CultureInfo` árvore. Por exemplo, se você defini-lo como `fr-CA` , a CLI encontrará e usará as `fr` traduções. Se você defini-lo como um idioma sem suporte, a CLI voltará para o inglês.

- `DOTNET_DISABLE_GUI_ERRORS`

  Para executáveis gerados por GUI habilitado-desabilita o Popup da caixa de diálogo, que normalmente mostra algumas classes de erros. Ele só grava `stderr` e sai nesses casos.
  
- `DOTNET_ADDITIONAL_DEPS`

  Equivalente a Option CLI `--additional-deps` .

- `DOTNET_RUNTIME_ID`

  Substitui o RID detectado.

- `DOTNET_SHARED_STORE`

  Local do "armazenamento compartilhado" para o qual a resolução de assembly volta para em alguns casos.

- `DOTNET_STARTUP_HOOKS`

  Lista de assemblies dos quais carregar e executar os ganchos de inicialização.

- `DOTNET_BUNDLE_EXTRACT_BASE_DIR`**Disponível a partir do .NET Core 3. x.**

  Especifica um diretório para o qual um aplicativo de arquivo único é extraído antes de ser executado.

  Para obter mais informações, consulte [executáveis de arquivo único](../whats-new/dotnet-core-3-0.md#single-file-executables).

- `COREHOST_TRACE`, `COREHOST_TRACEFILE`, `COREHOST_TRACE_VERBOSITY`

  Controla o rastreamento de diagnóstico dos componentes de hospedagem, como `dotnet.exe` , `hostfxr` e `hostpolicy` .

  * `COREHOST_TRACE=[0/1]` -o padrão é o `0` Rastreamento desabilitado. Se definido como `1` , o rastreamento de diagnóstico é habilitado.
  * `COREHOST_TRACEFILE=<file path>` -Só terá efeito se o rastreamento estiver habilitado via `COREHOST_TRACE=1` . Quando definido, as informações de rastreamento são gravadas no arquivo especificado, caso contrário, as informações de rastreamento são gravadas no `stderr` . **Disponível a partir do .NET Core 3. x.**
  * `COREHOST_TRACE_VERBOSITY=[1/2/3/4]` -o padrão é `4` . A configuração é usada somente quando o rastreamento está habilitado via `COREHOST_TRACE=1` . **Disponível a partir do .NET Core 3. x.**
    * `4` -todas as informações de rastreamento são gravadas
    * `3` -apenas mensagens informativas, de aviso e de erro são gravadas
    * `2` -somente avisos e mensagens de erro são gravados
    * `1` -somente as mensagens de erro são gravadas

  A maneira típica de obter informações detalhadas de rastreamento sobre a inicialização do aplicativo é definir `COREHOST_TRACE=1` e `COREHOST_TRACEFILE=host_trace.txt` , em seguida, executar o aplicativo. Um novo arquivo `host_trace.txt` será criado no diretório atual com as informações detalhadas.

## <a name="see-also"></a>Consulte também

- [Arquivos de configuração de runtime](https://github.com/dotnet/cli/blob/master/Documentation/specs/runtime-configuration-file.md)
- [Definições de configuração de tempo de execução do .NET](../run-time-config/index.md)
