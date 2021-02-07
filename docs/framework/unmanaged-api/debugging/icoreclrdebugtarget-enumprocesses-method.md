---
description: 'Saiba mais sobre o método: ICoreClrDebugTarget:: EnumProcesses'
title: Método ICoreClrDebugTarget::EnumProcesses
ms.date: 03/30/2017
api_name:
- ICoreClrDebugTarget.EnumProcesses
api_location:
- mscordbi_macx86.dll
api_type:
- COM
f1_keywords:
- ICoreClrDebugTarget::EnumProcesses
helpviewer_keywords:
- remote debugging API [Silverlight]
- EnumProcesses method, ICorClrDebugTarget interface [Silverlight debugging]
- ICorClrDebugTarget::EnumProcesses method [Silverlight debugging]
- Silverlight, remote debugging
ms.assetid: e00fd477-4f49-43d3-bd0e-3094824b1136
topic_type:
- apiref
ms.openlocfilehash: 73dc8a2b00f7a57879855158e6b871117d015f3c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99738033"
---
# <a name="icoreclrdebugtargetenumprocesses-method"></a>Método ICoreClrDebugTarget::EnumProcesses

Enumera os processos que estão sendo executados em um computador remoto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumProcesses (  
       [out]  DWORD*                  pcProcs,
       [out]  CoreClrDebugProcInfo**  ppProcs  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pcProcs`  
 fora O número de processos retornados em `ppProcs` . Esse valor pode ser 0 (zero).  
  
 `ppProcs`  
 fora Uma matriz de estruturas [CoreClrDebugProcInfo](coreclrdebugprocinfo-structure.md) que representam os processos em execução no computador remoto.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK  
 Sucesso.  
  
 E_OUTOFMEMORY  
 Não é possível alocar memória suficiente para `ppProcs` .  
  
 E_FAIL (ou outros códigos de retorno de E_)  
 Outras falhas.  
  
## <a name="remarks"></a>Comentários  

 Para liberar a memória que foi alocada por esse método, chame o método [ICoreClrDebugTarget:: freememory](icoreclrdebugtarget-freememory-method.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CoreClrRemoteDebuggingInterfaces. h  
  
 **Biblioteca:** mscordbi_macx86.dll  
  
 **Versões do .NET Framework:** 3,5 SP1  
  
## <a name="see-also"></a>Consulte também

- [Interface ICoreClrDebugTarget](icoreclrdebugtarget-interface.md)
