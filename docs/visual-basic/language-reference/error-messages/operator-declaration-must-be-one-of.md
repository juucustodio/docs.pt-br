---
description: 'Saiba mais sobre: a declaração de operador BC33000: deve ser um destes: +,-, *,,/, ^, &amp; , like, mod, and ou, Xor, not,  <<,  >>...'
title: 'A declaração do operador deve ser uma das: +,-, *,-,-, ^, &amp; , like, mod, and ou, Xor, not,  <<,  >>, =,  <>, <, <=, >, re>=, CType, IsTrue, IsFalse'
ms.date: 07/20/2015
f1_keywords:
- bc33000
- vbc33000
helpviewer_keywords:
- BC33000
ms.assetid: 15c5d8eb-3a8c-4141-8f41-33151afabf97
ms.openlocfilehash: 0ad82a6414387278622a10624952ebc35e7e9b83
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795554"
---
# <a name="bc33000-operator-declaration-must-be-one-of----amp-like-mod-and-or-xor-not--"></a>BC33000: a declaração do operador deve ser um destes: +,-, *, \, /, ^, &amp; , like, mod, and ou, Xor, not, \<\<, >>...

Você pode declarar apenas um operador que seja elegível para sobrecarga. A tabela a seguir lista os operadores que você pode declarar.

|Tipo|Operadores|
|----------|---------------|
|Unário|`+`, `-`, `IsFalse`, `IsTrue`, `Not`|
|Binário|`+`, `-`, `*`, `/`, `\`, `&`, `^`, `>>`, `<<`, `=`, `<>`, `>`, `>=`, `<`, `<=`, `And`, `Like`, `Mod`, `Or`, `Xor`|
|Conversão (unário)|`CType`|

 Observe que o operador `=` na lista binária é o operador de comparação, não o operador de atribuição.

 **ID do erro:** BC33000

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Selecione um operador do conjunto de operadores sobrecarregados.

- Se você precisar da funcionalidade de sobrecarregar um operador que você não pode sobrecarregar diretamente, crie um `Function` procedimento que aceite os parâmetros apropriados e retorne o valor apropriado.

## <a name="see-also"></a>Consulte também

- [Instrução Operator](../statements/operator-statement.md)
- [Procedimentos do operador](../../programming-guide/language-features/procedures/operator-procedures.md)
- [Como definir um operador](../../programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [Como definir um operador de conversão](../../programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
- [Instrução Function](../statements/function-statement.md)
