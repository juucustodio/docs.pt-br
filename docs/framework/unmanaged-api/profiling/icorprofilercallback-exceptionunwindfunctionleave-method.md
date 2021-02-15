---
description: 'Saiba mais sobre o método: ICorProfilerCallback:: ExceptionUnwindFunctionLeave'
title: Método ICorProfilerCallback::ExceptionUnwindFunctionLeave
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ExceptionUnwindFunctionLeave
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ExceptionUnwindFunctionLeave
helpviewer_keywords:
- ICorProfilerCallback::ExceptionUnwindFunctionLeave method [.NET Framework profiling]
- ExceptionUnwindFunctionLeave method [.NET Framework profiling]
ms.assetid: ebaad1d5-ee0a-4cb0-96bc-8ba5d371b747
topic_type:
- apiref
ms.openlocfilehash: f428230b017841e931463057144ef72cc1ead45f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99705950"
---
# <a name="icorprofilercallbackexceptionunwindfunctionleave-method"></a>Método ICorProfilerCallback::ExceptionUnwindFunctionLeave

Notifica o criador de perfil de que a fase de desenrolamento da manipulação de exceções concluiu o desenrolamento de uma função.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ExceptionUnwindFunctionLeave();  
```  
  
## <a name="remarks"></a>Comentários  

 Quando o `ExceptionUnwindFunctionLeave` método é chamado, a instância de função e seus dados de pilha são removidos da pilha.  
  
 O criador de perfil não deve bloquear durante essa chamada porque a pilha pode não estar em um estado que permita a coleta de lixo e, portanto, a coleta de lixo preemptiva não pode ser habilitada. Se o criador de perfil for bloqueado aqui e uma tentativa de coleta de lixo, o tempo de execução será bloqueado até que esse retorno de chamada seja retornado.  
  
 Além disso, durante essa chamada, o criador de perfil não deve chamar o código gerenciado ou, de qualquer forma, causar uma alocação de memória gerenciada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl, CorProf. h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerCallback](icorprofilercallback-interface.md)
- [Método ExceptionUnwindFunctionEnter](icorprofilercallback-exceptionunwindfunctionenter-method.md)
