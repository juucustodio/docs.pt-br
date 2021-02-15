---
ms.openlocfilehash: cac1fbd2369277b3a322247a7008f07929502437
ms.sourcegitcommit: bc9c63541c3dc756d48a7ce9d22b5583a18cf7fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94507007"
---

### <a name="install-the-sdk"></a>Instalar o SDK

O SDK do .NET Core permite que você desenvolva aplicativos com o .NET Core. Se você instalar o SDK do .NET Core, não será necessário instalar o tempo de execução correspondente. Para instalar o SDK do .NET Core, execute os seguintes comandos:

```bash
sudo apt-get update; \
  sudo apt-get install -y apt-transport-https && \
  sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-3.1
```

> [!IMPORTANT]
> Se você receber uma mensagem de erro semelhante a **não é possível localizar o pacote dotnet-SDK-3,1** , consulte a seção [solução de problemas da apt](#apt-troubleshooting) .

### <a name="install-the-runtime"></a>Instalar o runtime

O tempo de execução do .NET Core permite executar aplicativos que foram feitos com o .NET Core que não incluiu o tempo de execução. Os comandos a seguir instalam o tempo de execução do ASP.NET Core, que é o tempo de execução mais compatível para o .NET Core. Em seu terminal, execute os comandos a seguir.

```bash
sudo apt-get update; \
  sudo apt-get install -y apt-transport-https && \
  sudo apt-get update && \
  sudo apt-get install -y aspnetcore-runtime-3.1
```

> [!IMPORTANT]
> Se você receber uma mensagem de erro semelhante a **não é possível localizar o pacote aspnetcore-Runtime-3,1** , consulte a seção [solução de problemas da apt](#apt-troubleshooting) .

Como alternativa ao tempo de execução de ASP.NET Core, você pode instalar o tempo de execução do .NET Core, que não inclui suporte a ASP.NET Core: substitua `aspnetcore-runtime-3.1` no comando anterior por `dotnet-runtime-3.1` .

```bash
sudo apt-get install -y dotnet-runtime-3.1
```
