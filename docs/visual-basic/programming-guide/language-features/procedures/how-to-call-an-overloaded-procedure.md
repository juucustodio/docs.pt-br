---
description: 'Saiba mais sobre: como: chamar um procedimento sobrecarregado (Visual Basic)'
title: Como chamar um procedimento sobrecarregado
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- procedures [Visual Basic], overloading
- procedures [Visual Basic], calling
- procedures [Visual Basic], multiple versions
- procedure calls [Visual Basic], overloaded
ms.assetid: 3bb331fb-f6bc-406f-9ca0-9609b497014c
ms.openlocfilehash: 6a67a598bd4a42964fd8fc01bc22b1b919f5e2a9
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100472586"
---
# <a name="how-to-call-an-overloaded-procedure-visual-basic"></a>Como chamar um procedimento sobrecarregado (Visual Basic)

A vantagem de sobrecarregar um procedimento é a flexibilidade da chamada. O código de chamada pode obter as informações necessárias para passar para o procedimento e, em seguida, chamar um único nome de procedimento, independentemente de quais argumentos ele está passando.  
  
### <a name="to-call-a-procedure-that-has-more-than-one-version-defined"></a>Para chamar um procedimento que tem mais de uma versão definida  
  
1. No código de chamada, determine quais dados passar para o procedimento.  
  
2. Escreva a chamada de procedimento da maneira normal, apresentando os dados na lista de argumentos. Certifique-se de que os argumentos correspondam à lista de parâmetros em uma das versões definidas para o procedimento.  
  
3. Você não precisa determinar qual versão do procedimento chamar. Visual Basic passa o controle para a versão correspondente à sua lista de argumentos.  
  
     O exemplo a seguir chama o `post` procedimento declarado em [como: definir várias versões de um procedimento](./how-to-define-multiple-versions-of-a-procedure.md). Ele obtém a identificação do cliente, determina se ele é um `String` ou um `Integer` e, em qualquer caso, chama o mesmo procedimento.  
  
     [!code-vb[VbVbcnProcedures#56](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#56)]  
  
     [!code-vb[VbVbcnProcedures#57](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#57)]  
  
## <a name="see-also"></a>Consulte também

- [Procedimentos](./index.md)
- [Parâmetros e Argumentos de Procedimento](./procedure-parameters-and-arguments.md)
- [Sobrecarga de procedimento](./procedure-overloading.md)
- [Solucionando problemas de procedimentos](./troubleshooting-procedures.md)
- [Como definir várias versões de um procedimento](./how-to-define-multiple-versions-of-a-procedure.md)
- [Como sobrecarregar um procedimento que usa parâmetros opcionais](./how-to-overload-a-procedure-that-takes-optional-parameters.md)
- [Como sobrecarregar um procedimento que usa um número indefinido de parâmetros](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)
- [Considerações sobre procedimentos de sobrecarga](./considerations-in-overloading-procedures.md)
- [Resolução de sobrecarga](./overload-resolution.md)
- [Sobrecargas](../../../language-reference/modifiers/overloads.md)
