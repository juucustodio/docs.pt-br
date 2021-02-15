---
description: 'Saiba mais sobre: como: colocar um valor em uma propriedade (Visual Basic)'
title: Como inserir um valor em uma propriedade
ms.date: 07/20/2015
helpviewer_keywords:
- property values [Visual Basic]
- Visual Basic code, procedures
- values [Visual Basic], properties
- Visual Basic code, properties
- properties [Visual Basic], values
ms.assetid: c39401e5-b5fc-4439-8f31-ed640f7ce6ed
ms.openlocfilehash: 62f5552f821fb98bd3a4695505aba5ff73b08fc7
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100476196"
---
# <a name="how-to-put-a-value-in-a-property-visual-basic"></a>Como inserir um valor em uma propriedade (Visual Basic)

Você armazena um valor em uma propriedade colocando o nome da propriedade no lado esquerdo de uma instrução de atribuição.  
  
 O procedimento da propriedade `Set` armazena um valor, mas você não o chama explicitamente por nome. Você usa a propriedade da mesma forma como usaria uma variável. Visual Basic faz as chamadas para os procedimentos da propriedade.  
  
### <a name="to-store-a-value-in-a-property"></a>Para armazenar um valor em uma propriedade  
  
1. Use o nome da propriedade no lado esquerdo de uma instrução de atribuição.  
  
     O exemplo a seguir define o valor da `TimeOfDay` propriedade Visual Basic como meio-dia, chamando implicitamente seu `Set` procedimento.  
  
     [!code-vb[VbVbcnProcedures#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#11)]  
  
2. Se a propriedade usar argumentos, siga o nome da propriedade com parênteses para colocar a lista de argumentos. Se não houver argumentos, você pode opcionalmente omitir os parênteses.  
  
3. Coloque os argumentos na lista de argumentos dentro dos parênteses, separados por vírgulas. Certifique-se de fornecer os argumentos na mesma ordem em que a propriedade define os parâmetros correspondentes.  
  
4. O valor gerado no lado direito da instrução de atribuição é armazenado na propriedade.  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A>
- [Procedimentos de propriedade](./property-procedures.md)
- [Parâmetros e Argumentos de Procedimento](./procedure-parameters-and-arguments.md)
- [Instrução Property](../../../language-reference/statements/property-statement.md)
- [Diferenças entre propriedades e variáveis no Visual Basic](./differences-between-properties-and-variables.md)
- [Como criar uma propriedade](./how-to-create-a-property.md)
- [Como declarar uma propriedade com níveis de acesso mistos](./how-to-declare-a-property-with-mixed-access-levels.md)
- [Como chamar um procedimento de propriedade](./how-to-call-a-property-procedure.md)
- [Como declarar e chamar uma propriedade padrão no Visual Basic](./how-to-declare-and-call-a-default-property.md)
- [Como obter um valor a partir de uma propriedade](./how-to-get-a-value-from-a-property.md)
