---
description: 'Saiba mais sobre o método: ICorDebugProcess:: ReadMemory'
title: Método ICorDebugProcess::ReadMemory
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.ReadMemory
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::ReadMemory
helpviewer_keywords:
- ReadMemory method [.NET Framework debugging]
- ICorDebugProcess::ReadMemory method [.NET Framework debugging]
ms.assetid: 28e4b2f6-9589-445c-be24-24a3306795e7
topic_type:
- apiref
ms.openlocfilehash: bdf1bda9df416b6d3142e3ae09955e706f260802
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99746796"
---
# <a name="icordebugprocessreadmemory-method"></a>Método ICorDebugProcess::ReadMemory

Lê uma área especificada de memória para esse processo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ReadMemory(  
    [in]  CORDB_ADDRESS address,
    [in]  DWORD size,  
    [out, size_is(size), length_is(size)] BYTE buffer[],  
    [out] SIZE_T *read);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `address`  
 no Um `CORDB_ADDRESS` valor que especifica o endereço base da memória a ser lida.  
  
 `size`  
 no O número de bytes a serem lidos da memória.  
  
 `buffer`  
 fora Um buffer que recebe o conteúdo da memória.  
  
 `read`  
 fora Um ponteiro para o número de bytes transferidos para o buffer especificado.  
  
## <a name="remarks"></a>Comentários  

 O `ReadMemory` método destina-se principalmente a ser usado pela depuração de interoperabilidade para inspecionar regiões de memória que estão sendo usadas pela parte não gerenciada do depurador. Esse método também pode ser usado para ler o código MSIL (Microsoft Intermediate Language) e o código compilado por JIT nativo.  
  
 Todos os pontos de interrupção gerenciados serão removidos dos dados retornados no `buffer` parâmetro. Nenhum ajuste será feito para pontos de interrupção nativos definidos por [ICorDebugProcess2:: SetUnmanagedBreakpoint](icordebugprocess2-setunmanagedbreakpoint-method.md).  
  
 Nenhum cache de memória de processo é executado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
