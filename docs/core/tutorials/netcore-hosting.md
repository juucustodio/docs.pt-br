---
title: Escrever um host de runtime personalizado do .NET Core
description: Saiba como hospedar o runtime do .NET Core a partir do código nativo para dar suporte a cenários avançados que exigem o controle de como o runtime do .NET Core funciona.
author: mjrousos
ms.topic: how-to
ms.date: 12/21/2018
ms.openlocfilehash: 358cbff1ded3bd4ee9a3f78965eac1e1b1883ede
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633839"
---
# <a name="write-a-custom-net-core-host-to-control-the-net-runtime-from-your-native-code"></a>Escreva um host personalizado do .NET Core para controlar o runtime do .NET a partir de seu código nativo

Como todo código gerenciado, os aplicativos .NET Core são executados por um host. O host é responsável por iniciar o runtime (incluindo componentes como JIT e coletor de lixo) e invocar pontos de entrada gerenciados.

Hospedar o runtime do .NET Core é um cenário avançado e, na maioria dos casos, os desenvolvedores do .NET Core não precisam se preocupar com a hospedagem, pois os processos de build do .NET Core fornecem um host padrão para executar aplicativos .NET Core. No entanto, em algumas circunstâncias especializadas, pode ser útil hospedar explicitamente o runtime do .NET Core, como uma maneira de invocar o código gerenciado em um processo nativo ou para ter mais controle sobre o funcionamento do runtime.

Este artigo fornece uma visão geral das etapas necessárias para iniciar o runtime do .NET Core com base no código nativo e executar o código gerenciado nele.

## <a name="prerequisites"></a>Pré-requisitos

Como os hosts são aplicativos nativos, este tutorial aborda a construção de um aplicativo C++ para hospedar o .NET Core. Você precisará de um ambiente de desenvolvimento do C++ (como aquele fornecido pelo [Visual Studio](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs)).

