---
description: 'Saiba mais sobre o método: INotifySink2:: OnSyncCallReturn'
title: Método INotifySink2::OnSyncCallReturn
ms.date: 03/30/2017
api_name:
- INotifySink2.OnSyncCallReturn
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifySink2::OnSyncCallReturn
helpviewer_keywords:
- OnSyncCallReturn method [.NET Framework debugging]
- INotifySink2::OnSyncCallReturn method [.NET Framework debugging]
ms.assetid: c1bda761-6292-4750-a14b-7d5db8f33456
topic_type:
- apiref
ms.openlocfilehash: 01518de4e5a9e1374edddadb3c49f16e8fe679a8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800247"
---
# <a name="inotifysink2onsynccallreturn-method"></a>Método INotifySink2::OnSyncCallReturn

É invocado quando uma chamada retorna.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT OnSyncCallReturn  
(  
    [in]  CALL_ID   in_CallID,  
    [in, size_is(in_BufferSize)] BYTE*  in_pBuffer,  
    [in]  DWORD     in_BufferSize  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `in_CallID`  
 no ID da chamada de que está sendo retornada. Consulte [estrutura de CALL_ID](call-id-structure.md).  
  
 `in_pBuffer`  
 no Buffer de chamadas.  
  
 `in_BufferSize`  
 no Tamanho do buffer de chamada, em bytes.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** ProtocolNotify2. idl  
  
## <a name="see-also"></a>Consulte também

- [Interface INotifySink2](inotifysink2-interface.md)
- [Interface INotifySource2](inotifysource2-interface.md)
- [Interface INotifyConnection2](inotifyconnection2-interface.md)
