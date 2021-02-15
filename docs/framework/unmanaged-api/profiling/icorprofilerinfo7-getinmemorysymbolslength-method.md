---
description: 'Saiba mais sobre o método: ICorProfilerInfo7:: GetInMemorySymbolsLength'
title: 'Método ICorProfilerInfo7:: GetInMemorySymbolsLength'
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo7.GetInMemorySymbolsLength
api_location:
- mscorwks.dll
- icorprof.idl
api_type:
- COM
ms.assetid: d62c4a4c-8a62-45aa-8f01-a8387cf36159
ms.openlocfilehash: 5d96b17e8abbd023f2d050eff3f121a871a94754
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737110"
---
# <a name="icorprofilerinfo7getinmemorysymbolslength-method"></a>Método ICorProfilerInfo7:: GetInMemorySymbolsLength

[Com suporte no .NET Framework 4.6.1 e versões posteriores]  
  
 Retorna o comprimento de um fluxo de símbolo na memória.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetInMemorySymbolsLength(  
        [in] ModuleID moduleId,  
        [out] DWORD* pCountSymbolBytes  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `moduleId`  
 no O identificador do módulo que contém o fluxo na memória.  
  
 pCountSymbolBytes  
 fora Um ponteiro para um `DWORD` valor que, quando o método retorna, contém o comprimento do fluxo em bytes.  
  
## <a name="return-value"></a>Valor retornado  

 O método retorna `S_OK` se o comprimento do fluxo de memória pode ser determinado, mesmo se for zero (0).  
  
 O método retorna `CORPROF_E_MODULE_IS_DYNAMIC` se o método foi criado usando <xref:System.Reflection.Emit?displayProperty=nameWithType> .  
  
## <a name="remarks"></a>Comentários  

 Se o módulo tiver símbolos na memória, o comprimento do fluxo será colocado em `pCountSymbolBytes` . Se o módulo não tiver símbolos na memória, `*pCountSymbolBytes = 0` .  
  
> [!NOTE]
> A implementação atual não oferece suporte a Reflection. Emit. Se o módulo foi criado usando Reflection. Emit, o método retornará `CORPROF_E_MODULE_IS_DYNAMIC` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo7](icorprofilerinfo7-interface.md)
