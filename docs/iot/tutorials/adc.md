---
title: Ler valores de um conversor analógico/digital
description: Saiba como ler valores de tensão variável usando um conversor analógico para digital.
author: camsoper
ms.author: casoper
ms.date: 11/13/2020
ms.topic: tutorial
ms.prod: dotnet
ms.openlocfilehash: 7cf25f181997ed66639842727be57e7824ef5466
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739981"
---
<!--markdownlint-disable DOCSMD011 -->
# <a name="read-values-from-an-analog-to-digital-converter"></a>Ler valores de um conversor analógico/digital

Um ADC (conversor analógico para digital) é um dispositivo que pode ler um valor de tensão de entrada analógica e convertê-lo em um valor digital. ADCs são usados para ler valores de thermistors, potentiometers e outros dispositivos que alteram a resistência com base em determinadas condições.

Neste tópico, você usará o .NET para ler valores de um ADC à medida que você modular a voltagem de entrada com um potentiometer.

## <a name="prerequisites"></a>Pré-requisitos

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- [MCP3008](https://www.microchip.com/wwwproducts/MCP3008) <span class="docon docon-navigate-external x-hidden-focus"></span> conversor analógico para digital
- Potentiometer de três pinos
- Placa universal
- Cabos de jumper
- Painel de debates do Raspberry Pi GPIO (opcional/recomendado)
- [!INCLUDE [tutorial-prereq-dotnet](../includes/tutorial-prereq-dotnet.md)]

[!INCLUDE [prepare-pi-spi](../includes/prepare-pi-spi.md)]

## <a name="prepare-the-hardware"></a>Preparar o hardware

Use os componentes de hardware para criar o circuito, conforme ilustrado no diagrama a seguir:

:::image type="content" source="../media/rpi-trimpot_spi-thumb.png" alt-text="Um diagrama Fritzing mostrando um circuito com um MCP3008 ADC e um potentiometer" lightbox="../media/rpi-trimpot_spi.png":::

O MCP3008 usa a SPI (interface de periférico serial) para se comunicar. A seguir estão as conexões do MCP3008 com o Raspberry Pi e potentiometer:

- V<sub>DD</sub> para 3.3 v (mostrado em vermelho)
- V<sub>ref</sub> a 3.3 v (vermelho)
- AGND para terra (preto)
- CLK a SCLK (laranja)
- D de<sub>saída</sub> para miso (laranja)
- D<sub>no</sub> MOSI (laranja)
- CS/SHDN para CE0 (verde)
- DGND para terra (preto)
- CH0 para pino de variável (intermediária) em potentiometer (amarelo)

Forneça 3,3 V e terra para os Pins externos no potentiometer. A ordem não é importante.

Consulte os seguintes diagramas de pinagem conforme necessário:

| MCP3008  | Raspberry Pi GPIO |
|----------|-------------------|
| :::image type="content" source="../media/mcp3008-diagram-thumb.png" alt-text="Um diagrama que mostra a pinagem do MCP3008" lightbox="../media/mcp3008-diagram.png"::: | :::image type="content" source="../media/gpio-pinout-diagram-thumb.png" alt-text="Um diagrama que mostra a pinagem do cabeçalho GPIO do Raspberry Pi. Imagem de cortesia Raspberry Pi Foundation." lightbox="../media/gpio-pinout-diagram.png":::<br />[Imagem de cortesia Raspberry Pi Foundation](https://www.raspberrypi.org/documentation/usage/gpio/).
 |

[!INCLUDE [gpio-breakout](../includes/gpio-breakout.md)]

## <a name="create-the-app"></a>Crie o aplicativo

Conclua as seguintes etapas em seu ambiente de desenvolvimento preferido:

1. Crie um novo aplicativo de console .NET usando a [CLI do .net](../../core/tools/dotnet-new.md) ou o [Visual Studio](../../core/tutorials/with-visual-studio.md). Nomeie-o como *AdcTutorial*.

    ```dotnetcli
    dotnet new console -o AdcTutorial
    ```

1. [!INCLUDE [tutorial-add-packages](../includes/tutorial-add-packages.md)]
1. Substitua o conteúdo do *Program.cs* pelo seguinte código:

    :::code language="csharp" source="~/iot-samples/tutorials/AdcTutorial/Program.cs" :::

    No código anterior:

    - `hardwareSpiSettings` é definido como uma nova instância do `SpiConnectionSettings` . O construtor define o `busId` parâmetro como 0 e o `chipSelectLine` parâmetro como 0.
    - Uma [declaração using](../../csharp/whats-new/csharp-8.md#using-declarations) cria uma instância do `SpiDevice` chamando `SpiDevice.Create` e passando `hardwareSpiSettings` . Isso `SpiDevice` representa o barramento SPI. A `using` declaração garante que o objeto seja descartado e que os recursos de hardware sejam liberados corretamente.
    - Outra `using` declaração cria uma instância do `Mcp3008` e passa o `SpiDevice` para o construtor.
    - Um `while` loop é executado indefinidamente. Cada iteração:
        1. Lê o valor de CH0 no ADC chamando `mcp.Read(0)` .
        1. Divide o valor de 10,24. O MCP3008 é um ADC de 10 bits, o que significa que ele retorna 1024 valores possíveis variando 0-1023. Dividir o valor de 10,24 representa o valor como uma porcentagem.
        1. Arredonda o valor para o número inteiro mais próximo.
        1. Grava o valor no console formatado como uma porcentagem.
        1. Dorme 500 ms.

1. [!INCLUDE [tutorial-build](../includes/tutorial-build.md)]
1. [!INCLUDE [tutorial-deploy](../includes/tutorial-deploy.md)]
1. Execute o aplicativo no Raspberry Pi alternando para o diretório de implantação e executando o executável.

    ```bash
    ./AdcTutorial
    ```

    Observe a saída à medida que você gira o potentiometer de discagem. Isso ocorre devido ao potentiometer que varia a voltagem fornecida para CH0 no ADC. O ADC compara a tensão de entrada em CH0 com a voltagem de referência fornecida para V<sub>ref</sub> para gerar um valor.

1. Encerre o programa pressionando <kbd>Ctrl + C</kbd>.

Parabéns! Você usou o SPI para ler valores de um conversor analógico para digital.

## <a name="get-the-source-code"></a>Obter o código-fonte

A fonte deste tutorial está [disponível no GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/AdcTutorial) <span class="docon docon-navigate-external x-hidden-focus"></span> .

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Saiba como usar Uso Geral entrada/saída para piscar um LED](../tutorials/blink-led.md)
