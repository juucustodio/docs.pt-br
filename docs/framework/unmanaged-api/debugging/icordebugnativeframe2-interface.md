---
description: 'Saiba mais sobre: interface ICorDebugNativeFrame2'
title: Interface ICorDebugNativeFrame2
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame2
helpviewer_keywords:
- ICorDebugNativeFrame2 interface [.NET Framework debugging]
ms.assetid: 52a80838-af36-4399-bc97-d8a4c6d76df2
topic_type:
- apiref
ms.openlocfilehash: 9ed0e20bb29bef3b210258956ebecb1ee7a96df8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99722341"
---
# <a name="icordebugnativeframe2-interface"></a>Interface ICorDebugNativeFrame2

Fornece métodos que testam relações de quadros pai e filho.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método IsChild](icordebugnativeframe2-ischild-method.md)|Determina se o quadro atual é um quadro filho.|  
|[Método IsMatchingParentFrame](icordebugnativeframe2-ismatchingparentframe-method.md)|Determina se o quadro especificado é o pai do quadro atual.|  
|[Método GetStackParameterSize](icordebugnativeframe2-getstackparametersize-method.md)|Retorna o tamanho cumulativo dos parâmetros na pilha em sistemas operacionais x86.|  
  
## <a name="remarks"></a>Comentários  

 Essa interface estende logicamente a interface "ICorDebugNativeFrame".  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
