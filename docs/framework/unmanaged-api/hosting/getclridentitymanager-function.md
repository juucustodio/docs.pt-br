---
description: 'Saiba mais sobre: função GetCLRIdentityManager'
title: Função GetCLRIdentityManager
ms.date: 03/30/2017
api_name:
- GetCLRIdentityManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- GetCLRIdentityManager
helpviewer_keywords:
- GetCLRIdentityManager function [.NET Framework hosting]
ms.assetid: 66eeca30-adb4-45f4-aff5-347564c95724
topic_type:
- apiref
ms.openlocfilehash: 483cf0499fa162da4c89e350198a5609f9f1bab6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785361"
---
# <a name="getclridentitymanager-function"></a>Função GetCLRIdentityManager

Obtém um ponteiro para uma interface que permite que o Common Language Runtime (CLR) gerencie identidades.  
  
 Essa função foi preterida no .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
STDAPI GetCLRIdentityManager(  
    [in]  REFIID      riid,  
    [out] IUnknown  **ppManager  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `riid`  
 no Um `REFIID` (um identificador de interface) que especifica qual interface deve ser obtida. Esse valor deve ser IID_ICLRAssemblyIdentityManager ou IID_ICLRHostBindingPolicyManager.  
  
 `ppManager`  
 fora Um ponteiro para o endereço de um objeto [ICLRAssemblyIdentityManager](iclrassemblyidentitymanager-interface.md) ou [ICLRHostBindingPolicyManager](iclrhostbindingpolicymanager-interface.md) .  
  
## <a name="remarks"></a>Comentários  

 Chame a função [GetRealProcAddress](getrealprocaddress-function.md) para obter um ponteiro para a `GetCLRIdentityManager` função.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorWks.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
