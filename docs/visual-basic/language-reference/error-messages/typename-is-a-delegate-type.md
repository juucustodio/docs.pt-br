---
description: "Saiba mais sobre: BC32008: ' <typename> ' é um tipo delegado"
title: "'<typename>' é um tipo delegado"
ms.date: 07/20/2015
f1_keywords:
- bc32008
- vbc32008
helpviewer_keywords:
- BC32008
ms.assetid: dc6abba0-a9ad-450f-8899-87265bc84abc
ms.openlocfilehash: 72aac48038c433b7938c54e7f1138a5b91bf7689
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99675020"
---
# <a name="bc32008-typename-is-a-delegate-type"></a>BC32008: ' \<typename> ' é um tipo delegado

' \<typename> ' é um tipo delegado. A construção delegate permite apenas uma única expressão AddressOf como uma lista de argumentos. Geralmente, uma expressão AddressOf pode ser usada em vez de uma construção delegate.

 Uma `New` cláusula que cria uma instância de uma classe delegate fornece uma lista de argumentos inválida para o construtor delegate.

 Você pode fornecer apenas uma única `AddressOf` expressão ao criar uma nova instância de delegado.

 Esse erro pode ocorrer se você não passar nenhum argumento para o construtor delegado, se você passar mais de um argumento, ou se você passar um único argumento que não seja uma expressão válida `AddressOf` .

 **ID do erro:** BC32008

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Use uma única `AddressOf` expressão na lista de argumentos para a classe delegate na `New` cláusula.

## <a name="see-also"></a>Consulte também

- [Novo Operador](../operators/new-operator.md)
- [Operador AddressOf](../operators/addressof-operator.md)
- [Representantes](../../programming-guide/language-features/delegates/index.md)
- [Como invocar um método delegado](../../programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)
