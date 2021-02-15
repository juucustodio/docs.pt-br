---
title: Extensão de depuração SOS para .NET
description: Saiba mais sobre a extensão de depuração SOS para .NET, que fornece informações sobre o ambiente CLR interno.
ms.date: 12/21/2020
helpviewer_keywords:
- debugging extensions
- SOS debugging extensions
- SOS.dll
ms.openlocfilehash: a24b946c4ffda59e17f61c065d2846dc1a6effe0
ms.sourcegitcommit: c0b803bffaf101e12f071faf94ca21b46d04ff30
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/24/2020
ms.locfileid: "97764962"
---
# <a name="sos-debugging-extension"></a>Extensão de depuração SOS

A extensão de depuração SOS permite exibir informações sobre o código que está sendo executado dentro do tempo de execução do .NET Core, tanto em processos ao vivo quanto em despejos. A extensão é pré-instalado com [dotnet-dump](dotnet-dump.md) e [windbg/DBG](/windows-hardware/drivers/debugger/debugger-download-tools)e pode ser [baixada](dotnet-sos.md) para uso com LLDB.  A extensão de depuração do SOS é útil para coletar informações sobre o heap gerenciado, procurando por corrupções de heap, exibindo tipos de dados internos usados pelo tempo de execução e exibindo informações sobre todos os códigos gerenciados em execução dentro do tempo de execução.

## <a name="syntax"></a>Syntax

### <a name="windows"></a>Windows

`![command] [options]`

### <a name="linux-and-macos"></a>Linux e macOS

`sos [command] [options]`

Muitos dos comandos têm aliases ou atalhos em lldb:

`clrstack [options]`

## <a name="commands"></a>Comandos

A tabela de comandos a seguir também está disponível em **ajuda** ou **soshelp**.  A ajuda de comando individual está disponível usando o `soshelp <command>` .

