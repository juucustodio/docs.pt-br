---
description: 'Saiba mais sobre: método IMetaDataEmit:: sethandlers'
title: Método IMetaDataEmit::SetHandler
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetHandler
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetHandler
helpviewer_keywords:
- IMetaDataEmit::SetHandler method [.NET Framework metadata]
- SetHandler method [.NET Framework metadata]
ms.assetid: c6c1aaaf-e2cd-407c-b73e-fbe6ffd83bb3
topic_type:
- apiref
ms.openlocfilehash: 07ebf8eef816d373e92a82fc84adacfe5a8599fb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99657860"
---
# <a name="imetadataemitsethandler-method"></a>Método IMetaDataEmit::SetHandler

Define o método referenciado pelo `IUnknown` ponteiro especificado como um retorno de chamada de notificação para remapeamentos de token.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetHandler (
    [in]  IUnknown    *pUnk  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pUnk`  
 no O manipulador a ser registrado.  
  
## <a name="remarks"></a>Comentários  

 O mecanismo de metadados envia a notificação usando o método fornecido pelo `SetHandler` , para compiladores que não geram registros de forma otimizada e que gostaria de otimizar os registros salvos.  
  
 Se o método de retorno de chamada não for fornecido por meio `SetHandler` do, nenhuma otimização será executada no salvamento, exceto onde vários escopos de importação tiverem sido mesclados usando `IMapToken` na mesclagem para cada escopo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataEmit2](imetadataemit2-interface.md)
