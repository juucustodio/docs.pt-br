---
description: 'Saiba mais sobre o método: ICorPublishAppDomain:: GetName'
title: Método ICorPublishAppDomain::GetName
ms.date: 03/30/2017
api_name:
- ICorPublishAppDomain.GetName
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishAppDomain::GetName
helpviewer_keywords:
- GetName method, ICorPublishAppDomain interface [.NET Framework debugging]
- ICorPublishAppDomain::GetName method [.NET Framework debugging]
ms.assetid: 6ef8ac9b-9803-4b65-8b13-25f3e0b1bc6b
topic_type:
- apiref
ms.openlocfilehash: 05b1b14f7e0db371b29059ec3d44333ac40428e9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99721795"
---
# <a name="icorpublishappdomaingetname-method"></a>Método ICorPublishAppDomain::GetName

Obtém o nome do domínio do aplicativo que é representado por este [ICorPublishAppDomain](icorpublishappdomain-interface.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetName (  
    [in]  ULONG32   cchName,
    [out] ULONG32   *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]
        WCHAR       *szName  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cchName`  
 no O tamanho da `szName` matriz.  
  
 `pcchName`  
 fora Um ponteiro para o número de caracteres largos, incluindo o caractere nulo, retornado na `szName` matriz.  
  
 `szName`  
 fora Uma matriz na qual armazenar o nome.  
  
## <a name="remarks"></a>Comentários  

 Se `szName` for não nulo, o `GetName` método copiará até `cchName` caracteres (incluindo o terminador nulo) para o `szName` . Se um não nulo for retornado em `pcchName` , o número real de caracteres no nome (incluindo o terminador nulo) será armazenado na `szName` matriz.  
  
 O `GetName` método retorna um S_OK HRESULT, independentemente de quantos caracteres foram copiados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorPub. idl, CorPub. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorPublishAppDomain](icorpublishappdomain-interface.md)
