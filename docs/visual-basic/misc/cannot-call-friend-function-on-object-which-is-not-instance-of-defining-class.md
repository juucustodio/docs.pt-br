---
description: 'Saiba mais sobre: não é possível chamar a função Friend no objeto que não é uma instância da classe de definição'
title: Não é possível chamar a função friend no objeto que não é uma instância da classe de definição
ms.date: 07/20/2015
f1_keywords:
- vbrID97
ms.assetid: b9d821f0-8565-4f15-bb35-184789c69662
ms.openlocfilehash: 612a169cf976881b82cb0bb0c44ac6c6e7f91755
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100478692"
---
# <a name="cannot-call-friend-function-on-object-which-is-not-an-instance-of-defining-class"></a>Não é possível chamar a função friend no objeto que não é uma instância da classe de definição

Você tentou chamar o `Friend` procedimento de uma classe ou tentou acessar uma `Friend` propriedade ou um método entre processos ou entre threads. Um `Friend` procedimento é chamado de um módulo fora da classe, mas faz parte do projeto no qual a classe é definida.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Certifique-se de que você está chamando ou acessando o procedimento a partir de um módulo que faz parte do projeto no qual a classe está definida.  
  
## <a name="see-also"></a>Consulte também

- [Friend](../language-reference/modifiers/friend.md)
