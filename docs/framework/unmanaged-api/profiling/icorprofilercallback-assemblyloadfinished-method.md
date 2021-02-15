---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: AssemblyLoadFinished'
title: Método ICorProfilerCallback::AssemblyLoadFinished
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.AssemblyLoadFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::AssemblyLoadFinished
helpviewer_keywords:
- ICorProfilerCallback::AssemblyLoadFinished method [.NET Framework profiling]
- AssemblyLoadFinished method [.NET Framework profiling]
ms.assetid: 86d98f39-52e6-4c61-a625-9760f695ff12
topic_type:
- apiref
ms.openlocfilehash: 19c0871808455e64ad8a4eb002806a87030f7882
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99648032"
---
# <a name="icorprofilercallbackassemblyloadfinished-method"></a>Método ICorProfilerCallback::AssemblyLoadFinished

Notifica o criador de perfil que concluiu o carregamento de um assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT AssemblyLoadFinished(  
    [in] AssemblyID assemblyId,  
    [in] HRESULT    hrStatus);  
```  
  
## <a name="parameters"></a>Parâmetros

- `assemblyId`

  \[in] identifica o assembly que foi carregado.

- `hrStatus`

  \[in] um HRESULT que indica se o assembly terminou de ser carregado com êxito.

## <a name="remarks"></a>Comentários  

 O valor de `assemblyId` não é válido para uma solicitação de informações até que o `AssemblyLoadFinished` método seja chamado.  
  
 Algumas partes do carregamento do assembly podem continuar após o `AssemblyLoadFinished` retorno de chamada. Um HRESULT de falha em `hrStatus` indica uma falha. No entanto, um HRESULT de êxito em `hrStatus` indica apenas que a primeira parte do carregamento do assembly foi bem-sucedida.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
