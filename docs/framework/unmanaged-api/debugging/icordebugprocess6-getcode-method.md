---
description: 'Saiba mais sobre: método ICorDebugProcess6:: GetCode'
title: Método ICorDebugProcess6::GetCode
ms.date: 03/30/2017
ms.assetid: faa538c2-60c9-4064-b996-1b4c24ebd751
ms.openlocfilehash: a7cb71ddb1e65cda37d762a0fba958d413145138
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99649657"
---
# <a name="icordebugprocess6getcode-method"></a>Método ICorDebugProcess6::GetCode

Obtém informações sobre o código gerenciado em um endereço de código em particular.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCode(  
    [in] CORDB_ADDRESS codeAddress,
    [out] ICorDebugCode **ppCode);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `codeAddress`  
 no Um valor [CORDB_ADDRESS](../common-data-types-unmanaged-api-reference.md) que especifica o endereço inicial do segmento de código gerenciado.  
  
 `ppCode`  
 fora Um ponteiro para o endereço de um objeto "ICorDebugCode" que representa um segmento de código gerenciado.  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugProcess6](icordebugprocess6-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
