---
description: 'Saiba mais sobre: interface ICorDebugAppDomain3'
title: Interface ICorDebugAppDomain3
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain3
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain3
helpviewer_keywords:
- ICorDebugAppDomain3 interface [.NET Framework debugging]
ms.assetid: 875ef5be-c1e7-4d95-97e9-d3a667aeaba0
topic_type:
- apiref
ms.openlocfilehash: 6575aa685759102443babeaf82774e6221b80693
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772205"
---
# <a name="icordebugappdomain3-interface"></a>Interface ICorDebugAppDomain3

Fornece métodos para recuperar informações sobre as representações gerenciadas dos tipos de Windows Runtime atualmente carregados em um domínio de aplicativo. Essa interface é uma extensão das interfaces ICorDebugAppDomain e ICorDebugAppDomain2.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[ICorDebugAppDomain3::GetCachedWinRTTypes](icordebugappdomain3-getcachedwinrttypes-method.md)|Obtém um enumerador para todos os tipos de Windows Runtime em cache.|  
|[ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs](icordebugappdomain3-getcachedwinrttypesforiids-method.md)|Obtém um enumerador para tipos de Windows Runtime em cache em um domínio de aplicativo com base em seus identificadores de interface.|  
  
## <a name="remarks"></a>Comentários  

 Essa interface deve ser usada por um depurador em conjunto com uma chamada de avaliação de função para `M:System.Runtime.InteropServices.Marshal.GetInspectableIIDs(System.Object)` . Quando o método recupera os identificadores de interface com suporte de um objeto de servidor Windows Runtime, o depurador pode usar os métodos definidos nesta interface para mapeá-los para tipos gerenciados que correspondem a essas interfaces.  
  
 Para recuperar uma instância dessa interface, execute `QueryInterface` em uma instância da interface ICorDebugAppDomain ou ICorDebugAppDomain2.  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** Windows Runtime  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
