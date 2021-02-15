---
title: MDA notMarshalable
description: Examine o assistente de depuração gerenciada não Marshalable, que pode ser ativado se as chamadas não forem atendidas ou ocorrerem no contexto errado para ponteiros de interface COM.
ms.date: 03/30/2017
helpviewer_keywords:
- managed debugging assistants (MDAs), interface pointer not marshalable
- interface pointer not marshalable MDA
- MDAs (managed debugging assistants), interface pointer not marshalable
- marshaling, run-time errors
- managed debugging assistants (MDAs), marshaling
- marshalable interface pointers
- MDAs (managed debugging assistants), marshaling
- notMarshalable MDA
ms.assetid: 96e7b2c1-843f-4d64-b519-740c3a18b50a
ms.openlocfilehash: 344c275d8645b16de3ecb06517297df06323ced4
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96254552"
---
# <a name="notmarshalable-mda"></a>MDA notMarshalable

O MDA (Assistente de Depuração Gerenciado) de `notMarshalable` é ativado quando o CLR (Common Language Runtime) encontra um ponteiro de interface COM sem um proxy/stub registrado válido ou uma implementação incorreta da interface `IMarshal` ao tentar realizar marshaling da interface entre contextos.  
  
## <a name="symptoms"></a>Sintomas  

 Chamadas não são atendidas ou chamadas ocorrem no contexto errado para ponteiros de interface COM.  
  
## <a name="cause"></a>Causa  

 Nenhum proxy/stub registrado válido ou uma `IMarshal` incorreta ao tentar realizar marshaling da interface entre contextos.  
  
## <a name="resolution"></a>Resolução  

 Verifique se você tem um stub de proxy registrado e que a implementação `IMarshal` é válida.  
  
## <a name="effect-on-the-runtime"></a>Efeito sobre o runtime  

 Esse MDA não tem nenhum efeito sobre o runtime.  
  
## <a name="output"></a>Saída  

 Uma mensagem que descreve o problema.  
  
## <a name="configuration"></a>Configuração  
  
```xml  
<mdaConfig>  
  <assistants>  
    <notMarshalable/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Veja também

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Diagnosticando erros com assistentes de depuração gerenciados](diagnosing-errors-with-managed-debugging-assistants.md)
- [Realizando marshaling de interoperabilidade](../interop/interop-marshaling.md)
