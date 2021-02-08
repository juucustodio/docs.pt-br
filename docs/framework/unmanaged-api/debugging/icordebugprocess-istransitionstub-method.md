---
description: 'Saiba mais sobre o método: ICorDebugProcess:: IsTransitionStub'
title: Método ICorDebugProcess::IsTransitionStub
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.IsTransitionStub
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::IsTransitionStub
helpviewer_keywords:
- ICorDebugProcess::IsTransitionStub method [.NET Framework debugging]
- IsTransitionStub method [.NET Framework debugging]
ms.assetid: f7653317-7e48-4163-be03-f50f1a4b0f70
topic_type:
- apiref
ms.openlocfilehash: 0da8527538c2573b1ec0d26f8711644fe8fcca2a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781994"
---
# <a name="icordebugprocessistransitionstub-method"></a>Método ICorDebugProcess::IsTransitionStub

Obtém um valor que indica se um endereço está dentro de um stub que causará uma transição para o código gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsTransitionStub(  
    [in]  CORDB_ADDRESS address,  
    [out] BOOL *pbTransitionStub);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `address`  
 no Um `CORDB_ADDRESS` valor que especifica o endereço em questão.  
  
 `pbTransitionStub`  
 fora Um ponteiro para um valor booliano que é `true` se o endereço especificado estiver dentro de um stub que causará uma transição para o código gerenciado; caso contrário, * `pbTransitionStub` será `false` .  
  
## <a name="remarks"></a>Comentários  

 O `IsTransitionStub` método pode ser usado por código de depuração não gerenciado para decidir quando retornar o controle de etapas para o stepper gerenciado.  
  
 Você também pode identificar stubs de transição examinando as informações no arquivo executável portátil (PE).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
