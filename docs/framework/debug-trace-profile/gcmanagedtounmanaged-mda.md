---
title: MDA gcManagedToUnmanaged
description: Examine o assistente de depuração gerenciada do gcManagedToUnmanaged. Este MDA pode ser ativado por causa de uma coleta de lixo prematura durante a transição para código não gerenciado.
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), garbage collection
- GcManagedToUnmanaged MDA
- GC managed to unmanaged
- transitioning threads managed to unmanaged code
- threading [.NET Framework], garbage collection
- managed to unmanaged garbage collection
- managed debugging assistants (MDAs), garbage collection
- threading [.NET Framework], managed debugging assistants
- garbage collection, run-time errors
ms.assetid: 7417f837-805e-4fed-a430-ca919c8421dc
ms.openlocfilehash: 668b06109e59f1239cd2b3e3017aeee1916ce69e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96244230"
---
# <a name="gcmanagedtounmanaged-mda"></a>MDA gcManagedToUnmanaged

O MDA (assistente para depuração gerenciada) `gcManagedToUnmanaged` causa uma coleta de lixo sempre que um thread faz a transição de código gerenciado para código não gerenciado.  
  
## <a name="symptoms"></a>Sintomas  

 Um componente de usuário não gerenciado gera uma violação de acesso ao tentar usar um objeto gerenciado que tinha sido exposto a COM. O objeto COM parece ter sido liberado. A violação de acesso é não determinística.  
  
## <a name="cause"></a>Causa  

 Se um componente não gerenciado não estiver fazendo uma contagem de referência de um objeto COM gerenciado corretamente, o runtime poderá coletar um objeto gerenciado exposto ao COM quando o componente não gerenciado ainda contiver uma referência ao objeto. O runtime chama <xref:System.Runtime.InteropServices.Marshal.Release%2A> durante as coletas de lixo e, portanto, se o componente de usuário usar o objeto antes que a coleta de lixo ocorra, ele ainda não terá sido coletado. Essa é a origem do não determinismo.  
  
## <a name="resolution"></a>Resolução  

 A habilitação deste assistente reduz o tempo entre o período em que o objeto é qualificado para a coleta e <xref:System.Runtime.InteropServices.Marshal.Release%2A> é chamado, ajudando a rastrear qual componente não gerenciado tenta acessar o objeto coletado primeiro.  
  
## <a name="effect-on-the-runtime"></a>Efeito sobre o runtime  

 Causa uma coleta de lixo sempre que um thread faz a transição de código gerenciado para código não gerenciado.  
  
## <a name="output"></a>Saída  

 Esse MDA não produz nenhuma saída.  
  
## <a name="configuration"></a>Configuração  
  
```xml  
<mdaConfig>  
  <assistants>  
    <gcManagedToUnmanaged/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Veja também

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Diagnosticando erros com assistentes de depuração gerenciados](diagnosing-errors-with-managed-debugging-assistants.md)
- [Realizando marshaling de interoperabilidade](../interop/interop-marshaling.md)
- [gcUnmanagedToManaged](gcunmanagedtomanaged-mda.md)
