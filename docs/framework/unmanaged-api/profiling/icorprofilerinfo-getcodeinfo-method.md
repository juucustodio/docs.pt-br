---
description: 'Saiba mais sobre o método: ICorProfilerInfo:: GetCodeInfo'
title: Método ICorProfilerInfo::GetCodeInfo
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetCodeInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetCodeInfo
helpviewer_keywords:
- GetCodeInfo method [.NET Framework profiling]
- ICorProfilerInfo::GetCodeInfo method [.NET Framework profiling]
ms.assetid: 90140b0f-a926-4a7e-b6fa-23e05f703cce
topic_type:
- apiref
ms.openlocfilehash: e965e9c21b7add0367b08f152bf509ad6b6ed4cd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99647655"
---
# <a name="icorprofilerinfogetcodeinfo-method"></a>Método ICorProfilerInfo::GetCodeInfo

Obtém a extensão do código nativo associado à ID da função especificada.  
  
 Esse método é obsoleto. Em vez disso, use o método [ICorProfilerInfo2:: GetCodeInfo2](icorprofilerinfo2-getcodeinfo2-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCodeInfo(  
    [in]  FunctionID functionId,  
    [out] LPCBYTE    *pStart,  
    [out] ULONG      *pcSize);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `functionId`  
 no A ID da função à qual o código nativo está associado.  
  
 `pStart`  
 fora Um ponteiro para uma matriz de bytes que compõe o código nativo da função.  
  
 `pcSize`  
 fora Um ponteiro para um inteiro que especifica o tamanho, em bytes, do código nativo.  
  
## <a name="remarks"></a>Comentários  

 Para otimizar o desempenho, o tempo de execução na versão 2,0 do .NET Framework divide o código pré-compilado precompilado de uma função em várias regiões. Consequentemente, o `GetCodeInfo` método é obsoleto no .NET Framework 2,0 porque não é possível manipular a extensão do código nativo de uma função. Os profileres devem mudar para o uso do `ICorProfilerInfo2::GetCodeInfo2` método mais geral.  
  
 Essa função usa buffers alocados pelo chamador.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** 1,0  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo](icorprofilerinfo-interface.md)
- [Criação de perfil de interfaces](profiling-interfaces.md)
- [Criação de perfil](index.md)
