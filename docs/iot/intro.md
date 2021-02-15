---
title: Desenvolver aplicativos para dispositivos IoT com as bibliotecas IoT do .NET
description: Saiba como o .NET pode ser usado para criar aplicativos para dispositivos e cenários de IoT.
author: camsoper
ms.author: casoper
ms.date: 11/13/2020
ms.topic: overview
ms.prod: dotnet
ms.openlocfilehash: c3d05ec5b05780f91404c3c27e91bcd602b0faeb
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2020
ms.locfileid: "96585606"
---
# <a name="develop-apps-for-iot-devices-with-the-net-iot-libraries"></a>Desenvolver aplicativos para dispositivos IoT com as bibliotecas IoT do .NET

O .NET é executado em uma variedade de plataformas e arquiteturas. As placas IoT (Internet das coisas) comuns, como Raspberry Pi e Hummingboard, têm suporte. Os aplicativos de IoT normalmente interagem com hardware especializado, como sensores, conversores analógicos para digitais e dispositivos de LCD. As bibliotecas IoT do .NET habilitam esses cenários.

## <a name="video-overview"></a>Visão geral em vídeo

<!--markdownlint-disable MD034 -->
> [!VIDEO https://channel9.msdn.com/Series/IoT-101/Intro-to-IOT-with-NET-Core-1-of-9/player]

## <a name="libraries"></a>Bibliotecas

As bibliotecas IoT do .NET são compostas por dois pacotes NuGet:

- [System. Device. GPIO](https://www.nuget.org/packages/System.Device.Gpio/)<span class="docon docon-navigate-external x-hidden-focus"></span>
- [IOT. Device. Bindings](https://www.nuget.org/packages/Iot.Device.Bindings/)<span class="docon docon-navigate-external x-hidden-focus"></span>

### <a name="systemdevicegpio"></a>System.Device.Gpio

`System.Device.Gpio` o oferece suporte a uma variedade de protocolos para interagir com Pins de hardware de nível baixo para controlar dispositivos. Elas incluem:

- E/s de finalidade geral (GPIO)
- Circuito de Inter-Integrated (I2C)
- SPI (interface de periférico serial)
- Modulação de largura de pulso (PWM)
- Porta serial

### <a name="iotdevicebindings"></a>Iot.Device.Bindings

O `Iot.Device.Bindings` pacote:

* Contém [associações de dispositivo](https://github.com/dotnet/iot/blob/master/src/devices/README.md) <span class="docon docon-navigate-external x-hidden-focus"></span> para simplificar o desenvolvimento de aplicativos encapsulando System. Device. GPIO.
* O tem suporte da Comunidade e associações adicionais são adicionadas continuamente.

As associações de dispositivo usadas com frequência incluem:

- [CharacterLcd-exibição de caracteres de LCD](https://github.com/dotnet/iot/tree/master/src/devices/CharacterLcd)<span class="docon docon-navigate-external x-hidden-focus"></span>
- [SN74HC595-registro de deslocamento de 8 bits](https://github.com/dotnet/iot/tree/master/src/devices/Sn74hc595)<span class="docon docon-navigate-external x-hidden-focus"></span>
- [BrickPi3](https://github.com/dotnet/iot/tree/master/src/devices/BrickPi3)<span class="docon docon-navigate-external x-hidden-focus"></span>
- [Driver de matriz com LED de Max7219](https://github.com/dotnet/iot/tree/master/src/devices/Max7219)<span class="docon docon-navigate-external x-hidden-focus"></span>
- [Matriz de LED RGBLedMatrix-RGB](https://github.com/dotnet/iot/tree/master/src/devices/RGBLedMatrix)<span class="docon docon-navigate-external x-hidden-focus"></span>

## <a name="supported-operating-systems"></a>Sistemas operacionais compatíveis

`System.Device.Gpio` tem suporte na maioria das versões do Linux que dão suporte ao ARM/ARM64 e ao Windows 10 IoT Core.

> [!TIP]
> Para o Raspberry Pi, o [Raspberry Pi os](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) <span class="docon docon-navigate-external x-hidden-focus"></span> (anteriormente Raspbian) é recomendado.  

## <a name="supported-hardware-platforms"></a>Plataformas de hardware com suporte

`System.Device.Gpio` é compatível com a maioria das plataformas de quadro único. As plataformas recomendadas são Raspberry Pi (2 e superior) e Hummingboard. Outras plataformas conhecidas para serem compatíveis são BeagleBoard e ODROID.

As plataformas de PC têm suporte por meio do uso de uma ponte USB para SPI/I2C.

> [!IMPORTANT]
> Não há suporte para .NET em dispositivos de arquitetura ARMv6, incluindo dispositivos Raspberry Pi zero e Raspberry Pi antes do Raspberry Pi 2.

## <a name="resources"></a>Recursos

- [Bibliotecas IOT do .net no GitHub](https://github.com/dotnet/iot)<span class="docon docon-navigate-external x-hidden-focus"></span>
