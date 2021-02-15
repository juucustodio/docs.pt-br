---
description: 'Saiba mais sobre o método: ICorProfilerInfo:: GetInprocInspectionInterface'
title: Método ICorProfilerInfo::GetInprocInspectionInterface
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetInprocInspectionInterface
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetInprocInspectionInterface
helpviewer_keywords:
- GetInprocInspectionInterface method [.NET Framework profiling]
- ICorProfilerInfo::GetInprocInspectionInterface method [.NET Framework profiling]
ms.assetid: 22a92d1d-8849-4af6-8304-ecc53dd1d289
topic_type:
- apiref
ms.openlocfilehash: 5b7ce053f0a64afd5d702a4eb59c1712f4b26e9e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781461"
---
# <a name="icorprofilerinfogetinprocinspectioninterface-method"></a>Método ICorProfilerInfo::GetInprocInspectionInterface

Obtém um objeto que pode ser consultado para uma interface "ICorDebugProcess". Esse método é obsoleto no .NET Framework versão 2,0.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetInprocInspectionInterface(  
    [out] IUnknown **ppicd);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `ppicd`  
 objeto de [saída](/cpp/atl/iunknown) que pode ser consultado para uma `ICorDebugProcess` interface.  
  
## <a name="remarks"></a>Comentários  

 A API de depuração Common Language Runtime (CLR) com suporte para a depuração em processo limitada no .NET Framework versão 1,0. A depuração em processo habilitou um criador de perfil para usar as partes de inspeção da API de depuração. Como resultado dos comentários dos clientes, a depuração em processo foi removida da .NET Framework na versão 2,0 e substituída por um conjunto de funcionalidades que está mais alinhado com a API de criação de perfil.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versão do .NET Framework:** 1,0  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
