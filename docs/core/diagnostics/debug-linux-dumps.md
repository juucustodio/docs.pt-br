---
title: Depurar despejos do Linux
description: Neste artigo, você aprenderá a coletar e analisar despejos de ambientes Linux.
ms.date: 08/27/2020
ms.openlocfilehash: d62295e165f56e32ef73ab628ca9ebd77a4435d1
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89598324"
---
# <a name="debug-linux-dumps"></a>Depurar despejos do Linux

**Este artigo aplica-se a: ✔️** SDK do .net Core 3,0 e versões posteriores

## <a name="collect-dumps-on-linux"></a>Coletar despejos no Linux

As duas maneiras recomendadas de coletar despejos no Linux são [`dotnet-dump`](dotnet-dump.md) as [`createdump`](https://github.com/dotnet/runtime/blob/master/docs/design/coreclr/botr/xplat-minidump-generation.md) ferramentas ou.

### <a name="managed-dumps-with-dotnet-dump"></a>Despejos gerenciados com `dotnet-dump`

A [`dotnet-dump`](dotnet-dump.md) ferramenta é simples de usar e não tem uma dependência em nenhum depurador nativo. `dotnet-dump` funciona em uma ampla variedade de plataformas Linux (como Alpine ou ARM32/ARM64), em que as ferramentas de depuração tradicionais podem não estar disponíveis. No entanto, o `dotnet-dump` só captura o estado gerenciado para que ele não possa ser usado para problemas de depuração no código nativo. Os despejos coletados pelo `dotnet-dump` são analisados em um ambiente com o mesmo so e a arquitetura em que o despejo foi criado. A [`dotnet-gcdump`](dotnet-gcdump.md) ferramenta pode ser usada como uma alternativa que captura apenas informações de heap do GC, mas produz despejos que podem ser analisados no Windows.

### <a name="core-dumps-with-createdump"></a>Dumps principais com `createdump`

Alternativa ao `dotnet-dump` que cria despejos somente gerenciados, [`createdump`](https://github.com/dotnet/runtime/blob/master/docs/design/coreclr/botr/xplat-minidump-generation.md) é a ferramenta recomendada para criar dumps centrais no Linux contendo informações nativas e gerenciadas. Outras ferramentas como o gdb ou o gcore também podem ser usadas para criar dumps principais, mas podem perder o estado necessário para a depuração gerenciada, resultando em nomes de função ou tipo "desconhecido" durante a análise.

As `createdump` ferramentas são instaladas com o tempo de execução do .NET Core e podem ser encontradas ao lado de libcoreclr.so (normalmente em "/usr/share/dotnet/Shared/Microsoft.NETCore.app/[Version]"). A ferramenta usa uma ID de processo para coletar um despejo de como seu argumento principal e também pode usar parâmetros opcionais que especificam o tipo de despejo a ser coletado (um minidespejo com heap é o padrão). As opções incluem:

- **`<input-filename>`**

  Arquivo de rastreamento de entrada a ser convertido. O padrão é *trace. NetTrace*.

### <a name="options"></a>Opções

- **`-f|--name <output-filename>`**

  O arquivo no qual gravar o despejo. O padrão é '/tmp/coredump.%p ', em que% p é a ID de processo do processo de destino.

- **`-n|--normal`**

  Crie um minidespejo.

- **`-h|--withheap`**

  Crie um minidespejo com heap (padrão).

- **`-t|--triage`**

  Criar um minidespejo de triagem.

- **`-u|--full`**

  Crie um dump de núcleo completo.

- **`-d|--diag`**

  Habilitar mensagens de diagnóstico.

Observe que a coleta de despejos de núcleo requer a `SYS_PTRACE` capacidade ou que `createdump` seja executada com sudo ou su.

## <a name="analyze-dumps-on-linux"></a>Analisar despejos no Linux

Ambos os despejos gerenciados coletados com `dotnet-dump` o e os dumps principais coletados com `createdump` o podem ser analisados com a `dotnet-dump` ferramenta usando o `dotnet-dump analyze` comando. O `dotnet dump` requer que o ambiente que analisa o despejo tenha o mesmo sistema operacional e arquitetura que o ambiente no qual o despejo foi capturado.

Como alternativa, o [LLDB](https://lldb.llvm.org/) pode ser usado para analisar os dumps principais no Linux, que permite a análise de quadros gerenciados e nativos. LLDB usa a extensão SOS para depurar código gerenciado. A [`dotnet-sos`](dotnet-sos.md) ferramenta CLI pode ser usada para instalar o SOS, que tem [muitos comandos úteis](https://github.com/dotnet/diagnostics/blob/master/documentation/sos-debugging-extension.md) para depurar código gerenciado. Para analisar os despejos do .NET Core, o LLDB e o SOS exigem os seguintes binários do .NET Core do ambiente no qual o despejo foi criado:

1. libmscordaccore.so
2. libcoreclr.so
3. dotNet (o host usado para iniciar o aplicativo)

Na maioria dos casos, esses binários podem ser baixados usando a [`dotnet-symbol`](dotnet-symbol.md) ferramenta. Se os binários necessários não puderem ser baixados com `dotnet-symbol` (por exemplo, se uma versão particular do .NET Core criada a partir da origem estiver em uso), poderá ser necessário copiar os arquivos listados acima do ambiente no qual o despejo foi criado. Se os arquivos não estiverem localizados ao lado do arquivo de despejo, você poderá usar o comando LLDB/SOS `setclrpath <path>` para definir o caminho do qual eles devem ser carregados e `setsymbolserver -directory <path>` definir o caminho para procurar arquivos de símbolos.

Depois que os arquivos necessários estiverem disponíveis, o despejo poderá ser carregado em LLDB especificando o host dotnet como o executável a ser depurado:

```console
lldb --core <dump-file> <host-program>
```

Na linha de comando acima, `<dump-file>` é o caminho do despejo a ser analisado e `<host-program>` é o programa nativo que iniciou o aplicativo .NET Core. Normalmente, esse é o `dotnet` binário, a menos que o aplicativo seja independente; nesse caso, ele é o nome do aplicativo sem a extensão de dll.

Depois que o LLDB é iniciado, pode ser necessário usar o `setsymbolserver` comando para apontar para o local correto do símbolo ( `setsymbolserver -ms` para usar o servidor de símbolos da Microsoft ou `setsymbolserver -directory <path>` para especificar um caminho local). Os símbolos nativos podem ser carregados executando `loadsymbols` . Neste ponto, os [comandos do SOS](https://github.com/dotnet/diagnostics/blob/master/documentation/sos-debugging-extension.md) podem ser usados para analisar o despejo.

## <a name="see-also"></a>Confira também

- [dotnet-SOS](dotnet-sos.md) para obter mais detalhes sobre como instalar a extensão SOS.
- [dotnet-símbolo](dotnet-symbol.md) para obter mais detalhes sobre como instalar e usar a ferramenta de download de símbolos.
- [Repositório de diagnóstico do .NET Core](https://github.com/dotnet/diagnostics/blob/master/documentation/) para obter mais detalhes sobre a depuração, incluindo uma FAQ útil.
- [Instalando o LLDB](https://github.com/dotnet/diagnostics/blob/master/documentation/sos.md#getting-lldb) para obter instruções sobre como instalar o LLDB no Linux ou no Mac.
