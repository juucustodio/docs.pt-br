---
description: 'Saiba mais sobre: cadeia de caracteres de padrão inválida'
title: Cadeia de caracteres de padrão inválida
ms.date: 07/20/2015
ms.assetid: ec1aecdb-5339-4a93-be71-eec56b1d7438
ms.openlocfilehash: 4fbf16dd43ac4ae44e1a99d85caae4a7baf99109
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100462055"
---
# <a name="invalid-pattern-string"></a>Cadeia de caracteres de padrão inválida

A cadeia de caracteres de padrão especificada na `Like` operação de uma pesquisa é inválida.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1. Examine os caracteres válidos para expressões de lista.  
  
2. No intervalo de padrões, verifique se o caractere de intervalo inicial é menor que o caractere de intervalo final, como em `[a-z]` .  
  
3. No intervalo de padrões, verifique se não há vários hifens próximos um do outro, como em `[a--z]` .  
  
4. Intervalos de padrão de término com um colchete de fechamento.  
  
## <a name="see-also"></a>Consulte também

- [Operador Like](../language-reference/operators/like-operator.md)
