---
description: 'Saiba mais sobre o método: IMetaDataConverter:: GetTypeLibFromMetaData'
title: Método IMetaDataConverter::GetTypeLibFromMetaData
ms.date: 03/30/2017
api_name:
- IMetaDataConverter.GetTypeLibFromMetaData
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataConverter::GetTypeLibFromMetaData
helpviewer_keywords:
- GetTypeLibFromMetaData method [.NET Framework metadata]
- IMetaDataConverter::GetTypeLibFromMetaData method [.NET Framework metadata]
ms.assetid: 90eab7b3-1fae-4af4-8bce-f7bc0e188a99
topic_type:
- apiref
ms.openlocfilehash: 5eecc87f938740366b7938d6ec3d1460ebcfb7eb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789262"
---
# <a name="imetadataconvertergettypelibfrommetadata-method"></a>Método IMetaDataConverter::GetTypeLibFromMetaData

Obtém um ponteiro para uma `ITypeLib` instância que representa a biblioteca de tipos que tem os nomes de módulo e biblioteca especificados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetTypeLibFromMetaData (  
    [in]  BSTR     strModule,
    [in]  BSTR     strTlbName,
    [out] ITypeLib **ppITL  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `strModule`  
 no O nome do módulo da biblioteca de tipos.  
  
 `strTlbName`  
 no O nome da biblioteca de tipos.  
  
 `ppITL`  
 fora Um ponteiro para um local que recebe o endereço da `ITypeLib` instância que representa a biblioteca de tipos.  
  
## <a name="requirements"></a>Requisitos  

 **Plataforma:** Consulte [requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataConverter](imetadataconverter-interface.md)