|Comando|Descrição|
|-------------|-----------------|
|**bpmd** [**-nofuturemodule**] [ \<*module name*> \<*method name*> ] [**-MD**  < `MethodDesc`>] **-list** **-Clear** \<*pending breakpoint number*> **-ClearAll**|Cria um ponto de interrupção no método especificado do módulo especificado.<br /><br /> Se o módulo e o método especificados não forem carregados, esse comando aguardará uma notificação de que o módulo foi carregado e compilado JIT (just-in-time) antes de criar um ponto de interrupção.<br /><br /> É possível gerenciar a lista dos pontos de interrupção pendentes usando as opções **-list**, **-clear** e **-clearall**:<br /><br /> A opção **-list** gerencia uma lista de todos os pontos de interrupção pendentes. Se um ponto de interrupção pendente tiver uma ID de módulo diferente de zero, esse ponto de interrupção será específico de uma função nesse módulo carregado em especial. Se o ponto de interrupção pendente tiver uma ID de módulo zero, esse ponto de interrupção se aplicará aos módulos que ainda não foram carregados.<br /><br /> Use a opção **-clear** ou **-clearall** para remover os pontos de interrupção pendentes da lista.|
|**CLRStack** [**-a**] [**-l**] [**-p**] [**-n**] [**-f**] [**-r**] [**-All**]|Fornece um rastreamento de pilha apenas do código gerenciado.<br /><br /> A opção **-p** mostra argumentos para a função gerenciada.<br /><br /> A opção **-l** mostra informações sobre as variáveis locais em um quadro. A extensão de depuração SOS não pode recuperar nomes locais, portanto, a saída para nomes locais está no formato \<*local address*> **=** \<*value*> .<br /><br /> A opção **-a** é um atalho para **-l** e **-p** combinado.<br /><br /> A opção **-n** desabilita a exibição dos nomes de arquivo de origem e dos números de linha. Se o depurador tiver a opção SYMOPT_LOAD_LINES especificada, o SOS pesquisará os símbolos de cada quadro gerenciado e, se bem-sucedido, exibirá o nome do arquivo de origem e o número da linha correspondentes. O parâmetro **-n** (sem números de linha) pode ser especificado para desabilitar esse comportamento.<br /><br />A opção **-f** (modo completo) exibe os quadros nativos intermisturando-os com os quadros gerenciados e o nome do assembly e o deslocamento da função para os quadros gerenciados.  Essa opção não exibe quadros nativos quando usado com o `dotnet-dump` .<br /><br />A opção **-r** despeja os registros para cada quadro de pilha.<br /><br />A opção **-All** despeja todas as pilhas de threads gerenciados.|
|**COMState**|Lista o modelo de apartment COM para cada thread e um ponteiro `Context`, se disponível. Só há suporte para este comando no Windows.|
|**DumpArray** [**-início** \<*startIndex*> ] [**-comprimento** \<*length*> ] [**-detalhes**] [**-nofields**] \<*array object address*><br /><br /> - ou -<br /><br /> **Da** [**-Start** \<*startIndex*> ] [**comprimento** \<*length*> ] [**-detalhe**] [**-nofields**] *endereço do objeto de matriz*>|Examina elementos de um objeto da matriz.<br /><br /> A opção **-start** especifica o índice inicial no qual os elementos são exibidos.<br /><br /> A opção **-length** especifica quantos elementos devem ser mostrados.<br /><br /> A opção **-details** exibe detalhes do elemento usando os formatos **DumpObj** e **DumpVC**.<br /><br /> A opção **-nofields** impede que as matrizes sejam exibidas. Essa opção só está disponível quando a opção **-detail** é especificada.|
|**DumpAsync** (**DumpAsync**) [**-MT** \<*MethodTable address*> ] [**-Type** \<*partial type name*> ] [**-Wait**] [**-raízes**]|DumpAsync atravessa o heap coletado pelo lixo, procurando objetos que representam máquinas de estado assíncrono como criado quando o estado de um método assíncrono é transferido para o heap.  Esse comando reconhece os computadores de estado assíncrono definidos como `async void` , `async Task` , `async Task<T>` , `async ValueTask` e `async ValueTask<T>` .<br /><br />A saída inclui um bloco de detalhes para cada objeto de computador de estado assíncrono encontrado. Os detalhes incluem:<br />-uma linha para o tipo do objeto de computador de estado assíncrono, incluindo seu endereço MethodTable, seu endereço de objeto, seu tamanho e seu nome de tipo.<br />-uma linha para o nome do tipo de máquina de estado como contido no objeto.<br />-uma listagem de cada campo na máquina de estado.<br />-uma linha para uma continuação desse objeto de computador de estado, se um ou mais tiver sido registrado.<br />-raízes GC descobertas para este objeto de máquina de estado assíncrono.<br />|
|**DumpAssembly**\<*assembly address*>|Exibe informações sobre um assembly.<br /><br /> O comando **DumpAssembly** lista vários módulos, se existirem.<br /><br /> É possível obter um endereço de assembly usando o comando **DumpDomain**.|
|**DumpClass**\<*EEClass address*>|Exibe informações sobre a estrutura `EEClass` associada a um tipo.<br /><br /> O comando **DumpClass** exibe valores de campo estáticos, mas não exibe valores de campo não estáticos.<br /><br /> Use o comando **DumpMT**, **DumpObj**, **Name2EE** ou **Token2EE** para obter um endereço da estrutura do `EEClass`.|
|**DumpDomain** [ \<*domain address*> ]|Enumera cada objeto <xref:System.Reflection.Assembly> carregado no endereço do objeto <xref:System.AppDomain> especificado.  Quando chamado sem parâmetros, o comando **DumpDomain** lista todos os objetos <xref:System.AppDomain> em um processo. Como o .NET Core tem apenas um <xref:System.AppDomain> , **DumpDomain** retornará apenas um objeto.|
|**Dumpheap** [**-stat**] [**-Strings**] [**-Short**] [**-min** \<*size*> ] [-**Max** \<*size*> ] [**-thinlock**] [**-startAtLowerBound**] [**-MT** \<*MethodTable address*> ] [**-Type** \<*partial type name*> ] [*Start* [*end*]]|Exibe informações sobre o heap com coleta de lixo e as estatísticas de coleção sobre objetos.<br /><br /> O comando **DumpHeap** exibirá um aviso se detectar fragmentação excessiva no heap do coletor de lixo.<br /><br /> A opção **-stat** restringe a saída ao resumo de tipo estatístico.<br /><br /> A opção **-strings** restringe a saída a um resumo de valor da cadeia de caracteres estatístico.<br /><br /> A opção **-short** limita a saída apenas ao endereço de cada objeto. Isso permite redirecionar facilmente do comando para outro comando do depurador para automação.<br /><br /> A opção **-min** ignora objetos menores que o parâmetro `size`, especificado em bytes.<br /><br /> A opção **-max** ignora objetos maiores que o parâmetro `size`, especificado em bytes.<br /><br /> A opção **-thinlock** relata ThinLocks.  Para obter mais informações, consulte o comando **SyncBlk**.<br /><br /> A opção `-startAtLowerBound` força o exame do heap para iniciar no limite inferior de um intervalo de endereços fornecido. Durante a fase de planejamento, o heap não costuma ser examinável porque os objetos estão sendo movidos. Essa opção força **DumpHeap** para iniciar seu exame no limite inferior especificado. Você deve fornecer o endereço de um objeto válido como o limite inferior para que essa opção funcione. É possível exibir a memória no endereço de um objeto inválido para encontrar manualmente a próxima tabela do método. Se a coleta de lixo estiver atualmente em uma chamada para `memcopy`, você também poderá encontrar o endereço do próximo objeto adicionando o tamanho ao endereço inicial, fornecido como um parâmetro.<br /><br /> A opção **-mt** lista apenas os objetos que correspondem à estrutura especificada `MethodTable`.<br /><br /> A opção **-type** lista apenas esses objetos cujo nome do tipo é uma correspondência de subcadeia de caracteres da cadeia de caracteres especificada.<br /><br /> O parâmetro `start` inicia a listagem com base no endereço especificado.<br /><br /> O parâmetro `end` para a listagem no endereço especificado.|
|**DumpIL** \<*Managed DynamicMethod object*> &#124;       \<*DynamicMethodDesc pointer*> &#124;        \<*MethodDesc pointer*>|Exibe o MSIL (Microsoft Intermediate Language) associado a um método gerenciado.<br /><br /> O MSIL dinâmico é emitido de forma diferente do MSIL que é carregado de um assembly. O MSIL dinâmico faz referência a objetos em uma matriz de objetos gerenciados, em vez dos tokens de metadados.|
|**DumpLog** [**-addr** \<*addressOfStressLog*> ] [<*filename*>]|Grava o conteúdo de um log de estresse na memória no arquivo especificado. Se você não especificar um nome, esse comando criará um arquivo chamado StressLog.txt no diretório atual.<br /><br /> O log de estresse na memória ajuda a diagnosticar falhas de estresse sem usar bloqueios ou E/S. Para habilitar o log de estresse, defina as seguintes chaves do Registro em HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework:<br /><br /> (DWORD) StressLog = 1<br /><br /> (DWORD) LogFacility = 0xffffffff<br /><br /> (DWORD) StressLogSize = 65536<br /><br /> A opção `-addr` permite especificar um log de estresse diferente do log padrão.|
|**DumpMD**\<*MethodDesc address*>|Exibe informações sobre uma estrutura `MethodDesc` no endereço especificado.<br /><br /> É possível usar o comando **IP2MD** para obter o endereço da estrutura `MethodDesc` com base em uma função gerenciada.|
|**DumpMT** [**-MD**] \<*MethodTable address*>|Exibe informações sobre uma tabela de métodos no endereço especificado. A especificação da opção **-MD** exibe uma lista de todos os métodos definidos com o objeto.<br /><br /> Cada objeto gerenciado contém um ponteiro da tabela do método.|
|**DumpModule** [**-MT**] \<*Module address*>|Exibe informações sobre um módulo no endereço especificado. A opção **-mt** exibe os tipos definidos em um módulo e os tipos referenciados pelo módulo<br /><br /> É possível usar o comando **DumpDomain** ou **DumpAssembly** para recuperar o endereço de um módulo.|
|**DumpObj** [**-nofields**] \<*object address*><br /><br /> - ou -<br /><br /> **Fazer**\<*object address*>|Exibe informações sobre um objeto no endereço especificado. O comando **DumpObj** exibe os campos, as informações da estrutura `EEClass`, a tabela do método e o tamanho do objeto.<br /><br /> É possível usar o comando **DumpStackObjects** para recuperar o endereço de um objeto.<br /><br /> Você pode executar o comando **DumpObj** em campos do tipo `CLASS` porque eles também são objetos.<br /><br /> A opção `-`**nofields** evita a exibição de campos do objeto e é útil para objetos como String.|
|**DumpRuntimeTypes**|Exibe os objetos de tipo do runtime no heap do coletor de lixo e lista seus nomes de tipo associados e tabelas de método.|
|**DumpStack** [**-EE**] [**-n**] [ `top` *pilha* [ `bottom` *STAC* `k` ]]|Exibe um rastreamento de pilha.<br /><br /> A opção **-EE** faz com que o comando **DumpStack** exiba apenas funções gerenciadas. Use os parâmetros `top` e `bottom` para limitar os quadros de pilha exibidos em plataformas x86.<br /><br /> A opção **-n** desabilita a exibição dos nomes de arquivo de origem e dos números de linha. Se o depurador tiver a opção SYMOPT_LOAD_LINES especificada, o SOS pesquisará os símbolos de cada quadro gerenciado e, se bem-sucedido, exibirá o nome do arquivo de origem e o número da linha correspondentes. O parâmetro **-n** (sem números de linha) pode ser especificado para desabilitar esse comportamento.<br /><br />
|**DumpSig** \<*sigaddr*>\<*moduleaddr*>|Exibe informações sobre uma estrutura `Sig` no endereço especificado.|
|**DumpSigElem** \<*sigaddr*>\<*moduleaddr*>|Exibe um único elemento de um objeto de assinatura. Na maioria dos casos, você deve usar **DumpSig** para observar objetos de assinatura individuais. No entanto, se uma assinatura tiver sido corrompida de alguma forma, será possível usar **DumpSigElem** para ler partes válidas dela.|
|**DumpStackObjects** [**-verificar**] [ `top` *pilha* [ `bottom` *pilha*]]<br /><br /> - ou -<br /><br /> **DSO** [**-Verify**] [ `top` *pilha* [ `bottom` *pilha*]]|Exibe todos os objetos gerenciados encontradas dentro dos limites da pilha atual.<br /><br /> A opção **-verify** valida cada campo `CLASS` não estático de um campo do objeto.<br /><br /> Use o comando **DumpStackObject** com comandos de rastreamento de pilha como **K** (windbg) ou **BT** (lldb) junto com o comando **CLRStack** para determinar os valores de variáveis e parâmetros locais.|
|**DumpVC** \<*MethodTable address*>\<*Address*>|Exibe informações sobre os campos de uma classe de valor no endereço especificado.<br /><br /> O parâmetro **MethodTable** permite que o comando **DumpVC** interprete os campos corretamente. As classes de valor não têm uma tabela de método como seu primeiro campo.|
|**EEHeap** [**-gc**] [**-loader**]|Exibe informações sobre a memória de processo consumida por estruturas de dados de tempo de execução internas.<br /><br /> As opções **-gc** e **-loader** limitam a saída desse comando ao coletor de lixo ou a estruturas de dados do carregador.<br /><br /> As informações do coletor de lixo lista os intervalos de cada segmento no heap gerenciado.  Se o ponteiro estiver dentro de um intervalo de segmentos indicado por **-gc**, o ponteiro será um ponteiro de objeto.|
|**EEStack** [**-short**] [**-EE**]|Executa o comando **DumpStack** em todos os threads no processo.<br /><br /> A opção **-EE** é passada diretamente para o comando **DumpStack**. O parâmetro **-short** limita a saída aos seguintes tipos de threads:<br /><br />Threads que tenham utilizado um bloqueio.<br /><br />Threads que foram interrompidos para permitir uma coleta de lixo.<br /><br /> Threads que estão atualmente em código gerenciado.|
|**Ehinfo** [ \<*MethodDesc address*> ] [ \<*Code address*> ]|Exibe os blocos de tratamento de exceções em um método especificado.  Este comando exibe os endereços de código e os deslocamentos do bloco de cláusula (o bloco `try`) e o bloco do manipulador (o bloco `catch`).|
|**perguntas frequentes**|Exibe perguntas frequentes  Não há suporte no `dotnet-dump`.|
|**FinalizeQueue** [**-detail**] &#124; [**-allReady**] [**-short**]|Exibe todos os objetos registrados para a finalização.<br /><br /> A opção **-detail** exibe informações extras sobre todos os `SyncBlocks` que precisam ser limpos e todos os `RuntimeCallableWrappers` (RCWs) que aguardam limpeza. Ambas as estruturas de dados são armazenadas em cache e limpas pelo thread de finalizador quando é executado.<br /><br /> A opção `-allReady` exibe todos os objetos prontos para finalização, independentemente de também já estarem marcados assim pela coleta de lixo, ou serão marcado pela próxima coleta de lixo. Os objetos prontos na lista "pronta para finalização" são objetos finalizáveis que não têm mais raízes. Essa opção pode ser muito cara, porque verifica se todos os objetos nas filas finalizáveis ainda têm raízes.<br /><br /> A opção `-short` limita a saída ao endereço de cada objeto. Se for usado com **-allReady**, ele enumerará todos os objetos que têm um finalizador que não tem mais raiz. Se for usado independentemente, ele listará todos os objetos nas filas finalizáveis e "prontas para finalização".|
|**FindAppDomain**\<*Object address*>|Determina o domínio do aplicativo de um objeto no endereço especificado.|
|**FindRoots** **-Gen** \<*N*> &#124; **-Gen qualquer** &#124;\<*object address*>|Faz o depurador parar no elemento a ser depurado na próxima coleção da geração especificada. O efeito será redefinido assim que ocorrer a parada. Para parar na próxima coleção, você precisa reemitir o comando. A *\<object address>* forma desse comando é usada após a interrupção causada pelo **-Gen** ou **-Gen** que ocorreu. Nesse momento, o depurador está no estado correto de **FindRoots** para identificar raízes para objetos nas gerações condenadas atuais. Somente com suporte no Windows.|
|**GCHandles** [**-perdomain**]|Exibe estatísticas sobre identificadores do coletor de lixo no processo.<br /><br /> A opção **-perdomain** organiza as estatísticas por domínio do aplicativo.<br /><br /> Use o comando **GCHandles** para encontrar perdas de memória causadas por perdas de identificador do coletor de lixo. Por exemplo, uma perda de memória ocorre quando o código mantém uma grande matriz porque um identificador do coletor de lixo forte continua apontando para ela e o identificador é descartado sem liberá-lo. <br /><br />Somente com suporte no Windows.|
|**GCHandleLeaks**|Procura na memória referências para identificadores do coletor de lixo fortes e fixos no processo e exibe os resultados. Se um identificador for encontrado, o comando **GCHandleLeaks** exibirá o endereço da referência. Se um identificador não for encontrado na memória, esse comando exibirá uma notificação. Somente com suporte no Windows.|
|**GCInfo**\<*MethodDesc address*>\<*Code address*>|Exibe dados que indicam quando registros ou locais da pilha contêm objetos gerenciados. Se ocorrer uma coleta de lixo, o coletor deverá saber os locais de referências para objetos de forma que possa atualizá-los com novos valores de ponteiro do objeto.|
|**Gcroot** [**-nostacks**] [**-todos**] \<*Object address*>|Exibe informações sobre referências (ou nós) para um objeto no endereço especificado.<br /><br /> O comando **GCRoot** examina todo o heap gerenciado e a tabela do identificador para identificadores dentro de outros objetos e identificadores na pilha. Em seguida, cada pilha é pesquisada em busca de ponteiros para objetos, e a fila de finalizadores também é pesquisada.<br /><br /> Este comando não determina se uma raiz da pilha é válida ou se é descartada. Use os comandos **CLRStack** e **U** para desmontar o quadro ao qual o valor local ou de argumento pertence para determinar se a raiz da pilha ainda está em uso.<br /><br /> A opção **-nostacks** restringe a pesquisa a identificadores do coletor de lixo e objetos alcançáveis.<br /><br /> A opção **-All** força a exibição de todas as raízes em vez de apenas as raízes exclusivas.|
|**GCWhere**  *\<object address>*|Exibe o local e o tamanho no heap da coleta de lixo do argumento passado. Quando o argumento está no heap gerenciado, mas não é um endereço de objeto válido, o tamanho é exibido como 0 (zero).|
|**Ajuda** (**soshelp**) [ \<*command*> ] [ `faq` ]|Exibe todos os comandos disponíveis quando nenhum parâmetro é especificado ou exibe informações detalhadas sobre o comando especificado.<br /><br /> O parâmetro `faq` exibe respostas para perguntas frequentes.|
|**HeapStat** [**-inclUnrooted** &#124; **-iu**]|Exibe os tamanhos de geração para cada heap e o espaço livre total em cada geração em cada heap. Se a opção -**inclUnrooted** for especificada, o relatório incluirá informações sobre os objetos gerenciados do heap da coleta de lixo que não tem mais raiz. Somente com suporte no Windows.|
|**HistClear**|Libera todos os recursos usados pela família de comandos `Hist`.<br /><br /> Em geral, você não precisa chamar explicitamente `HistClear`, porque cada `HistInit` limpa os recursos anteriores.|
|**HistInit**|Inicializa as estruturas de SOS com base no log de estresse salvo no elemento a ser depurado.|
|**HistObj** *<obj_address>*|Examina todos os registros de realocação do log de estresse e exibe a cadeia de realocações da coleta de lixo que podem ter levado o endereço a ser passado como um argumento.|
|**HistObjFind** *<obj_address>*  |Exibe todas as entradas de log que fazem referência a um objeto no endereço especificado.|
|**HistRoot***\<root>*|Exibe informações relacionadas a ambas as promoções e realocações da raiz especificada.<br /><br /> O valor raiz pode ser usado para rastrear o movimento de um objeto por meio das coletas de lixo.|
|**IP2MD** (**IP2MD**) \<*Code address*>|Exibe a estrutura `MethodDesc` no endereço especificado no código compilado com JIT.|
|**ListNearObj** (**lno**) *<obj_address>*|Exibe os objetos anteriores e posteriores ao endereço especificado. O comando procura o endereço no heap da coleta de lixo semelhante a um início válido de um objeto gerenciado (com base em uma tabela de método válida) e o objeto posterior ao endereço do argumento. Somente com suporte no Windows.|
|**MinidumpMode** [**0**] [**1**]|Impede a execução de comandos não seguros durante o uso de um minidespejo.<br /><br /> Passe **0** para desabilitar esse recurso ou **1** para habilitar esse recurso. Por padrão, o valor **MinidumpMode** é definido como **0**.<br /><br /> Minidespejos criados com os comandos **.dump /m** ou **.dump** têm dados específicos limitados a CLR e permitem que você execute apenas um subconjunto de comandos SOS corretamente. Alguns comandos podem falhar com erros inesperados porque as áreas necessárias de memória não são mapeadas ou estão mapeadas apenas parcialmente. Essa opção evita a execução de comandos não seguros em minidespejos. <br /><br />Somente com suporte no WinDbg.|
|**Name2EE** (**Name2EE**) \<*module name*>\<*type or method name*><br /><br /> - ou -<br /><br /> **Name2EE** \<*module name*> **!**\<*type or method name*>|Exibe a estrutura `MethodTable` e a estrutura `EEClass` do tipo ou do método especificado no módulo especificado.<br /><br /> O módulo especificado deve ser carregado no processo.<br /><br /> Para obter o nome do tipo apropriado, procure o módulo usando o [Ildasm.exe (IL Disassembler)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md). Também é possível passar `*` como o parâmetro de nome do módulo para pesquisar todos os módulos gerenciados carregados. O parâmetro *module name* também pode ser o nome do depurador para um módulo, como `mscorlib` ou `image00400000`.<br /><br /> Este comando dá suporte à sintaxe do depurador do Windows de <`module`>`!`<`type`>. O tipo deve estar totalmente qualificado.|
|**ObjSize** [ \<*Object address*> ] &#124; [**-Aggregate**] [**-stat**]|Exibe o tamanho do objeto especificado. Se você não especificar parâmetros, o comando **ObjSize** exibirá o tamanho de todos os objetos encontrados em threads gerenciados, exibirá todos os identificadores do coletor de lixo do processo e totalizará o tamanho de todos os objetos apontados por esses identificadores. O comando **ObjSize** inclui o tamanho de todos os objetos filho além do pai.<br /><br /> A opção **-aggregate** pode ser usada com o argumento **-stat** para obter uma exibição detalhada dos tipos que ainda têm raízes. Usando **!dumpheap -stat** e **!objsize -aggregate -stat**, é possível determinar quais objetos não têm mais raízes e diagnosticar diversos problemas de memória. <br /><br /> Somente com suporte no Windows.|
|**Reexception** [**-Nested**] [**-Lines**] [ \<*Exception object address*> ]<br /><br /> - ou -<br /><br /> **PE** [**-aninhado**] [ \<*Exception object address*> ]|Exibe e formata campos de qualquer objeto derivado da classe <xref:System.Exception> no endereço especificado. Se você não especificar um endereço, o comando **PrintException** exibirá a última exceção gerada no thread atual.<br /><br /> A opção **-nested** exibe detalhes sobre objetos de exceção aninhados.<br /><br /> A opção **-lines** exibe informações da origem, se disponível.<br /><br /> É possível usar esse comando para formatar e exibir o campo `_stackTrace`, que é uma matriz binária.|
|**ProcInfo** [**-env**] [**-time**] [**-mem**]|Exibe variáveis de ambiente do processo, o tempo de CPU do kernel e as estatísticas de uso da memória. Somente com suporte no WinDbg.|
|**RCWCleanupList**\<*RCWCleanupList address*>|Exibe a lista de runtime callable wrappers no endereço especificado que aguardam limpeza. Somente com suporte no WinDbg.|
|**SaveModule** \<*Base address*>\<*Filename*>|Grava uma imagem, carregada na memória do endereço especificado, no arquivo especificado. Somente com suporte no WinDbg.|
|**SetHostRuntime** [ \<runtime-directory\> ]|Este comando define o caminho para o tempo de execução do .NET Core a ser usado para hospedar o código gerenciado que é executado como parte do SOS no depurador (lldb). O tempo de execução precisa ter pelo menos a versão 2.1.0 ou superior. Se houver espaços no diretório, ele precisará ter aspas simples (').<br/><br/>Normalmente, o SOS tenta encontrar um tempo de execução do .NET Core instalado para executar seu código gerenciado automaticamente, mas esse comando estará disponível se falhar. O padrão é usar o mesmo tempo de execução (libcoreclr) que está sendo depurado. Use este comando se o tempo de execução padrão que está sendo depurado não estiver funcionando o suficiente para executar o código SOS ou se a versão for menor que 2.1.0.<br/><br/>Se você recebeu a seguinte mensagem de erro ao executar um comando SOS, use este comando para definir o caminho para 2.1.0 ou maior tempo de execução do .NET Core. <br/><br/>`(lldb) clrstack`<br/>`Error: Fail to initialize CoreCLR 80004005 ClrStack failed`<br/><br/>`(lldb) sethostruntime /usr/share/dotnet/shared/Microsoft.NETCore.App/2.1.6`<br/><br/>Você pode usar o "dotnet--informações" em um shell de comando para localizar o caminho de um tempo de execução do .NET Core instalado.|
|**SetSymbolServer** [**-MS**] [**-Disable**] [**-log**] [**-LoadSymbols**] [**-cache** \<cache-path> ] [**-Directory** \<search-directory> ] [**-Sympath** \<windows-symbol-path> ] [ \<symbol-server-URL> ]|Habilita o download do servidor de símbolos.<br/><br/>A opção **-MS** habilita o download do servidor de símbolos público da Microsoft.<br/><br/>A opção **-Disable** ativa o suporte ao download do símbolo.<br/><br/>A opção **-cache** \<cache-path> especifica um diretório de cache de símbolos. O padrão é $HOME/.dotnet/symbolcache se não for especificado.<br/><br/>A opção **-Directory** adiciona um caminho para procurar por símbolos. Pode ser mais de um.<br/><br/>A opção **-Sympath** adiciona o servidor, o cache e os caminhos de diretório no formato de caminho de símbolo do Windows.<br/><br/>A opção **-log** habilita o log de download de símbolo.<br/><br/>A opção **-LoadSymbols** tenta baixar os símbolos nativos do .NET Core para o tempo de execução. Com suporte em lldb e dotnet-dump|
|**SOSFlush**|Libera um cache SOS interno.|
|**SOSStatus** [**-Redefinir**]|Exibe o status SOS interno ou redefine o estado armazenado em cache interno.|
|**StopOnException** [**-Derived**] [**-Create** &#124; **-create2**] \<*Exception*>\<*Pseudo-register number*>|Faz com que o depurador pare quando a exceção especificada é lançada, mas continua executando enquanto outras exceções são lançadas.<br /><br /> A opção **-derived** captura a exceção especificada e cada exceção derivada da exceção especificada. <br /><br /> Somente com suporte no WinDbg.|
|**SyncBlk** [**-todos os** &#124; \<*syncblk number*> ]|Exibe a estrutura `SyncBlock` especificada ou todas as estruturas `SyncBlock`.  Se você não passar argumentos, o comando **SyncBlk** exibirá a estrutura `SyncBlock` correspondente aos objetos pertencentes a um thread.<br /><br /> Uma estrutura `SyncBlock` é um contêiner de informações extras que não precisa ser criada para cada objeto. Ele pode armazenar dados de interoperabilidade COM, códigos de hash e informações de bloqueio para operações thread-safe.|
|**ThreadPool**|Exibe informações sobre o pool de threads gerenciados, inclusive o número de solicitações de trabalho na fila, o número de threads de porta de conclusão e o número de timers.|
|**Threads** (**clrthreads**) [**-Live**] [**-Special**]|Exibe todos os threads gerenciados no processo.<br /><br /> O comando **Threads** exibe a ID abreviada do depurador, a ID do thread do CLR e a ID do thread do sistema operacional.  Além disso, o comando **Threads** exibe uma coluna Domain que indica o domínio do aplicativo no qual um thread está em execução, uma coluna APT que exibe o modo apartment COM e uma coluna Exception que exibe a última exceção gerada no thread.<br /><br /> A opção **-live** exibe threads associados a um thread dinâmico.<br /><br /> A opção **-special** exibe todos os threads especiais criados pelo CLR. Entre os threads especiais estão threads de coleta de lixo (em coleta de lixo simultânea e de servidor), threads auxiliares de depurador, threads finalizadores, threads de descarregamento <xref:System.AppDomain> e threads de timer do pool de threads.|
|**ThreadState \<** *State value field* **>**|Exibe o estado do thread. O parâmetro `value` é o valor do campo `State` na saída de relatório **Threads**.|
|**Token2EE** \<*module name*>\<*token*>|Transforma o token de metadados especificado no módulo especificado em uma estrutura `MethodTable` ou na estrutura `MethodDesc`.<br /><br /> É possível passar `*` para o parâmetro de nome do módulo para saber para o que o token é mapeado em cada módulo gerenciado carregado. Também é possível passar o nome do depurador para um módulo como, por exemplo, `mscorlib` ou `image00400000`.|
|**U** [**-GCInfo**] [**-ehinfo**] [**-n**] \<*MethodDesc address*> &#124; \<*Code address*>|Exibe uma desmontagem anotada de um método gerenciado especificado por um ponteiro de estrutura `MethodDesc` para o método ou por um endereço de código dentro do corpo do método. O comando **U** exibe todo o método do começo ao fim, com anotações que convertem tokens de metadados em nomes.<br /><br /> A opção **-gcinfo** faz o comando **U** exibir a estrutura `GCInfo` do método.<br /><br /> A opção **-ehinfo** exibe informações sobre exceção do método. Também é possível pode obter essas informações com o comando **EHInfo**.<br /><br /> A opção **-n** desabilita a exibição dos nomes de arquivo de origem e dos números de linha. Se o depurador tiver a opção SYMOPT_LOAD_LINES especificada, o SOS pesquisará os símbolos de cada quadro gerenciado e, se bem-sucedido, exibirá o nome do arquivo de origem e o número da linha correspondentes. Especifique a opção **-n** para desabilitar esse comportamento.|
|**VerifyHeap**|Verifica o heap do coletor de lixo em busca de sinais de corrupção e exibe todos os erros encontrados.<br /><br /> As corrupções de heap podem ser causadas por chamadas de invocação da plataforma construídas incorretamente. |
|**VerifyObj**\<*object address*>|Verifica o objeto passado como um argumento em busca de sinais de corrupção. Somente com suporte no Windows.|
|**VMMap**|Atravessa o espaço do endereço virtual e exibe o tipo de proteção aplicado a cada região. Somente com suporte no WinDbg.|
|**VMStat**|Fornece uma exibição resumida do espaço de endereço virtual, ordenado pelo tipo de proteção aplicado a essa memória (livre, reservada, confirmada, particular, mapeada, imagem). A coluna TOTAL exibe o resultado da coluna AVERAGE multiplicada pela coluna BLK COUNT. Somente com suporte no WinDbg.|

### <a name="dotnet-dump"></a>Dotnet-Dump

Para obter uma lista de comandos SOS disponíveis com `dotnet-dump analyze` , consulte [dotnet-dump](dotnet-dump.md#analyze-sos-commands).

### <a name="windows-debugger"></a>Depurador do Windows

Você também pode usar a extensão de depuração do SOS carregando-a no [depurador do WinDbg/DBG](/windows-hardware/drivers/debugger/debugger-download-tools) e executando comandos no depurador do Windows.  Os comandos SOS podem ser usados em processos ou despejos ao vivo.

Para carregar a extensão de depuração SOS no depurador do Windows, execute o seguinte comando na ferramenta:

```console
.loadby sos clr
```

WinDbg.exe e o Visual Studio usam uma versão de SOS.dll que corresponde à versão de Mscorwks.dll atualmente em uso. Por padrão, você deve usar a versão de SOS.dll correspondente à versão atual de Mscorwks.dll.

Para usar um arquivo de despejo criado em outro computador, verifique se o arquivo Mscorwks.dll que acompanha essa instalação está no caminho do símbolo e carregue a versão correspondente de SOS.dll.

Para carregar uma versão específica do SOS.dll, digite o seguinte comando no depurador do Windows:

```console
.load <full path to sos.dll>
```

### <a name="lldb-debugger"></a>Depurador do LLDB

Para obter instruções sobre como configurar o SOS para LLDB, consulte [dotnet-SOS](dotnet-sos.md). Os comandos SOS podem ser usados em processos ou despejos ao vivo.

Por padrão, você pode acessar todos os comandos SOS digitando: `sos [command\_name]` . No entanto, os comandos comuns têm um alias para que você não precise do `sos` prefixo:

| Comando                               | Função
| ------------------------------------- | ---------------------------------------------------------------------------------------------
|    `bpmd`                             | Cria um ponto de interrupção no método gerenciado especificado no módulo especificado.
|    `clrstack`                         | Fornece um rastreamento de pilha apenas do código gerenciado.
|    `clrthreads`                       | Liste os threads gerenciados que estão em execução.
|    `clru`                             | Exibe uma desmontagem anotada de um método gerenciado.
|    `dso`                              | Exibe todos os objetos gerenciados encontradas dentro dos limites da pilha atual.
|    `dumpasync`                        | Exibe informações sobre máquinas de estado assíncrono no heap coletado por lixo.
|    `dumpclass`                        | Exibe informações sobre a `EEClass` estrutura no endereço especificado.
|    `dumpdomain`                       | Exibe informações sobre todos os AppDomains e todos os assemblies no domínio especificado.
|    `dumpheap`                         | Exibe informações sobre o heap coletado por lixo e estatísticas de coleção sobre objetos.
|    `dumpil`                           | Exibe o MSIL (Microsoft Intermediate Language) associado a um método gerenciado.
|    `dumplog`                          | Grava o conteúdo de um log de estresse na memória no arquivo especificado.
|    `dumpmd`                           | Exibe informações sobre a `MethodDesc` estrutura no endereço especificado.
|    `dumpmodule`                       | Exibe informações sobre o módulo no endereço especificado.
|    `dumpmt`                           | Exibe informações sobre a tabela de métodos no endereço especificado.
|    `dumpobj`                          | Exibe informações sobre o objeto no endereço especificado.
|    `dumpstack`                        | Exibe um rastreamento de pilha gerenciado e nativo.
|    `eeheap`                           | Exibe informações sobre a memória de processo consumida por estruturas de dados de tempo de execução internas.
|    `eestack`                          | É executado `dumpstack` em todos os threads no processo.
|    `gcroot`                           | Exibe informações sobre referências (ou raízes) para o objeto no endereço especificado.
|    `histclear`                        | Libera todos os recursos usados pela família de comandos sua.
|    `histinit`                         | Inicializa as estruturas de SOS com base no log de estresse salvo no elemento a ser depurado.
|    `histobj`                          | Examina todos os registros de realocação do log de estresse e exibe a cadeia de realocações da coleta de lixo que podem ter levado o endereço a ser passado como um argumento.
|    `histobjfind`                      | Exibe todas as entradas de log que fazem referência ao objeto no endereço especificado.
|    `histroot`                         | Exibe informações relacionadas a ambas as promoções e realocações da raiz especificada.
|    `ip2md`                            | Exibe a estrutura `MethodDesc` no endereço especificado no código compilado com JIT.
|    `loadsymbols`                      | Carregue os símbolos do módulo nativo do .NET Core.
|    `name2ee`                          | Exibe as `MethodTable` `EEClass` estruturas e para o tipo ou método especificado no módulo especificado.
|    `pe`                               | Exibe e formata campos de qualquer objeto derivado da classe <xref:System.Exception> no endereço especificado.
|    `setclrpath`                       | Define o caminho para carregar arquivos de DAC/DBI do CoreCLR. `setclrpath <path>`
|    `sethostruntime`                   | Define ou exibe o diretório de tempo de execução do .NET Core a ser usado para executar código gerenciado em SOS.
|    `setsymbolserver`                  | Habilita o suporte ao servidor de símbolos.
|    `setsostid`                        | Define o índice de tid/thread do sistema operacional atual em vez de usar um lldb fornecido. `setsostid <tid> <index>`
|    `sos`                              | Vários comandos de depuração de CoreCLR. Para obter mais informações, consulte ' soshelp '. `sos <command-name> <args>`
|    `soshelp`                          | Exibe todos os comandos disponíveis quando nenhum parâmetro é especificado ou exibe informações de ajuda detalhadas sobre o comando especificado: `soshelp <command>`
|    `syncblk`                          | Exibe as informações do SyncBlock de suporte.

## <a name="windbgcdb-example-usage"></a>Exemplo de uso do WinDbg/CDB

| Comando  | Descrição
| - | -
| `!dumparray -start 2 -length 5 -detail 00ad28d0` | Exibe o conteúdo de uma matriz no endereço `00ad28d0` .  A exibição começa pelo segundo elemento e continua por mais cinco elementos.
| `!dumpassembly 1ca248` | Exibe o conteúdo de um assembly no endereço `1ca248` .
| `!dumpheap` | Exibe informações sobre o heap do coletor de lixo.
| `!DumpLog` | Grava o conteúdo do log de estresse na memória em um arquivo (padrão) chamado StressLog.txt no diretório atual.
 `!dumpmd 902f40` | Exibe a `MethodDesc` estrutura no endereço `902f40` .
| `!dumpmodule 1caa50` | Exibe informações sobre um módulo no endereço `1caa50` .
| `!DumpObj a79d40` | Exibe informações sobre um objeto no endereço `a79d40` .
| `!DumpVC 0090320c 00a79d9c` | Exibe os campos de uma classe de valor no endereço `00a79d9c` usando a tabela de métodos no endereço `0090320c` .
| `!eeheap` -GC | Exibe a memória de processo usada pelo coletor de lixo.
| `!finalizequeue` | Exibe todos os objetos agendados para finalização.
| `!findappdomain 00a79d98` |  Determina o domínio do aplicativo de um objeto no endereço `00a79d98` .
| `!gcinfo 5b68dbb8` | Exibe todos os identificadores do coletor de lixo no processo atual.
| `!name2ee unittest.exe MainClass.Main` | Exibe as `MethodTable` `EEClass` estruturas e para o `Main` método na classe `MainClass` no módulo `unittest.exe` .
| `!token2ee unittest.exe 02000003` | Exibe informações sobre o token de metadados no endereço `02000003` no módulo `unittest.exe` .

## <a name="lldb-example-usage"></a>Uso de exemplo de LLDB

| Comando  | Descrição
| - | -
| `sos DumpArray -start 2 -length 5 -detail 00ad28d0` | Exibe o conteúdo de uma matriz no endereço `00ad28d0` .  A exibição começa pelo segundo elemento e continua por mais cinco elementos.
| `sos DumpAssembly 1ca248` | Exibe o conteúdo de um assembly no endereço `1ca248` .
| `dumpheap` | Exibe informações sobre o heap do coletor de lixo.
| `dumplog` | Grava o conteúdo do log de estresse na memória em um arquivo (padrão) chamado StressLog.txt no diretório atual.
| `dumpmd 902f40` | Exibe a `MethodDesc` estrutura no endereço `902f40` .
| `dumpmodule 1caa50` | Exibe informações sobre um módulo no endereço `1caa50` .
| `dumpobj a79d40` | Exibe informações sobre um objeto no endereço `a79d40` .
| `sos DumpVC 0090320c 00a79d9c` | Exibe os campos de uma classe de valor no endereço `00a79d9c` usando a tabela de métodos no endereço `0090320c` .
| `eeheap -gc` | Exibe a memória de processo usada pelo coletor de lixo.
| `sos FindAppDomain 00a79d98` | Determina o domínio do aplicativo de um objeto no endereço `00a79d98` .
| `sos GCInfo 5b68dbb8` | Exibe todos os identificadores do coletor de lixo no processo atual.
| `name2ee unittest.exe MainClass.Main` | Exibe as `MethodTable` `EEClass` estruturas e para o `Main` método na classe `MainClass` no módulo `unittest.exe` .
| `sos Token2EE unittest.exe 02000003` | Exibe informações sobre o token de metadados no endereço `02000003` no módulo `unittest.exe` .
| `clrthreads` | Exibe os threads gerenciados.

## <a name="see-also"></a>Veja também

- [Uma introdução aos despejos no .NET](dumps.md)
- [Saiba como depurar um vazamento de memória no .NET Core](debug-memory-leak.md)
- [Blog sobre coleta e análise de despejos de memória](https://devblogs.microsoft.com/dotnet/collecting-and-analyzing-memory-dumps/)
- [Ferramenta de análise de despejo (dotNet-dump)](dotnet-dump.md)
- [Ferramenta de instalação do SOS (dotNet-SOS)](dotnet-sos.md)
- [Ferramenta de análise de heap (dotNet-gcdump)](dotnet-gcdump.md)
