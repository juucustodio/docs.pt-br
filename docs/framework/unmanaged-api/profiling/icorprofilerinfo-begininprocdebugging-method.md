---
description: 'Saiba mais sobre o método: ICorProfilerInfo:: BeginInprocDebugging'
title: Método ICorProfilerInfo::BeginInprocDebugging
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.BeginInprocDebugging
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::BeginInprocDebugging
helpviewer_keywords:
- BeginInprocDebugging method [.NET Framework profiling]
- ICorProfilerInfo::BeginInprocDebugging method [.NET Framework profiling]
ms.assetid: c5c82c69-99f8-4447-aee0-42cca0a5eb5c
topic_type:
- apiref
ms.openlocfilehash: 151aa3604d61e4c5d9e7e24fe9f17bf754d72233
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737396"
---
# <a name="icorprofilerinfobegininprocdebugging-method"></a>Método ICorProfilerInfo::BeginInprocDebugging

Inicializa o suporte à depuração em processo. Esse método é obsoleto no .NET Framework versão 2,0.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT BeginInprocDebugging(  
    [in]  BOOL   fThisThreadOnly,  
    [out] DWORD *pdwProfilerContext);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `fThisThreadOnly`  
 no Defina esse valor como `true` para inicializar o suporte de depuração somente para o thread atual; defina-o como `false` para inicializar o suporte à depuração para todos os threads.  
  
 `pdwProfilerContext`  
 fora O ponteiro para um valor retornado que identifica a sessão de depuração.  
  
## <a name="remarks"></a>Comentários  

 Os serviços de depuração CLR oferecem suporte à depuração em processo limitada no .NET Framework versões 1,0 e 1,1. A depuração em processo habilitou um criador de perfil para usar as partes de inspeção da API de depuração. No entanto, devido aos comentários do cliente, a depuração em processo foi removida da .NET Framework na versão 2,0 e substituída por um conjunto de funcionalidades que está mais alinhado com a API de criação de perfil.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versão do .NET Framework:** 1,0  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
