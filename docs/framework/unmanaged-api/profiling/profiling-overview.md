---
description: 'Saiba mais sobre: visão geral da criação de perfil'
title: Visão geral da criação de perfil
ms.date: 03/30/2017
helpviewer_keywords:
- managed code, profiling API support
- unmanaged code, combining with managed code in profiling
- notification threads [.NET Framework profiling]
- unmanaged code, profiling
- profiling API [.NET Framework], and COM
- profiling API [.NET Framework], unmanaged code profiling
- profilers, writing
- profiling API [.NET Framework], call stacks
- code profilers, writing
- profiling API [.NET Framework], security considerations
- profiling API [.NET Framework], managed code support
- common language runtime, profiling
- profiling API [.NET Framework], notification threads
- call stacks [.NET Framework profiling]
- profiling API [.NET Framework], stack depth
- common language runtime, writing a profiler
- profiling API [.NET Framework], information retrieval interfaces
- shadow stacks [.NET Framework profiling]
- COM, using in the profiling API
- stack snapshots [.NET Framework profiling]
- profiling API [.NET Framework], supported features
- profiling API [.NET Framework], overview
- security, profiling API considerations
- stack depth [.NET Framework profiling]
ms.assetid: 864c2344-71dc-46f9-96b2-ed59fb6427a8
ms.openlocfilehash: f83a4435f6a4a62a190383543cf824c76a54a838
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99798908"
---
# <a name="profiling-overview"></a>Visão geral da criação de perfil

Um criador de perfil é uma ferramenta que monitora a execução de outro aplicativo. Um criador de perfil Common Language Runtime (CLR) é uma DLL (biblioteca de vínculo dinâmico) que consiste em funções que recebem mensagens e enviam mensagens para o CLR usando a API de criação de perfil. A DLL do criador de perfil é carregada pelo CLR em tempo de execução.

As ferramentas de criação de perfil tradicionais se concentram em medir a execução do aplicativo. Ou seja, eles medem o tempo gasto em cada função ou o uso de memória do aplicativo ao longo do tempo. A API de criação de perfil tem como alvo uma classe mais ampla de ferramentas de diagnóstico, como utilitários de cobertura de código e até mesmo auxílios de depuração avançados. Esses usos são todos os diagnósticos por natureza. A API de criação de perfil não apenas mede, mas também monitora a execução de um aplicativo. Por esse motivo, a API de criação de perfil nunca deve ser usada pelo próprio aplicativo, e a execução do aplicativo não deve depender (ou ser afetada pelo) o criador de perfil.

A criação de perfil de um aplicativo CLR requer mais suporte do que a criação de perfil de código de máquina compilado de uma convenção. Isso ocorre porque o CLR apresenta conceitos como domínios de aplicativo, coleta de lixo, tratamento de exceção gerenciada, compilação JIT (just-in-time) de código (convertendo a linguagem intermediária da Microsoft ou MSIL, código no código do computador nativo) e recursos semelhantes. Os mecanismos de criação de perfil convencionais não podem identificar ou fornecer informações úteis sobre esses recursos. A API de criação de perfil fornece essas informações ausentes com eficiência, com efeito mínimo sobre o desempenho do CLR e do aplicativo de criação de perfil.

A compilação JIT em tempo de execução fornece boas oportunidades de criação de perfil. A API de criação de perfil permite que um criador de perfil altere o fluxo de código MSIL na memória para uma rotina antes de ser compilado em JIT. Dessa maneira, o criador de perfil pode adicionar dinamicamente o código de instrumentação a rotinas específicas que precisam de uma investigação mais profunda. Embora essa abordagem seja possível em cenários convencionais, é muito mais fácil implementar para o CLR usando a API de criação de perfil.

## <a name="the-profiling-api"></a>A API de criação de perfil

Normalmente, a API de criação de perfil é usada para escrever um *criador de perfil de código*, que é um programa que monitora a execução de um aplicativo gerenciado.

