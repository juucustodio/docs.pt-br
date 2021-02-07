---
description: 'Saiba mais sobre o operador: GetType (Visual Basic)'
title: Operador GetType
ms.date: 07/20/2015
f1_keywords:
- vb.GetType
helpviewer_keywords:
- GetType operator [Visual Basic]
- GetType keyword [Visual Basic]
ms.assetid: 4f733297-2503-4607-850c-15eba65fff90
ms.openlocfilehash: 15fe9c28997aa01527f23c0cc8fdbb0fe6cc53f7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99665985"
---
# <a name="gettype-operator-visual-basic"></a>Operador GetType (Visual Basic)

Retorna um <xref:System.Type> objeto para o tipo especificado. O <xref:System.Type> objeto fornece informações sobre o tipo, como suas propriedades, métodos e eventos.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
GetType(typename)  
```  
  
## <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---|---|  
|`typename`|O nome do tipo para o qual você deseja informações.|  
  
## <a name="remarks"></a>Comentários  

 O `GetType` operador retorna o <xref:System.Type> objeto para o especificado `typename` . Você pode passar o nome de qualquer tipo definido em `typename` . Isso inclui o seguinte:  
  
- Qualquer Visual Basic tipo de dados, como `Boolean` ou `Date` .  
  
- Qualquer .NET Framework classe, estrutura, módulo ou interface, como <xref:System.ArgumentException?displayProperty=nameWithType> ou <xref:System.Double?displayProperty=nameWithType> .  
  
- Qualquer classe, estrutura, módulo ou interface definida pelo seu aplicativo.  
  
- Qualquer matriz definida pelo seu aplicativo.  
  
- Qualquer delegado definido pelo seu aplicativo.  
  
- Qualquer Enumeração definida por Visual Basic, o .NET Framework ou seu aplicativo.  
  
 Se você quiser obter o objeto de tipo de uma variável de objeto, use o <xref:System.Type.GetType%2A?displayProperty=nameWithType> método.  
  
 O `GetType` operador pode ser útil nas seguintes circunstâncias:  
  
- Você deve acessar os metadados para um tipo em tempo de execução. O <xref:System.Type> objeto fornece metadados como membros de tipo e informações de implantação. Você precisa disso, por exemplo, para refletir sobre um assembly. Para obter mais informações, consulte <xref:System.Reflection?displayProperty=nameWithType>.  
  
- Você deseja comparar duas referências de objeto para ver se elas se referem a instâncias do mesmo tipo. Se isso for feito, o `GetType` retornará referências ao mesmo <xref:System.Type> objeto.  
  
## <a name="example"></a>Exemplo  

 Os exemplos a seguir mostram o `GetType` operador em uso.  
  
 [!code-vb[VbVbalrOperators#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#26)]  
  
## <a name="see-also"></a>Consulte também

- [Precedência do operador no Visual Basic](operator-precedence.md)
- [Operadores Listados por Funcionalidade](operators-listed-by-functionality.md)
- [Operadores e expressões](../../programming-guide/language-features/operators-and-expressions/index.md)
