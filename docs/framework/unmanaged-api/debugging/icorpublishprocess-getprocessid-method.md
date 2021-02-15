---
description: 'Saiba mais sobre o método: ICorPublishProcess:: getprocessid'
title: Método ICorPublishProcess::GetProcessID
ms.date: 03/30/2017
api_name:
- ICorPublishProcess.GetProcessID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishProcess::GetProcessID
helpviewer_keywords:
- ICorPublishProcess::GetProcessID method [.NET Framework debugging]
- GetProcessID method [.NET Framework debugging]
ms.assetid: f31185e0-f01d-463a-b392-42163e39bfe9
topic_type:
- apiref
ms.openlocfilehash: f959a49330e0ef4ade2a878acfd287657b5086ec
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99728802"
---
# <a name="icorpublishprocessgetprocessid-method"></a>Método ICorPublishProcess::GetProcessID

Obtém o identificador do sistema operacional para esse processo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetProcessID (  
    [out] unsigned   *pid  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pid`  
 fora Um ponteiro para o identificador do processo representado por esse objeto [ICorPublishProcess](icorpublishprocess-interface.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorPub. idl, CorPub. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorPublishProcess](icorpublishprocess-interface.md)
