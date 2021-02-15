---
description: 'Saiba mais sobre: ponteiro de função FLockClrVersionCallback'
title: Ponteiro de função FLockClrVersionCallback
ms.date: 03/30/2017
api_name:
- FLockClrVersionCallback
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- FLockClrVersionCallback
helpviewer_keywords:
- FLockClrVersionCallback function pointer [.NET Framework hosting]
ms.assetid: 98a4762d-9ad2-45bd-9d03-39064a028b44
topic_type:
- apiref
ms.openlocfilehash: 3506cd30ab2a9e5a06b03f5010c9870280a38378
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785374"
---
# <a name="flockclrversioncallback-function-pointer"></a>Ponteiro de função FLockClrVersionCallback

Aponta para uma função que o Common Language Runtime (CLR) chama para indicar que a inicialização foi iniciada ou concluída.  
  
 Esse ponteiro de função foi preterido no .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef HRESULT (__stdcall *FLockClrVersionCallback) ( );  
```  
  
## <a name="remarks"></a>Comentários  

 Essa função é implementada pelo host.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorWks.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Função LockClrVersion](lockclrversion-function.md)
- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
