---
ms.openlocfilehash: 87c7abf6a20dd8e9769f3b3b3cbe271d32fd62c3
ms.sourcegitcommit: bc9c63541c3dc756d48a7ce9d22b5583a18cf7fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94506946"
---

### <a name="install-the-sdk"></a>Instalar o SDK

O SDK do .NET permite que você desenvolva aplicativos com o .NET. Se você instalar o SDK do .NET, não precisará instalar o tempo de execução correspondente. Para instalar o SDK do .NET, execute os seguintes comandos:

```bash
sudo apt-get update; \
  sudo apt-get install -y apt-transport-https && \
  sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-5.0
```

> [!IMPORTANT]
> Se você receber uma mensagem de erro semelhante a **não é possível localizar o pacote dotnet-SDK-5,0** , consulte a seção [solução de problemas da apt](#apt-troubleshooting) .

### <a name="install-the-runtime"></a>Instalar o runtime

O tempo de execução de ASP.NET Core permite que você execute aplicativos que foram feitos com o .NET que não forneceu o tempo de execução. Os comandos a seguir instalam o tempo de execução do ASP.NET Core, que é o tempo de execução mais compatível para o .NET. Em seu terminal, execute os seguintes comandos:

```bash
sudo apt-get update; \
  sudo apt-get install -y apt-transport-https && \
  sudo apt-get update && \
  sudo apt-get install -y aspnetcore-runtime-5.0
```

> [!IMPORTANT]
> Se você receber uma mensagem de erro semelhante a **não é possível localizar o pacote aspnetcore-Runtime-5,0** , consulte a seção [solução de problemas da apt](#apt-troubleshooting) .

Como alternativa ao tempo de execução de ASP.NET Core, você pode instalar o tempo de execução do .NET, que não inclui suporte a ASP.NET Core: substitua `aspnetcore-runtime-5.0` no comando anterior por `dotnet-runtime-5.0` :

```bash
sudo apt-get install -y dotnet-runtime-5.0
```
