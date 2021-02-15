---
description: 'Saiba mais sobre: função CorExitProcess'
title: Função CorExitProcess
ms.date: 03/30/2017
api_name:
- CorExitProcess
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CorExitProcess
helpviewer_keywords:
- CorExitProcess function [.NET Framework hosting]
ms.assetid: a5cab4c6-990e-47f3-8798-cf422b791015
topic_type:
- apiref
ms.openlocfilehash: 68d33dec76387e103a34e99c529a4e7aff7535b4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99649579"
---
# <a name="corexitprocess-function"></a>Função CorExitProcess

Desliga o processo atual não gerenciado.  
  
 Essa função foi preterida no .NET Framework 4. Em vez disso, use o método [ICLRMetaHost:: ExitProcess](iclrmetahost-exitprocess-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
void STDMETHODCALLTYPE CorExitProcess (
  int  exitCode  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `exitCode`  
 Um inteiro que especifica o código de saída do processo.  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Começando com o .NET Framework 4, `CorExitProcess` sai de cada tempo de execução iniciado no processo, não apenas o tempo de execução ao qual as APIs herdadas foram associadas.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
