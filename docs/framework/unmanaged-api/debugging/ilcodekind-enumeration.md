---
description: 'Saiba mais sobre: Enumeração ILCodeKind'
title: Enumeração ILCodeKind
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ILCodeKind
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: b91765e4-82db-46f9-a6dc-6b80610276af
topic_type:
- apiref
ms.openlocfilehash: 2d3163b2c601c6f53d9a532fa877c014a67b3e18
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790458"
---
# <a name="ilcodekind-enumeration"></a>Enumeração ILCodeKind

[Com suporte no .NET Framework 4.5.2 e versões posteriores]  
  
 Fornece valores que especificam se o depurador é capaz de acessar variáveis locais ou o código incluído na instrumentação ReJIT do criador de perfis.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
typedef enum ILCodeKind {  
   ILCODE_ORIGINAL_IL = 0x1,  
   ILCODE_REJIT_IL = 0x2,  
} ILCodeKind;  
```  
  
## <a name="members"></a>Membros  
  
|Nome do membro|Descrição|  
|-----------------|-----------------|  
|`ILCODE_ORIGINAL_IL`|O depurador não tem acesso a informações de instrumentação ReJIT.|  
|`ILCODE_REJIT_IL`|O depurador tem acesso a informações de instrumentação ReJIT.|  
  
## <a name="remarks"></a>Comentários  

 Um membro da `ILCodeKind` enumeração pode ser passado para os métodos [EnumerateLocalVariablesEx](icordebugilframe4-enumeratelocalvariablesex-method.md) e [GetLocalVariableEx](icordebugilframe4-getlocalvariableex-method.md) para determinar se o depurador pode acessar variáveis adicionadas na instrumentação ReJIT do Profiler e ao método [GetCodeEx](icordebugilframe4-getcodeex-method.md) para determinar se o depurador pode acessar o Il instrumentado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Declarando enumerações](debugging-enumerations.md)
- [Interface ICorDebugILFrame4](icordebugilframe4-interface.md)
- [ReJIT: um guia de How-To](/archive/blogs/davbr/rejit-a-how-to-guide)
