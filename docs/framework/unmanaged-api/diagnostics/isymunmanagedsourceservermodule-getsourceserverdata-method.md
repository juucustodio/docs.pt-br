---
description: 'Saiba mais sobre o método: ISymUnmanagedSourceServerModule:: GetSourceServerData'
title: Método ISymUnmanagedSourceServerModule::GetSourceServerData
ms.date: 03/30/2017
api_name:
- ISymUnmanagedSourceServerModule.GetSourceServerData
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedSourceServerModule::GetSourceServerData
helpviewer_keywords:
- ISymUnmanagedSourceServerModule::GetSourceServerData method [.NET Framework debugging]
- GetSourceServerData method [.NET Framework debugging]
ms.assetid: 20bdf8ff-2d15-4c64-8950-6888f642d6c0
topic_type:
- apiref
ms.openlocfilehash: cdba764534000273170ccd693a3fbc7b5df9c3c9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99763157"
---
# <a name="isymunmanagedsourceservermodulegetsourceserverdata-method"></a>Método ISymUnmanagedSourceServerModule::GetSourceServerData

Retorna os dados do servidor de origem para o módulo. O chamador deve liberar recursos usando o `CoTaskMemFree` .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSourceServerData(  
    [out] ULONG* pDataByteCount,
    [out, size_is (, *pDataByteCount)] BYTE** ppData);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pDataByteCount`  
 fora Um ponteiro para um `ULONG32` que recebe o tamanho, em bytes, dos dados do servidor de origem.  
  
 `ppData`  
 fora Um ponteiro para o `pDataByteCount` valor retornado.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedSourceServerModule](isymunmanagedsourceservermodule-interface.md)
