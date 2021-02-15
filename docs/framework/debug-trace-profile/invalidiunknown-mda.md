---
title: MDA invalidIUnknown
description: Examine o MDA (Assistente de depuração gerenciada) invalidIUnknown, que é ativado quando um ponteiro IUnknown inválido é passado para o código gerenciado do código nativo.
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), invalid IUnknown pointer
- InvalidIUnknown MDA
- invalid IUnknown pointers
- IUnknown pointers
- managed debugging assistants (MDAs), invalid IUnknown pointer
ms.assetid: c7924771-a16b-40fe-b337-ce51dcdf6a12
ms.openlocfilehash: 8e7ca6c9c43c4f507d235c879498b2e831c6eba9
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96272534"
---
# <a name="invalidiunknown-mda"></a>MDA invalidIUnknown

O MDA (Assistente de Depuração Gerenciado) de `invalidIUnknown` é ativado quando um ponteiro `IUnknown` inválido é passado do código nativo para o código gerenciado. O `IUnknown` falha em retornar êxito quando consultado para a interface `IUnknown`.  
  
## <a name="symptoms"></a>Sintomas  

 Um erro inesperado ocorre ao fazer marshaling de um ponteiro de interface COM durante o marshaling de argumento.  
  
## <a name="cause"></a>Causa  

 Uma implementação de `QueryInterface` incorreta na interface COM passada para o CLR.  
  
## <a name="resolution"></a>Resolução  

 Corrija a implementação de `QueryInterface`.  
  
## <a name="effect-on-the-runtime"></a>Efeito sobre o runtime  

 Esse MDA não tem efeito sobre o CLR.  
  
## <a name="output"></a>Saída  

 A descrição do erro.  
  
## <a name="configuration"></a>Configuração  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidIUnknown />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Veja também

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Diagnosticando erros com assistentes de depuração gerenciados](diagnosing-errors-with-managed-debugging-assistants.md)
- [Realizando marshaling de interoperabilidade](../interop/interop-marshaling.md)
