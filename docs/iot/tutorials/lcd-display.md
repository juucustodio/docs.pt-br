---
title: Exibir texto em uma tela LCD
description: Saiba como exibir caracteres em uma tela de cristal líquido com as bibliotecas IoT do .NET.
author: camsoper
ms.author: casoper
ms.date: 11/13/2020
ms.topic: tutorial
ms.prod: dotnet
ms.openlocfilehash: d4c3e373207e23877903491871f4d09e11000c1a
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96585641"
---
<!--markdownlint-disable DOCSMD011 -->
# <a name="display-text-on-an-lcd"></a>Exibir texto em uma tela LCD

As exibições de caractere LCD são úteis para exibir informações sem a necessidade de um monitor externo. As exibições comuns de caracteres de LCD podem ser conectadas diretamente aos pins do GPIO, mas essa abordagem requer o uso de até 10 pinos do GPIO. Para cenários que exigem a conexão a uma combinação de dispositivos, a maior parte do cabeçalho GPIO para uma exibição de caractere geralmente é impraticável.

Muitos fabricantes vendem 20x4 de caracteres de LCD com um expansor de GPIO integrado. A exibição de caractere conecta-se diretamente ao expansor do GPIO, que se conecta ao Raspberry Pi por meio do protocolo serial do circuito de Inter-Integrated (I2C).

Neste tópico, você usará o .NET para exibir texto em uma exibição de caractere de LCD usando um expansor de GPIO I2C.

## <a name="prerequisites"></a>Pré-requisitos

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- [exibição de caractere LCD 20x4 com interface I2C](https://www.bing.com/images/search?q=20x4+lcd+display+with+i2c)<span class="docon docon-navigate-external x-hidden-focus"></span>
- Cabos de jumper
- Placa universal (opcional/recomendado)
- Painel de debates do Raspberry Pi GPIO (opcional/recomendado)
- [!INCLUDE [tutorial-prereq-dotnet](../includes/tutorial-prereq-dotnet.md)]

> [!NOTE]
> Há muitos fabricantes de telas de caracteres de LCD. A maioria dos designs são idênticos e o fabricante não deve fazer nenhuma diferença na funcionalidade. Para referência, este tutorial foi desenvolvido com o [LCD2004 do amfundador](https://www.sunfounder.com/lcd2004-module.html) <span class="docon docon-navigate-external x-hidden-focus"></span> .

[!INCLUDE [prepare-pi-i2c](../includes/prepare-pi-i2c.md)]

## <a name="prepare-the-hardware"></a>Preparar o hardware

Use cabos de jumper para conectar os quatro Pins no expansor do GPIO do I2C ao Raspberry Pi da seguinte maneira:

- GND para terra
- VCC a 5V
- SDA para SDA (GPIO 2)
- SCL para SCL (GPIO 3)

Consulte as seguintes figuras, conforme necessário:

| Interface I2C (parte traseira da exibição) | Raspberry Pi GPIO |
|---------------------------------|-------------------|
| :::image type="content" source="../media/character-display-i2c-thumb.png" alt-text="Uma imagem da parte traseira da exibição de caractere mostrando o expansor de GPIO de I2C." lightbox="../media/character-display-i2c.png"::: | :::image type="content" source="../media/gpio-pinout-diagram-thumb.png" alt-text="Um diagrama que mostra a pinagem do cabeçalho GPIO do Raspberry Pi. Imagem de cortesia Raspberry Pi Foundation." lightbox="../media/gpio-pinout-diagram.png":::<br />[Imagem de cortesia Raspberry Pi Foundation](https://www.raspberrypi.org/documentation/usage/gpio/) <span class="docon docon-navigate-external x-hidden-focus"></span> .
 |

[!INCLUDE [gpio-breakout](../includes/gpio-breakout.md)]

## <a name="create-the-app"></a>Crie o aplicativo

Conclua as seguintes etapas em seu ambiente de desenvolvimento preferido:

1. Crie um novo aplicativo de console .NET usando a [CLI do .net](../../core/tools/dotnet-new.md) ou o [Visual Studio](../../core/tutorials/with-visual-studio.md). Nomeie-o como *LcdTutorial*.

    ```dotnetcli
    dotnet new console -o LcdTutorial
    ```

1. [!INCLUDE [tutorial-add-packages](../includes/tutorial-add-packages.md)]
1. Substitua o conteúdo do *Program.cs* pelo seguinte código:

    :::code language="csharp" source="~/iot-samples/tutorials/LcdTutorial/Program.cs" :::

    No código anterior:

    - Uma [declaração using](../../csharp/whats-new/csharp-8.md#using-declarations) cria uma instância do `I2cDevice` chamando `I2cDevice.Create` e passando um novo `I2cConnectionSettings` com os `busId` `deviceAddress` parâmetros e. Isso `I2cDevice` representa o barramento I2C. A `using` declaração garante que o objeto seja descartado e que os recursos de hardware sejam liberados corretamente.

        > [!WARNING]
        > O endereço do dispositivo para o expansor do GPIO depende do chip usado pelo fabricante. Os expansores GPIO equipados com um PCF8574 usam o endereço `0x27` , enquanto aqueles que usam chips PCF8574A usam `0x3F` . Consulte a documentação do LCD.

    - Outra `using` declaração cria uma instância do `Pcf8574` e passa o `I2cDevice` para o construtor. Essa instância representa o expansor do GPIO.
    - Outra `using` declaração cria uma instância do `Lcd2004` para representar a exibição. Vários parâmetros são passados para o construtor que descreve as configurações a serem usadas para se comunicar com o expansor do GPIO. O expansor do GPIO é passado como o `controller` parâmetro.
    - Um `while` loop é executado indefinidamente. Cada iteração:
        1. Limpa a exibição.
        1. Define a posição do cursor para a primeira posição na linha atual.
        1. Grava a hora atual para a exibição na posição atual do cursor.
        1. Itera o contador de linha atual.
        1. Dorme 1000 MS.

1. [!INCLUDE [tutorial-build](../includes/tutorial-build.md)]
1. [!INCLUDE [tutorial-deploy](../includes/tutorial-deploy.md)]
1. Execute o aplicativo no Raspberry Pi alternando para o diretório de implantação e executando o executável.

    ```bash
    ./LcdTutorial
    ```

    Observe que o caractere LCD é exibido conforme a hora atual é exibida em cada linha.

    > [!TIP]
    > Se a exibição estiver acesa, mas você não vir nenhum texto, tente ajustar o contraste de discagem na parte traseira da tela.

1. Encerre o programa pressionando <kbd>Ctrl + C</kbd>.

Parabéns! Você exibiu o texto em um LCD usando um expansor I2C e um de GPIO!

## <a name="get-the-source-code"></a>Obter o código-fonte

A fonte deste tutorial está [disponível no GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/LcdTutorial) <span class="docon docon-navigate-external x-hidden-focus"></span> .

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Saiba como usar Uso Geral entrada/saída para piscar um LED](../tutorials/blink-led.md)
