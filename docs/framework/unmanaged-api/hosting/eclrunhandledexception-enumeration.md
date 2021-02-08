---
description: 'Saiba mais sobre: Enumeração EClrUnhandledException'
title: Enumeração EClrUnhandledException
ms.date: 03/30/2017
api_name:
- EClrUnhandledException
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrUnhandledException
helpviewer_keywords:
- EClrUnhandledException enumeration [.NET Framework hosting]
ms.assetid: d231044e-2b53-4836-93f9-8117ff0e5c3a
topic_type:
- apiref
ms.openlocfilehash: 088d448a92c4d9030208537b9c788477c85f9d37
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785543"
---
# <a name="eclrunhandledexception-enumeration"></a>Enumeração EClrUnhandledException

Descreve as opções disponíveis para gerenciar exceções que não são manipuladas no código do usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef enum {  
    eRuntimeDeterminedPolicy,  
    eHostDeterminedPolicy  
} EClrUnhandledException;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`eRuntimeDeterminedPolicy`|Especifica que o comportamento padrão ocorre. O processo é interrompido.|  
|`eHostDeterminedPolicy`|Especifica que o Common Language Runtime (CLR) ignora exceções sem tratamento e permite que o host determine qualquer ação adicional.|  
  
## <a name="remarks"></a>Comentários  

 Para especificar que o CLR se comporte como versões anteriores, use o `eHostDeterminedPolicy` membro.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumeração EClrFailure](eclrfailure-enumeration.md)
- [Enumeração EClrOperation](eclroperation-enumeration.md)
- [Interface ICLRPolicyManager](iclrpolicymanager-interface.md)
- [Método SetUnhandledExceptionPolicy](iclrpolicymanager-setunhandledexceptionpolicy-method.md)
- [Interface IHostPolicyManager](ihostpolicymanager-interface.md)
- [Hospedando enumerações](hosting-enumerations.md)
