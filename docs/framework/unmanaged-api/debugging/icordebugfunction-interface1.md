---
description: 'Saiba mais sobre: interface ICorDebugFunction'
title: Interface ICorDebugFunction
ms.date: 03/30/2017
api_name:
- ICorDebugFunction
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction
helpviewer_keywords:
- ICorDebugFunction interface [.NET Framework debugging]
ms.assetid: 783faea9-8083-41c1-b04a-51a81ac4c8f3
topic_type:
- apiref
ms.openlocfilehash: 835625341889e89e15ceb66ca71531cf7b8311c4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99692362"
---
# <a name="icordebugfunction-interface"></a>Interface ICorDebugFunction

Representa uma função ou um método gerenciado.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método CreateBreakpoint](icordebugfunction-createbreakpoint-method.md)|Cria um ponto de interrupção no início desta função.|  
|[Método GetClass](icordebugfunction-getclass-method.md)|Obtém um objeto ICorDebugClass que representa a classe da qual essa função é membro.|  
|[Método GetCurrentVersionNumber](icordebugfunction-getcurrentversionnumber-method.md)|Obtém o número de versão da edição mais recente feita a esta função.|  
|[Método GetILCode](icordebugfunction-getilcode-method.md)|Obtém o código da MSIL (Microsoft Intermediate Language) para esta função.|  
|[Método GetLocalVarSigToken](icordebugfunction-getlocalvarsigtoken-method.md)|Obtém o token de metadados para a assinatura de variável local da função que é representada por essa `ICorDebugFunction` instância.|  
|[Método GetModule](icordebugfunction-getmodule-method.md)|Obtém o módulo no qual essa função é definida.|  
|[Método GetNativeCode](icordebugfunction-getnativecode-method.md)|Obtém o código nativo para esta função.|  
|[Método GetToken](icordebugfunction-gettoken-method.md)|Obtém o token de metadados para esta função.|  
  
## <a name="remarks"></a>Comentários  

 A `ICorDebugFunction` interface não representa uma função com parâmetros de tipo genérico. Por exemplo, uma `ICorDebugFunction` instância representaria `Func<T>` , mas não `Func<string>` . Chame [ICorDebugILFrame2:: EnumerateTypeParameters](icordebugilframe2-enumeratetypeparameters-method.md) para obter os parâmetros de tipo genérico.  
  
 A relação entre o token de metadados de um método, o `mdMethodDef` e o objeto de um método `ICorDebugFunction` depende se editar e continuar é permitido na função:  
  
- Se editar e continuar não for permitido na função, existirá uma relação um-para-um entre o `ICorDebugFunction` objeto e o `mdMethodDef` token. Ou seja, a função tem um `ICorDebugFunction` objeto e um `mdMethodDef` token.  
  
- Se editar e continuar for permitido na função, existirá uma relação muitos-para-um entre o `ICorDebugFunction` objeto e o `mdMethodDef` token. Ou seja, a função pode ter muitas instâncias de `ICorDebugFunction` , uma para cada versão da função, mas apenas um `mdMethodDef` token.  
  
> [!NOTE]
> Esta interface não dá suporte para chamada remota, seja entre computadores ou processos cruzados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:**  CorGuids. lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
