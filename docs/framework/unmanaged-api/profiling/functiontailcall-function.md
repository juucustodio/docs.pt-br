---
description: 'Saiba mais sobre: função FunctionTailcall'
title: Função FunctionTailcall
ms.date: 03/30/2017
api_name:
- FunctionTailcall
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionTailcall
helpviewer_keywords:
- FunctionTailcall function [.NET Framework profiling]
ms.assetid: 66347e03-9a97-41e8-8f9d-89b80803f7b5
topic_type:
- apiref
ms.openlocfilehash: 8da3efde7d925fdb02232ca98662f8d6a6fd0adf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99687305"
---
# <a name="functiontailcall-function"></a>Função FunctionTailcall

Notifica o criador de perfil de que a função atualmente em execução está prestes a executar uma chamada tail para outra função.  
  
> [!NOTE]
> A `FunctionTailcall` função foi preterida na versão .NET Framework 2,0. Ele continuará funcionando, mas incorrerá em uma penalidade de desempenho. Em vez disso, use a função [FunctionTailcall2](functiontailcall2-function.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
void __stdcall FunctionTailcall (  
    [in] FunctionID funcID  
);  
```  
  
## <a name="parameters"></a>Parâmetros

- `funcID`

  \[in] o identificador da função atualmente em execução que está prestes a fazer uma chamada tail.

## <a name="remarks"></a>Comentários  

 A função de destino da chamada tail usará o quadro de pilhas atual e retornará diretamente para o chamador da função que fez a chamada final. Isso significa que um retorno de chamada [FunctionLeave](functionleave-function.md) não será emitido para uma função que seja o destino de uma chamada tail.  
  
 A `FunctionTailcall` função é um retorno de chamada; você deve implementá-la. A implementação deve usar o `__declspec` `naked` atributo de classe de armazenamento ().  
  
 O mecanismo de execução não salva nenhum registro antes de chamar essa função.  
  
- Na entrada, você deve salvar todos os registros que usar, incluindo aqueles na FPU (unidade de ponto flutuante).  
  
- Ao sair, você deve restaurar a pilha removendo todos os parâmetros que foram enviados por Push por seu chamador.  
  
 A implementação de `FunctionTailcall` não deve bloquear, pois atrasará a coleta de lixo. A implementação não deve tentar uma coleta de lixo porque a pilha pode não estar em um estado amigável de coleta de lixo. Se for feita uma tentativa de coleta de lixo, o tempo de execução será bloqueado até o `FunctionTailcall` retorno.  
  
 Além disso, a `FunctionTailcall` função não deve chamar um código gerenciado ou, de qualquer forma, causar uma alocação de memória gerenciada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf. idl  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** 1,1, 1,0  
  
## <a name="see-also"></a>Consulte também

- [Função FunctionEnter2](functionenter2-function.md)
- [Função FunctionLeave2](functionleave2-function.md)
- [Método SetEnterLeaveFunctionHooks2](icorprofilerinfo2-setenterleavefunctionhooks2-method.md)
- [Criando perfil de funções estáticas globais](profiling-global-static-functions.md)
