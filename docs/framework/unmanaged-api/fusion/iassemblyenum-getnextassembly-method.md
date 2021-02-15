---
description: 'Saiba mais sobre o método: IAssemblyEnum:: GetNextAssembly'
title: Método IAssemblyEnum::GetNextAssembly
ms.date: 03/30/2017
api_name:
- IAssemblyEnum.GetNextAssembly
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyEnum::GetNextAssembly
helpviewer_keywords:
- GetNextAssembly method [.NET Framework fusion]
- IAssemblyEnum::GetNextAssembly method [.NET Framework fusion]
ms.assetid: 5d7a4ca2-5f46-4ef1-a9a2-257884e9dc11
topic_type:
- apiref
ms.openlocfilehash: 52b264b1d8efad54168a6bf69fd0c715cbfa7e2a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99760804"
---
# <a name="iassemblyenumgetnextassembly-method"></a>Método IAssemblyEnum::GetNextAssembly

Obtém um ponteiro para o próximo [IAssemblyName](iassemblyname-interface.md) contido neste objeto [IAssemblyEnum](iassemblyenum-interface.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetNextAssembly (  
    [in]  LPVOID          pvReserved,  
    [out] IAssemblyName   **ppName,  
    [in]  DWORD           dwFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pvReserved`  
 no Reservado para extensibilidade futura. `pvReserved` deve ser uma referência nula.  
  
 `ppName`  
 fora O `IAssemblyName` ponteiro retornado.  
  
 `dwFlags`  
 no Reservado para extensibilidade futura. `dwFlags` deve ser 0 (zero).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Fusion. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IAssemblyName](iassemblyname-interface.md)
- [Interface IAssemblyEnum](iassemblyenum-interface.md)
