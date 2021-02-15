---
title: MDA exceptionSwallowedOnCallFromCom
description: Examine o assistente de depuração gerenciada do exceptionSwallowedOnCallFromCOM no .NET. Esse MDA ocorre se uma exceção foi lançada, mas não há uma boa maneira de relatá-la.
ms.date: 03/30/2017
helpviewer_keywords:
- messages, informational
- informational messages
- managed debugging assistants (MDAs), exceptions
- exception handling, managed debugging assistants
- MDAs (managed debugging assistants), exceptions
- ExceptionSwallowedOnCallFromCOM MDA
ms.assetid: 55d6ab12-f251-4aab-aa64-aacbe9d9f974
ms.openlocfilehash: 11daccb4d1e757bf2fae25858d706eee5921c509
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96244347"
---
# <a name="exceptionswallowedoncallfromcom-mda"></a>MDA exceptionSwallowedOnCallFromCom

O `exceptionSwallowedOnCallFromCOM` MDA (assistente para depuração gerenciada) é ativado quando uma exceção é lançada do código do CLR (Common Language Runtime) chamado do COM por meio de um método que não tem um tipo de retorno HRESULT não gerenciado.  
  
## <a name="symptoms"></a>Sintomas  

 Uma chamada para um componente gerenciado de COM retorna um valor de FALSE ou 0. Como alternativa, se o método tiver um tipo de retorno nulo, pode não haver indicação de que foi lançada uma exceção durante a execução do método. Nesse caso, a exceção será capturada silenciosamente e a execução retornará ao chamador do COM.  
  
## <a name="cause"></a>Causa  

 Uma exceção foi lançada, mas não há uma maneira válida de relatá-la.  
  
## <a name="resolution"></a>Resolução  

 Somente informativo, não indica necessariamente um bug.  
  
## <a name="effect-on-the-runtime"></a>Efeito sobre o runtime  

 Esse MDA não tem efeito sobre o CLR. Ele apenas relata dados sobre exceções capturadas silenciosamente.  
  
## <a name="output"></a>Saída  

 Mensagem informativa contendo o nome do método, o nome do tipo e a mensagem de exceção.  
  
## <a name="configuration"></a>Configuração  
  
```xml  
<mdaConfig>  
  <assistants>  
    <exceptionSwallowedOnCallFromCom />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Veja também

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Diagnosticando erros com assistentes de depuração gerenciados](diagnosing-errors-with-managed-debugging-assistants.md)
- [Realizando marshaling de interoperabilidade](../interop/interop-marshaling.md)
