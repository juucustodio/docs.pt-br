---
description: 'Saiba mais sobre: como validar cadeias de caracteres que representam datas ou horas (Visual Basic)'
title: Como validar cadeias de caracteres que representam datas ou horas
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], validating
- String data type [Visual Basic], validation
ms.assetid: ae7d4b29-3436-4032-bdbf-4650eb1c8e19
ms.openlocfilehash: 4e9255717d1711d8e9839c218a78b359549d9eef
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100424249"
---
# <a name="how-to-validate-strings-that-represent-dates-or-times-visual-basic"></a>Como validar cadeias de caracteres que representam datas ou horas (Visual Basic)

O exemplo de código a seguir define um `Boolean` valor que indica se uma cadeia de caracteres representa uma data ou hora válida.  
  
## <a name="example"></a>Exemplo  

 [!code-vb[VbVbcnRegEx#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnRegEx/VB/Class1.vb#2)]  
  
## <a name="compile-the-code"></a>Compilar o código  

 Substitua `("01/01/03")` e `"9:30 PM"` pela data e hora que você deseja validar. Você pode substituir a cadeia de caracteres por outra cadeia de caracteres embutida em código, com uma `String` variável ou por um método que retorne uma cadeia de caracteres, como `InputBox` .  
  
## <a name="robust-programming"></a>Programação robusta  

 Use este método para validar a cadeia de caracteres antes de tentar converter o `String` em uma `DateTime` variável. Ao marcar a data ou hora primeiro, você pode evitar a geração de uma exceção em tempo de execução.  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.Information.IsDate%2A>
- <xref:Microsoft.VisualBasic.Interaction.InputBox%2A>
- [Validando cadeias de caracteres no Visual Basic](validating-strings.md)
