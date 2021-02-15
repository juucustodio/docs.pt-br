---
title: Ler condições ambientais com um sensor
description: Saiba como ler termperature, pressão barométrica e umidade com as bibliotecas IoT .NET.
author: camsoper
ms.author: casoper
ms.date: 11/14/2020
ms.topic: tutorial
ms.prod: dotnet
ms.openlocfilehash: 1270e7629e9afc12b1d76d260d4b8b51428f1040
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96585647"
---
# <a name="read-environmental-conditions-from-a-sensor"></a>Ler condições ambientais com um sensor

Um dos cenários mais comuns para dispositivos IoT é a detecção de condições ambientais. Uma variedade de sensores está disponível para monitorar a temperatura, a umidade, a pressão barométrica e muito mais.

Neste tópico, você usará o .NET para ler as condições ambientais de um sensor.

## <a name="prerequisites"></a>Pré-requisitos

- [!INCLUDE [prereq-rpi](../includes/prereq-rpi.md)]
- [BME280](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout) <span class="docon docon-navigate-external x-hidden-focus"></span> análise de sensor de temperatura/pressão de umidade/barométrica
- Cabos de jumper
- Placa universal (opcional)
- Painel de debates do Raspberry Pi GPIO (opcional)
- [!INCLUDE [tutorial-prereq-dotnet](../includes/tutorial-prereq-dotnet.md)]

> [!IMPORTANT]
> Há muitos fabricantes de debates de BME280. A maioria dos designs são semelhantes, e o fabricante não deve fazer nenhuma diferença na funcionalidade. Este tutorial tenta considerar as variações. Certifique-se de que sua análise de BME280 inclui uma interface de circuito de Inter-Integrated (I2C).

[!INCLUDE [prepare-pi-i2c](../includes/prepare-pi-i2c.md)]

## <a name="prepare-the-hardware"></a>Preparar o hardware

Use os componentes de hardware para criar o circuito, conforme ilustrado no diagrama a seguir:

:::image type="content" source="../media/rpi-bmp280_i2c-thumb.png" alt-text="Um diagrama do Fritzing mostrando a conexão do Raspberry Pi com o painel de debates do BME280" lightbox="../media/rpi-bmp280_i2c.png":::

A seguir estão as conexões do Raspberry Pi com a análise de BME280:

- 3.3 v a VIN *ou* 3v3 (mostrado em vermelho)
- Terra a terra (preto)
- SDA (GPIO 2) para SDI *ou* SDA (azul)
- SCL (GPIO 3) a SCK *ou* SCL (laranja)

[!INCLUDE [tutorial-rpi-gpio](../includes/tutorial-rpi-gpio.md)]

[!INCLUDE [gpio-breakout](../includes/gpio-breakout.md)]

## <a name="create-the-app"></a>Crie o aplicativo

Conclua as seguintes etapas em seu ambiente de desenvolvimento preferido:

1. Crie um novo aplicativo de console .NET usando a [CLI do .net](../../core/tools/dotnet-new.md) ou o [Visual Studio](../../core/tutorials/with-visual-studio.md). Nomeie-o como *SensorTutorial*.

    ```dotnetcli
    dotnet new console -o SensorTutorial
    ```

1. [!INCLUDE [tutorial-add-packages](../includes/tutorial-add-packages.md)]
1. Substitua o conteúdo do *Program.cs* pelo seguinte código:

    :::code language="csharp" source="~/iot-samples/tutorials/SensorTutorial/Program.cs" :::

    No código anterior:

    - `i2cSettings` é definido como uma nova instância do `I2cConnectionSettings` . O construtor define o `busId` parâmetro como 1 e o `deviceAddress` parâmetro como `Bme280.DefaultI2cAddress` .

        > [!IMPORTANT]
        > Alguns fabricantes de debates BME280 usam o valor de endereço secundário. Para esses dispositivos, use `Bme280.SecondaryI2cAddress` .

    - Uma [declaração using](../../csharp/whats-new/csharp-8.md#using-declarations) cria uma instância do `I2cDevice` chamando `I2cDevice.Create` e passando `i2cSettings` . Isso `I2cDevice` representa o barramento I2C. A `using` declaração garante que o objeto seja descartado e que os recursos de hardware sejam liberados corretamente.
    - Outra `using` declaração cria uma instância do `Bme280` para representar o sensor. O `I2cDevice` é passado no construtor.
    - O tempo necessário para o chip tomar medidas com as configurações atuais (padrão) do chip é recuperado chamando `GetMeasurementDuration` .
    - Um `while` loop é executado indefinidamente. Cada iteração:
        1. Limpa o console.
        1. Define o modo de energia como `Bmx280PowerMode.Forced` . Isso força o chip a executar uma medição, armazenar os resultados e, em seguida, dormir.
        1. Lê os valores de temperatura, pressão, umidade e altitude.

            > [!NOTE]
            > A altitude é calculada pela Associação de dispositivo. Essa sobrecarga de `TryReadAltitude` usa pressão do nível médio do mar para gerar uma estimativa.

        1. Grava as condições ambientais atuais no console.
        1. Dorme 1000 MS.

1. [!INCLUDE [tutorial-build](../includes/tutorial-build.md)]
1. [!INCLUDE [tutorial-deploy](../includes/tutorial-deploy.md)]
1. Execute o aplicativo no Raspberry Pi alternando para o diretório de implantação e executando o executável.

    ```bash
    ./SensorTutorial
    ```

    Observe a saída do sensor no console.

1. Encerre o programa pressionando <kbd>Ctrl + C</kbd>.

Parabéns! Você usou I2C para ler valores de um sensor de pressão de temperatura/umidade/barométrica!

## <a name="get-the-source-code"></a>Obter o código-fonte

A fonte deste tutorial está [disponível no GitHub](https://github.com/MicrosoftDocs/dotnet-iot-assets/tree/master/tutorials/SensorTutorial) <span class="docon docon-navigate-external x-hidden-focus"></span> .

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Saiba como exibir texto em um LCD](../tutorials/lcd-display.md)
