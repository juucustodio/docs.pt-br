---
description: 'Saiba mais sobre: interfaces de depuração'
title: Depurando interfaces
ms.date: 02/07/2019
helpviewer_keywords:
- unmanaged interfaces [.NET Framework], debugging
- debugging interfaces [.NET Framework]
- interfaces [.NET Framework debugging]
ms.assetid: b6297c26-7624-4431-8af4-14112d07bcd5
ms.openlocfilehash: 6e6cc07e200b9ecf6bf4039f4fd5fd69e27b6fda
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99717960"
---
# <a name="debugging-interfaces"></a>Depurando interfaces

Esta seção descreve as interfaces não gerenciadas que lidam com a depuração de um programa que está sendo executado no CLR (Common Language Runtime).  
  
## <a name="in-this-section"></a>Nesta seção  

 [Interface ICLRDataEnumMemoryRegions](iclrdataenummemoryregions-interface.md)\
 Fornece um método para enumerar as regiões da memória que são especificadas por chamadores.  
  
 [Interface ICLRDataEnumMemoryRegionsCallback](iclrdataenummemoryregionscallback-interface.md)\
 Fornece um método de retorno de chamada para `EnumMemoryRegions` relatar ao depurador o resultado de uma tentativa de enumerar uma região especificada da memória.  
  
 [Interface ICLRDataTarget](iclrdatatarget-interface.md)\
 Fornece métodos para interação com um processo de CLR de destino.  
  
 [Interface ICLRDataTarget2](iclrdatatarget2-interface.md)\
 Uma subclasse de `ICLRDataTarget` que é usada pela camada de serviços de acesso a dados para manipular as regiões de memória virtual no processo de destino.  
  
 [Interface ICLRDataTarget3](iclrdatatarget3-interface.md)\
 Uma subclasse de [ICLRDataTarget2](iclrdatatarget2-interface.md) que fornece acesso a informações de exceção.  
  
 [Interface ICLRDebugging](iclrdebugging-interface.md)\
 Fornece métodos que manipulam os módulos de carregamento e descarregamento para depuração.  
  
 [Interface ICLRDebuggingLibraryProvider](iclrdebugginglibraryprovider-interface.md)\
 Inclui o método de [método ProvideLibrary](iclrdebugginglibraryprovider-providelibrary-method.md) , que obtém uma interface de retorno de chamada do provedor de biblioteca que permite que Common Language Runtime bibliotecas de depuração específicas à versão sejam localizadas e carregadas sob demanda.  
  
 [Interface ICLRMetadataLocator](iclrmetadatalocator-interface.md)\
 A interface usada pela camada de serviços de acesso a dados para localizar metadados de assemblies em um processo de destino.  
  
 [Interface ICorDebug](icordebug-interface.md)\
 Fornece métodos que permitem que os desenvolvedores depurem aplicativos no ambiente do CLR.  
  
 [Interface ICorDebugAppDomain](icordebugappdomain-interface.md)\
 Fornece métodos para depurar domínios de aplicativo.  
  
 [Interface ICorDebugAppDomain2](icordebugappdomain2-interface.md)\
 Fornece métodos para trabalhar com matrizes, ponteiros, ponteiros de função e tipos ByRef. Essa interface é uma extensão da interface `ICorDebugAppDomain`.  
  
 [Interface ICorDebugAppDomain3](icordebugappdomain3-interface.md)\
 Fornece métodos para trabalhar com os tipos de Windows Runtime em um domínio de aplicativo. Essa interface é uma extensão das interfaces `ICorDebugAppDomain` e `ICorDebugAppDomain2`.  
  
 [Interface ICorDebugAppDomain4](icordebugappdomain4-interface.md)\
 Estende logicamente a interface [ICorDebugAppDomain](icordebugappdomain-interface.md) para obter um objeto gerenciado de um com callable wrapper.  
  
 [Interface ICorDebugAppDomainEnum](icordebugappdomainenum-interface.md)\
 Fornece um método que retorna um número especificado de valores `ICorDebugAppDomain` iniciando no próximo local na enumeração.  
  
 [Interface ICorDebugArrayValue](icordebugarrayvalue-interface.md)\
 Uma subclasse de `ICorDebugHeapValue` que representa uma matriz unidimensional ou multidimensional.  
  
 [Interface ICorDebugAssembly](icordebugassembly-interface.md)\
 Representa um assembly.  
  
 [Interface ICorDebugAssembly2](icordebugassembly2-interface.md)\
 Representa um assembly. Essa interface é uma extensão da interface `ICorDebugAssembly`.  
  
 [Interface ICorDebugAssembly3](icordebugassembly3-interface.md)\
 Estende logicamente a interface [ICorDebugAssembly](icordebugassembly-interface.md) para fornecer suporte para assemblies de contêiner e seus assemblies contidos. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugAssemblyEnum](icordebugassemblyenum-interface.md)\
 Implementa métodos `ICorDebugEnum` e enumera matrizes de `ICorDebugAssembly`.  
  
 [Interface ICorDebugBlockingObjectEnum](icordebugblockingobjectenum-interface.md)\
 Fornece um enumerador para uma lista de estruturas [CorDebugBlockingObject](cordebugblockingobject-structure.md) .  
  
 [Interface ICorDebugBoxValue](icordebugboxvalue-interface.md)\
 Uma subclasse de `ICorDebugHeapValue` que representa um objeto de classe com valor boxed.  
  
 [Interface ICorDebugBreakpoint](icordebugbreakpoint-interface.md)\
 Representa um ponto de interrupção em uma função ou um ponto de inspeção em um valor.  
  
 [Interface ICorDebugBreakpointEnum](icordebugbreakpointenum-interface.md)\
 Implementa métodos `ICorDebugEnum` e enumera matrizes de `ICorDebugBreakpoint`.  
  
 [Interface ICorDebugChain](icordebugchain-interface.md)\
 Representa um segmento de uma pilha de chamadas física ou lógica.  
  
 [Interface ICorDebugChainEnum](icordebugchainenum-interface.md)\
 Implementa métodos `ICorDebugEnum` e enumera matrizes de `ICorDebugChain`.  
  
 [Interface ICorDebugClass](icordebugclass-interface.md)\
 Representa um tipo, que pode ser básico ou complexo (isto é, definido pelo usuário). Se o tipo for genérico, `ICorDebugClass` representará o tipo genérico sem instância.  
  
 [Interface ICorDebugClass2](icordebugclass2-interface.md)\
 Representa uma classe genérica ou uma classe com um parâmetro do método do tipo <xref:System.Type>. Essa interface estende `ICorDebugClass`.  
  
 [Interface ICorDebugCode](icordebugcode-interface1.md)\
 Representa um segmento de código MSIL (Microsoft Intermediate Language) ou código nativo.  
  
 [Interface ICorDebugCode2](icordebugcode2-interface.md)\
 Fornece métodos que estendem os recursos de `ICorDebugCode`.  
  
 [Interface ICorDebugCode3](icordebugcode3-interface.md)\
 Fornece um método que estende [ICorDebugCode](icordebugcode-interface1.md) e [ICorDebugCode2](icordebugcode2-interface.md) para fornecer informações sobre um valor de retorno gerenciado.  
  
 [Interface ICorDebugCode4](icordebugcode4-interface.md)\
 Fornece um método que permite que um depurador Enumere as variáveis locais e os argumentos em uma função.  
  
 [Interface ICorDebugCodeEnum](icordebugcodeenum-interface.md)\
 Implementa métodos `ICorDebugEnum` e enumera matrizes de `ICorDebugCode`.  
  
 [Interface ICorDebugComObjectValue](icordebugcomobjectvalue-interface.md)\
 Fornece métodos para recuperar objetos da interface armazenados em cache.  
  
 [Interface ICorDebugContext](icordebugcontext-interface.md)\
 Representa um objeto de contexto. Essa interface ainda não foi implementada.  
  
 [Interface ICorDebugController](icordebugcontroller-interface.md)\
 Representa um escopo, um <xref:System.Diagnostics.Process> ou um <xref:System.AppDomain>, em que o contexto de execução de código pode ser controlado.  
  
 [Interface ICorDebugDataTarget](icordebugdatatarget-interface.md)\
 Fornece uma interface de retorno de chamada que oferece acesso a um determinado processo de destino.  
  
 [Interface ICorDebugDataTarget2](icordebugdatatarget2-interface.md)\
 Estende logicamente a interface [ICorDebugDataTarget](icordebugdatatarget-interface.md) . **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugDataTarget3](icordebugdatatarget3-interface.md)\
 Estende logicamente a interface [ICorDebugDataTarget](icordebugdatatarget-interface.md) para fornecer informações sobre os módulos carregados. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugDebugEvent](icordebugdebugevent-interface.md)\
 Define a interface base da qual derivam todos os eventos de depuração `ICorDebug`. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugEditAndContinueErrorInfo](icordebugeditandcontinueerrorinfo-interface.md)\
 Obsoleto. Não use essa interface.  
  
 [Interface ICorDebugEditAndContinueSnapshot](icordebugeditandcontinuesnapshot-interface.md)\
 Obsoleto. Não use essa interface.  
  
 [Interface ICorDebugEnum](icordebugenum-interface1.md)\
 Serve como a interface da base abstrata para depurar enumeradores.  
  
 [Interface ICorDebugErrorInfoEnum](icordebugerrorinfoenum-interface.md)\
 Obsoleto. Não use essa interface.  
  
 [Interface ICorDebugEval](icordebugeval-interface.md)\
 Fornece métodos para permitir que o depurador execute um código no contexto do código que está sendo depurado.  
  
 [Interface ICorDebugEval2](icordebugeval2-interface.md)\
 Estende `ICorDebugEval` para fornecer suporte a tipos genéricos.  
  
 [Interface ICorDebugExceptionDebugEvent](icordebugexceptiondebugevent-interface.md)\
 Estende a interface [ICorDebugDebugEvent](icordebugdebugevent-interface.md) para dar suporte a eventos de exceção. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugExceptionObjectCallStackEnum](icordebugexceptionobjectcallstackenum-interface.md)\
 Fornece um enumerador para informações de pilha de chamadas que são inseridas em um objeto de exceção.  
  
 [Interface ICorDebugExceptionObjectValue](icordebugexceptionobjectvalue-interface.md)\
 Estende a interface [ICorDebugObjectValue](icordebugobjectvalue-interface.md) para fornecer informações de rastreamento de pilha de um objeto de exceção gerenciado.  
  
 [Interface ICorDebugFrame](icordebugframe-interface.md)\
 Representa um quadro na pilha atual.  
  
 [Interface ICorDebugFrameEnum](icordebugframeenum-interface.md)\
 Implementa métodos `ICorDebugEnum` e enumera matrizes de `ICorDebugFrame`.  
  
 [Interface ICorDebugFunction](icordebugfunction-interface1.md)\
 Representa uma função ou um método gerenciado.  
  
 [Interface ICorDebugFunction2](icordebugfunction2-interface.md)\
 Estende `ICorDebugFunction` logicamente para fornecer suporte à depuração passo a passo Apenas Meu Código.  
  
 [Interface ICorDebugFunction3](icordebugfunction3-interface.md)\
 Estende logicamente a interface [ICorDebugFunction](icordebugfunction-interface1.md) para fornecer acesso ao código de uma solicitação ReJIT.  
  
 [Interface ICorDebugFunctionBreakpoint](icordebugfunctionbreakpoint-interface.md)\
 Estende `ICorDebugBreakpoint` para fornecer suporte a pontos de interrupção dentro de funções.  
  
 [Interface ICorDebugGCReferenceEnum](icordebuggcreferenceenum-interface.md)\
 Fornece um enumerador para objetos que serão coletados do lixo.  
  
 [Interface ICorDebugGenericValue](icordebuggenericvalue-interface.md)\
 Uma subclasse de `ICorDebugValue` que se aplica a todos os valores. Essa interface fornece métodos Get e Set para o valor.  
  
 [Interface ICorDebugGuidToTypeEnum](icordebugguidtotypeenum-interface.md)\
 Fornece um enumerador para um objeto que mapeia GUIDs e seus objetos `ICorDebugType` correspondentes.  
  
 [Interface ICorDebugHandleValue](icordebughandlevalue-interface.md)\
 Uma subclasse de `ICorDebugReferenceValue` que representa um valor de referência para o qual o depurador criou um identificador para coleta de lixo.  
  
 [Interface ICorDebugHeapEnum](icordebugheapenum-interface.md)\
 Fornece um enumerador para objetos no heap gerenciado.  
  
 [Interface ICorDebugHeapSegmentEnum](icordebugheapsegmentenum-interface.md)\
 Fornece um enumerador para regiões de memória do heap gerenciado.  
  
 [Interface ICorDebugHeapValue](icordebugheapvalue-interface.md)\
 Uma subclasse de `ICorDebugValue` que representa um objeto coletado pelo coletor de lixo do CLR.  
  
 [Interface ICorDebugHeapValue2](icordebugheapvalue2-interface1.md)\
 Uma extensão de `ICorDebugHeapValue` que fornece suporte aos identificadores de runtime.  
  
 [Interface ICorDebugHeapValue3](icordebugheapvalue3-interface.md)\
 Expõe as propriedades de bloqueio de monitoramento de objetos.  
  
 [Interface ICorDebugILCode](icordebugilcode-interface.md)\
 Representa um segmento de código IL (Intermediate Language).  
  
 [Interface ICorDebugILCode2](icordebugilcode2-interface.md)\
 Estende logicamente a interface [ICorDebugILCode](icordebugilcode-interface.md) para fornecer métodos que retornam o token para a assinatura de variável local de uma função e que mapeiam os deslocamentos de Il (linguagem intermediária instrumentada) de um criador de perfil para os deslocamentos de Il do método original.  
  
 [Interface ICorDebugILFrame](icordebugilframe-interface.md)\
 Representa um registro de ativação do código MSIL.  
  
 [Interface ICorDebugILFrame2](icordebugilframe2-interface.md)\
 Uma extensão lógica de `ICorDebugILFrame`.  
  
 [Interface ICorDebugILFrame3](icordebugilframe3-interface.md)\
 Fornece um método que encapsula o valor de retorno de uma função.  
  
 [Interface ICorDebugILFrame4](icordebugilframe4-interface.md)\
 Fornece métodos que permitem acessar as variáveis locais e inserir o código em um registro de ativação de código IL. Um parâmetro especifica se o depurador possui acesso às variáveis e ao código adicionados na instrumentação do criador de perfil ReJIT.  
  
 [Interface ICorDebugInstanceFieldSymbol](icordebuginstancefieldsymbol-interface.md)\
 Representa as informações de símbolo de depuração de um campo de instância. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugInternalFrame](icordebuginternalframe-interface.md)\
 Identifica os tipos de quadro para o depurador.  
  
 [Interface ICorDebugInternalFrame2](icordebuginternalframe2-interface.md)\
 Fornece informações sobre quadros internos, incluindo o endereço de pilha e a posição em relação aos objetos [ICorDebugFrame](icordebugframe-interface.md) .  
  
 [Interface ICorDebugLoadedModule](icordebugloadedmodule-interface.md)\
 Fornece informações sobre um módulo carregado. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)\
 Fornece métodos para processar retornos de chamada do depurador.  
  
 [Interface ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md)\
 Fornece métodos para oferecer suporte à manipulação de exceção do depurador e aos assistentes de depuração gerenciados (MDAs). `ICorDebugManagedCallback2` é uma extensão lógica de `ICorDebugManagedCallback`.  
  
 [Interface ICorDebugManagedCallback3](icordebugmanagedcallback3-interface.md)\
 Fornece um método de retorno de chamada que indica que uma notificação personalizada ativada do depurador foi gerada.  
  
 [Interface ICorDebugMDA](icordebugmda-interface.md)\
 Representa uma mensagem do assistente de depuração gerenciado (MDA).  
  
 [Interface ICorDebugMemoryBuffer](icordebugmemorybuffer-interface.md)\
 Representa um buffer na memória. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugMergedAssemblyRecord](icordebugmergedassemblyrecord-interface.md)\
 Fornece informações sobre um assembly mesclado. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugMetaDataLocator](icordebugmetadatalocator-interface.md)\
 Fornece informações de metadados ao depurador.  
  
 [Interface ICorDebugModule](icordebugmodule-interface.md)\
 Representa um módulo de CLR, que é um executável ou uma biblioteca de vínculo dinâmico (DLL).  
  
 [Interface ICorDebugModule2](icordebugmodule2-interface.md)\
 Serve como extensão lógica para `ICorDebugModule`.  
  
 [Interface ICorDebugModule3](icordebugmodule3-interface.md)\
 Cria um leitor de símbolos para um módulo dinâmico.  
  
 [Interface ICorDebugModuleBreakpoint](icordebugmodulebreakpoint-interface.md)\
 Estende `ICorDebugBreakpoint` para fornecer acesso aos módulos específicos.  
  
 [Interface ICorDebugModuleDebugEvent](icordebugmoduledebugevent-interface.md)\
 Estende a interface [ICorDebugDebugEvent](icordebugdebugevent-interface.md) para dar suporte a eventos no nível do módulo. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugModuleEnum](icordebugmoduleenum-interface.md)\
 Implementa métodos `ICorDebugEnum` e enumera matrizes de `ICorDebugModule`.  
  
 [Interface ICorDebugMutableDataTarget](icordebugmutabledatatarget-interface.md)\
 Estende a interface [ICorDebugDataTarget](icordebugdatatarget-interface.md) para dar suporte a destinos de dados mutáveis.  
  
 [Interface ICorDebugNativeFrame](icordebugnativeframe-interface.md)\
 Uma implementação especializada de `ICorDebugFrame` usada para quadros nativos.  
  
 [Interface ICorDebugNativeFrame2](icordebugnativeframe2-interface.md)\
 Fornece métodos que testam relações de quadros pai e filho.  
  
 [Interface ICorDebugObjectEnum](icordebugobjectenum-interface.md)\
 Implementa métodos `ICorDebugEnum` e enumera matrizes de objetos pelos endereços virtuais relacionados (RVAs).  
  
 [Interface ICorDebugObjectValue](icordebugobjectvalue-interface.md)\
 Uma subclasse de `ICorDebugValue` que representa um valor que contém um objeto.  
  
 [Interface ICorDebugObjectValue2](icordebugobjectvalue2-interface.md)\
 Estende `ICorDebugObjectValue` para oferecer suporte a herança e substituição.  
  
 [Interface ICorDebugProcess](icordebugprocess-interface.md)\
 Representa um processo que está executando o código gerenciado.  
  
 [Interface ICorDebugProcess2](icordebugprocess2-interface1.md)\
 Uma extensão lógica de `ICorDebugProcess`.  
  
 [Interface ICorDebugProcess3](icordebugprocess3-interface.md)\
 Controla as notificações personalizadas do depurador.

 [Interface ICorDebugProcess4](icordebugprocess4-interface.md)\
 Fornece suporte para controle de execução fora do processo.
  
 [Interface ICorDebugProcess5](icordebugprocess5-interface.md)\
 Estende a interface [ICorDebugProcess](icordebugprocess-interface.md) para dar suporte ao acesso ao heap gerenciado, para fornecer informações sobre a coleta de lixo de objetos gerenciados e para determinar se um depurador carrega imagens do cache de imagem nativa local do aplicativo.  
  
 [Interface ICorDebugProcess6](icordebugprocess6-interface.md)\
 Estende logicamente a interface [ICorDebugProcess](icordebugprocess-interface.md) para habilitar recursos como decodificação de eventos de depuração gerenciados que são codificados em eventos de depuração de exceção nativa e divisão de módulo virtual. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugProcess7](icordebugprocess7-interface.md)\
 Fornece um método que configura o depurador para manipular atualizações de metadados na memória no processo de destino.  
  
 [Interface ICorDebugProcess8](icordebugprocess8-interface.md)\
 Estende logicamente a interface [ICorDebugProcess](icordebugprocess-interface.md) para habilitar ou desabilitar determinados tipos de retornos de chamada de exceção [ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md) .  
  
 [Interface ICorDebugProcessEnum](icordebugprocessenum-interface.md)\
 Implementa métodos `ICorDebugEnum` e enumera matrizes de `ICorDebugProcess`.  
  
 [Interface ICorDebugReferenceValue](icordebugreferencevalue-interface.md)\
 Uma subclasse de `ICorDebugValue` que oferece suporte a tipos de referência.  
  
 [Interface ICorDebugRegisterSet](icordebugregisterset-interface.md)\
 Representa o conjunto de registros disponíveis no computador que está executando o código no momento.  
  
 [Interface ICorDebugRegisterSet2](icordebugregisterset2-interface.md)\
 Estende os recursos de `ICorDebugRegisterSet` para as plataformas de hardware que possuem mais de 64 registros.  
  
 [Interface ICorDebugRemote](icordebugremote-interface.md)\
 Fornece a capacidade de iniciar ou anexar um depurador gerenciado a um processo remoto de destino.  
  
 [Interface ICorDebugRemoteTarget](icordebugremotetarget-interface.md)\
 Fornece métodos que permitem a você depurar aplicativos baseados no Silverlight no ambiente do CLR.  
  
 [Interface ICorDebugRuntimeUnwindableFrame](icordebugruntimeunwindableframe-interface.md)\
 Fornece suporte para os métodos não gerenciados que exigem que o CLR (Common Language Runtime) desenrole um quadro.  
  
 [Interface ICorDebugStackWalk](icordebugstackwalk-interface.md)\
 Fornece métodos para colocar os métodos gerenciados, ou quadros, em uma pilha de thread.  
  
 [Interface ICorDebugStaticFieldSymbol](icordebugstaticfieldsymbol-interface.md)\
 Representa as informações de símbolo de depuração de um campo estático. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugStepper](icordebugstepper-interface.md)\
 Representa uma etapa na execução do código que é realizada por um depurador, serve como um identificador entre a emissão e a conclusão de um comando e fornece uma maneira de cancelar uma etapa.  
  
 [Interface ICorDebugStepper2](icordebugstepper2-interface1.md)\
 Fornece suporte para a depuração JMC (Apenas Meu Código).  
  
 [Interface ICorDebugStepperEnum](icordebugstepperenum-interface.md)\
 Implementa métodos `ICorDebugEnum` e enumera matrizes de `ICorDebugStepper`.  
  
 [Interface ICorDebugStringValue](icordebugstringvalue-interface.md)\
 Uma subclasse de `ICorDebugHeapValue` que se aplica a valores de cadeia de caracteres.  
  
 [Interface ICorDebugSymbolProvider](icordebugsymbolprovider-interface.md)\
 Fornece métodos que podem ser usados para recuperar informações de símbolo de depuração. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugSymbolProvider2](icordebugsymbolprovider2-interface.md)\
 Estende logicamente a interface [ICorDebugSymbolProvider](icordebugsymbolprovider-interface.md) para recuperar informações adicionais de símbolo de depuração. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugThread](icordebugthread-interface.md)\
 Representa um thread em um processo. O tempo de vida de uma instância `ICorDebugThread` é igual ao tempo de vida do thread que ela representa.  
  
 [Interface ICorDebugThread2](icordebugthread2-interface.md)\
 Serve como extensão lógica para `ICorDebugThread`.  
  
 [Interface ICorDebugThread3](icordebugthread3-interface.md)\
 Fornece o ponto de entrada para o [ICorDebugStackWalk](icordebugstackwalk-interface.md) e as interfaces correspondentes.  
  
 [Interface ICorDebugThread4](icordebugthread4-interface.md)\
 Fornece informações de bloqueio de thread.  
  
 [Interface ICorDebugThreadEnum](icordebugthreadenum-interface1.md)\
 Implementa métodos `ICorDebugEnum` e enumera matrizes de `ICorDebugThread`.  
  
 [Interface ICorDebugType](icordebugtype-interface.md)\
 Representa um tipo, que pode ser básico ou complexo (isto é, definido pelo usuário). Se o tipo for genérico, `ICorDebugType` representará o tipo genérico instanciado.  
  
 [Interface ICorDebugType2](icordebugtype2-interface.md)\
 Estende a interface [ICorDebugType](icordebugtype-interface.md) para recuperar o identificador de tipo de um tipo base ou tipo complexo (definido pelo usuário).  
  
 [Interface ICorDebugTypeEnum](icordebugtypeenum-interface.md)\
 Implementa métodos `ICorDebugEnum` e enumera matrizes de `ICorDebugType`.  
  
 [Interface ICorDebugUnmanagedCallback](icordebugunmanagedcallback-interface.md)\
 Fornece notificação de eventos nativos que não estão diretamente relacionados ao CLR.  
  
 [ICorDebugValue](icordebugvalue-interface.md)\
 Representa um valor de leitura ou gravação no processo que está sendo depurado.  
  
 [ICorDebugValue2](icordebugvalue2-interface.md)\
 Estende `ICorDebugValue` para oferecer suporte a `ICorDebugType`.  
  
 [Interface ICorDebugValue3](icordebugvalue3-interface.md)\
 Estende as interfaces "ICorDebugValue" e "ICorDebugValue2" para fornecer suporte a matrizes com mais de 2 GB.  
  
 [ICorDebugValueBreakpoint](icordebugvaluebreakpoint-interface.md)\
 Estende `ICorDebugBreakpoint` para fornecer acesso a valores específicos.  
  
 [ICorDebugValueEnum](icordebugvalueenum-interface.md)\
 Implementa métodos `ICorDebugEnum` e enumera matrizes de `ICorDebugValue`.  
  
 [Interface ICorDebugVariableHome](icordebugvariablehome-interface.md)\
 Representa uma variável local ou um argumento de uma função.  
  
 [Interface ICorDebugVariableHomeEnum](icordebugvariablehomeenum-interface.md)\
 Fornece um enumerador para as variáveis locais e argumentos em uma função.  
  
 [Interface ICorDebugVariableSymbol](icordebugvariablesymbol-interface.md)\
 Recupera as informações de símbolo de depuração para uma variável. **Disponível somente em .NET Native.**  
  
 [Interface ICorDebugVirtualUnwinder](icordebugvirtualunwinder-interface.md)\
 Fornece métodos para ajudar no desenrolamento de pilha. **Disponível somente em .NET Native.**  
  
 [Interface ICorPublish](icorpublish-interface.md)\
 Serve como a interface geral para os processos de publicação.  
  
 [Interface ICorPublishAppDomain](icorpublishappdomain-interface.md)\
 Representa e fornece informações sobre um domínio de aplicativo.  
  
 [Interface ICorPublishAppDomainEnum](icorpublishappdomainenum-interface.md)\
 Fornece métodos que percorrem uma coleção de objetos `ICorPublishAppDomain` existentes em um processo.  
  
 [Interface ICorPublishEnum](icorpublishenum-interface.md)\
 Serve como a base abstrata para a publicação de enumeradores.  
  
 [Interface ICorPublishProcess](icorpublishprocess-interface.md)\
 Fornece métodos que acessam informações sobre um processo.  
  
 [Interface ICorPublishProcessEnum](icorpublishprocessenum-interface.md)\
 Fornece métodos que percorrem uma coleção de objetos `ICorPublishProcess`.  

 [Interface ISOSDacInterface](isosdacinterface-interface.md)\
 Fornece métodos auxiliares para acessar dados do `SOS` .

 [Interface IXCLRDataMethodDefinition](ixclrdatamethoddefinition-interface.md)\
 Fornece métodos para consultar informações sobre uma definição de método.

 [Interface IXCLRDataMethodInstance](ixclrdatamethodinstance-interface.md)\
 Fornece métodos para consultar informações sobre uma instância de método.

 [Interface IXCLRDataModule](ixclrdatamodule-interface.md)\
 Fornece métodos para consultar informações sobre um módulo carregado.

 [Interface IXCLRDataProcess](ixclrdataprocess-interface.md)\
 Fornece métodos para consultar informações sobre um processo.
  
## <a name="related-sections"></a>Seções relacionadas  

 [Depurando coclasses](debugging-coclasses.md)\
 [Depurando funções estáticas globais](debugging-global-static-functions.md)\
 [Depurando enumerações](debugging-enumerations.md)\
 [Estruturas de depuração](debugging-structures.md)\
