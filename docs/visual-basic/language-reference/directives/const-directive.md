---
description: 'Saiba mais sobre a diretiva: #Const'
title: '#Diretiva Const'
ms.date: 07/20/2015
f1_keywords:
- vb.#Const
- '#vb.Const'
- '#Const'
helpviewer_keywords:
- '#Const directive'
- conditional compilation [Visual Basic], directives
- Const directive (#Const)
- Visual Basic compiler, compiler directives
- constants [Visual Basic], Const directive
- constants [Visual Basic], declaring
- Const statement [Visual Basic], directive (#Const)
- 'declaring constants [Visual Basic], #const directive'
ms.assetid: 707669e5-23f9-4f17-8622-a0d534429386
ms.openlocfilehash: 9597666ee1320f5dfda226040f93a84eb60a3deb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99797270"
---
# <a name="const-directive"></a>Diretiva #Const

Define constantes de compilador condicional para Visual Basic.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
#Const constname = expression  
```  
  
## <a name="parts"></a>Partes  

 `constname`  
 Obrigatório. Nome da constante que está sendo definida.  
  
 `expression`  
 Obrigatório. Literal, outra constante de compilador condicional ou qualquer combinação que inclua qualquer ou todos os operadores aritméticos ou lógicos, exceto `Is` .  
  
## <a name="remarks"></a>Comentários  

 Constantes de compilador condicional são sempre particulares para o arquivo no qual aparecem. Você não pode criar constantes de compilador público usando a `#Const` diretiva; você pode criá-las somente na interface do usuário ou com a `/define` opção do compilador.  
  
 Você pode usar apenas constantes de compilador condicionais e literais no `expression` . Usar uma constante padrão definida com `Const` causa um erro. Por outro lado, você pode usar constantes definidas com a `#Const` palavra-chave somente para compilação condicional. As constantes também podem ser indefinidas; nesse caso, elas têm um valor de `Nothing` .  
  
## <a name="example"></a>Exemplo  

 Este exemplo usa a `#Const` diretiva.  
  
 [!code-vb[VbVbalrConditionalComp#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#3)]  
  
## <a name="see-also"></a>Consulte também

- [-definir (Visual Basic)](../../reference/command-line-compiler/define.md)
- [#If... Diretivas then... #Else](if-then-else-directives.md)
- [Instrução Const](../statements/const-statement.md)
- [Compilação condicional](../../programming-guide/program-structure/conditional-compilation.md)
- [Instrução If...Then...Else](../statements/if-then-else-statement.md)
