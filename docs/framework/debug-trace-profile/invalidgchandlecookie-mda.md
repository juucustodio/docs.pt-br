---
title: MDA invalidGCHandleCookie
description: Examine o MDA (Assistente de depuração gerenciada) invalidGCHandleCookie, que é ativado quando uma conversão de um cookie IntPtr inválido para um GCHandle é tentada.
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), invalid cookies
- cookies, invalid
- managed debugging assistants (MDAs), invalid cookies
- InvalidGCHandleCookie MDA
- invalid cookies
ms.assetid: 613ad742-3c11-401d-a6b3-893ceb8de4f8
ms.openlocfilehash: 36806498445da78c8d9dd5c51c1903b253a39da0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96272599"
---
# <a name="invalidgchandlecookie-mda"></a>MDA invalidGCHandleCookie

O MDA (Assistente de Depuração Gerenciado) de `invalidGCHandleCookie` é ativado quando há uma tentativa de conversão de um cookie <xref:System.IntPtr> inválido em um <xref:System.Runtime.InteropServices.GCHandle>.  
  
## <a name="symptoms"></a>Sintomas  

 Um comportamento indefinido, tal como violações de acesso e corrupção de memória, durante a tentativa de usar ou recuperar um <xref:System.Runtime.InteropServices.GCHandle> de um <xref:System.IntPtr>.  
  
## <a name="cause"></a>Causa  

 O cookie é provavelmente inválido porque ele não foi criado originalmente de um <xref:System.Runtime.InteropServices.GCHandle>, representa um <xref:System.Runtime.InteropServices.GCHandle> que já foi liberado, é um cookie para um <xref:System.Runtime.InteropServices.GCHandle> em um domínio do aplicativo diferente ou então realizou-se marshaling dele para código nativo como um <xref:System.Runtime.InteropServices.GCHandle> mas ele foi passado de volta para o CLR como um <xref:System.IntPtr>, ponto em que foi tentada uma conversão.  
  
## <a name="resolution"></a>Resolução  

 Especifique um cookie <xref:System.IntPtr> válido para o <xref:System.Runtime.InteropServices.GCHandle>.  
  
## <a name="effect-on-the-runtime"></a>Efeito sobre o runtime  

 Quando esse MDA está habilitado, o depurador não é capaz de rastrear as raízes de volta para seus objetos porque os valores de cookie passados de volta são diferentes daqueles retornados quando o MDA não está habilitado.  
  
## <a name="output"></a>Saída  

 O valor do cookie <xref:System.IntPtr> inválido é relatado.  
  
## <a name="configuration"></a>Configuração  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidGCHandleCookie />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Veja também

- <xref:System.Runtime.InteropServices.GCHandle.FromIntPtr%2A>
- <xref:System.Runtime.InteropServices.GCHandle>
- [Diagnosticando erros com assistentes de depuração gerenciados](diagnosing-errors-with-managed-debugging-assistants.md)
