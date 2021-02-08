---
description: 'Saiba mais sobre o método: ICorDebugManagedCallback2:: Exception'
title: Método ICorDebugManagedCallback2::Exception
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback2.Exception
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback2::Exception
helpviewer_keywords:
- ICorDebugManagedCallback2::Exception method [.NET Framework debugging]
- Exception method, ICorDebugManagedCallback2 interface [.NET Framework debugging]
ms.assetid: 78b0f14f-2fae-4e63-8412-4df119ee8468
topic_type:
- apiref
ms.openlocfilehash: 18fd4efcfbd1f13ce527b212d7450ba0d7651a3c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790874"
---
# <a name="icordebugmanagedcallback2exception-method"></a>Método ICorDebugManagedCallback2::Exception

Notifica o depurador de que uma pesquisa de um manipulador de exceção foi iniciada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Exception (  
    [in] ICorDebugAppDomain   *pAppDomain,  
    [in] ICorDebugThread      *pThread,  
    [in] ICorDebugFrame       *pFrame,  
    [in] ULONG32              nOffset,  
    [in] CorDebugExceptionCallbackType dwEventType,  
    [in] DWORD                dwFlags  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pAppDomain`  
 no Um ponteiro para um objeto ICorDebugAppDomain que representa o domínio do aplicativo que contém o thread no qual a exceção foi gerada.  
  
 `pThread`  
 no Um ponteiro para um objeto ICorDebugThread que representa o thread no qual a exceção foi gerada.  
  
 `pFrame`  
 no Um ponteiro para um objeto ICorDebugFrame que representa um quadro, conforme determinado pelo `dwEventType` parâmetro. Para obter mais informações, consulte a tabela na seção comentários.  
  
 `nOffset`  
 no Um inteiro que especifica um deslocamento, conforme determinado pelo `dwEventType` parâmetro. Para obter mais informações, consulte a tabela na seção comentários.  
  
 `dwEventType`  
 no Um valor da enumeração CorDebugExceptionCallbackType que especifica o tipo deste retorno de chamada de exceção.  
  
 `dwFlags`  
 no Um valor da enumeração [CorDebugExceptionFlags](cordebugexceptionflags-enumeration.md) que especifica informações adicionais sobre a exceção  
  
## <a name="remarks"></a>Comentários  

 O `Exception` retorno de chamada é chamado em vários pontos durante a fase de pesquisa do processo de tratamento de exceção. Ou seja, ele pode ser chamado mais de uma vez ao desenrolar uma exceção.  
  
 A exceção que está sendo processada pode ser recuperada do objeto ICorDebugThread referenciado pelo `pThread` parâmetro.  
  
 O quadro e o deslocamento específicos são determinados pelo `dwEventType` parâmetro da seguinte maneira:  
  
|Valor de `dwEventType`|Valor de `pFrame`|Valor de `nOffset`|  
|----------------------------|-----------------------|------------------------|  
|DEBUG_EXCEPTION_FIRST_CHANCE|O quadro que gerou a exceção.|O ponteiro de instrução no quadro.|  
|DEBUG_EXCEPTION_USER_FIRST_CHANCE|O quadro de código do usuário mais próximo do ponto da exceção gerada.|O ponteiro de instrução no quadro.|  
|DEBUG_EXCEPTION_CATCH_HANDLER_FOUND|O quadro que contém o manipulador catch.|O deslocamento da MSIL (Microsoft Intermediate Language) do início do manipulador catch.|  
|DEBUG_EXCEPTION_UNHANDLED|NULO|Indefinido.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md)
- [Interface ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)
