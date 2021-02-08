---
description: 'Saiba mais sobre o método: IMetaDataValidate:: ValidatorInit'
title: Método IMetaDataValidate::ValidatorInit
ms.date: 03/30/2017
api_name:
- IMetaDataValidate.ValidatorInit
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataValidate::ValidatorInit
helpviewer_keywords:
- IMetaDataValidate::ValidatorInit method [.NET Framework metadata]
- ValidatorInit method [.NET Framework metadata]
ms.assetid: 6bafd75a-e2d0-4aea-aed1-074374d5dff6
topic_type:
- apiref
ms.openlocfilehash: 99435eeab542e9cb3bb679ad146b546ce51c8df4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799181"
---
# <a name="imetadatavalidatevalidatorinit-method"></a>Método IMetaDataValidate::ValidatorInit

Define um sinalizador que especifica o tipo do módulo no escopo de metadados atual e registra o método de retorno de chamada especificado para erros de validação.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ValidatorInit (  
   [in] DWORD       dwModuleType,  
   [in] IUnknown    *pUnk  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwModule`  
 no Um valor da enumeração [CorValidatorModuleType](corvalidatormoduletype-enumeration.md) que especifica o tipo do módulo no escopo de metadados atual.  
  
 `pUnk`  
 no Um ponteiro para uma instância [IUnknown](/cpp/atl/iunknown) que serve como um retorno de chamada de função para erros de validação.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataValidate](imetadatavalidate-interface.md)
