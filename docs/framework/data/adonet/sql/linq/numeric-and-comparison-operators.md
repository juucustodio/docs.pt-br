---
description: 'Saiba mais sobre: operadores numéricos e de comparação'
title: Numérico e operadores de comparação
ms.date: 03/30/2017
ms.assetid: 25b4a26a-06f2-4f80-87a9-76705ed46197
ms.openlocfilehash: 5b17f19769436ac4e575ac974668eadc3b17b8f6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99695522"
---
# <a name="numeric-and-comparison-operators"></a>Numérico e operadores de comparação

Aritmética e operadores de comparação funciona como esperado em Common Language Runtime (CLR) exceto como segue:

- O SQL não suporta o operador de módulo em números de ponto flutuante.

- O SQL não oferece suporte a aritmética não-verificada.

- Operadores de incremento e de redução causam efeitos colaterais quando você usa os em expressões que não podem ser replicadas no SQL e, portanto, não são suportados.

## <a name="supported-operators"></a>Operadores com suporte

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] oferece suporte aos seguintes operadores.

- Operadores aritméticos básicos:

  - `+`

  - `-` (subtração)

  - `*`

  - `/`

  - Divisão de inteiro Visual Basic ( `\` )

  - `%` (Visual Basic) `Mod`

  - `<<`

  - `>>`

  - `-` (negação unária)

- Operadores de comparação básicos:

  - `=` Visual Basic e C# `==`

  - `<>` Visual Basic e C# `!=`

  - Visual Basic `Is/IsNot`

  - `<`

  - `<=`

  - `>`

  - `>=`

## <a name="see-also"></a>Consulte também

- [Tipos de dados e funções](data-types-and-functions.md)
- [Operadores do C#](../../../../../csharp/language-reference/operators/index.md)
- [Operadores](../../../../../visual-basic/language-reference/operators/index.md)
