---
description: 'Saiba mais sobre: método ICorDebugModule:: GetToken'
title: Método ICorDebugModule::GetToken
ms.date: 03/30/2017
api_name:
- ICorDebugModule.GetToken
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::GetToken
helpviewer_keywords:
- ICorDebugModule::GetToken method [.NET Framework debugging]
- GetToken method, ICorDebugModule interface [.NET Framework debugging]
ms.assetid: f759f87a-18ae-4c1a-8300-29b803432d0a
topic_type:
- apiref
ms.openlocfilehash: fd1bc4bc397e7f81c77f2fe784c68dbaaceb2695
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99660161"
---
# <a name="icordebugmodulegettoken-method"></a>Método ICorDebugModule::GetToken

Obtém o token para a entrada de tabela deste módulo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetToken(  
    [out] mdModule *pToken  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pToken`  
 fora Um ponteiro para o `mdModule` token que faz referência aos metadados do módulo.  
  
## <a name="remarks"></a>Comentários  

 O token pode ser passado para as interfaces de importação de metadados [IMetaDataImport](../metadata/imetadataimport-interface.md), [IMetaDataImport2](../metadata/imetadataimport2-interface.md)e [IMetaDataAssemblyImport](../metadata/imetadataassemblyimport-interface.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Metadados](../metadata/index.md)
