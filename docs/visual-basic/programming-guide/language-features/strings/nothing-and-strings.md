---
description: 'Saiba mais sobre: Nothing e cadeias de caracteres em Visual Basic'
title: Nothing e cadeias de caracteres
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], Nothing
ms.assetid: 261380af-2024-4ecf-823b-43b1034d92cd
ms.openlocfilehash: a32dd8b38033f1845f2ada87bf5f538d45fede18
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100424340"
---
# <a name="nothing-and-strings-in-visual-basic"></a>Nada e cadeias de caracteres no Visual Basic

O tempo de execução Visual Basic e o .NET Framework são avaliados de `Nothing` maneira diferente quando se trata de cadeias de caracteres.  
  
## <a name="visual-basic-runtime-and-the-net-framework"></a>Tempo de execução de Visual Basic e o .NET Framework  

 Considere o seguinte exemplo:  
  
 [!code-vb[VbVbalrStrings#47](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#47)]  
  
 O tempo de execução de Visual Basic geralmente é avaliado `Nothing` como uma cadeia de caracteres vazia (""). O .NET Framework não, no entanto, e gera uma exceção sempre que é feita uma tentativa de executar uma operação de cadeia de caracteres no `Nothing` .  
  
## <a name="see-also"></a>Consulte também

- [Introdução a cadeias de caracteres no Visual Basic](introduction-to-strings.md)
