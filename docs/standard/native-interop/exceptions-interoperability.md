---
description: 'Saiba mais sobre: trabalhando com exceções de interoperabilidade em código não gerenciado'
title: Interoperabilidade de exceções
ms.date: 01/16/2020
helpviewer_keywords:
- unmanaged code, exceptions
- exceptions, unmanaged code
- interop, exceptions
- exceptions, interop
ms.openlocfilehash: 3062aea2632771605c5a3c942c8471309e043f60
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99713189"
---
# <a name="working-with-interop-exceptions-in-unmanaged-code"></a>Trabalhando com exceções de interoperabilidade em código não gerenciado

A interoperabilidade de exceção de código não gerenciado tem suporte apenas em plataformas Windows. Os problemas de portabilidade surgem em plataformas que não são do Windows. Como a ABI do Unix não tem nenhuma definição para tratamento de exceções, o código gerenciado não sabe como os mecanismos de exceção funcionam nos bastidores. Portanto, as exceções podem acabar resultando em comportamentos imprevisíveis e falhas.

## <a name="setjmplongjmp-behaviors"></a>Comportamentos de setjmp/longjmp

`setjmp` `longjmp` Não há suporte para as funções Interop com e C. Não é possível usar o `longjmp` para ignorar os quadros gerenciados.

Para obter mais informações, consulte a [documentação do longjmp](/cpp/c-runtime-library/reference/longjmp).

## <a name="see-also"></a>Consulte também

- [Exceções](index.md)
- [Interoperabilidade com bibliotecas nativas](https://www.mono-project.com/docs/advanced/pinvoke/#runtime-exception-propagation)
