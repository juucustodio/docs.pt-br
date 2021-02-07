---
description: 'Saiba mais sobre o método: ICLRDebugging:: OpenVirtualProcess'
title: Método ICLRDebugging::OpenVirtualProcess
ms.date: 03/30/2017
api_name:
- ICLRDebugging.OpenVirtualProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDebugging::OpenVirtualProcess
helpviewer_keywords:
- OpenVirtualProcess method [.NET Framework debugging]
- ICLRDebugging::OpenVirtualProcess method [.NET Framework debugging]
ms.assetid: e8ab7c41-d508-4ed9-8a31-ead072b5a314
topic_type:
- apiref
ms.openlocfilehash: f9f195e1202a26a13b09cace74328c3937a9fcf1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99723290"
---
# <a name="iclrdebuggingopenvirtualprocess-method"></a>Método ICLRDebugging::OpenVirtualProcess

Obtém a interface ICorDebugProcess que corresponde a um módulo Common Language Runtime (CLR) carregado no processo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT OpenVirtualProcess(  
    [in] ULONG64 moduleBaseAddress,  
    [in] IUnknown * pDataTarget,  
    [in] ICLRDebuggingLibraryProvider * pLibraryProvider,  
    [in] CLR_DEBUGGING_VERSION * pMaxDebuggerSupportedVersion,  
    [in] REFIID riidProcess,  
    [out, iid_is(riidProcess)] IUnknown ** ppProcess,  
    [in, out] CLR_DEBUGGING_VERSION * pVersion,  
    [out] CLR_DEBUGGING_PROCESS_FLAGS * pdwFlags);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `moduleBaseAddress`  
 no O endereço base de um módulo no processo de destino. COR_E_NOT_CLR será retornado se o módulo especificado não for um módulo CLR.  
  
 `pDataTarget`  
 no Uma abstração de destino de dados que permite que o depurador gerenciado Inspecione o estado do processo. O depurador deve implementar a interface [ICorDebugDataTarget](icordebugdatatarget-interface.md) . Você deve implementar a interface [ICLRDebuggingLibraryProvider](iclrdebugginglibraryprovider-interface.md) para dar suporte a cenários em que o CLR que está sendo depurado não está instalado localmente no computador.  
  
 `pLibraryProvider`  
 no Uma interface de retorno de chamada do provedor de biblioteca que permite que bibliotecas de depuração específicas da versão sejam localizadas e carregadas sob demanda. Esse parâmetro será necessário somente se `ppProcess` ou `pFlags` não for `null` .  
  
 `pMaxDebuggerSupportedVersion`  
 no A versão mais recente do CLR que este depurador pode depurar. Você deve especificar as versões principal, secundária e de compilação da última versão do CLR à qual este depurador dá suporte e definir o número de revisão como 65535 para acomodar futuras versões de serviço do CLR in-loco.  
  
 `riidProcess`  
 no A ID da interface ICorDebugProcess a ser recuperada. Atualmente, os únicos valores aceitos são IID_CORDEBUGPROCESS3, IID_CORDEBUGPROCESS2 e IID_CORDEBUGPROCESS.  
  
 `ppProcess`  
 fora Um ponteiro para a interface COM que é identificado pelo `riidProcess` .  
  
 `pVersion`  
 [entrada, saída] A versão do CLR. Na entrada, esse valor pode ser `null` . Ele também pode apontar para uma estrutura de [CLR_DEBUGGING_VERSION](clr-debugging-version-structure.md) ; nesse caso, o campo da estrutura `wStructVersion` deve ser inicializado como 0 (zero).  
  
 Na saída, a `CLR_DEBUGGING_VERSION` estrutura retornada será preenchida com as informações de versão do CLR.  
  
 `pdwFlags`  
 fora Sinalizadores informativos sobre o tempo de execução especificado. Consulte o tópico [CLR_DEBUGGING_PROCESS_FLAGS](clr-debugging-process-flags-enumeration.md) para obter uma descrição dos sinalizadores.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|E_POINTER|`pDataTarget` é `null`.|  
|CORDBG_E_LIBRARY_PROVIDER_ERROR|O retorno de chamada [ICLRDebuggingLibraryProvider](iclrdebugginglibraryprovider-interface.md) retorna um erro ou não fornece um identificador válido.|  
|CORDBG_E_MISSING_DATA_TARGET_INTERFACE|`pDataTarget` não implementa as interfaces de destino de dados necessárias para esta versão do tempo de execução.|  
|CORDBG_E_NOT_CLR|O módulo indicado não é um módulo CLR. Esse HRESULT também é retornado quando um módulo CLR não pode ser detectado porque a memória foi corrompida, o módulo não está disponível ou a versão do CLR é posterior à versão de Shim.|  
|CORDBG_E_UNSUPPORTED_DEBUGGING_MODEL|Esta versão de tempo de execução não dá suporte a este modelo de depuração. Atualmente, o modelo de depuração não tem suporte das versões do CLR antes do .NET Framework 4. O `pwszVersion` parâmetro de saída ainda é definido como o valor correto após esse erro.|  
|CORDBG_E_UNSUPPORTED_FORWARD_COMPAT|A versão do CLR é maior que a versão que este depurador declara para dar suporte. O `pwszVersion` parâmetro de saída ainda é definido como o valor correto após esse erro.|  
|E_NO_INTERFACE|A `riidProcess` interface não está disponível.|  
|CORDBG_E_UNSUPPORTED_VERSION_STRUCT|A `CLR_DEBUGGING_VERSION` estrutura não tem um valor reconhecido para `wStructVersion` . O único valor aceito neste momento é 0.|  
  
## <a name="exceptions"></a>Exceções  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
