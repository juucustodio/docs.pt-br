---
description: 'Saiba mais sobre: interface ICorDebugFunction2'
title: Interface ICorDebugFunction2
ms.date: 03/30/2017
api_name:
- ICorDebugFunction2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction2
helpviewer_keywords:
- ICorDebugFunction2 interface [.NET Framework debugging]
ms.assetid: 2b936bef-9b75-48bf-859f-42e419c65f1c
topic_type:
- apiref
ms.openlocfilehash: e5297d46acb9b174537363fc185fa2d540d55a75
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99692189"
---
# <a name="icordebugfunction2-interface"></a>Interface ICorDebugFunction2

Estende logicamente a interface ICorDebugFunction para fornecer suporte para depuração passo a Apenas Meu Código, que ignora o código que não é do usuário.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método EnumerateNativeCode](icordebugfunction2-enumeratenativecode-method.md)|(Ainda não implementado.) Obtém um ponteiro de interface para um ICorDebugCodeEnum que contém as instruções de código nativo na função referenciada por este objeto ICorDebugFunction2.|  
|[Método GetJMCStatus](icordebugfunction2-getjmcstatus-method.md)|Obtém um valor que indica se esta função está marcada como código de usuário.|  
|[Método GetVersionNumber](icordebugfunction2-getversionnumber-method.md)|Obtém a versão editar e continuar desta função.|  
|[Método SetJMCStatus](icordebugfunction2-setjmcstatus-method.md)|Marca essa função para Apenas Meu Código stepping.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
