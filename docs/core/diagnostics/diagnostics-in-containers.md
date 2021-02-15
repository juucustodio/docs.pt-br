---
title: Coletar diagnósticos em contêineres
description: Neste artigo, você aprenderá como as ferramentas de diagnóstico do .NET Core podem ser usadas em contêineres do Docker.
ms.date: 09/01/2020
ms.openlocfilehash: cf4bbdf75e943f093a2202f91303a2eea7125487
ms.sourcegitcommit: 5114e7847e0ff8ddb8c266802d47af78567949cf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2020
ms.locfileid: "94916203"
---
# <a name="collect-diagnostics-in-containers"></a>Coletar diagnósticos em contêineres

As mesmas ferramentas de diagnóstico que são úteis para diagnosticar problemas do .NET Core em outros cenários também funcionam em contêineres do Docker. No entanto, algumas das ferramentas exigem etapas especiais para trabalhar em um contêiner. Este artigo aborda como as ferramentas para reunir rastreamentos de desempenho e coletar despejos podem ser usadas em contêineres do Docker.

## <a name="using-net-core-cli-tools-in-a-container"></a>Usando ferramentas de CLI do .NET Core em um contêiner

**Essas ferramentas se aplicam a: ✔️** SDK do .net Core 3,0 e versões posteriores

As ferramentas de diagnóstico da CLI global do .NET Core ( [`dotnet-counters`](dotnet-counters.md) , [`dotnet-dump`](dotnet-dump.md) , e [`dotnet-gcdump`](dotnet-gcdump.md) [`dotnet-trace`](dotnet-trace.md) ) foram projetadas para funcionar em uma ampla variedade de ambientes e devem funcionar diretamente em contêineres do Docker. Por isso, essas ferramentas são o método preferencial para coletar informações de diagnóstico para cenários do .NET Core visando o .NET Core 3,0 ou superior (ou 3,1 ou superior no caso do `dotnet-gcdump` ) em contêineres.

