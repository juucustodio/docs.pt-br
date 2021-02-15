---
description: 'Saiba mais sobre: ponteiro de função FExecuteInAppDomainCallback'
title: Ponteiro de função FExecuteInAppDomainCallback
ms.date: 03/30/2017
api_name:
- FExecuteInAppDomainCallback
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- FExecuteInAppDomainCallback
helpviewer_keywords:
- FExecuteInAppDomainCallback function pointer [.NET Framework hosting]
ms.assetid: 2709f18f-3eee-497f-bc33-3ab7a485599b
topic_type:
- apiref
ms.openlocfilehash: 97c7fe14a3eafd6f4626d8729be3b45ad5502f1a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785387"
---
# <a name="fexecuteinappdomaincallback-function-pointer"></a>Ponteiro de função FExecuteInAppDomainCallback

Aponta para uma função que é chamada pelo Common Language Runtime (CLR) para executar código gerenciado.  
  
 Esse ponteiro de função foi preterido no .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef HRESULT (__stdcall *FExecuteInAppDomainCallback) (  
    [in] void  *cookie  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cookie`  
 no Um ponteiro para uma memória opaca alocada pelo chamador que contém o código gerenciado a ser executado.  
  
 A alocação e o tempo de vida dessa memória são controlados pelo chamador (ou seja, o CLR). Essa não é uma memória de heap gerenciada pelo CLR.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorWks.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
