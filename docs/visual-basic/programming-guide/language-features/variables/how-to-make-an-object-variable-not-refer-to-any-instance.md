---
description: 'Saiba mais sobre: como fazer uma variável de objeto não se referir a nenhuma instância (Visual Basic)'
title: Como fazer uma variável de objeto não se referir a nenhuma instância
ms.date: 07/20/2015
helpviewer_keywords:
- Nothing keyword [Visual Basic], variable assignment
- object variables [Visual Basic], null reference
ms.assetid: e6d30578-bdae-4142-a3ac-a10697bf696a
ms.openlocfilehash: 2897720b52e708847fdd139be512e578a7420241
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100481864"
---
# <a name="how-to-make-an-object-variable-not-refer-to-any-instance-visual-basic"></a>Como fazer uma variável de objeto não se referir a nenhuma instância (Visual Basic)

Você pode desassociar uma variável de objeto de qualquer instância de objeto, definindo-a como [Nothing](../../../language-reference/nothing.md).  
  
### <a name="to-disassociate-an-object-variable-from-any-object-instance"></a>Para desassociar uma variável de objeto de qualquer instância de objeto  
  
- Defina a variável como `Nothing` em uma instrução de atribuição.  
  
    ```vb  
    ' Assume account is a defined class  
    Dim currentAccount As account  
    currentAccount = Nothing  
    ```  
  
## <a name="robust-programming"></a>Programação robusta  

 Se o seu código tentar acessar um membro de uma variável de objeto que foi definida como `Nothing` , <xref:System.NullReferenceException> ocorrerá um. Se você definir uma variável de objeto com `Nothing` frequência ou se for possível que a variável não seja inicializada, é uma boa ideia colocar os acessos de membros em um `Try...Catch...Finally` bloco.  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  

 Se você usar uma variável de objeto para objetos que contêm dados confidenciais ou confidenciais, poderá definir a variável como `Nothing` quando não estiver lidando ativamente com um desses objetos. Isso reduz a chance de código mal-intencionado obter acesso aos dados.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.NullReferenceException>
- [Variáveis de Objeto](object-variables.md)
- [Atribuição de variável do objeto](object-variable-assignment.md)
- [Nothing](../../../language-reference/nothing.md)
- [Instrução Try...Catch...Finally](../../../language-reference/statements/try-catch-finally-statement.md)
