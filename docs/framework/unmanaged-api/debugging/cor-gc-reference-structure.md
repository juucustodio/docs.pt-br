---
description: 'Saiba mais sobre: estrutura de COR_GC_REFERENCE'
title: Estrutura COR_GC_REFERENCE
ms.date: 03/30/2017
api_name:
- COR_GC_REFERENCE
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_GC_REFERENCE
helpviewer_keywords:
- COR_GC_REFERENCE structure [.NET Framework debugging]
ms.assetid: 162e8179-0cd4-4110-8f06-5f387698bd62
topic_type:
- apiref
ms.openlocfilehash: 38518bb1eb870081621bf32af9e63cdaa208dbd3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801807"
---
# <a name="cor_gc_reference-structure"></a>Estrutura COR_GC_REFERENCE

Contém informações sobre um objeto que será coletado como lixo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _COR_GC_REFERENCE {  
    ICorDebugAppDomain *domain;
    ICorDebugValue *location;  
    CorGCReferenceType type;  
    UINT64 extraData;  
} COR_GC_REFERENCE;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`domain`|Um ponteiro para o domínio do aplicativo ao qual o identificador ou objeto pertence. Seu valor pode ser `null` .|  
|`location`|Uma interface ICorDebugValue ou ICorDebugReferenceValue que corresponde ao objeto a ser coletado como lixo.|  
|`type`|Um valor de enumeração [CorGCReferenceType](corgcreferencetype-enumeration.md) que indica de onde veio a raiz. Para obter mais informações, consulte a seção Comentários.|  
|`extraData`|Dados adicionais sobre o objeto a ser coletado pelo lixo. Essas informações dependem da origem do objeto, conforme indicado pelo `type` campo. Para obter mais informações, consulte a seção Comentários.|  
  
## <a name="remarks"></a>Comentários  

 O `type` campo é um valor de enumeração [CorGCReferenceType](corgcreferencetype-enumeration.md) que indica de onde veio a referência. Um `COR_GC_REFERENCE` valor específico pode refletir qualquer um dos seguintes tipos de objetos gerenciados:  
  
- Objetos de todas as pilhas gerenciadas ( `CorGCReferenceType.CorReferenceStack` ). Isso inclui referências dinâmicas em código gerenciado, bem como objetos criados pelo Common Language Runtime.  
  
- Objetos da tabela de identificadores ( `CorGCReferenceType.CorHandle*` ). Isso inclui referências fortes ( `HNDTYPE_STRONG` e `HNDTYPE_REFCOUNT` ) e variáveis estáticas em um módulo.  
  
- Objetos da fila do finalizador ( `CorGCReferenceType.CorReferenceFinalizer` ). O finalizador enfileira objetos de raízes até que o finalizador tenha sido executado.  
  
 O `extraData` campo contém dados extras dependendo da origem (ou tipo) da referência. Os valores possíveis são:  
  
- `DependentSource`. Se `type` for `CorGCREferenceType.CorHandleStrongDependent` , esse campo será o objeto que, se estiver ativo, faz a raiz do objeto a ser coletado como lixo `COR_GC_REFERENCE.Location` .  
  
- `RefCount`. Se `type` for `CorGCREferenceType.CorHandleStrongRefCount` , esse campo será a contagem de referência do identificador.  
  
- `Size`. Se `type` for `CorGCREferenceType.CorHandleStrongSizedByref` , esse campo será o último tamanho da árvore de objetos para a qual o coletor de lixo calculou as raízes de objeto. Observe que esse cálculo não está necessariamente atualizado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de depuração](debugging-structures.md)
- [Depuração](index.md)
