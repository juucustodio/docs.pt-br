---
description: 'Saiba mais sobre: como chamar um serviço Web de forma assíncrona (Visual Basic)'
title: 'Como: Chamar um serviço Web de forma assíncrona'
ms.date: 07/20/2015
helpviewer_keywords:
- asynchronous calls [Visual Basic]
- Web services [Visual Basic], accessing
ms.assetid: ff8046f4-f1f2-4d8b-90b7-95e3f7415418
ms.openlocfilehash: a702177f60ac598f624676072116bd3ce78da0bb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99775247"
---
# <a name="how-to-call-a-web-service-asynchronously-visual-basic"></a>Como chamar um serviço Web de forma assíncrona (Visual Basic)

Este exemplo conecta um manipulador a um evento de manipulador assíncrono do serviço Web, para que ele possa recuperar o resultado de uma chamada de método assíncrono. Este exemplo usou o serviço Web DemoTemperatureService em `http://www.xmethods.net`.

Quando você faz referência a um serviço Web em seu projeto no IDE (Ambiente de Desenvolvimento Integrado) do Visual Studio, ele é adicionado ao objeto `My.WebServices`, e o IDE gera uma classe proxy do cliente para acesso a um serviço Web especificado

A classe proxy permite chamar os métodos de serviço Web de forma síncrona, em que seu aplicativo aguarda até que a função seja concluída. Além disso, o proxy cria membros adicionais para ajudar a chamar o método de forma assíncrona. Para cada função de serviço Web, *NameOfWebServiceFunction*, o proxy cria uma sub-rotina *NameOfWebServiceFunction*`Async`, um evento *NameOfWebServiceFunction*`Completed` e uma classe *NameOfWebServiceFunction*`CompletedEventArgs`. Este exemplo demonstra como usar os membros assíncronos para acessar a função `getTemp` do serviço Web DemoTemperatureService.

> [!NOTE]
> Esse código não funciona em aplicativos Web, pois o ASP.NET não oferece suporte ao objeto `My.WebServices`.

## <a name="call-a-web-service-asynchronously"></a>Chamar um serviço Web de forma assíncrona

1. Consulte o serviço Web DemoTemperatureService em `http://www.xmethods.net`. O endereço é

    ```http
    http://www.xmethods.net/sd/2001/DemoTemperatureService.wsdl
    ```

2. Adicione um manipulador de eventos ao evento `getTempCompleted`:

    ```vb
    Private Sub getTempCompletedHandler(ByVal sender As Object,
        ByVal e As net.xmethods.www.getTempCompletedEventArgs)

        MsgBox("Temperature: " & e.Result)
    End Sub
    ```

    > [!NOTE]
    > Você não pode usar a instrução `Handles` para associar um manipulador de eventos aos eventos do objeto `My.WebServices`.

3. Adicione um campo para acompanhar se o manipulador de eventos tiver sido adicionado ao evento `getTempCompleted`:

    ```vb
    Private handlerAttached As Boolean = False
    ```

4. Adicione um método para adicionar ao manipulador de eventos ao evento `getTempCompleted`, se necessário, e para chamar o método `getTempAsync`:

    ```vb
    Sub CallGetTempAsync(ByVal zipCode As Integer)
        If Not handlerAttached Then
            AddHandler My.WebServices.
                TemperatureService.getTempCompleted,
                AddressOf Me.TS_getTempCompleted
            handlerAttached = True
        End If
        My.WebServices.TemperatureService.getTempAsync(zipCode)
    End Sub
    ```

    Para chamar o método Web `getTemp` de forma assíncrona, chame o método `CallGetTempAsync`. Quando o método Web for concluído, seu valor retornado será transmitido ao manipulador de eventos `getTempCompletedHandler`.

## <a name="see-also"></a>Consulte também

- [Como acessar serviços Web de aplicativo](accessing-application-web-services.md)
- [Objeto My.WebServices](../../language-reference/objects/my-webservices-object.md)
