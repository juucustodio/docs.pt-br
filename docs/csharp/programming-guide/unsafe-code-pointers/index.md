---
title: Código e ponteiros não seguros – Guia de Programação em C#
description: Saiba mais sobre códigos e ponteiros sem segurança. O C# não dá suporte a ponteiros, mas você pode definir um contexto não seguro no qual os ponteiros podem ser usados com uma palavra-chave ' unsafe '.
ms.date: 07/20/2015
helpviewer_keywords:
- security [C#], type safety
- C# language, unsafe code
- type safety [C#]
- unsafe keyword [C#]
- unsafe code [C#]
- C# language, pointers
- pointers [C#], about pointers
ms.assetid: b0fcca10-a92d-4f2a-835b-b0ccae6739ee
ms.openlocfilehash: 4d624bdc8fc4a756f47d66c9dec6eba8c24a9d9a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99782384"
---
# <a name="unsafe-code-and-pointers-c-programming-guide"></a>Código e ponteiros não seguros (Guia de Programação em C#)

Para manter a segurança de tipos e a segurança, o C# não dá suporte à aritmética de ponteiro por padrão. No entanto, usando a palavra-chave [unsafe](../../language-reference/keywords/unsafe.md), você pode definir um contexto não seguro no qual os ponteiros podem ser usados. Para obter mais informações sobre ponteiros, confira [Tipos de ponteiro](pointer-types.md).  
  
> [!NOTE]
> No CLR (Common Language Runtime), o código não seguro é conhecido como código não verificado. O código não seguro em C# não é necessariamente perigoso. Ele é apenas o código cuja segurança não pode ser verificada pelo CLR. O CLR, portanto, executará somente o código não seguro se ele estiver em um assembly totalmente confiável. Se você usar código não seguro, será sua responsabilidade assegurar que seu código não apresente riscos de segurança ou erros de ponteiro.  
  
## <a name="unsafe-code-overview"></a>Visão Geral de código não seguro

O código não seguro tem as propriedades a seguir:

- Blocos de código, tipos e métodos podem ser definidos como não seguros.

- Em alguns casos, o código não seguro pode aumentar o desempenho de um aplicativo removendo as verificações de limites de matriz.

- O código não seguro é necessário quando você chama funções nativas que exigem ponteiros.

- Usar o código não seguro apresenta riscos de segurança e estabilidade.

- O código que contém blocos não seguros deve ser compilado com a opção do compilador [-unsafe](../../language-reference/compiler-options/unsafe-compiler-option.md).
  
## <a name="related-sections"></a>Seções relacionadas

Para obter mais informações, consulte:

- [Tipos de ponteiro](pointer-types.md)

- [Buffers de tamanho fixo](fixed-size-buffers.md)

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, confira o tópico [Código não seguro](~/_csharplang/spec/unsafe-code.md) na [especificação da linguagem C#](~/_csharplang/spec/introduction.md).
  
## <a name="see-also"></a>Consulte também

- [Guia de programação C#](../index.md)
- [UNSAFE](../../language-reference/keywords/unsafe.md)
