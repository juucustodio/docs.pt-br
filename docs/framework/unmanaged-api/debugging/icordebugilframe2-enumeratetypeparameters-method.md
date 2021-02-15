---
description: 'Saiba mais sobre o método: ICorDebugILFrame2:: EnumerateTypeParameters'
title: Método ICorDebugILFrame2::EnumerateTypeParameters
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame2.EnumerateTypeParameters
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame2::EnumerateTypeParameters
helpviewer_keywords:
- EnumerateTypeParameters method, ICorDebugILFrame2 interface [.NET Framework debugging]
- ICorDebugILFrame2::EnumerateTypeParameters method [.NET Framework debugging]
ms.assetid: 722d0d74-e0df-491f-98c4-62d501dfaf6f
topic_type:
- apiref
ms.openlocfilehash: 34f305b7793e4909318ae2301d72e2af7c12f2c1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791279"
---
# <a name="icordebugilframe2enumeratetypeparameters-method"></a>Método ICorDebugILFrame2::EnumerateTypeParameters

Obtém um objeto ICorDebugTypeEnum que contém os <xref:System.Type> parâmetros neste quadro.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumerateTypeParameters (  
    [out] ICorDebugTypeEnum    **ppTyParEnum  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppTyParEnum`  
 Um ponteiro para o endereço de um objeto de interface ICorDebugTypeEnum que permite a enumeração de parâmetros de tipo.  
  
 A lista de parâmetros de tipo inclui os parâmetros de tipo de classe (se houver) seguidos pelos parâmetros de tipo de método (se houver).  
  
## <a name="remarks"></a>Comentários  

 Use o método [IMetaDataImport2:: EnumGenericParams](../metadata/imetadataimport2-enumgenericparams-method.md) para determinar quantos parâmetros de tipo de classe e parâmetros de tipo de método essa lista contém.  
  
 Os parâmetros de tipo nem sempre estão disponíveis.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
