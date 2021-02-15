---
ms.openlocfilehash: ed269683f5c4569c21ae53e9a3c1ec65eb5ebd43
ms.sourcegitcommit: bc9c63541c3dc756d48a7ce9d22b5583a18cf7fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94506838"
---

### <a name="install-the-sdk"></a>Instalar o SDK

O SDK do .NET permite que você desenvolva aplicativos com o .NET. Se você instalar o SDK do .NET, não precisará instalar o tempo de execução correspondente. Para instalar o SDK do .NET, execute os seguintes comandos:

```bash
sudo zypper install dotnet-sdk-5.0
```

### <a name="install-the-runtime"></a>Instalar o runtime

O tempo de execução de ASP.NET Core permite que você execute aplicativos que foram feitos com o .NET que não forneceu o tempo de execução. Os comandos a seguir instalam o tempo de execução do ASP.NET Core, que é o tempo de execução mais compatível para o .NET. Em seu terminal, execute os seguintes comandos:

```bash
sudo zypper install aspnetcore-runtime-5.0
```

Como alternativa ao tempo de execução de ASP.NET Core, você pode instalar o tempo de execução do .NET, que não inclui suporte a ASP.NET Core: substitua `aspnetcore-runtime-5.0` no comando anterior por `dotnet-runtime-5.0` :

```bash
sudo zypper install dotnet-runtime-5.0
```
