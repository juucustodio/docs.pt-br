---
title: MDA pInvokeLog
description: Entenda o MDA (Assistente de depuração gerenciada) pInvokeLog, que é ativado para cada assinatura de invocação de plataforma exclusiva usada durante a execução no .NET.
ms.date: 03/30/2017
helpviewer_keywords:
- signatures, platform invoke
- MDAs (managed debugging assistants), platform invoke
- platform invoke, run-time errors
- platform invoke log
- PInvokeLog MDA
- managed debugging assistants (MDAs), platform invoke
ms.assetid: b830444a-5003-49fe-b89b-b8bee22f7b1a
ms.openlocfilehash: b8cb4805663a2b28a133f98503730199af695c4f
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96271454"
---
# <a name="pinvokelog-mda"></a>MDA pInvokeLog

O MDA (Assistente de Depuração Gerenciado) de `pInvokeLog` é ativado para cada assinatura de invocação de plataforma exclusiva usada durante a execução.  
  
## <a name="effect-on-the-runtime"></a>Efeito sobre o runtime  

 Esse MDA não tem efeito sobre o CLR.  
  
## <a name="output"></a>Saída  

 Uma mensagem que indica a assinatura de invocação de plataforma usada durante a execução.  
  
## <a name="configuration"></a>Configuração  

 Cada elemento de correspondência filtra os arquivos .dll para os quais as chamadas de invocação de plataforma são feitas.  
  
```xml  
<mdaConfig>  
  <assistants>  
    <pInvokeLog>  
      <filter>  
        <match dllName="user32.dll"/>  
        <match dllName="kernel32.dll"/>  
      </filter>  
    </pInvokeLog>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Veja também

- [Diagnosticando erros com assistentes de depuração gerenciados](diagnosing-errors-with-managed-debugging-assistants.md)
- [Consumindo funções de DLL não gerenciadas](../interop/consuming-unmanaged-dll-functions.md)
