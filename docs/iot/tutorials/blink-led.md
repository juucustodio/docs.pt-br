---
title: Fazer um LED piscar
description: Saiba como piscar um LED com as bibliotecas IoT do .NET.
author: camsoper
ms.author: casoper
ms.date: 11/13/2020
ms.topic: tutorial
ms.prod: dotnet
ms.openlocfilehash: 07a050c0655f9cae3d7f2b924c0dd07ac1c6c0b9
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96585646"
---
# <a name="blink-an-led"></a>Fazer um LED piscar

Os Pins de e/s de uso geral (GPIO) podem ser controlados individualmente. Isso é útil para controlar LEDs, retransmissões e outros dispositivos com estado. Neste tópico, você usará o .NET e seus PINs de GPIO do Raspberry Pi para ligar um LED e piscar repetidamente.

## <a name="prerequisites"></a>Pré-requisitos

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- LED de 5 mm
- 330 resresistência Ω
- Placa universal
- Cabos de jumper
- Painel de debates do Raspberry Pi GPIO (opcional/recomendado)
- [!INCLUDE [tutorial-prereq-dotnet](../includes/tutorial-prereq-dotnet.md)]

[!INCLUDE [ensure-ssh](../includes/ensure-ssh.md)]

## <a name="prepare-the-hardware"></a>Preparar o hardware

Use os componentes de hardware para criar o circuito, conforme ilustrado no diagrama a seguir:

:::image type="content" source="../media/rpi-led_bb-thumb.png" alt-text="Um diagrama Fritzing mostrando um circuito com um LED e um resistor" lightbox="../media/rpi-led_bb.png":::

A imagem acima ilustra as seguintes conexões:

- GPIO 18 para LEDs nó (mais longo, líder positivo)
- Catodo de LED (Lead de menor, negativo) a 330 Ω de resresistência (qualquer fim)
- 330 resresistência Ω (outra extremidade) ao solo

[!INCLUDE [tutorial-rpi-gpio](../includes/tutorial-rpi-gpio.md)]

[!INCLUDE [gpio-breakout](../includes/gpio-breakout.md)]

## <a name="create-the-app"></a>Crie o aplicativo

Conclua as seguintes etapas em seu ambiente de desenvolvimento preferido:

1. Crie um novo aplicativo de console .NET usando a [CLI do .net](../../core/tools/dotnet-new.md) ou o [Visual Studio](../../core/tutorials/with-visual-studio.md). Nomeie-o como *BlinkTutorial*.

    ```dotnetcli
    dotnet new console -o BlinkTutorial
    ```

1. [!INCLUDE [tutorial-add-packages](../includes/tutorial-add-packages.md)]
1. Substitua o conteúdo do *Program.cs* pelo seguinte código:

    :::code language="csharp" source="~/iot-samples/tutorials/BlinkTutorial/Program.cs" :::

    No código anterior:

    - Uma [declaração using](../../csharp/whats-new/csharp-8.md#using-declarations) cria uma instância do `GpioController` . A `using` declaração garante que o objeto seja descartado e que os recursos de hardware sejam liberados corretamente.
    - O GPIO pino 18 está aberto para saída
    - Um `while` loop é executado indefinidamente. Cada iteração:
        1. Grava um valor no GPIO pino 18. Se `ledOn` for true, ele gravará `PinValue.High` (ativado). Caso contrário, ele grava `PinValue.Low` .
        1. Dorme 1000 MS.
        1. Alterna o valor de `ledOn` .

1. [!INCLUDE [tutorial-build](../includes/tutorial-build.md)]
1. [!INCLUDE [tutorial-deploy](../includes/tutorial-deploy.md)]
1. Execute o aplicativo no Raspberry Pi alternando para o diretório de implantação e executando o executável.

    ```bash
    ./BlinkTutorial
    ```

    O LED pisca e a cada segundo.

1. Encerre o programa pressionando <kbd>Ctrl + C</kbd>.

Parabéns! Você usou o GPIO para piscar um LED.

## <a name="get-the-source-code"></a>Obter o código-fonte

A fonte deste tutorial está [disponível no GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/BlinkTutorial) <span class="docon docon-navigate-external x-hidden-focus"></span> .

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Saiba como ler condições ambientais de um sensor](../tutorials/temp-sensor.md)