Você também desejará ter um aplicativo .NET Core simples com o qual testará o host e, portanto, deverá instalar o [SDK do .NET Core](https://dotnet.microsoft.com/download) e [compilar um aplicativo .NET Core de teste pequeno](with-visual-studio.md) (como um aplicativo “Olá, Mundo”). O aplicativo “Olá, Mundo” criado pelo novo modelo de projeto de console do .NET Core é suficiente.

## <a name="hosting-apis"></a>APIs de hospedagem

Há duas APIs diferentes que podem ser usadas para hospedar o .NET Core. Este artigo (e seus [exemplos](https://github.com/dotnet/samples/tree/master/core/hosting)associados) abrange essas duas opções.

* O método preferencial de hospedar o runtime do .NET Core no .NET Core 3.0 e posteriores é com as APIs das bibliotecas `nethost` e `hostfxr`. Esses pontos de entrada tratam a complexidade de localizar e configurar o runtime para inicialização, bem como permitem iniciar um aplicativo gerenciado e chamar um método gerenciado estático.
* O método preferencial de hospedar o tempo de execução do .NET Core antes do .NET Core 3,0 é com a [`coreclrhost.h`](https://github.com/dotnet/runtime/blob/master/src/coreclr/hosts/inc/coreclrhost.h) API. Essa API expõe funções para iniciar e interromper facilmente o runtime e invocar o código gerenciado (iniciando um exe gerenciado ou chamando métodos estáticos gerenciados).

## <a name="sample-hosts"></a>Hosts de exemplo

Há [hosts de exemplo](https://github.com/dotnet/samples/tree/master/core/hosting) que demonstram as etapas descritas nos tutoriais abaixo disponíveis no repositório dotnet/samples do GitHub. Os comentários nos exemplos associam claramente as etapas numeradas destes tutoriais aos pontos em que elas são executadas no exemplo. Para obter instruções de download, consulte [Exemplos e tutoriais](../../samples-and-tutorials/index.md#view-and-download-samples).

Lembre-se de que os hosts de exemplo devem ser usados para fins de aprendizado e, portanto, não fazem uma verificação de erros rigorosa e são projetados para enfatizar a legibilidade e não a eficiência.

## <a name="create-a-host-using-nethosth-and-hostfxrh"></a>Criar um host usando o `nethost.h` e o `hostfxr.h`

As etapas a seguir detalham como usar as bibliotecas `nethost` e `hostfxr` para iniciar o runtime do .NET Core em um aplicativo nativo e chamar um método estático gerenciado. O [exemplo](https://github.com/dotnet/samples/tree/master/core/hosting/HostWithHostFxr) usa o `nethost` cabeçalho e a biblioteca instalados com o SDK do .net e copia [`coreclr_delegates.h`](https://github.com/dotnet/runtime/blob/master/src/installer/corehost/cli/coreclr_delegates.h) os [`hostfxr.h`](https://github.com/dotnet/runtime/blob/master/src/installer/corehost/cli/hostfxr.h) arquivos e do repositório [dotnet/tempo de execução](https://github.com/dotnet/runtime) .

### <a name="step-1---load-hostfxr-and-get-exported-hosting-functions"></a>Etapa 1-carregar `hostfxr` e obter funções de hospedagem exportadas

A biblioteca `nethost` fornece a função `get_hostfxr_path` para localizar a biblioteca `hostfxr`. A biblioteca `hostfxr` expõe funções para hospedar o runtime do .NET Core. A lista completa de funções pode ser encontrada no [`hostfxr.h`](https://github.com/dotnet/runtime/blob/master/src/installer/corehost/cli/hostfxr.h) e no [documento de design de hospedagem nativa](https://github.com/dotnet/runtime/blob/master/docs/design/features/native-hosting.md). A amostra e este tutorial usam o seguinte:

* `hostfxr_initialize_for_runtime_config`: Inicializa um contexto de host e se prepara para a inicialização do tempo de execução do .NET Core usando a configuração de tempo de execução especificada.
* `hostfxr_get_runtime_delegate`: Obtém um delegado para a funcionalidade de tempo de execução.
* `hostfxr_close`: Fecha um contexto de host.

A biblioteca `hostfxr` é encontrada usando `get_hostfxr_path`. Ela é carregada e suas exportações são recuperadas.

[!code-cpp[HostFxrHost#LoadHostFxr](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithHostFxr/src/NativeHost/nativehost.cpp#LoadHostFxr)]

### <a name="step-2---initialize-and-start-the-net-core-runtime"></a>Etapa 2 – Inicializar e iniciar o runtime do .NET Core

As funções `hostfxr_initialize_for_runtime_config` e `hostfxr_get_runtime_delegate` inicializam e iniciam o runtime do .NET Core usando a configuração do runtime para o componente gerenciado que será carregado. A função `hostfxr_get_runtime_delegate` é usada para obter um representante do runtime que permite carregar um assembly gerenciado e obter um ponteiro de função para um método estático no assembly em questão.

[!code-cpp[HostFxrHost#Initialize](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithHostFxr/src/NativeHost/nativehost.cpp#Initialize)]

### <a name="step-3---load-managed-assembly-and-get-function-pointer-to-a-managed-method"></a>Etapa 3 – Carregar o assembly gerenciado e obter o ponteiro de função para um método gerenciado

O representante do runtime é chamado para carregar o assembly gerenciado e obter um ponteiro de função para um método gerenciado. O representante exige o caminho do assembly, o nome do tipo e o nome do método como entradas e retorna um ponteiro de função que pode ser usado para invocar o método gerenciado.

[!code-cpp[HostFxrHost#LoadAndGet](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithHostFxr/src/NativeHost/nativehost.cpp#LoadAndGet)]

Ao passar `nullptr` como o nome do tipo de representante chamando o representante do runtime, a amostra usa uma assinatura padrão para o método gerenciado:

```csharp
public delegate int ComponentEntryPoint(IntPtr args, int sizeBytes);
```

Uma assinatura diferente pode ser usada especificando o nome do tipo de representante ao chamar o representante do runtime.

### <a name="step-4---run-managed-code"></a>Etapa 4 – Executar o código gerenciado!

O host nativo agora pode chamar o método gerenciado e passar a ele os parâmetros desejados.

[!code-cpp[HostFxrHost#CallManaged](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithHostFxr/src/NativeHost/nativehost.cpp#CallManaged)]

## <a name="create-a-host-using-coreclrhosth"></a>Criar um host usando `coreclrhost.h`

As etapas a seguir detalham como usar a `coreclrhost.h` API para iniciar o tempo de execução do .NET Core em um aplicativo nativo e chamar um método estático gerenciado. Os snippets de código neste documento usam algumas APIs específicas do Windows, mas o [host de exemplo completo](https://github.com/dotnet/samples/tree/master/core/hosting/HostWithCoreClrHost) mostra os caminhos de código do Windows e do Linux.

O [host Coexecutar UNIX](https://github.com/dotnet/runtime/tree/master/src/coreclr/hosts/unixcorerun) mostra um exemplo real mais complexo de hospedagem usando `coreclrhost.h` .

### <a name="step-1---find-and-load-coreclr"></a>Etapa 1 – Localizar e carregar a CoreCLR

As APIs de runtime do .NET Core estão em *coreclr.dll* (no Windows), em *libcoreclr.so* (no Linux) ou em *libcoreclr.dylib* (no macOS). A primeira etapa para hospedar o .NET Core é carregar a biblioteca do CoreCLR. Alguns hosts investigam diferentes caminhos ou usam parâmetros de entrada para localizar a biblioteca, enquanto outros sabem carregá-la de um determinado caminho (por exemplo, próximo ao host ou de um local geral no computador).

Depois de encontrada, a biblioteca é carregada com `LoadLibraryEx` (no Windows) ou `dlopen` (no linux/MacOS).

[!code-cpp[CoreClrHost#1](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#1)]

### <a name="step-2---get-net-core-hosting-functions"></a>Etapa 2: Obter funções de hospedagem do .NET Core

A CoreClrHost tem vários métodos importantes úteis para a hospedagem do .NET Core:

* `coreclr_initialize`: Inicia o tempo de execução do .NET Core e configura o AppDomain (e somente) padrão.
* `coreclr_execute_assembly`: Executa um assembly gerenciado.
* `coreclr_create_delegate`: Cria um ponteiro de função para um método gerenciado.
* `coreclr_shutdown`: Desliga o tempo de execução do .NET Core.
* `coreclr_shutdown_2`: Like `coreclr_shutdown` , mas também recupera o código de saída do código gerenciado.

Depois de carregar a biblioteca do CoreCLR, a próxima etapa é obter referências a essas funções usando `GetProcAddress` (no Windows) ou `dlsym` (no linux/MacOS).

[!code-cpp[CoreClrHost#2](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#2)]

### <a name="step-3---prepare-runtime-properties"></a>Etapa 3 – Preparar as propriedades do runtime

Antes de iniciar o runtime, é necessário preparar algumas propriedades para especificar o comportamento (especialmente em relação ao carregador de assembly).

As propriedades comuns incluem:

* `TRUSTED_PLATFORM_ASSEMBLIES` Essa é uma lista de caminhos de assembly (delimitada por ";" no Windows e por ":" no Linux) que o runtime poderá resolver por padrão. Alguns hosts têm manifestos embutidos em código que listam os assemblies que eles podem carregar. Outros usuários colocarão uma biblioteca em determinados locais (próximos a *coreclr.dll*, por exemplo) nessa lista.
* `APP_PATHS` Essa é uma lista de caminhos a serem investigados quanto a um assembly se ele não for encontrado na lista de TPA (assemblies de plataforma confiáveis). Como o host tem mais controle sobre quais assemblies são carregados usando a lista de TPA, uma prática recomendada para hosts é determinar quais assemblies eles esperam carregar e listá-los explicitamente. No entanto, se a investigação em tempo de execução for necessária, essa propriedade poderá habilitar esse cenário.
* `APP_NI_PATHS` Essa lista é semelhante à APP_PATHS, exceto que ela foi projetada para conter os caminhos que serão investigados para imagens nativas.
* `NATIVE_DLL_SEARCH_DIRECTORIES` Essa propriedade é uma lista de caminhos que o carregador deverá investigar ao procurar bibliotecas nativas chamadas por meio de p/invoke.
* `PLATFORM_RESOURCE_ROOTS` Essa lista inclui caminhos para investigação para assemblies de satélite de recursos (em subdiretórios específicos de cultura).

Neste host de exemplo, a lista de TPA é construída simplesmente listando todas as bibliotecas no diretório atual:

[!code-cpp[CoreClrHost#7](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#7)]

Como o exemplo é simples, ele só precisa da propriedade `TRUSTED_PLATFORM_ASSEMBLIES`:

[!code-cpp[CoreClrHost#3](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#3)]

### <a name="step-4---start-the-runtime"></a>Etapa 4 – Iniciar o runtime

`coreclrhost.h` As APIs iniciam o tempo de execução e criam o AppDomain padrão todos com uma única chamada. A função `coreclr_initialize` usa um caminho base, um nome e as propriedades já descritas e retorna um identificador ao host por meio do parâmetro `hostHandle`.

[!code-cpp[CoreClrHost#4](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#4)]

### <a name="step-5---run-managed-code"></a>Etapa 5: Executar o código gerenciado

Com o runtime iniciado, o host pode chamar o código gerenciado. Isso pode ser feito de duas maneiras diferentes. O código de exemplo vinculado a este tutorial usa a função `coreclr_create_delegate` para criar um delegado para um método estático gerenciado. Essa API usa o [nome do assembly](../../standard/assembly/names.md), o nome de tipo qualificado pelo namespace e o nome do método como entradas e retorna um delegado que pode ser usado para invocar o método.

[!code-cpp[CoreClrHost#5](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#5)]

Neste exemplo, agora o host pode chamar `managedDelegate` para executar o método `ManagedWorker.DoWork`.

Como alternativa, a função `coreclr_execute_assembly` pode ser usada para iniciar um executável gerenciado. Essa API usa um caminho de assembly e a matriz de argumentos como parâmetros de entrada. Ela carrega o assembly nesse caminho e invoca seu método principal.

```c++
int hr = executeAssembly(
        hostHandle,
        domainId,
        argumentCount,
        arguments,
        "HelloWorld.exe",
        (unsigned int*)&exitCode);
```

### <a name="step-6---shutdown-and-clean-up"></a>Etapa 6 – Desligamento e limpeza

Por fim, quando o host concluir a execução do código gerenciado, o runtime do .NET Core será desligado com `coreclr_shutdown` ou `coreclr_shutdown_2`.

[!code-cpp[CoreClrHost#6](~/samples/snippets/core/tutorials/netcore-hosting/csharp/HostWithCoreClrHost/src/SampleHost.cpp#6)]

O CoreCLR não oferece suporte à reinicialização ou descarregamento. Não chame `coreclr_initialize` novamente ou descarregue a biblioteca CoreCLR.

## <a name="conclusion"></a>Conclusão

Depois que o host for criado, ele poderá ser testado executando-o na linha de comando e passando os argumentos esperados pelo host. Ao especificar o aplicativo .NET Core a ser executado pelo host, lembre-se de usar o arquivo .dll produzido por `dotnet build`. Os executáveis (arquivos .exe) produzidos por `dotnet publish` para aplicativos autossuficientes são, na verdade, o host padrão do .NET Core (para que o aplicativo possa ser iniciado diretamente na linha de comando nos principais cenários). O código de usuário é compilado em uma dll com o mesmo nome.

Se as coisas não funcionarem inicialmente, verifique se *coreclr.dll* está disponível no local esperado pelo host, se todas as bibliotecas de estrutura necessárias estão na lista TPA e se o bit de bits do CoreCLR (32 bits ou 64 bits) corresponde à forma como o host foi criado.

A hospedagem do runtime do .NET Core é um cenário avançado do qual muitos desenvolvedores não precisarão. No entanto, para aqueles que precisam inicializar o código gerenciado de um processo nativo ou que precisam de mais controle sobre o comportamento do runtime do .NET Core, ela pode ser muito útil.
