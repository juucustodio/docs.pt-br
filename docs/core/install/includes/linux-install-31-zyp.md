---
ms.openlocfilehash: 36f1ee26def82d426b6637ae96f382fc89791a2f
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93135589"
---

### <a name="install-the-sdk"></a>Instalar o SDK

O SDK do .NET Core permite que você desenvolva aplicativos com o .NET Core. Para instalar o SDK do .NET Core, execute os comandos a seguir.

```bash
sudo zypper install dotnet-sdk-3.1
```

### <a name="install-the-runtime"></a>Instalar o runtime

O tempo de execução do .NET Core permite executar aplicativos que foram feitos com o .NET Core que não incluiu o tempo de execução. Os comandos a seguir instalam o tempo de execução do ASP.NET Core, que é o tempo de execução mais compatível para o .NET Core. Em seu terminal, execute os comandos a seguir.

```bash
sudo zypper install aspnetcore-runtime-3.1
```

Como alternativa ao tempo de execução de ASP.NET Core, você pode instalar o tempo de execução do .NET Core que não inclui suporte a ASP.NET Core: substitua `aspnetcore-runtime-2.1` no comando anterior por `dotnet-runtime-3.1` .

```bash
sudo zypper install dotnet-runtime-3.1
```
