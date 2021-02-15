---
description: 'Saiba mais sobre: IDebugAutoAttach:: método de anexação automática'
title: Método IDebugAutoAttach::AutoAttach
ms.date: 03/30/2017
api_name:
- IDebugAutoAttach.AutoAttach
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- IDebugAutoAttach::AutoAttach
helpviewer_keywords:
- AutoAttach method [.NET Framework debugging]
- IDebugAutoAttach::AutoAttach method [.NET Framework debugging]
ms.assetid: 3cf3bd9c-7d88-4afa-a476-94cdc7609aa6
topic_type:
- apiref
ms.openlocfilehash: 8abd35b1d94fc074d4dafe424c52c274b1de1541
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800351"
---
# <a name="idebugautoattachautoattach-method"></a>Método IDebugAutoAttach::AutoAttach

Executa a anexação automática do depurador invocado pelo servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT AutoAttach  
(  
    [in]  REFGUID   guidPort,  
    [in]  DWORD     dwPid,  
    [in]  AUTOATTACH_PROGRAM_TYPE dwProgramType,  
    [in]  DWORD     dwProgramId,  
    [in]  LPCWSTR   pszSessionId  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `guidPort`  
 no Sempre definido como `GUID_NULL` .  
  
 `dwPid`  
 no ID do processo, normalmente recuperada com a `GetCurrentProcessId` função.  
  
 `dwProgramType`  
 no Tipo de programa: `AUTOATTACH_PROGRAM_WIN32` , `AUTOATTACH_PROGRAM_COMPLUS` ou `AUTOATTACH_PROGRAM_UNKNOWN` .  
  
 `dwProgramId`  
 no ID do programa.  
  
 `pszSessionId`  
 no Cadeia de caracteres passada pelo verbo Debug.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** DbgAutoAttach. h  
  
## <a name="see-also"></a>Consulte também

- [Interface IDebugAutoAttach](idebugautoattach-interface.md)
