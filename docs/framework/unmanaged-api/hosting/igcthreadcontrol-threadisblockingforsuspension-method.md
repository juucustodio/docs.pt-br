---
description: 'Saiba mais sobre o método: IGCThreadControl:: ThreadIsBlockingForSuspension'
title: Método IGCThreadControl::ThreadIsBlockingForSuspension
ms.date: 03/30/2017
api_name:
- IGCThreadControl.ThreadIsBlockingForSuspension
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ThreadIsBlockingForSuspension
helpviewer_keywords:
- IGCThreadControl::ThreadIsBlockingForSuspension method [.NET Framework hosting]
- ThreadIsBlockingForSuspension method [.NET Framework hosting]
ms.assetid: ed5b5b58-7db7-46b5-9e2c-278db7159cee
topic_type:
- apiref
ms.openlocfilehash: 13023a75ab1c438abebbeb16fd9fe7c4b95c37ab
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709198"
---
# <a name="igcthreadcontrolthreadisblockingforsuspension-method"></a>Método IGCThreadControl::ThreadIsBlockingForSuspension

Notifica o host que o thread que está fazendo a chamada está prestes a bloquear, talvez para uma coleta de lixo ou outra suspensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ThreadIsBlockingForSuspension ( );  
```  
  
## <a name="remarks"></a>Comentários  

 O host pode escolher dentro do `ThreadIsBlockingForSuspension` retorno de chamada se você deseja reagendar um thread.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IGCThreadControl](igcthreadcontrol-interface.md)
