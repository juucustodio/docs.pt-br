---
description: 'Saiba mais sobre o método: ICorDebugNativeFrame:: GetLocalRegisterMemoryValue'
title: Método ICorDebugNativeFrame::GetLocalRegisterMemoryValue
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetLocalRegisterMemoryValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetLocalRegisterMemoryValue
helpviewer_keywords:
- ICorDebugNativeFrame::GetLocalRegisterMemoryValue method [.NET Framework debugging]
- GetLocalRegisterMemoryValue method [.NET Framework debugging]
ms.assetid: d350f69d-9aff-4f5a-8301-daea22dee2da
topic_type:
- apiref
ms.openlocfilehash: 36cf4d38c65e233a8be91a1e2aeca01ea009f340
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99729179"
---
# <a name="icordebugnativeframegetlocalregistermemoryvalue-method"></a>Método ICorDebugNativeFrame::GetLocalRegisterMemoryValue

Obtém o valor de um argumento ou uma variável local, da qual a palavra inferior e a palavra alta são armazenadas no local da memória e no registro especificado, respectivamente, para esse quadro nativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetLocalRegisterMemoryValue (  
    [in] CorDebugRegister   highWordReg,  
    [in] CORDB_ADDRESS      lowWordAddress,  
    [in] ULONG              cbSigBlob,  
    [in] PCCOR_SIGNATURE    pvSigBlob,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `highWordReg`  
 no Um valor da enumeração "CorDebugRegister" que especifica o registro que contém a palavra alta do valor.  
  
 `lowWordAddress`  
 no Um `CORDB_ADDRESS` valor que especifica o local da memória que contém a palavra inferior do valor.  
  
 `cbSigBlob`  
 no Um inteiro que especifica o tamanho da assinatura de metadados binários que é referenciada pelo `pvSigBlob` parâmetro.  
  
 `pvSigBlob`  
 no Um `PCCOR_SIGNATURE` valor que aponta para a assinatura de metadados binários do tipo do valor.  
  
 `ppValue`  
 fora Um ponteiro para o endereço de um objeto "ICorDebugValue" que representa o valor recuperado que é armazenado no registro especificado e no local da memória.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Confira também
