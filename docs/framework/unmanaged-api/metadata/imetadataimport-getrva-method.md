---
description: 'Saiba mais sobre o método: IMetaDataImport:: GetRVA'
title: Método IMetaDataImport::GetRVA
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetRVA
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetRVA
helpviewer_keywords:
- GetRVA method [.NET Framework metadata]
- IMetaDataImport::GetRVA method [.NET Framework metadata]
ms.assetid: ea422217-988b-4acd-b2db-c55357938275
topic_type:
- apiref
ms.openlocfilehash: 8d6439bcad50a6311e7bb1408f4c86144a5026ce
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789158"
---
# <a name="imetadataimportgetrva-method"></a>Método IMetaDataImport::GetRVA

Obtém o endereço virtual relativo (RVA) e os sinalizadores de implementação do método ou do campo representado pelo token especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetRVA (  
   [in]  mdToken     tk,
   [out] ULONG       *pulCodeRVA,
   [out]  DWORD      *pdwImplFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `tk`  
 no Um token de metadados MethodDef ou FieldDef que representa o objeto de código para o qual retornar o RVA. Se o token for um FieldDef, o campo deverá ser uma variável global.  
  
 `pulCodeRVA`  
 fora Um ponteiro para o endereço virtual relativo do objeto de código representado pelo token.  
  
 `pdwImplFlags`  
 fora Um ponteiro para os sinalizadores de implementação do método. Esse valor é um bitmask da enumeração [CorMethodImpl](cormethodimpl-enumeration.md) . O valor de `pdwImplFlags` será válido somente se `tk` for um token MethodDef.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport](imetadataimport-interface.md)
- [Interface IMetaDataImport2](imetadataimport2-interface.md)
