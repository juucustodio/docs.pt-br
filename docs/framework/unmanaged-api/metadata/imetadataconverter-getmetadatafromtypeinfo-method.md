---
description: 'Saiba mais sobre o método: IMetaDataConverter:: GetMetaDataFromTypeInfo'
title: Método IMetaDataConverter::GetMetaDataFromTypeInfo
ms.date: 03/30/2017
api_name:
- IMetaDataConverter.GetMetaDataFromTypeInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataConverter::GetMetaDataFromTypeInfo
helpviewer_keywords:
- GetMetaDataFromTypeInfo method [.NET Framework metadata]
- IMetaDataConverter::GetMetaDataFromTypeInfo method [.NET Framework metadata]
ms.assetid: d44484bb-23a3-49c3-9e46-69d0d9ab4f0f
topic_type:
- apiref
ms.openlocfilehash: 224be07463b19ed9e22bef1a9d454d91a8086304
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753618"
---
# <a name="imetadataconvertergetmetadatafromtypeinfo-method"></a>Método IMetaDataConverter::GetMetaDataFromTypeInfo

Obtém um ponteiro para uma instância de [IMetaDataImport](imetadataimport-interface.md) que representa a assinatura de metadados da biblioteca de tipos referenciada pela `ITypeInfo` instância especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMetaDataFromTypeInfo (  
    [in]  ITypeInfo         *pITI,  
    [out] IMetaDataImport   **ppMDI  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pITI`  
 no Um ponteiro para um `ITypeInfo` objeto que se refere à biblioteca de tipos.  
  
 `ppMDI`  
 fora Um ponteiro para um local que recebe o endereço da `IMetaDataImport` instância que representa a assinatura de metadados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataforma:** Consulte [requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataImport](imetadataimport-interface.md)
