---
description: 'Saiba mais sobre o método: ICorDebugNativeFrame:: GetLocalMemoryValue'
title: Método ICorDebugNativeFrame::GetLocalMemoryValue
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetLocalMemoryValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetLocalMemoryValue
helpviewer_keywords:
- GetLocalMemoryValue method [.NET Framework debugging]
- ICorDebugNativeFrame::GetLocalMemoryValue method [.NET Framework debugging]
ms.assetid: b600b3a2-9908-42d8-8093-ab6f39e9a2c9
topic_type:
- apiref
ms.openlocfilehash: 5fbdf9474ca8c5849b7d917ecddff491b329113b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99729231"
---
# <a name="icordebugnativeframegetlocalmemoryvalue-method"></a>Método ICorDebugNativeFrame::GetLocalMemoryValue

Obtém o valor de um argumento ou uma variável local que é armazenada no local de memória especificado para esse quadro nativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetLocalMemoryValue (  
    [in]  CORDB_ADDRESS      address,  
    [in]  ULONG              cbSigBlob,  
    [in]  PCCOR_SIGNATURE    pvSigBlob,  
    [out] ICorDebugValue     **ppValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `address`  
 no Um `CORDB_ADDRESS` valor que especifica o local da memória que contém o valor.  
  
 `cbSigBlob`  
 no Um inteiro que especifica o tamanho da assinatura de metadados binários que é referenciada pelo `pvSigBlob` parâmetro.  
  
 `pvSigBlob`  
 no Um `PCCOR_SIGNATURE` valor que aponta para a assinatura de metadados binários do tipo do valor.  
  
 `ppValue`  
 fora Um ponteiro para o endereço de um objeto "ICorDebugValue" que representa o valor recuperado que é armazenado no local da memória especificado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Confira também
