---
title: Introdução ao .NET
description: Crie um aplicativo .NET Olá, Mundo.
author: adegeo
ms.author: adegeo
ms.date: 09/29/2020
ms.custom: vs-dotnet
ms.openlocfilehash: 6ad2b96e668c52ee80b707e31a63eac2433f3c9e
ms.sourcegitcommit: a8a205034eeffc7c3e1bdd6f506a75b0f7099ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91756085"
---
# <a name="get-started-with-net"></a>Introdução ao .NET

Este artigo ensina como criar e executar um "Olá, Mundo!" Aplicativo .NET.

Se você não tiver certeza do que é o .NET, comece com a [introdução ao .net](introduction.md).

## <a name="create-an-application"></a>Criar um aplicativo

Primeiro, baixe e instale o [SDK do .net](https://dotnet.microsoft.com/download/dotnet-core) em seu computador.

Em seguida, abra um terminal, como o **PowerShell**, um **prompt de comando** ou o **Bash**. Insira os seguintes `dotnet` comandos para criar e executar um aplicativo C#:

```dotnetcli
dotnet new console --output sample1
dotnet run --project sample1
```

Você verá esta saída:

```output
Hello World!
```

Parabéns! Você criou um aplicativo .NET simples.

## <a name="next-steps"></a>Próximas etapas

Comece a desenvolver aplicativos .NET seguindo um tutorial passo a [passo](../standard/get-started.md) ou assistindo aos [vídeos do .net 101](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oWoazjhXQzBKMrFuArxpW80) no YouTube.
