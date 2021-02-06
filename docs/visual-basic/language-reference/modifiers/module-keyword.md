---
description: 'Saiba mais sobre: módulo <keyword> (Visual Basic)'
title: Modulo <keyword>
ms.date: 07/20/2015
f1_keywords:
- vb.ModuleAttribute
helpviewer_keywords:
- Module keyword [Visual Basic]
- Module modifier
- attribute blocks, Module keyword
ms.assetid: d971b940-05ab-4d56-8485-e3b8a661906b
ms.openlocfilehash: 1bd25b00b41f5da4fca535220fe4e1694c81baca
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99640687"
---
# <a name="module-keyword-visual-basic"></a>Módulo \<keyword> (Visual Basic)

Especifica que um atributo no início de um arquivo de origem se aplica ao módulo do assembly atual.  
  
## <a name="remarks"></a>Comentários  

 Muitos atributos pertencem a um elemento de programação individual, como uma classe ou propriedade. Você aplica esse atributo, anexando o bloco de atributo, entre colchetes angulares ( `< >` ), diretamente à instrução de declaração.  
  
 Se um atributo pertencer não apenas ao elemento a seguir, mas ao módulo do assembly atual, você coloca o bloco de atributo no início do arquivo de origem e identifica o atributo com a `Module` palavra-chave. Se ele se aplicar a todo o assembly, você usará a palavra-chave [assembly](assembly.md) .  
  
 O `Module` modificador não é o mesmo que a [instrução do módulo](../statements/module-statement.md).  
  
## <a name="see-also"></a>Consulte também

- [Assembly](assembly.md)
- [Instrução Module](../statements/module-statement.md)
- [Visão geral de atributos](../../programming-guide/concepts/attributes/index.md)
