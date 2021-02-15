---
description: 'Saiba mais sobre: método EmitAssemblyCustomAttribute'
title: Método EmitAssemblyCustomAttribute
ms.date: 03/30/2017
api_name:
- IALink.EmitAssemblyCustomAttribute
- EmitAssemblyCustomAttribute
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- EmitAssemblyCustomAttribute
helpviewer_keywords:
- EmitAssemblyCustomAttribute method
ms.assetid: b72f5409-79af-4fa7-90a7-7630eec170f1
topic_type:
- apiref
ms.openlocfilehash: c91eb563c14b442a22db8f328287c10e5cc9a63c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638321"
---
# <a name="emitassemblycustomattribute-method"></a>Método EmitAssemblyCustomAttribute

Chamada para definir atributos personalizados no nível do assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EmitAssemblyCustomAttribute(  
    mdAssembly   AssemblyID,  
    mdToken      FileToken,  
    mdToken      tkType,  
    void const*  pCustomValue,  
    DWORD        cbCustomValue,  
    BOOL         bSecurity,  
    BOOL         bAllowMulti  
) PURE;  
```  
  
## <a name="parameters"></a>Parâmetros  

 `AssemblyID`  
 ID do assembly.  
  
 `FileToken`  
 Arquivo que rearquivou o atributo. Pode ser NULL se não `AssemblyID` indicar um netmodule não associado.  
  
 `tkType`  
 Tipo do atributo personalizado.  
  
 `pCustomValue`  
 Dados de valor personalizado.  
  
 `cbCustomValue`  
 Comprimento dos dados do valor personalizado.  
  
 `bSecurity`  
 TRUE se o atributo personalizado estiver relacionado à assinatura de assembly.  
  
 `bAllowMulti`  
 TRUE se vários atributos forem emitidos.  
  
## <a name="return-value"></a>Valor retornado  

 Retorna S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 Requer ALink. h  
  
## <a name="see-also"></a>Consulte também

- [Interface IALink](ialink-interface.md)
- [Interface IALink2](ialink2-interface.md)
- [API do ALink](index.md)
