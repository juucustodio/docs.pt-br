---
description: 'Saiba mais sobre: método ICorPublish:: GetProcess'
title: Método ICorPublish::GetProcess
ms.date: 03/30/2017
api_name:
- ICorPublish.GetProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublish::GetProcess
helpviewer_keywords:
- ICorPublish::GetProcess method [.NET Framework debugging]
- GetProcess method, ICorPublish interface [.NET Framework debugging]
ms.assetid: c5143805-2eb7-45b8-85ed-c8fb34df1084
topic_type:
- apiref
ms.openlocfilehash: d288a772274618cc99b63a68b37e84e543957b44
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99721964"
---
# <a name="icorpublishgetprocess-method"></a>Método ICorPublish::GetProcess

Obtém uma instância de [ICorPublishProcess](icorpublishprocess-interface.md) que representa o processo com o identificador especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetProcess(  
    [in] unsigned              pid,
    [out] ICorPublishProcess   **ppProcess  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pid`  
 no O identificador do processo.  
  
 `ppProcess`  
 fora Um ponteiro para o endereço de uma `ICorPublishProcess` instância que representa o processo.  
  
## <a name="remarks"></a>Comentários  

 `GetProcess` falhará se o processo não existir ou não for um processo gerenciado que possa ser depurado pelo usuário atual.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorPub. idl, CorPub. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorPublish](icorpublish-interface.md)
