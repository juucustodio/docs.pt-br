---
description: 'Saiba mais sobre o método: ICorProfilerInfo2:: EnumModuleFrozenObjects'
title: Método ICorProfilerInfo2::EnumModuleFrozenObjects
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.EnumModuleFrozenObjects
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::EnumModuleFrozenObjects
helpviewer_keywords:
- EnumModuleFrozenObjects method [.NET Framework profiling]
- ICorProfilerInfo2::EnumModuleFrozenObjects method [.NET Framework profiling]
ms.assetid: 920b6483-7064-4d64-8613-fcc38ccf9b1e
topic_type:
- apiref
ms.openlocfilehash: b68571544c00c8c234a73404a95433e91f0cfdcf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753205"
---
# <a name="icorprofilerinfo2enummodulefrozenobjects-method"></a>Método ICorProfilerInfo2::EnumModuleFrozenObjects

Obtém um enumerador que permite a iteração sobre os objetos congelados no módulo especificado. Este método é obsoleto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumModuleFrozenObjects(  
    [in] ModuleID moduleID,  
    [out] ICorProfilerObjectEnum** ppEnum);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `moduleID`  
 no A ID do módulo que contém os objetos congelados a serem enumerados.  
  
 `ppEnum`  
 fora Um ponteiro para o endereço de uma interface [ICorProfilerObjectEnum](icorprofilerobjectenum-interface.md) , que enumera os objetos congelados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:** 3,5, 3,0 sp1, 3,0, 2,0 SP1, 2,0  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
- [Interface ICorProfilerInfo2](icorprofilerinfo2-interface.md)
