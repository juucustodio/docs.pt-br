---
title: Como definir constantes em C#
description: Saiba como definir constantes em C#, que são campos cujos valores são definidos no momento da compilação. Use constantes para fornecer nomes significativos para valores especiais.
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, constants
- constants [C#]
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 43f511be-346c-4b8a-995e-aded94542ece
ms.openlocfilehash: 972deaa4616c15c00e83e26891c4473eae7bfcf8
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513049"
---
# <a name="how-to-define-constants-in-c"></a>Como definir constantes em C\#

As constantes são campos cujos valores são definidos em tempo de compilação e nunca podem ser alterados. Use constantes para fornecer nomes significativos em vez de literais numéricos ("números mágicos") a valores especiais.  
  
> [!NOTE]
> No C#, a diretiva de pré-processador [#define](../../language-reference/preprocessor-directives/preprocessor-define.md) não pode ser utilizada para definir constantes da mesma maneira que é normalmente usada no C e no C++.  
  
 Para definir valores de constantes de tipos integrais (`int`, `byte` e assim por diante), use um tipo enumerado. Para obter mais informações, consulte [enum](../../language-reference/builtin-types/enum.md).  
  
 Para definir constantes não integrais, uma abordagem é agrupá-las em uma única classe estática de nome `Constants`. Isso exigirá que todas as referências às constantes sejam precedidas com o nome de classe, conforme mostrado no exemplo a seguir.  
  
## <a name="example"></a>Exemplo  

 [!code-csharp[csProgGuideObjects#89](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#89)]  
  
 O uso do qualificador de nome de classe ajuda a garantir que você e outras pessoas que usam a constante entendam que ele é constante e não pode ser modificado.  
  
## <a name="see-also"></a>Consulte também

- [Classes e structs](./index.md)
