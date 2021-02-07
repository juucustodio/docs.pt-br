---
description: 'Saiba mais sobre: interface ICorDebugCode2'
title: Interface ICorDebugCode2
ms.date: 03/30/2017
api_name:
- ICorDebugCode2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode2
helpviewer_keywords:
- ICorDebugCode2 interface [.NET Framework debugging]
ms.assetid: 9321903b-7dea-40d8-ba32-99016c00cc46
topic_type:
- apiref
ms.openlocfilehash: 29fd657ec56993d47ee57aa41c81b45e75352697
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765021"
---
# <a name="icordebugcode2-interface"></a>Interface ICorDebugCode2

Fornece métodos que estendem os recursos de "ICorDebugCode".  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetCodeChunks](icordebugcode2-getcodechunks-method.md)|Obtém as partes de código das quais este objeto de código é composto.|  
|[Método GetCompilerFlags](icordebugcode2-getcompilerflags-method.md)|Obtém os sinalizadores que especificam as condições sob as quais esse objeto de código era JIT (just-in-time) compilado ou gerado usando o gerador de imagem nativa (Ngen.exe).|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugCode3](icordebugcode3-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
