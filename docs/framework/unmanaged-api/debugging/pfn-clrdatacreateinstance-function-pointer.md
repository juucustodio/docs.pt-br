---
description: 'Saiba mais sobre: ponteiro de função PFN_CLRDataCreateInstance'
title: Ponteiro de função PFN_CLRDataCreateInstance
ms.date: 03/30/2017
api_name:
- PFN_CLRDataCreateInstance
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- PFN_CLRDataCreateInstance
helpviewer_keywords:
- PFN_CLRDataCreateInstance function pointer [.NET Framework debugging]
ms.assetid: 5c66ac57-d751-4de5-af9f-26ceb949af8b
topic_type:
- apiref
ms.openlocfilehash: fc048f840084eff0270944d3190ccbb153bf22d8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800624"
---
# <a name="pfn_clrdatacreateinstance-function-pointer"></a>Ponteiro de função PFN_CLRDataCreateInstance

Aponta para uma função que cria um objeto de interface para o item de destino especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef HRESULT (STDAPICALLTYPE* PFN_CLRDataCreateInstance) (  
    [in]  REFIID           iid,  
    [in]  ICLRDataTarget  *target,  
    [out] void           **iface  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `iid`  
 no O identificador da interface a ser instanciada.  
  
 `target`  
 no Um ponteiro para um objeto [ICLRDataTarget](iclrdatatarget-interface.md) implementado pelo usuário que representa o item de destino para o qual criar o objeto de interface.  
  
 `iface`  
 fora Um ponteiro para o endereço do objeto de interface retornado.  
  
## <a name="remarks"></a>Comentários  

 O `ICLRDataTarget` objeto é implementado pelo gravador do aplicativo de depuração. A implementação depende do tipo de item de destino que está sendo representado. O item de destino pode ser um processo, despejo de memória, computador remoto e assim por diante.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** ClrData. idl  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando funções estáticas globais](debugging-global-static-functions.md)
