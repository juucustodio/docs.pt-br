---
description: 'Saiba mais sobre o método: ICorDebugModule3:: CreateReaderForInMemorySymbols'
title: Método ICorDebugModule3::CreateReaderForInMemorySymbols
ms.date: 03/30/2017
api_name:
- ICorDebugModule3.CreateReaderForInMemorySymbols
api_location:
- CorDebug.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule3::CreateReaderForInMemorySymbols
helpviewer_keywords:
- CreateReaderForInMemorySymbols method, ICorDebugModule3 interface [.NET Framework debugging]
- ICorDebugModule3::CreateReaderForInMemorySymbols method [.NET Framework debugging]
ms.assetid: af317171-d66d-4114-89eb-063554c74940
topic_type:
- apiref
ms.openlocfilehash: af037cc891e83f53fd94bad290f40286ed665e6f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790770"
---
# <a name="icordebugmodule3createreaderforinmemorysymbols-method"></a>Método ICorDebugModule3::CreateReaderForInMemorySymbols

Cria um leitor de símbolo de depuração para um módulo dinâmico.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateReaderForInMemorySymbols (  
      [in] REFIID riid,  
      [out][iid_is(riid)] void **    ppObj  
```  
  
## <a name="parameters"></a>Parâmetros  

 riid  
 no O IID da interface COM a ser retornada. Normalmente, essa é uma [interface ISymUnmanagedReader](../diagnostics/isymunmanagedreader-interface.md).  
  
 ppObj  
 fora Ponteiro para um ponteiro para a interface retornada.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK  
 Leitor criado com êxito.  
  
 CORDBG_E_MODULE_LOADED_FROM_DISK  
 O módulo não é um módulo na memória ou dinâmico.  
  
 CORDBG_E_SYMBOLS_NOT_AVAILABLE  
 Os símbolos não foram fornecidos pelo aplicativo ou ainda não estão disponíveis.  
  
 E_FAIL (ou outros códigos de retorno de E_)  
 Não é possível criar o leitor.  
  
## <a name="remarks"></a>Comentários  

 Esse método também pode ser usado para criar um objeto de leitor de símbolo para módulos na memória (não dinâmicos), mas somente depois que os símbolos são disponibilizados pela primeira vez (indicado pelo retorno de chamada do [método UpdateModuleSymbols](icordebugmanagedcallback-updatemodulesymbols-method.md) ).  
  
 Esse método retorna uma nova instância de leitor toda vez que é chamado (como [CComPtrBase:: CoCreateInstance](/cpp/atl/reference/ccomptrbase-class#cocreateinstance)). Portanto, o depurador deve armazenar em cache o resultado e solicitar uma nova instância somente quando os dados subjacentes podem ter mudado (ou seja, quando um retorno de chamada de [método LoadClass](icordebugmanagedcallback-loadclass-method.md) é recebido).  
  
 Módulos dinâmicos não têm nenhum símbolo disponível até que o primeiro tipo seja carregado (conforme indicado pelo retorno de chamada do [método LoadClass](icordebugmanagedcallback-loadclass-method.md) ).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** 4,5, 4, 3,5 SP1  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugRemoteTarget](icordebugremotetarget-interface.md)
- [Interface ICorDebug](icordebug-interface.md)

- [Depurando interfaces](debugging-interfaces.md)
