---
description: 'Saiba mais sobre o método: ICLRMetaHost:: RequestRuntimeLoadedNotification'
title: Método ICLRMetaHost::RequestRuntimeLoadedNotification
ms.date: 03/30/2017
api_name:
- ICLRMetaHost.RequestRuntimeLoadedNotification
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost::RequestRuntimeLoadedNotification
helpviewer_keywords:
- RequestRuntimeLoadedNotification method [.NET Framework hosting]
- ICLRMetaHost::RequestRuntimeLoadedNotification method [.NET Framework hosting]
ms.assetid: 0d5ccc4d-0193-41f5-af54-45d7b70d5321
topic_type:
- apiref
ms.openlocfilehash: c385d2d845642605ad47944794f6274e8d472071
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99637489"
---
# <a name="iclrmetahostrequestruntimeloadednotification-method"></a>Método ICLRMetaHost::RequestRuntimeLoadedNotification

Fornece uma função de retorno de chamada que tem a garantia de ser chamada quando uma versão Common Language Runtime (CLR) é carregada pela primeira vez, mas ainda não foi iniciada. Esse método substitui a função [LockClrVersion](lockclrversion-function.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT RequestRuntimeLoadedNotification (  
    [in] RuntimeLoadedCallbackFnPtr pCallbackFunction);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pCallbackFunction`  
 no A função de retorno de chamada que é invocada quando um novo tempo de execução é carregado.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|E_POINTER|`pCallbackFunction` é nulo.|  
  
## <a name="remarks"></a>Comentários  

 O retorno de chamada funciona da seguinte maneira:  
  
- O retorno de chamada é invocado somente quando um tempo de execução é carregado pela primeira vez.  
  
- O retorno de chamada não é invocado para cargas reentrante do mesmo tempo de execução.  
  
- Para cargas de tempo de execução não reentrante, as chamadas para a função de retorno de chamada são serializadas.  
  
 A função de retorno de chamada tem o seguinte protótipo:  
  
```cpp  
typedef void (__stdcall *RuntimeLoadedCallbackFnPtr)(  
                     ICLRRuntimeInfo *pRuntimeInfo,  
                     CallbackThreadSetFnPtr pfnCallbackThreadSet,  
                     CallbackThreadUnsetFnPtr pfnCallbackThreadUnset);  
```  
  
 Os protótipos de função de retorno de chamada são os seguintes:  
  
- `pfnCallbackThreadSet`:  
  
    ```cpp  
    typedef HRESULT (__stdcall *CallbackThreadSetFnPtr)();  
    ```  
  
- `pfnCallbackThreadUnset`:  
  
    ```cpp  
    typedef HRESULT (__stdcall *CallbackThreadUnsetFnPtr)();  
    ```  
  
 Se o host pretende carregar ou fazer com que outro tempo de execução seja carregado de maneira reentrante, os `pfnCallbackThreadSet` `pfnCallbackThreadUnset` parâmetros e fornecidos na função de retorno de chamada devem ser usados da seguinte maneira:  
  
- `pfnCallbackThreadSet` deve ser chamado pelo thread que pode causar uma carga de tempo de execução antes que essa carga seja tentada.  
  
- `pfnCallbackThreadUnset` deve ser chamado quando o thread não causar mais tal carga de tempo de execução (e antes de retornar do retorno de chamada inicial).  
  
- `pfnCallbackThreadSet` e `pfnCallbackThreadUnset` que não são reentrante.  
  
> [!NOTE]
> Os aplicativos host não devem chamar `pfnCallbackThreadSet` e `pfnCallbackThreadUnset` fora do escopo do `pCallbackFunction` parâmetro.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRMetaHost](iclrmetahost-interface.md)
- [Hospedagem](index.md)
