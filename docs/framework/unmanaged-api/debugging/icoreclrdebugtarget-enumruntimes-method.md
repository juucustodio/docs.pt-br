---
description: 'Saiba mais sobre o método: ICoreClrDebugTarget:: EnumRuntimes'
title: Método ICoreClrDebugTarget::EnumRuntimes
ms.date: 03/30/2017
api_name:
- ICoreClrDebugTarget.EnumRuntimes
api_location:
- mscordbi_macx86.dll
api_type:
- COM
f1_keywords:
- ICoreClrDebugTarget::EnumRuntimes
helpviewer_keywords:
- remote debugging API [Silverlight]
- ICorClrDebugTarget::EnumRuntimes method [Silverlight debugging]
- EnumRuntimes method, ICoreClrDebugTarget interface [Silverlight debugging]
- Silverlight, remote debugging
ms.assetid: 316df866-442d-40cc-b049-45e8adcb65d1
topic_type:
- apiref
ms.openlocfilehash: 675747106b2acec2e8be3fcdf15831958bea7c7c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794618"
---
# <a name="icoreclrdebugtargetenumruntimes-method"></a>Método ICoreClrDebugTarget::EnumRuntimes

Enumera os Common Language runtimes (CLRs) no processo especificado que está sendo executado em um computador remoto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumRuntimes (  
      [in] DWORD       dwInternalProcessID,  
      [out] DWORD*     pcRuntimes,  
      [out] CoreClrDebugRuntimeInfo**    ppRuntimes  
    );  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwInternalProcessID`  
 no A ID do processo interno do processo para o qual você deseja enumerar os tempos de execução. Isso será `m_dwInternalID` proveniente do [CoreClrDebugProcInfo](coreclrdebugprocinfo-structure.md)correspondente.  
  
 `pcRuntimes`  
 fora O número de tempos de execução retornados em `ppRuntimes` . Esse valor pode ser 0 (zero).  
  
 `ppRuntimes`  
 fora Uma matriz de estruturas [CoreClrDebugRuntimeInfo](coreclrdebugruntimeinfo-structure.md) que representam os tempos de execução carregados no processo de destino remoto.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK  
 Sucesso.  
  
 S_FALSE  
 `dwInternalProcessID` não corresponde a nenhum processo em execução no computador, provavelmente porque o processo foi encerrado. `pcRuntimes` e `ppRuntimes` será NULL.  
  
 E_OUTOFMEMORY  
 Não é possível alocar memória suficiente para `ppRuntimes` .  
  
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
