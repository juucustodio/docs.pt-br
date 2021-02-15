---
description: 'Saiba mais sobre o método: IMetaDataImport2:: EnumGenericParams'
title: Método IMetaDataImport2::EnumGenericParams
ms.date: 03/30/2017
api_name:
- IMetaDataImport2.EnumGenericParams
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2::EnumGenericParams
helpviewer_keywords:
- EnumGenericParams method [.NET Framework metadata]
- IMetaDataImport2::EnumGenericParams method [.NET Framework metadata]
ms.assetid: b50488a5-3cf0-483c-82dc-2892a3ec61ac
topic_type:
- apiref
ms.openlocfilehash: 9d4e9d163da07ec4a3af1aa628b8b6ec4b2338fe
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99720931"
---
# <a name="imetadataimport2enumgenericparams-method"></a>Método IMetaDataImport2::EnumGenericParams

Obtém um enumerador para uma matriz de tokens de parâmetro genéricos associados ao TypeDef ou token MethodDef especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT EnumGenericParams (  
   [in, out] HCORENUM     *phEnum,
   [in]  mdToken          tk,  
   [out] mdGenericParam   rGenericParams[],
   [in]  ULONG            cMax,
   [out] ULONG            *pcGenericParams  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `phEnum`  
 [entrada, saída] Um ponteiro para o enumerador.  
  
 `tk`  
 no O TypeDef ou o token MethodDef cujos parâmetros genéricos devem ser enumerados.  
  
 `rGenericParams`  
 fora A matriz de parâmetros genéricos a ser enumerada.  
  
 `cMax`  
 no O número máximo solicitado de tokens a serem colocados `rGenericParams` .  
  
 `pcGenericParams`  
 fora O número retornado de tokens colocados em `rGenericParams` .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|`S_OK`|`EnumGenericParams` retornado com êxito.|  
|`S_FALSE`|`phEnum` Não tem elementos de membro. Nesse caso, `pcGenericParams` é definido como 0 (zero).|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataImport2](imetadataimport2-interface.md)
- [Interface IMetaDataImport](imetadataimport-interface.md)