A API de criação de perfil é usada por uma DLL do criador de perfil, que é carregada no mesmo processo que o aplicativo cujo perfil está sendo criado. A DLL do criador de perfil implementa uma interface de retorno de chamada ([ICorProfilerCallback](icorprofilercallback-interface.md) no .NET Framework versão 1,0 e 1,1, [ICorProfilerCallback2](icorprofilercallback2-interface.md) na versão 2,0 e posterior). O CLR chama os métodos nessa interface para notificar o criador de perfil de eventos no processo de perfil. O criador de perfil pode chamar de volta para o tempo de execução usando os métodos nas interfaces [ICorProfilerInfo](icorprofilerinfo-interface.md) e [ICorProfilerInfo2](icorprofilerinfo2-interface.md) para obter informações sobre o estado do aplicativo de perfil.

> [!NOTE]
> Somente a parte de coleta de dados da solução do criador de perfil deve estar em execução no mesmo processo que o aplicativo com perfil. Toda a interface do usuário e a análise de dados devem ser executadas em um processo separado.

A ilustração a seguir mostra como a DLL do criador de perfil interage com o aplicativo cujo perfil está sendo criado e o CLR.

![Captura de tela que mostra a arquitetura de criação de perfil.](./media/profiling-overview/profiling-architecture.png)

### <a name="the-notification-interfaces"></a>As interfaces de notificação

[ICorProfilerCallback](icorprofilercallback-interface.md) e [ICorProfilerCallback2](icorprofilercallback2-interface.md) podem ser considerados interfaces de notificação. Essas interfaces consistem em métodos como [ClassLoadStarted](icorprofilercallback-classloadstarted-method.md), [ClassLoadFinished](icorprofilercallback-classloadfinished-method.md)e [JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md). Cada vez que o CLR carrega ou descarrega uma classe, compila uma função e assim por diante, ele chama o método correspondente na interface ou do criador de perfil `ICorProfilerCallback` `ICorProfilerCallback2` .

Por exemplo, um criador de perfil pode medir o desempenho do código por meio de duas funções de notificação: [FunctionEnter2](functionenter2-function.md) e [FunctionLeave2](functionleave2-function.md). Apenas os carimbos de data/hora de cada notificação, acumula resultados e gera uma lista que indica quais funções consumiram a maior parte da CPU ou do tempo de entrada de parede durante a execução do aplicativo.

### <a name="the-information-retrieval-interfaces"></a>As interfaces de recuperação de informações

As outras interfaces principais envolvidas na criação de perfil são [ICorProfilerInfo](icorprofilerinfo-interface.md) e [ICorProfilerInfo2](icorprofilerinfo2-interface.md). O criador de perfil chama essas interfaces conforme necessário para obter mais informações para ajudar sua análise. Por exemplo, sempre que o CLR chama a função [FunctionEnter2](functionenter2-function.md) , ele fornece um identificador de função. O criador de perfil pode obter mais informações sobre essa função chamando o método [ICorProfilerInfo2:: GetFunctionInfo2](icorprofilerinfo2-getfunctioninfo2-method.md) para descobrir a classe pai da função, seu nome e assim por diante.

## <a name="supported-features"></a>Recursos compatíveis

A API de criação de perfil fornece informações sobre uma variedade de eventos e ações que ocorrem no Common Language Runtime. Você pode usar essas informações para monitorar o funcionamento interno dos processos e analisar o desempenho do seu aplicativo .NET Framework.

A API de criação de perfil recupera informações sobre as seguintes ações e eventos que ocorrem no CLR:

- Eventos de inicialização e desligamento CLR.

- Eventos de criação e desligamento de domínio do aplicativo.

- Assembly carregando e descarregando eventos.

- Carregando e descarregando eventos do módulo.

- Eventos de criação e destruição COM vtable.

- Compilação JIT (just-in-time) e eventos de densidade de código.

- Carregamento de classe e descarregamento de eventos.

- Criação de threads e eventos de destruição.

- Eventos de entrada e saída de função.

