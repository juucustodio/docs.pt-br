---
description: 'Saiba mais sobre o método: IMetaDataConverter:: GetMetaDataFromTypeLib'
title: Método IMetaDataConverter::GetMetaDataFromTypeLib
ms.date: 03/30/2017
api_name:
- IMetaDataConverter.GetMetaDataFromTypeLib
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataConverter::GetMetaDataFromTypeLib
helpviewer_keywords:
- IMetaDataConverter::GetMetaDataFromTypeLib method [.NET Framework metadata]
- GetMetaDataFromTypeLib method [.NET Framework metadata]
ms.assetid: 97dc3a56-adfa-431f-889e-06a35ac84d51
topic_type:
- apiref
ms.openlocfilehash: d1ed5feb9f42ea0f8dc802c4dad527be5d2ed25f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789275"
---
# <a name="imetadataconvertergetmetadatafromtypelib-method"></a>Método IMetaDataConverter::GetMetaDataFromTypeLib

Obtém um ponteiro de interface para uma instância de [IMetaDataImport](imetadataimport-interface.md) que representa a assinatura de metadados da biblioteca de tipos representada pela `ITypeLib` instância especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMetaDataFromTypeLib (  
    [in]  ITypeLib        *pITL,
    [out] IMetaDataImport **ppMDI  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pITL`  
 no Ponteiro para um `ITypeLib` objeto que representa a biblioteca de tipos.  
  
 `ppMDI`  
 fora Ponteiro para um local que recebe o endereço da `IMetaDataImport` instância que representa a assinatura de metadados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataforma:** Consulte [requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataImport](imetadataimport-interface.md)
