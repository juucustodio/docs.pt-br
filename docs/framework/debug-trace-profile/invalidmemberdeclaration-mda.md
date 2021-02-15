---
title: MDA invalidMemberDeclaration
description: Examine o assistente de depuração gerenciada do invalidMemberDeclaration, que será invocado se um HRESULT de falha for retornado para COM sem chamar o método gerenciado.
ms.date: 03/30/2017
helpviewer_keywords:
- invalid member declaration
- InvalidMemberDeclaration MDA
- marshaling, run-time errors
- managed debugging assistants (MDAs), marshaling
- MDAs (managed debugging assistants), marshaling
ms.assetid: a84dd9a3-d6cf-4824-989a-ecbbf443eeb4
ms.openlocfilehash: c8d6c69fc6eb4f5f690b02809fdc492da675c3b1
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96272547"
---
# <a name="invalidmemberdeclaration-mda"></a>MDA invalidMemberDeclaration

O MDA (Assistente de Depuração Gerenciado) de `invalidMemberDeclaration` é ativado para relatar um erro que ocorre ao determinar como realizar marshaling dos parâmetros de um membro a ser chamado do COM.  
  
## <a name="symptoms"></a>Sintomas  

 Uma falha de HRESULT é retornada ao COM sem o método gerenciado ter sido chamado.  
  
## <a name="cause"></a>Causa  

 Isso ocorre provavelmente devido a um atributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> incompatível em um dos parâmetros.  
  
## <a name="resolution"></a>Resolução  

 Especifique atributos <xref:System.Runtime.InteropServices.MarshalAsAttribute> válidos nos parâmetros.  
  
## <a name="effect-on-the-runtime"></a>Efeito sobre o runtime  

 Esse MDA não tem efeito sobre o CLR.  
  
## <a name="output"></a>Saída  

 Uma mensagem informativa contendo o nome do membro, o nome do tipo e a mensagem de erro.  
  
## <a name="configuration"></a>Configuração  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidMemberDeclaration/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Veja também

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Diagnosticando erros com assistentes de depuração gerenciados](diagnosing-errors-with-managed-debugging-assistants.md)
- [Realizando marshaling de interoperabilidade](../interop/interop-marshaling.md)