- Exceções.

- Transições entre a execução de código gerenciado e não gerenciado.

- Transições entre diferentes contextos de tempo de execução.

- Informações sobre as suspensões de tempo de execução.

- Informações sobre a pilha de memória de tempo de execução e a atividade de coleta de lixo.

A API de criação de perfil pode ser chamada de qualquer linguagem compatível COM COM (não gerenciado).

A API é eficiente em relação ao consumo de CPU e de memória. A criação de perfil não envolve alterações no aplicativo de perfil que são significativas o suficiente para causar resultados enganosos.

A API de criação de perfil é útil para os infileres de amostragem e não amostragem. Um *gerador de perfil de amostragem* inspeciona o perfil em tiques regulares do relógio, digamos, a 5 milissegundos de distância. Um *criador de perfil de não amostragem* é informado de um evento de forma síncrona com o thread que causa o evento.

### <a name="unsupported-functionality"></a>Funcionalidade sem suporte

A API de criação de perfil não oferece suporte para a seguinte funcionalidade:

- Código não gerenciado, que deve ser criado com o uso de métodos Win32 convencionais. No entanto, o criador de perfil do CLR inclui eventos de transição para determinar os limites entre código gerenciado e não gerenciado.

- Aplicativos de modificação automática que modificam seu próprio código para fins como programação orientada a aspectos.

- Verificação de limites, porque a API de criação de perfil não fornece essas informações. O CLR fornece suporte intrínseco para a verificação de limites de todo o código gerenciado.

- Criação de perfil remota, que não tem suporte pelos seguintes motivos:

  - A criação de perfil remota estende o tempo de execução. Ao usar as interfaces de criação de perfil, você deve minimizar o tempo de execução para que os resultados da criação de perfil não sejam afetados de forma indevidamente. Isso é especialmente verdadeiro quando o desempenho da execução está sendo monitorado. No entanto, a criação de perfil remota não é uma limitação quando as interfaces de criação de perfil são usadas para monitorar o uso de memória ou para obter informações em tempo de execução sobre quadros de pilha, objetos e assim por diante.

  - O criador de perfil de código CLR deve registrar uma ou mais interfaces de retorno de chamada com o tempo de execução no computador local no qual o aplicativo de perfil está sendo executado. Isso limita a capacidade de criar um criador de perfil de código remoto.

## <a name="notification-threads"></a>Threads de notificação

Na maioria dos casos, o thread que gera um evento também executa notificações. Essas notificações (por exemplo, [FunctionEnter](functionenter-function.md) e [FunctionLeave](functionleave-function.md)) não precisam fornecer o Explicit `ThreadID` . Além disso, o criador de perfil pode decidir usar o armazenamento local de thread para armazenar e atualizar seus blocos de análise em vez de indexar os blocos de análise no armazenamento global, com base no `ThreadID` thread afetado.

Observe que esses retornos de chamada não são serializados. Os usuários devem proteger seu código criando estruturas de dados thread-safe e bloqueando o código do criador de perfil quando necessário para impedir o acesso paralelo de vários threads. Portanto, em alguns casos, você pode receber uma sequência incomum de retornos de chamada. Por exemplo, suponha que um aplicativo gerenciado está gerando dois threads que estão executando código idêntico. Nesse caso, é possível receber um evento [ICorProfilerCallback:: JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md) para algumas funções de um thread e um `FunctionEnter` retorno de chamada do outro thread antes de receber o retorno de chamada [ICorProfilerCallback:: JITCompilationFinished](icorprofilercallback-jitcompilationfinished-method.md) . Nesse caso, o usuário receberá um `FunctionEnter` retorno de chamada para uma função que talvez não tenha sido totalmente compilada JIT (just-in-time) ainda.

## <a name="security"></a>Segurança

Uma DLL do criador de perfil é uma DLL não gerenciada que é executada como parte do mecanismo de execução de Common Language Runtime. Como resultado, o código na DLL do criador de perfil não está sujeito às restrições da segurança de acesso ao código gerenciado. As únicas limitações na DLL do criador de perfil são aquelas impostas pelo sistema operacional no usuário que está executando o aplicativo de perfil.

