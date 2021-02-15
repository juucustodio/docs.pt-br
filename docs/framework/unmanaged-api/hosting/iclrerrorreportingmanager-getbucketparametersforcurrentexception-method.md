---
description: 'Saiba mais sobre o método: ICLRErrorReportingManager:: GetBucketParametersForCurrentException'
title: Método ICLRErrorReportingManager::GetBucketParametersForCurrentException
ms.date: 03/30/2017
api_name:
- ICLRErrorReportingManager.GetBucketParametersForCurrentException
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRErrorReportingManager::GetBucketParametersForCurrentException
helpviewer_keywords:
- ICLRErrorReportingManager::GetBucketParametersForCurrentException method [.NET Framework hosting]
- GetBucketParametersForCurrentException method [.NET Framework hosting]
ms.assetid: a13ec8a6-8e18-4acb-8054-77f5b1a0e0b9
topic_type:
- apiref
ms.openlocfilehash: ba2b6cf1215e5d57f608a76a870b0a9c846ee8ac
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689398"
---
# <a name="iclrerrorreportingmanagergetbucketparametersforcurrentexception-method"></a>Método ICLRErrorReportingManager::GetBucketParametersForCurrentException

Obtém o Bucket do Watson para a exceção atual no thread de chamada.  
  
 Um *Bucket* é uma coleção de dados de erro que está relacionada ao mesmo defeito de código. *Watson* refere-se a um conjunto de tecnologias para coletar e analisar dados associados a uma exceção.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetBucketParametersForCurrentException(  
    [out] BucketParameters *pParams  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pParams`  
 fora Um ponteiro para uma estrutura [BucketParameters](bucketparameters-structure.md) que contém dados de erro para a exceção.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRErrorReportingManager](iclrerrorreportingmanager-interface.md)
