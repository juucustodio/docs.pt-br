---
description: 'Saiba mais sobre: mensagens de erro no Visual Basic'
title: Visual Basic mensagens de erro
titleSuffix: ''
ms.date: 10/13/2020
helpviewer_keywords:
- errors [Visual Basic]
- error messages
ms.assetid: f2dda05b-baef-41f5-8bb1-598bd7cf239f
ms.openlocfilehash: 28e59a47c47ff7905dfec93b057f7cb534842b91
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796061"
---
# <a name="error-messages-in-visual-basic"></a>Mensagens de erro no Visual Basic

Quando você compila ou executa um aplicativo Visual Basic, os seguintes tipos de erros podem ocorrer:

- Erros de tempo de compilação, que ocorrem quando você compila um aplicativo.

- Erros de tempo de execução, que ocorrem quando um aplicativo está em execução.

Para obter informações sobre como solucionar um erro específico, consulte [Recursos adicionais para programadores do Visual Basic](../../getting-started/additional-resources.md).

## <a name="run-time-errors"></a>Erros de tempo de execução

Se um aplicativo Visual Basic tentar executar uma ação que o sistema não pode executar, ocorrerá um erro em tempo de execução e Visual Basic lançará um <xref:System.Exception> objeto. Visual Basic pode gerar erros personalizados de qualquer tipo de dados, incluindo `Exception` objetos, usando a `Throw` instrução. Um aplicativo pode identificar o erro exibindo o número do erro e a mensagem de uma exceção capturada. Se não for detectado um erro, o aplicativo será encerrado.

O código pode interceptar e examine os erros em tempo de execução. Se você colocar o código que produz o erro em um bloco `Try`, você poderá capturar qualquer erro gerado em um bloco `Catch` correspondente. Para obter informações sobre como interceptar erros em tempo de execução e responder a eles em seu código, consulte [Instrução Try... Catch... Finally](../statements/try-catch-finally-statement.md).

## <a name="compile-time-errors"></a>Erros de tempo de compilação

Se o compilador do Visual Basic encontrar um problema no código, ocorrerá um erro em tempo de compilação. No editor de código do Visual Studio, você pode identificar facilmente qual linha de código causou o erro porque uma linha ondulada aparece sob essa linha de código. A mensagem de erro será exibida se você apontar para a linha ondulada ou abrir a **Lista de Erros**, que também mostra outras mensagens.

Se um identificador tiver um sublinhado ondulado e um pequeno sublinhado aparecer sob o caractere mais à direita, você poderá gerar um stub para a classe, o construtor, o método, a propriedade, o campo ou a enumeração. Para obter mais informações, consulte [gerar com base no uso (Visual Studio)](/visualstudio/ide/visual-csharp-intellisense#generate-from-usage).

Ao resolver os avisos do compilador do Visual Basic, você poderá escrever um código que é executado mais rápido e com menos erros. Esses avisos identificam códigos que podem causar erros quando o aplicativo é executado. Por exemplo, o compilador avisará se você tentar invocar um membro de uma variável de objeto não atribuída, retornar de uma função sem definir o valor retornado ou executar um bloco `Try` com erros na lógica para capturar exceções. Para obter mais informações sobre avisos, incluindo como ativar e desativar, consulte [Configurando avisos no Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).