Os autores do criador de perfil devem tomar as precauções apropriadas para evitar problemas relacionados à segurança. Por exemplo, durante a instalação, uma DLL do criador de perfil deve ser adicionada a uma ACL (lista de controle de acesso) para que um usuário mal-intencionado não possa modificá-la.

## <a name="combining-managed-and-unmanaged-code-in-a-code-profiler"></a>Combinando código gerenciado e não gerenciado em um criador de perfil de código

Um criador de perfil escrito incorretamente pode causar referências circulares a si mesmo, resultando em um comportamento imprevisível.

Uma revisão da API de criação de perfil do CLR pode criar a impressão de que você pode escrever um criador de perfil que contém componentes gerenciados e não gerenciados que chamam uns aos outros por meio de interoperabilidade COM ou chamadas indiretas.

Embora isso seja possível a partir de uma perspectiva de design, a API de criação de perfil não oferece suporte a componentes gerenciados. Um criador de perfil do CLR deve ser completamente não gerenciado. As tentativas de combinar código gerenciado e não gerenciado em um criador de perfil do CLR podem causar violações de acesso, falha do programa ou deadlocks. Os componentes gerenciados do criador de perfil irão acionar eventos de volta para seus componentes não gerenciados, o que chamaria posteriormente os componentes gerenciados, resultando em referências circulares.

O único local em que um criador de perfil do CLR pode chamar o código gerenciado com segurança está no corpo da MSIL (Microsoft Intermediate Language) de um método. A prática recomendada para modificar o corpo da MSIL é usar os métodos de recompilação JIT na interface [ICorProfilerCallback4](icorprofilercallback4-interface.md) .

Também é possível usar os métodos de instrumentação mais antigos para modificar a MSIL. Antes que a compilação JIT (just-in-time) de uma função seja concluída, o criador de perfil pode inserir chamadas gerenciadas no corpo MSIL de um método e, em seguida, compilá-la JIT (consulte o método [ICorProfilerInfo:: GetILFunctionBody](icorprofilerinfo-getilfunctionbody-method.md) ). Essa técnica pode ser usada com êxito para instrumentação seletiva de código gerenciado ou para coletar estatísticas e dados de desempenho sobre o JIT.

Como alternativa, um criador de perfil de código pode inserir ganchos nativos no corpo MSIL de cada função gerenciada que chama o código não gerenciado. Essa técnica pode ser usada para instrumentação e cobertura. Por exemplo, um criador de perfil de código poderia inserir ganchos de instrumentação depois de cada bloco MSIL para garantir que o bloco tenha sido executado. A modificação do corpo MSIL de um método é uma operação muito delicado, e há muitos fatores que devem ser levados em consideração.

## <a name="profiling-unmanaged-code"></a>Criando perfil de código não gerenciado

A API de criação de perfil do Common Language Runtime (CLR) fornece suporte mínimo para a criação de perfil de código não gerenciado. A seguinte funcionalidade é fornecida:

- Enumeração de cadeias de pilha. Esse recurso permite que um criador de perfil de código determine o limite entre código gerenciado e código não gerenciado.

- Determinar se uma cadeia de pilha corresponde ao código gerenciado ou ao código nativo.

No .NET Framework versões 1,0 e 1,1, esses métodos estão disponíveis por meio do subconjunto em processo da API de depuração CLR. Eles são definidos no arquivo CorDebug. idl.

No .NET Framework 2,0 e posterior, você pode usar o método [ICorProfilerInfo2::D ostacksnapshot](icorprofilerinfo2-dostacksnapshot-method.md) para essa funcionalidade.

## <a name="using-com"></a>Usando COM

