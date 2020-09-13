---
title: dotnet-despejo-.NET Core
description: Instalando e usando a ferramenta de linha de comando dotnet-dump.
ms.date: 10/14/2019
ms.openlocfilehash: e008dcfc734a8742c495ea32a7a149c9a55c54c6
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89598103"
---
# <a name="dump-collection-and-analysis-utility-dotnet-dump"></a>Utilitário de coleta e análise de despejo (dotNet-dump)

**Este artigo aplica-se a:** ✔️ SDK do .net Core 3,0 e versões posteriores

> [!NOTE]
> `dotnet-dump` Não tem suporte no macOS.

## <a name="install-dotnet-dump"></a>Instalar dotnet-dump

Para instalar a versão de lançamento mais recente do `dotnet-dump` [pacote NuGet](https://www.nuget.org/packages/dotnet-dump), use o comando de [instalação da ferramenta dotnet](../tools/dotnet-tool-install.md) :

```dotnetcli
dotnet tool install -g dotnet-dump
```

## <a name="synopsis"></a>Sinopse

```console
dotnet-dump [-h|--help] [--version] <command>
```

## <a name="description"></a>Descrição

A `dotnet-dump` ferramenta global é uma maneira de coletar e analisar despejos do Windows e do Linux sem nenhum depurador nativo envolvido como `lldb` no Linux. Essa ferramenta é importante em plataformas como o Alpine Linux, onde um trabalho completo `lldb` não está disponível. A `dotnet-dump` ferramenta permite que você execute comandos SOS para analisar falhas e o GC (coletor de lixo), mas não é um depurador nativo para que não haja suporte para a exibição de quadros de pilha nativos.

## <a name="options"></a>Opções

- **`--version`**

  Exibe a versão do utilitário dotnet-dump.

- **`-h|--help`**

  Mostra a ajuda da linha de comando.

## <a name="commands"></a>Comandos

| Comando                                     |
| ------------------------------------------- |
| [dotnet-despejo de coleta](#dotnet-dump-collect) |
| [dotnet-análise de despejo](#dotnet-dump-analyze) |

## <a name="dotnet-dump-collect"></a>dotnet-despejo de coleta

Captura um despejo de um processo.

### <a name="synopsis"></a>Sinopse

```console
dotnet-dump collect [-h|--help] [-p|--process-id] [--type] [-o|--output] [--diag]
```

### <a name="options"></a>Opções

- **`-h|--help`**

  Mostra a ajuda da linha de comando.

- **`-p|--process-id <PID>`**

  Especifica o número de identificação do processo do qual coletar um despejo de memória.

- **`--type <Full|Heap|Mini>`**

  Especifica o tipo de despejo, que determina os tipos de informações que são coletadas do processo. Há três tipos:

  - `Full` -O maior despejo que contém toda a memória, incluindo as imagens de módulo.
  - `Heap` -Um despejo grande e relativamente abrangente contendo listas de módulos, listas de threads, todas as pilhas, informações de exceção, informações de identificador e toda a memória, exceto imagens mapeadas.
  - `Mini` -Um despejo pequeno contendo listas de módulos, listas de threads, informações de exceção e todas as pilhas.

  Se não for especificado, `Full` será o padrão.

- **`-o|--output <output_dump_path>`**

  O caminho completo e o nome do arquivo em que o despejo coletado deve ser gravado.

  Se não for especificado:

  - O padrão é *. \ dump_YYYYMMDD_HHMMSS. dmp* no Windows.
  - O padrão é *./core_YYYYMMDD_HHMMSS* no Linux.

  AAAAMMDD é ano/mês/dia e HHMMSS é hora/minuto/segundo.

- **`--diag`**

  Habilita o log de diagnóstico de coleta de despejo.

## <a name="dotnet-dump-analyze"></a>dotnet-análise de despejo

Inicia um shell interativo para explorar um despejo. O Shell aceita vários [comandos SOS](#analyze-sos-commands).

### <a name="synopsis"></a>Sinopse

```console
dotnet-dump analyze <dump_path> [-h|--help] [-c|--command]
```

### <a name="arguments"></a>Argumentos

- **`<dump_path>`**

  Especifica o caminho para o arquivo de despejo a ser analisado.

### <a name="options"></a>Opções

- **`-c|--command <debug_command>`**

  Especifica o [comando](#analyze-sos-commands) a ser executado no Shell em Iniciar.

### <a name="analyze-sos-commands"></a>Analisar comandos SOS

| Comando                             | Função                                                                                      |
| ----------------------------------- | --------------------------------------------------------------------------------------------- |
| `soshelp`                           | Exibe todos os comandos disponíveis                                                               |
| `soshelp|help <command>`            | Exibe o comando especificado.                                                               |
| `exit|quit`                         | Sai do modo interativo.                                                                       |
| `clrstack <arguments>`              | Fornece um rastreamento de pilha apenas do código gerenciado.                                                  |
| `clrthreads <arguments>`            | Lista os threads gerenciados em execução.                                                            |
| `dumpasync <arguments>`             | Exibe informações sobre máquinas de estado assíncrono no heap coletado por lixo.                |
| `dumpassembly <arguments>`          | Exibe detalhes sobre um assembly.                                                           |
| `dumpclass <arguments>`             | Exibe informações sobre uma estrutura de classe do EE no endereço especificado.                     |
| `dumpdelegate <arguments>`          | Exibe informações sobre um delegado.                                                        |
| `dumpdomain <arguments>`            | Exibe informações sobre todos os AppDomains e todos os assemblies nos domínios.                |
| `dumpheap <arguments>`              | Exibe informações sobre o heap coletado por lixo e estatísticas de coleção sobre objetos.       |
| `dumpil <arguments>`                | Exibe o MSIL (Microsoft Intermediate Language) associado a um método gerenciado. |
| `dumplog <arguments>`               | Grava o conteúdo de um log de estresse na memória no arquivo especificado.                         |
| `dumpmd <arguments>`                | Exibe informações sobre uma estrutura MethodDesc no endereço especificado.                   |
| `dumpmodule <arguments>`            | Exibe informações sobre uma estrutura de módulo do EE no endereço especificado.                    |
| `dumpmt <arguments>`                | Exibe informações sobre uma tabela de métodos no endereço especificado.                           |
| `dumpobj <arguments>`               | Exibe informações sobre um objeto no endereço especificado.                                       |
| `dso|dumpstackobjects <arguments>`  | Exibe todos os objetos gerenciados encontradas dentro dos limites da pilha atual.                    |
| `eeheap <arguments>`                | Exibe informações sobre a memória de processo consumida por estruturas de dados de tempo de execução internas.              |
| `finalizequeue <arguments>`         | Exibe todos os objetos registrados para a finalização.                                             |
| `gcroot <arguments>`                | Exibe informações sobre referências (ou raízes) para um objeto no endereço especificado.              |
| `gcwhere <arguments>`               | Exibe o local no heap de GC do argumento passado.                               |
| `ip2md <arguments>`                 | Exibe a estrutura MethodDesc no endereço especificado no código JIT.                       |
| `histclear <arguments>`             | Libera todos os recursos usados pela família de comandos `hist*`.                                |
| `histinit <arguments>`              | Inicializa as estruturas de SOS com base no log de estresse salvo no elemento a ser depurado.                     |
| `histobj <arguments>`               | Exibe as realocações de log de estresse da coleta de lixo relacionadas ao `<arguments>` .              |
| `histobjfind <arguments>`           | Exibe todas as entradas de log que fazem referência a um objeto no endereço especificado.               |
| `histroot <arguments>`              | Exibe informações relacionadas a ambas as promoções e realocações da raiz especificada.        |
| `lm|modules`                        | Exibe os módulos nativos no processo.                                                   |
| `name2ee <arguments>`               | Exibe a estrutura de MethodTable e a estrutura EEClass para o `<argument>` .                |
| `pe|printexception <arguments>`     | Exibe qualquer objeto derivado da classe de exceção no endereço `<argument>` .             |
| `setsymbolserver <arguments>`       | Habilita o suporte ao servidor de símbolos                                                             |
| `syncblk <arguments>`               | Exibe as informações do SyncBlock de suporte.                                                           |
| `threads|setthread <threadid>`      | Define ou exibe a ID de thread atual para os comandos SOS.                                  |

## <a name="using-dotnet-dump"></a>Usando `dotnet-dump`

A primeira etapa é coletar um despejo. Esta etapa poderá ser ignorada se um dump principal já tiver sido gerado. O sistema operacional ou o [recurso de geração de despejo](https://github.com/dotnet/runtime/blob/master/docs/design/coreclr/botr/xplat-minidump-generation.md) interno do tempo de execução do .NET Core pode criar dumps de núcleo.

```console
$ dotnet-dump collect --process-id 1902
Writing minidump to file ./core_20190226_135837
Written 98983936 bytes (24166 pages) to core file
Complete
```

Agora, analise o dump principal com o `analyze` comando:

```console
$ dotnet-dump analyze ./core_20190226_135850
Loading core dump: ./core_20190226_135850
Ready to process analysis commands. Type 'help' to list available commands or 'help [command]' to get detailed help on a command.
Type 'quit' or 'exit' to exit the session.
>
```

Essa ação abre uma sessão interativa que aceita comandos como:

```console
> clrstack
OS Thread Id: 0x573d (0)
    Child SP               IP Call Site
00007FFD28B42C58 00007fb22c1a8ed9 [HelperMethodFrame_PROTECTOBJ: 00007ffd28b42c58] System.RuntimeMethodHandle.InvokeMethod(System.Object, System.Object[], System.Signature, Boolean, Boolean)
00007FFD28B42DD0 00007FB1B1334F67 System.Reflection.RuntimeMethodInfo.Invoke(System.Object, System.Reflection.BindingFlags, System.Reflection.Binder, System.Object[], System.Globalization.CultureInfo) [/root/coreclr/src/mscorlib/src/System/Reflection/RuntimeMethodInfo.cs @ 472]
00007FFD28B42E20 00007FB1B18D33ED SymbolTestApp.Program.Foo4(System.String) [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 54]
00007FFD28B42ED0 00007FB1B18D2FC4 SymbolTestApp.Program.Foo2(Int32, System.String) [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 29]
00007FFD28B42F00 00007FB1B18D2F5A SymbolTestApp.Program.Foo1(Int32, System.String) [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 24]
00007FFD28B42F30 00007FB1B18D168E SymbolTestApp.Program.Main(System.String[]) [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 19]
00007FFD28B43210 00007fb22aa9cedf [GCFrame: 00007ffd28b43210]
00007FFD28B43610 00007fb22aa9cedf [GCFrame: 00007ffd28b43610]
```

Para ver uma exceção sem tratamento que eliminou seu aplicativo:

```console
> pe -lines
Exception object: 00007fb18c038590
Exception type:   System.Reflection.TargetInvocationException
Message:          Exception has been thrown by the target of an invocation.
InnerException:   System.Exception, Use !PrintException 00007FB18C038368 to see more.
StackTrace (generated):
SP               IP               Function
00007FFD28B42DD0 0000000000000000 System.Private.CoreLib.dll!System.RuntimeMethodHandle.InvokeMethod(System.Object, System.Object[], System.Signature, Boolean, Boolean)
00007FFD28B42DD0 00007FB1B1334F67 System.Private.CoreLib.dll!System.Reflection.RuntimeMethodInfo.Invoke(System.Object, System.Reflection.BindingFlags, System.Reflection.Binder, System.Object[], System.Globalization.CultureInfo)+0xa7 [/root/coreclr/src/mscorlib/src/System/Reflection/RuntimeMethodInfo.cs @ 472]
00007FFD28B42E20 00007FB1B18D33ED SymbolTestApp.dll!SymbolTestApp.Program.Foo4(System.String)+0x15d [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 54]
00007FFD28B42ED0 00007FB1B18D2FC4 SymbolTestApp.dll!SymbolTestApp.Program.Foo2(Int32, System.String)+0x34 [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 29]
00007FFD28B42F00 00007FB1B18D2F5A SymbolTestApp.dll!SymbolTestApp.Program.Foo1(Int32, System.String)+0x3a [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 24]
00007FFD28B42F30 00007FB1B18D168E SymbolTestApp.dll!SymbolTestApp.Program.Main(System.String[])+0x6e [/home/mikem/builds/SymbolTestApp/SymbolTestApp/SymbolTestApp.cs @ 19]

StackTraceString: <none>
HResult: 80131604
```

## <a name="special-instructions-for-docker"></a>Instruções especiais para o Docker

Se você estiver executando sob o Docker, a coleta de despejo exigirá `SYS_PTRACE` recursos ( `--cap-add=SYS_PTRACE` ou `--privileged` ).

Em Microsoft .NET principais imagens do Docker do SDK do Linux, alguns `dotnet-dump` comandos podem gerar a seguinte exceção:

> Exceção sem tratamento: System.DllNotFoundException: não é possível carregar a biblioteca compartilhada ' libdl.so ' ou uma de suas exceções de dependência.

Para contornar esse problema, instale o pacote "libc6-dev".

## <a name="see-also"></a>Confira também

- [Blog sobre coleta e análise de despejos de memória](https://devblogs.microsoft.com/dotnet/collecting-and-analyzing-memory-dumps/)
- [Ferramenta de análise de heap (dotNet-gcdump)](dotnet-gcdump.md)
