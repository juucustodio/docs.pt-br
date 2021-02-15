---
description: 'Saiba mais sobre: método ICorDebugThread2:: GetConnectionID'
title: Método ICorDebugThread2::GetConnectionID
ms.date: 03/30/2017
api_name:
- ICorDebugThread2.GetConnectionID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread2::GetConnectionID
helpviewer_keywords:
- ICorDebugThread2::GetConnectionID method [.NET Framework debugging]
- GetConnectionID method [.NET Framework debugging]
ms.assetid: 9c76b587-f941-4fa1-8b86-f3494fb10c8e
topic_type:
- apiref
ms.openlocfilehash: 0f8035e703d3638b11f4206d9c47e39fe487d71d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99658731"
---
# <a name="icordebugthread2getconnectionid-method"></a>Método ICorDebugThread2::GetConnectionID

Obtém o identificador de conexão para este objeto ICorDebugThread2.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetConnectionID (  
    [out] CONNID *pdwConnectionId  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pdwConnectionId`  
 fora Um `CONNID` que representa o identificador de conexão.  
  
## <a name="remarks"></a>Comentários  

 O `GetConnectionID` método retornará zero no `pdwConnectionId` parâmetro, se esse thread não fizer parte de uma conexão.  
  
 Se esse thread estiver conectado a uma instância do Microsoft SQL Server 2005 Analysis Services (SSAS), o `CONNID` será mapeado para um identificador de processo do servidor (SPID).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
