---
description: 'Saiba mais sobre: como criar uma coleção usada por um inicializador de coleção (Visual Basic)'
title: Como criar uma coleção usada por um inicializador de coleção
ms.date: 07/20/2015
helpviewer_keywords:
- collection initializers [Visual Basic]
ms.assetid: c858db10-424d-47e0-92cd-e08087cc5ebc
ms.openlocfilehash: 09928cb0fbeb0346fd0e1148ffcd6ddce54279c0
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100460014"
---
# <a name="how-to-create-a-collection-used-by-a-collection-initializer-visual-basic"></a>Como criar uma coleção usada por um inicializador de coleção (Visual Basic)

Quando você usa um inicializador de coleção para criar uma coleção, o compilador Visual Basic procura um `Add` método do tipo de coleção para o qual os parâmetros do `Add` método correspondem aos tipos de valores no inicializador de coleção. Esse `Add` método é usado para popular a coleção com os valores do inicializador de coleção.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra uma `OrderCollection` coleção que contém um `Add` método público que um inicializador de coleção pode usar para adicionar objetos do tipo `Order` . O `Add` método permite que você use a sintaxe de inicializador de coleção abreviada.  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo2#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo2/VB/Module1.vb#4)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo2#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo2/VB/Module1.vb#1)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo2#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo2/VB/Module1.vb#2)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo2#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo2/VB/Module1.vb#3)]  
  
## <a name="see-also"></a>Consulte também

- [Inicializadores de coleção](index.md)
- [Como criar um método para adicionar extensão usado por um inicializador de coleção](how-to-create-an-add-extension-method-used-by-a-collection-initializer.md)
