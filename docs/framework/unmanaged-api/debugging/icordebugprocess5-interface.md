---
description: 'Saiba mais sobre: interface ICorDebugProcess5'
title: Interface ICorDebugProcess5
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5
helpviewer_keywords:
- ICorDebugProcess5 interface [.NET Framework debugging]
ms.assetid: 30a39d79-1f10-4328-9c5d-094ed824e2ba
topic_type:
- apiref
ms.openlocfilehash: 880c305c1d9786f87d9727836a973696aa686ecf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99649761"
---
# <a name="icordebugprocess5-interface"></a>Interface ICorDebugProcess5

Estende a interface ICorDebugProcess para dar suporte ao acesso ao heap gerenciado, para fornecer informações sobre a coleta de lixo de objetos gerenciados e para determinar se um depurador carrega imagens do cache de imagem nativa local do aplicativo.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método EnableNGenPolicy](icordebugprocess5-enablengenpolicy-method.md)|Define um valor que determina como um aplicativo carrega imagens nativas durante a execução em um depurador gerenciado.|  
|[Método EnumerateGCReferences](icordebugprocess5-enumerategcreferences-method.md)|Obtém um enumerador para todos os objetos que devem ser coletados pelo lixo em um processo.|  
|[Método EnumerateHandles](icordebugprocess5-enumeratehandles-method.md)|Obtém um enumerador para identificadores de objeto em um processo.|  
|[Método EnumerateHeap](icordebugprocess5-enumerateheap-method.md)|Obtém um enumerador para objetos no heap gerenciado.|  
|[Método EnumerateHeapRegions](icordebugprocess5-enumerateheapregions-method.md)|Obtém um enumerador para regiões do heap gerenciado.|  
|[Método GetArrayLayout](icordebugprocess5-getarraylayout-method.md)|Obtém informações sobre o layout de uma matriz na memória.|  
|[Método GetGCHeapInformation](icordebugprocess5-getgcheapinformation-method.md)|Obtém um ponteiro para uma estrutura de [COR_HEAPINFO](cor-heapinfo-structure.md) que contém informações sobre objetos que devem ser coletados pelo lixo no heap gerenciado.|  
|[Método GetObject](icordebugprocess5-getobject-method.md)|Obtém um ponteiro para um objeto no heap gerenciado.|  
|[Método GetTypeFields](icordebugprocess5-gettypefields-method.md)|Obtém um ponteiro para uma matriz que contém informações de campo para um tipo com base em seu identificador de tipo.|  
|[Método GetTypeForTypeID](icordebugprocess5-gettypefortypeid-method.md)|Obtém um objeto de tipo que fornece informações sobre um objeto com base em seus identificadores de tipo.|  
|[Método GetTypeID](icordebugprocess5-gettypeid-method.md)|Obtém o identificador de tipo para o objeto em um endereço especificado.|  
|[Método GetTypeLayout](icordebugprocess5-gettypelayout-method.md)|Obtém informações sobre o layout de um objeto na memória com base em seu identificador de tipo.|  
  
## <a name="remarks"></a>Comentários  

 Essa interface estende logicamente as interfaces ICorDebugProcess, ICorDebugProcess2 e [ICorDebugProcess3](icordebugprocess3-interface.md) .  
  
> [!NOTE]
> Esta interface não dá suporte a chamadas remotas de outro computador ou de outro processo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
