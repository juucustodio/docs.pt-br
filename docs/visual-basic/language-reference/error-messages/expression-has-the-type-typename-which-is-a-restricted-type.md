---
description: "Saiba mais sobre: BC31393: a expressão tem o tipo ' <typename> ', que é um tipo restrito e não pode ser usado para acessar membros herdados de ' Object ' ou ' ValueType"
title: A expressão tem o tipo '<typename>', que é um tipo restrito e não pode ser usado para acessar membros herdados de 'Object' ou 'ValueType'
ms.date: 07/20/2015
f1_keywords:
- bc31393
- vbc31393
helpviewer_keywords:
- BC31393
ms.assetid: 2963cf3f-c527-4aa7-b67c-ee80b6d23186
ms.openlocfilehash: 3b5f9bbb85d1645936286ea0e907e3e25764f69a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796373"
---
# <a name="bc31393-expression-has-the-type-typename-which-is-a-restricted-type-and-cannot-be-used-to-access-members-inherited-from-object-or-valuetype"></a>BC31393: a expressão tem o tipo ' \<typename> ', que é um tipo restrito e não pode ser usado para acessar membros herdados de ' Object ' ou ' ValueType '

Uma expressão é avaliada como um tipo que não pode ser encaixado pelo Common Language Runtime (CLR), mas acessa um membro que requer boxing.

 *Boxing* refere-se ao processamento necessário para converter um tipo para `Object` ou, ocasionalmente, para <xref:System.ValueType> . O Common Language Runtime não pode digitar determinados tipos de estrutura, por exemplo <xref:System.ArgIterator> , <xref:System.RuntimeArgumentHandle> e <xref:System.TypedReference> .

 Essa expressão tenta usar o tipo restrito para chamar um método herdado de <xref:System.Object> ou <xref:System.ValueType> , como <xref:System.Object.GetHashCode%2A> ou <xref:System.Object.ToString%2A> . Para acessar esse método, Visual Basic tentou uma conversão implícita de Boxing que causa esse erro.

 **ID do erro:** BC31393

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Localize a expressão que é avaliada como o tipo citado.

2. Localize a parte da sua instrução que tenta chamar o método herdado de <xref:System.Object> ou <xref:System.ValueType> .

3. Reescreva a instrução para evitar a chamada de método.

## <a name="see-also"></a>Consulte também

- [Conversões implícitas e explícitas](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
