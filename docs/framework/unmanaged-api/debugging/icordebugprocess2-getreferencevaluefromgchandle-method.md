---
description: 'Saiba mais sobre o método: ICorDebugProcess2:: GetReferenceValueFromGCHandle'
title: Método ICorDebugProcess2::GetReferenceValueFromGCHandle
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.GetReferenceValueFromGCHandle
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::GetReferenceValueFromGCHandle
helpviewer_keywords:
- GetReferenceValueFromGCHandle method [.NET Framework debugging]
- ICorDebugProcess2::GetReferenceValueFromGCHandle method [.NET Framework debugging]
ms.assetid: 8bdd7f4c-19f2-4ede-875e-603773e8c128
topic_type:
- apiref
ms.openlocfilehash: 02047dee9116d34a365242f2a532766eb60e1c81
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99650209"
---
# <a name="icordebugprocess2getreferencevaluefromgchandle-method"></a>Método ICorDebugProcess2::GetReferenceValueFromGCHandle

Obtém um ponteiro de referência para o objeto gerenciado especificado que tem um identificador de coleta de lixo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetReferenceValueFromGCHandle (  
    [in]  UINT_PTR                 handle,  
    [out] ICorDebugReferenceValue  **pOutValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `handle`  
 no Um ponteiro para um objeto gerenciado que tem um identificador de coleta de lixo. Esse valor é um <xref:System.IntPtr> objeto e pode ser recuperado do <xref:System.Runtime.InteropServices.GCHandle> para o objeto gerenciado.  
  
 `pOutValue`  
 fora Um ponteiro para o endereço de um objeto ICorDebugReferenceValue que representa uma referência ao objeto gerenciado especificado.  
  
## <a name="remarks"></a>Comentários  

 Não confunda o valor de referência retornado com um valor de referência de coleta de lixo.  
  
 A referência retornada se comporta como uma referência normal. Ele é desabilitado quando a execução do código continua após um ponto de interrupção. O tempo de vida do objeto de destino não é afetado pelo tempo de vida do valor de referência.  
  
> [!NOTE]
> O `GetReferenceValueFromGCHandle` método não valida o identificador. Portanto, o `GetReferenceValueFromGCHandle` método pode potencialmente corromper o depurador e o código que está sendo depurado se um identificador inválido for passado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
