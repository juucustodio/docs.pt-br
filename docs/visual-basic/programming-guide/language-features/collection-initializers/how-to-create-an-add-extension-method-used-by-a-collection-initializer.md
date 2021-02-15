---
description: 'Saiba mais sobre: como criar um método de extensão de adição usado por um inicializador de coleção (Visual Basic)'
title: Como criar um método para adicionar extensão usado por um inicializador de coleção
ms.date: 07/20/2015
helpviewer_keywords:
- collection initializers [Visual Basic]
ms.assetid: f64b52c7-8b11-4410-93a6-cb3aeebcc772
ms.openlocfilehash: 1fbe6f438c4761ae668a6bd6a0a2c38c8efdb439
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100475468"
---
# <a name="how-to-create-an-add-extension-method-used-by-a-collection-initializer-visual-basic"></a>Como criar um método para adicionar extensão usado por um inicializador de coleção (Visual Basic)

Quando você usa um inicializador de coleção para criar uma coleção, o compilador Visual Basic procura um `Add` método do tipo de coleção para o qual os parâmetros do `Add` método correspondem aos tipos de valores no inicializador de coleção. Esse `Add` método é usado para popular a coleção com os valores do inicializador de coleção.  
  
 Se não houver nenhum `Add` método correspondente e você não puder modificar o código da coleção, você poderá adicionar um método de extensão chamado `Add` que usa os parâmetros exigidos pelo inicializador de coleção. Normalmente, isso é o que você precisa fazer quando usa inicializadores de coleção para coleções genéricas.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como adicionar um método de extensão ao tipo genérico para <xref:System.Collections.Generic.List%601> que um inicializador de coleção possa ser usado para adicionar objetos do tipo `Employee` . O método de extensão permite que você use a sintaxe de inicializador de coleção abreviada.  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo1#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo1/VB/Module1.vb#1)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo1#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo1/VB/Module1.vb#2)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo1#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo1/VB/Module1.vb#3)]  
  
## <a name="see-also"></a>Consulte também

- [Inicializadores de coleção](index.md)
- [Como criar uma coleção usada por um inicializador de coleção](how-to-create-a-collection-used-by-a-collection-initializer.md)
