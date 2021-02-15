---
description: 'Saiba mais sobre: interface ICorDebugMergedAssemblyRecord'
title: Interface ICorDebugMergedAssemblyRecord
ms.date: 03/30/2017
ms.assetid: fe280b11-9479-4e34-a07c-0d1ea8088422
ms.openlocfilehash: e64c0ee30a8e8956dd336a30e6c81962c75f04e9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99650281"
---
# <a name="icordebugmergedassemblyrecord-interface"></a>Interface ICorDebugMergedAssemblyRecord

Fornece informações sobre um assembly mesclado.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetCulture](icordebugmergedassemblyrecord-getculture-method.md)|Obtém a cadeia de caracteres do nome da cultura do assembly.|  
|[Método GetIndex](icordebugmergedassemblyrecord-getindex-method.md)|Obtém o índice de prefixo do assembly.|  
|[Método GetPublicKey](icordebugmergedassemblyrecord-getpublickey-method.md)|Obtém a chave pública do assembly.|  
|[Método GetPublicKeyToken](icordebugmergedassemblyrecord-getpublickeytoken-method.md)|Obtém o token de chave pública do assembly.|  
|[Método GetSimpleName](icordebugmergedassemblyrecord-getsimplename-method.md)|Obtém o nome simples do assembly.|  
|[Método GetVersion](icordebugmergedassemblyrecord-getversion-method.md)|Obtém as informações de versão do assembly.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Essa interface está disponível somente com .NET Native. Se você implementar essa interface para cenários ICorDebug fora do .NET Native, o Common Language Runtime ignorará essa interface.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
