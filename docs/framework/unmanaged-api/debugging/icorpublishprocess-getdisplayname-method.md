---
description: 'Saiba mais sobre o método: ICorPublishProcess:: GetDisplayName'
title: Método ICorPublishProcess::GetDisplayName
ms.date: 03/30/2017
api_name:
- ICorPublishProcess.GetDisplayName
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishProcess::GetDisplayName
helpviewer_keywords:
- ICorPublishProcess::GetDisplayName method [.NET Framework debugging]
- GetDisplayName method, ICorPublishProcess interface [.NET Framework debugging]
ms.assetid: 7c0af9e9-a73f-41aa-a685-b21c439e059d
topic_type:
- apiref
ms.openlocfilehash: 7aef55a40c24953766377f21e8291bceb1594480
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794579"
---
# <a name="icorpublishprocessgetdisplayname-method"></a>Método ICorPublishProcess::GetDisplayName

Obtém o caminho completo do executável para o processo referenciado por este [ICorPublishProcess](icorpublishprocess-interface.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetDisplayName (  
    [in]  ULONG32                    cchName,
    [out] ULONG32                    *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]
        WCHAR                        *szName  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `cchName`  
 no O tamanho da `szName` matriz.  
  
 `pcchName`  
 fora O número de caracteres largos retornados na `szName` matriz.  
  
 `szName`  
 fora Uma matriz para armazenar o nome, incluindo o caminho completo do executável. O nome é encerrado em nulo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorPub. idl, CorPub. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorPublishProcess](icorpublishprocess-interface.md)
