---
title: Despejos-.NET
description: Uma introdução a despejos no .NET.
ms.date: 10/12/2020
ms.openlocfilehash: f68d9bd804350366625df014df4d9ca0641d5d4d
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188550"
---
# <a name="dumps"></a>Despejos

Um despejo é um arquivo que contém um instantâneo do processo no momento em que ele foi criado e pode ser útil para examinar o estado do seu aplicativo. Os despejos podem ser usados para depurar seu aplicativo .NET quando é difícil anexar um depurador a ele, como ambientes de produção ou de CI. O uso de despejos permite capturar o estado do processo problemático e examiná-lo sem a necessidade de parar o aplicativo.

## <a name="collect-dumps"></a>Coletar despejos

Os despejos podem ser coletados de diversas maneiras, dependendo de em qual plataforma você está executando seu aplicativo.

> [!NOTE]
> A coleta de um despejo dentro de um contêiner requer o recurso PTRACE, que pode ser adicionado via `--cap-add=SYS_PTRACE` ou `--privileged` .
> [!NOTE]
> Os despejos podem conter informações confidenciais, pois podem conter a memória total do processo em execução. Lide com as restrições de segurança e as orientações em mente.

### <a name="collecting-dumps-on-crash"></a>Coletando despejos na falha

Você pode usar variáveis de ambiente para configurar seu aplicativo para coletar um despejo após uma falha. Isso é útil quando você deseja entender por que ocorreu uma falha. Por exemplo, capturar um despejo quando uma exceção é gerada ajuda a identificar um problema examinando o estado do aplicativo quando ele falhou.

A tabela a seguir mostra as variáveis de ambiente que você pode configurar para coletar despejos em uma falha.

|Variável de ambiente|Descrição|Valor padrão|
|-------|---------|---|
|`COMPlus_DbgEnableMiniDump`|Se definido como 1, habilite a geração de despejo principal.|0|
|`COMPlus_DbgMiniDumpType`|Tipo de despejo a ser coletado. Para obter mais informações, consulte a tabela abaixo|2 ( `MiniDumpWithPrivateReadWriteMemory` )|
|`COMPlus_DbgMiniDumpName`|Caminho para um arquivo no qual gravar o despejo.|`/tmp/coredump.<pid>`|
|`COMPlus_CreateDumpDiagnostics`|Se definido como 1, habilite o log de diagnóstico do processo de despejo.|0|

A tabela a seguir mostra todas as opções que podem ser usadas para `COMPlus_DbgMiniDumpType` que possam ser especificadas como um valor. Por exemplo, definir `COMPlus_DbgMiniDumpType` como 1 significa que `MiniDumpNormal` o despejo de tipo será coletado em uma falha.

|Valor|Nome|Descrição|
|-----|----|-----------|
|1|`MiniDumpNormal`|Inclua apenas as informações necessárias para capturar rastreamentos de pilha para todos os threads existentes em um processo. Memória e informações de heap de GC limitadas.|
|2|`MiniDumpWithPrivateReadWriteMemory`|Inclui os heaps do GC e as informações necessárias para capturar rastreamentos de pilha para todos os threads existentes em um processo.|
|3|`MiniDumpFilterTriage`|Inclua apenas as informações necessárias para capturar rastreamentos de pilha para todos os threads existentes em um processo. Memória e informações de heap de GC limitadas.|
|4|`MiniDumpWithFullMemory`|Inclua toda a memória acessível no processo. Os dados brutos da memória são incluídos no final, para que as estruturas iniciais possam ser mapeadas diretamente sem as informações de memória bruta. Essa opção pode resultar em um arquivo muito grande.|

### <a name="collecting-dumps-at-specific-point-in-time"></a>Coletando despejos em um momento específico

Talvez você queira coletar um despejo quando o aplicativo ainda não tiver falhado. Por exemplo, se você quiser examinar o estado de um aplicativo que parece estar em um deadlock, a configuração das variáveis de ambiente para coletar despejos na falha não será útil porque o aplicativo ainda está em execução.

Para coletar o despejo em sua própria solicitação, você pode usar o `dotnet-dump` , que é uma ferramenta CLI para coletar e analisar despejos. Para obter mais informações sobre como usá-lo para coletar despejos com o `dotnet-dump` , consulte [dump Collection and Analysis Utility](dotnet-dump.md).

## <a name="analyze-dumps"></a>Analisar despejos

Você pode anlayze despejos usando a [`dotnet-dump`](dotnet-dump.md) ferramenta CLI ou com o [Visual Studio](/visualstudio/debugger/using-dump-files).

> [!NOTE]
> O Visual Studio versão 16,8 e posterior permite que você [abra despejos do Linux](https://devblogs.microsoft.com/visualstudio/linux-managed-memory-dump-debugging/) gerados no .NET Core 3.1.7 ou posterior.  
> [!NOTE]
> Se a depuração nativa for necessária, a [extensão do depurador SOS](sos-debugging-extension.md) poderá ser usada com [LLDB no Linux e no MacOS](debug-linux-dumps.md#analyze-dumps-on-linux). O SOS também tem suporte com o [windbg/CDB](/windows-hardware/drivers/debugger/debugger-download-tools) no Windows, embora o Visual Studio seja recomendado.

## <a name="see-also"></a>Confira também

Saiba mais sobre como você pode aproveitar os despejos para ajudar a diagnosticar problemas em seu aplicativo .NET.

* O tutorial [depurar despejos do Linux](debug-linux-dumps.md) orienta você sobre como depurar um despejo que foi coletado no Linux.

* Tutorial de [depuração de deadlock](debug-deadlock.md) orienta você sobre como depurar um deadlock em seu aplicativo .NET usando despejos.
