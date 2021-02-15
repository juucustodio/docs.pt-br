---
description: 'Saiba mais sobre o método: IGCThreadControl:: SuspensionStarting'
title: Método IGCThreadControl::SuspensionStarting
ms.date: 03/30/2017
api_name:
- IGCThreadControl.SuspensionStarting
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- SuspensionStarting
helpviewer_keywords:
- IGCThreadControl::SuspensionStarting method [.NET Framework hosting]
- SuspensionStarting method, IGCThreadControl interface [.NET Framework hosting]
ms.assetid: 0af312af-98e9-415e-b182-42e80a1aee51
topic_type:
- apiref
ms.openlocfilehash: b9d068e6995a73e9a9a31d5d5debf008f9748630
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99709285"
---
# <a name="igcthreadcontrolsuspensionstarting-method"></a>Método IGCThreadControl::SuspensionStarting

Notifica o host de que o tempo de execução está começando uma suspensão de thread para uma coleta de lixo ou outra suspensão.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SuspensionStarting ( );  
```  
  
## <a name="remarks"></a>Comentários  

 Não reagende nenhum thread durante o `SuspensionStarting` retorno de chamada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IGCThreadControl](igcthreadcontrol-interface.md)