Embora as interfaces de criação de perfil sejam definidas como interfaces COM, o Common Language Runtime (CLR) não inicializa de fato COM para usar essas interfaces. O motivo é evitar a necessidade de definir o modelo de threading usando a função [CoInitialize](/windows/desktop/api/objbase/nf-objbase-coinitialize) antes que o aplicativo gerenciado tenha a oportunidade de especificar seu modelo de threading desejado. Da mesma forma, o criador de perfil em si não deve chamar `CoInitialize` , pois pode escolher um modelo de Threading que é incompatível com o aplicativo cujo perfil está sendo criado e pode causar uma falha no aplicativo.

## <a name="call-stacks"></a>Pilhas de Chamadas

A API de criação de perfil fornece duas maneiras de obter pilhas de chamadas: um método de instantâneo de pilha, que permite a coleta esparsa de pilhas de chamadas e um método de pilha de sombra, que controla a pilha de chamadas em todos os instantes.

### <a name="stack-snapshot"></a>Instantâneo da pilha

Um instantâneo de pilha é um rastreamento da pilha de um thread em um instante no tempo. A API de criação de perfil dá suporte ao rastreamento de funções gerenciadas na pilha, mas deixa o rastreamento de funções não gerenciadas para o próprio Stack Walker do criador de perfil.

Para obter mais informações sobre como programar o criador de perfil para movimentar pilhas gerenciadas, consulte o método [ICorProfilerInfo2::D ostacksnapshot](icorprofilerinfo2-dostacksnapshot-method.md) neste conjunto de documentação e [movimentação de pilha do profiler no .NET Framework 2,0: Noções básicas e além disso](/previous-versions/dotnet/articles/bb264782(v=msdn.10)).

### <a name="shadow-stack"></a>Pilha de sombra

Usar o método de instantâneo com muita frequência pode criar rapidamente um problema de desempenho. Se você quiser fazer rastreamentos de pilha com frequência, seu criador de perfil deverá criar uma pilha de sombra usando os retornos de chamada de exceção [FunctionEnter2](functionenter2-function.md), [FunctionLeave2](functionleave2-function.md), [FunctionTailcall2](functiontailcall2-function.md)e [ICorProfilerCallback2](icorprofilercallback2-interface.md) . A pilha de sombra é sempre atual e pode ser copiada rapidamente para o armazenamento sempre que um instantâneo de pilha é necessário.

Uma pilha de sombra pode obter argumentos de função, valores de retorno e informações sobre instanciações genéricas. Essas informações estão disponíveis apenas por meio da pilha de sombra e podem ser obtidas quando o controle é entregue a uma função. No entanto, essas informações podem não estar disponíveis posteriormente durante a execução da função.

## <a name="callbacks-and-stack-depth"></a>Retornos de chamada e profundidade da pilha

Os retornos de chamada do profiler podem ser emitidos em circunstâncias com restrições de pilha e um estouro de pilha em um retorno de chamada do criador de perfil levará a uma saída de processo imediata. Um criador de perfil deve se certificar de usar a menor pilha possível em resposta a retornos de chamada. Se o criador de perfil for destinado ao uso em processos que são robustos contra estouro de pilha, o criador de perfil em si também deve evitar o disparo do estouro de pilha.

## <a name="related-topics"></a>Tópicos relacionados

|Title|Descrição|
|-----------|-----------------|
|[Configurando um ambiente de criação de perfil](setting-up-a-profiling-environment.md)|Explica como inicializar um profiler, definir notificações de eventos e criar um perfil de um serviço do Windows.|
|[Criação de perfil de interfaces](profiling-interfaces.md)|Descreve as interfaces não gerenciadas que a API de criação de perfil usa.|
|[Criando perfil de funções estáticas globais](profiling-global-static-functions.md)|Descreve as funções estáticas globais não gerenciadas que a API de criação de perfil usa.|
|[Criando perfil de enumerações](profiling-enumerations.md)|Descreve as enumerações não gerenciadas que a API de criação de perfil usa.|
|[Estruturas de criação de perfil](profiling-structures.md)|Descreve as estruturas não gerenciadas que a API de criação de perfil usa.|
