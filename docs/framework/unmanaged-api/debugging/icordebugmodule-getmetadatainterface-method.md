---
description: 'Saiba mais sobre o método: ICorDebugModule:: GetMetaDataInterface'
title: Método ICorDebugModule::GetMetaDataInterface
ms.date: 03/30/2017
api_name:
- ICorDebugModule.GetMetaDataInterface
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::GetMetaDataInterface
helpviewer_keywords:
- ICorDebugModule::GetMetaDatainterface method [.NET Framework debugging]
- GetMetaDatainterface method [.NET Framework debugging]
ms.assetid: 30d906f2-cf35-4fa9-9d4c-0c31b58c9f3a
topic_type:
- apiref
ms.openlocfilehash: 39af2560b4c10f6dc490bfba5425e2339a7c1823
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99691634"
---
# <a name="icordebugmodulegetmetadatainterface-method"></a>Método ICorDebugModule::GetMetaDataInterface

Obtém um objeto de interface de metadados que pode ser usado para examinar os metadados do módulo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMetaDataInterface (  
    [in] REFIID      riid,  
    [out] IUnknown **ppObj  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `riid`  
 no A ID de referência que especifica a interface de metadados.  
  
 `ppObj`  
 fora Um ponteiro para o endereço de um `T:IUnknown` objeto que é uma das [interfaces de metadados](../metadata/metadata-interfaces.md).  
  
## <a name="remarks"></a>Comentários  

 O depurador pode usar o `GetMetaDataInterface` método para fazer uma cópia dos metadados originais de um módulo, o que deve ser feito para editar esse módulo. O depurador chama `GetMetaDataInterface` para obter um objeto de interface [IMetaDataEmit](../metadata/imetadataemit-interface.md) para o módulo e, em seguida, chama [IMetaDataEmit:: SaveToMemory](../metadata/imetadataemit-savetomemory-method.md) para salvar uma cópia dos metadados do módulo na memória.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Metadados](../metadata/index.md)
