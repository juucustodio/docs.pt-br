---
description: 'Saiba mais sobre o método: ICorThreadpool:: CorDeleteTimer'
title: Método ICorThreadpool::CorDeleteTimer
ms.date: 03/30/2017
api_name:
- ICorThreadpool.CorDeleteTimer
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorDeleteTimer
helpviewer_keywords:
- ICorThreadpool::CorDeleteTimer method [.NET Framework hosting]
- CorDeleteTimer method [.NET Framework hosting]
ms.assetid: 74847c35-7ca1-466a-b750-b25e7b03d100
topic_type:
- apiref
ms.openlocfilehash: 9096f9969702d522427640b2f881cae4aa23284d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737695"
---
# <a name="icorthreadpoolcordeletetimer-method"></a>Método ICorThreadpool::CorDeleteTimer

Esse método oferece suporte a infraestrutura do .NET Framework e não se destina a ser usado diretamente do seu código.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT CorDeleteTimer (  
    [in]  HANDLE Timer,  
    [in]  HANDLE CompletionEvent,  
    [out] BOOL*  result  
);  
```  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorThreadpool](icorthreadpool-interface.md)
