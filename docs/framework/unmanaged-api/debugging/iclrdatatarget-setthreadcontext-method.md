---
description: 'Saiba mais sobre o método: ICLRDataTarget:: SetThreadContext'
title: Método ICLRDataTarget::SetThreadContext
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.SetThreadContext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::SetThreadContext
helpviewer_keywords:
- SetThreadContext method, ICLRDataTarget interface [.NET Framework debugging]
- ICLRDataTarget::SetThreadContext method [.NET Framework debugging]
ms.assetid: 103c8502-81fe-40d7-9c1e-9008d8fb19e1
topic_type:
- apiref
ms.openlocfilehash: fc428bc887f7ba10f3096cdf17a757fb252418f0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99738181"
---
# <a name="iclrdatatargetsetthreadcontext-method"></a>Método ICLRDataTarget::SetThreadContext

Define o contexto atual do thread especificado no processo de destino. Esse método é chamado pelos serviços de acesso a dados do Common Language Runtime (CLR).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetThreadContext (  
    [in] ULONG32            threadID,  
    [in] ULONG32            contextSize,  
    [in, size_is(contextSize)]
         BYTE               *context  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `threadID`  
 no O identificador do sistema operacional de um thread no processo de destino.  
  
 `contextSize`  
 no O tamanho do contexto.  
  
 `context`  
 no Ponteiro para um buffer que contém o contexto.  
  
 Os dados no `context` buffer estarão no formato da estrutura do Win32 `CONTEXT` . O contexto especifica dados de registro específicos do processador, de modo que a definição da estrutura do Win32 `CONTEXT` depende da arquitetura do processador. Consulte o arquivo de cabeçalho WinNT. h para obter a definição da estrutura do Win32 `CONTEXT` .  
  
## <a name="remarks"></a>Comentários  

 Este método é implementado pelo autor do aplicativo de depuração.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** ClrData. idl, ClrData. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRDataTarget](iclrdatatarget-interface.md)
