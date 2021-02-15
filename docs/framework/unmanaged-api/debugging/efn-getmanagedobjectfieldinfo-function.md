---
description: 'Saiba mais sobre: _EFN_GetManagedObjectFieldInfo função'
title: Função _EFN_GetManagedObjectFieldInfo
ms.date: 03/30/2017
api_name:
- _EFN_GetManagedObjectFieldInfo
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- _EFN_GetManagedObjectFieldInfo
helpviewer_keywords:
- _EFN_GetManagedObjectFieldInfo function [.NET Framework debugging]
ms.assetid: 3b93bcff-62a4-47b2-babc-6bcf4216119a
topic_type:
- apiref
ms.openlocfilehash: 749ab286a86db07c1b66ff2b61ff073d15334800
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99637879"
---
# <a name="_efn_getmanagedobjectfieldinfo-function"></a>\_\_Função EFN GetManagedObjectFieldInfo

Obtém o deslocamento do início de um objeto para um campo e o valor do campo, usando o ponteiro do objeto fornecido e o nome do campo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT _EFN_GetManagedObjectFieldInfo(  
    [in]  PDEBUG_CLIENT Client,  
    [in]  ULONG64       objAddr,  
    [in]  __out_ecount (mdNameLen) PSTR szFieldName,  
    [out] PULONG64      pValue,  
    [out] PULONG        pOffset  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `Client`  
 no Um ponteiro para o cliente de depuração.  
  
 `objAddr`  
 no Um ponteiro de objeto gerenciado.  
  
 szFieldName  
 no Um ponteiro de objeto gerenciado para o nome do campo.  
  
 `pValue`  
 fora O valor do campo. Este parâmetro pode ser nulo.  
  
 `pOffset`  
 fora O deslocamento de `objAddr` para o campo. Este parâmetro pode ser nulo.  
  
## <a name="remarks"></a>Comentários  

 Se o deslocamento for 0, nenhum deslocamento será gravado.  
  
 Se não houver nenhum código gerenciado no thread atualmente no contexto, a função retornará HRESULT SOS_E_NOMANAGEDCODE com um valor de recurso de 0XA0 e um código de erro de 0x1000.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** SOS_Stacktrace. h  
  
 **Versão do .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando funções estáticas globais](debugging-global-static-functions.md)