O único fator de complicação de usar essas ferramentas em um contêiner é que elas são instaladas com o SDK do .NET Core e muitos contêineres do Docker são executados sem o SDK do .NET Core presente. Uma solução fácil para esse problema é instalar as ferramentas na imagem inicial do Docker. As ferramentas não precisam do SDK do .NET Core para serem executadas, apenas para serem instaladas. Portanto, é possível criar um Dockerfile com uma compilação de [vários estágios](https://docs.docker.com/develop/develop-images/multistage-build/) que instala as ferramentas em um estágio de compilação (em que o SDK do .NET Core está presente) e, em seguida, copia os binários na imagem final. A única desvantagem dessa abordagem é o tamanho maior da imagem do Docker.

```dockerfile
# In build stage
# Install desired .NET CLI diagnostics tools
RUN dotnet tool install --tool-path /tools dotnet-trace
RUN dotnet tool install --tool-path /tools dotnet-counters
RUN dotnet tool install --tool-path /tools dotnet-dump

...

# In final stage
# Copy diagnostics tools
WORKDIR /tools
COPY --from=build /tools .
```

Como alternativa, o SDK do .NET Core pode ser instalado em um contêiner quando necessário para instalar as ferramentas da CLI. Lembre-se de que a instalação do SDK do .NET Core terá o efeito colateral de reinstalar o tempo de execução do .NET Core. Portanto, certifique-se de instalar a versão do SDK que corresponde ao tempo de execução presente no contêiner.

### <a name="using-net-core-global-cli-tools-in-a-sidecar-container"></a>Usando as ferramentas da CLI global do .NET Core em um contêiner sidecar

Se você quiser usar as ferramentas de diagnóstico da CLI global do .NET Core para diagnosticar processos em um contêiner diferente, tenha em mente os seguintes requisitos adicionais:

1. Os contêineres devem [compartilhar um namespace de processo](https://docs.docker.com/engine/reference/run/#pid-settings---pid) (para que as ferramentas no contêiner sidecar possam acessar processos no contêiner de destino).
2. As ferramentas de diagnóstico da CLI global do .NET Core precisam acessar os arquivos que o tempo de execução do .NET Core grava no diretório/tmp, de modo que o diretório/tmp deve ser compartilhado entre o contêiner de destino e o sidecar por meio de uma montagem de volume. Isso pode ser feito, por exemplo, fazendo com que os contêineres compartilhem um [volume comum ou um volume kubernetes](https://docs.docker.com/storage/volumes/#create-and-manage-volumes) [emptyDir](https://kubernetes.io/docs/concepts/storage/volumes/#emptydir) . Se você tentar usar as ferramentas de diagnóstico de um contêiner sidecar sem compartilhar o diretório/tmp, receberá um erro sobre o processo "não está executando o tempo de execução do .NET compatível".

## <a name="using-perfcollect-in-a-container"></a>Usando `PerfCollect` em um contêiner

**Essa ferramenta se aplica a: ✔️** .net Core 2,1 e versões posteriores

O [`PerfCollect`](./trace-perfcollect-lttng.md) script é útil para coletar rastreamentos de desempenho e é a ferramenta recomendada para coletar rastreamentos antes do .NET Core 3,0. Se estiver usando `PerfCollect` em um contêiner, tenha em mente os seguintes requisitos:

1. `PerfCollect`requer o [ `SYS_ADMIN` recurso](https://man7.org/linux/man-pages/man7/capabilities.7.html) (para executar a `perf` ferramenta), portanto, verifique se o contêiner foi [iniciado com esse recurso](https://docs.docker.com/engine/reference/run/#runtime-privilege-and-linux-capabilities).
2. `PerfCollect` requer que algumas variáveis de ambiente sejam definidas antes do aplicativo que está iniciando a criação de perfil. Eles podem ser definidos em um [Dockerfile](https://docs.docker.com/engine/reference/builder/#env) ou ao [iniciar o contêiner](https://docs.docker.com/engine/reference/run/#env-environment-variables). Como essas variáveis não devem ser definidas em ambientes de produção normais, é comum apenas adicioná-las ao iniciar um contêiner cujo perfil será criado. As duas variáveis que o PerfCollect requer são:
    1. COMPlus_PerfMapEnabled = 1
    1. COMPlus_EnableEventLog = 1

### <a name="using-perfcollect-in-a-sidecar-container"></a>Usando `PerfCollect` em um contêiner sidecar

Se você quiser executar `PerfCollect` em um contêiner para criar o perfil de um processo do .NET Core em um contêiner diferente, a experiência será quase a mesma, exceto para essas diferenças:

1. As variáveis de ambiente mencionadas anteriormente (COMPlus_PerfMapEnabled e COMPlus_EnableEventLog) devem ser definidas para o contêiner de destino (não o que está em execução `PerfCollect` ).
2. O contêiner em execução `PerfCollect` deve ter a `SYS_ADMIN` capacidade (não o contêiner de destino).
3. Os dois contêineres devem [compartilhar um namespace de processo](https://docs.docker.com/engine/reference/run/#pid-settings---pid).

## <a name="using-createdump-in-a-container"></a>Usando `createdump` em um contêiner

**Essa ferramenta se aplica a: ✔️** .net Core 2,1 e versões posteriores

Uma alternativa ao `dotnet-dump` , [`createdump`](https://github.com/dotnet/runtime/blob/master/docs/design/coreclr/botr/xplat-minidump-generation.md) pode ser usada para criar dumps de núcleo no Linux contendo informações nativas e gerenciadas. A `createdump` ferramenta é instalada com o tempo de execução do .NET Core e pode ser encontrada ao lado de libcoreclr.so (normalmente em "/usr/share/dotnet/Shared/Microsoft.NETCore.app/[Version]"). A ferramenta funciona da mesma forma em um contêiner como acontece em ambientes Linux não-contêineres, com a única exceção de que a ferramenta requer o [ `SYS_PTRACE` recurso](https://man7.org/linux/man-pages/man7/capabilities.7.html), portanto, o contêiner do Docker deve ser [iniciado com esse recurso](https://docs.docker.com/engine/reference/run/#runtime-privilege-and-linux-capabilities).

### <a name="using-createdump-in-a-sidecar-container"></a>Usando `createdump` em um contêiner sidecar

Se você quiser usar o `createdump` para criar um despejo de um processo em um contêiner diferente, a experiência será quase a mesma, exceto para essas diferenças:

1. O contêiner em execução `createdump` deve ter a `SYS_PTRACE` capacidade (não o contêiner de destino).
2. Os dois contêineres devem [compartilhar um namespace de processo](https://docs.docker.com/engine/reference/run/#pid-settings---pid).
