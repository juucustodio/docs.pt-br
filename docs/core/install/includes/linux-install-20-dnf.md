---
ms.openlocfilehash: bd0953697ee3a9e928d09c1f270a4af5606ee0d9
ms.sourcegitcommit: bc9c63541c3dc756d48a7ce9d22b5583a18cf7fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94507035"
---

### <a name="install-the-sdk"></a>Instalar o SDK

O SDK do .NET Core permite que você desenvolva aplicativos com o .NET Core. Se você instalar o SDK do .NET Core, não será necessário instalar o tempo de execução correspondente. Para instalar o SDK do .NET Core, execute os seguintes comandos:

```bash
sudo dnf install dotnet-sdk-2.0
```

### <a name="install-the-runtime"></a>Instalar o runtime

O tempo de execução do .NET Core permite executar aplicativos que foram feitos com o .NET Core que não incluiu o tempo de execução. Os comandos a seguir instalam o tempo de execução do ASP.NET Core, que é o tempo de execução mais compatível para o .NET Core. Em seu terminal, execute os comandos a seguir.

```bash
sudo dnf install aspnetcore-runtime-2.0
```

Como alternativa ao tempo de execução de ASP.NET Core, você pode instalar o tempo de execução do .NET Core, que não inclui suporte a ASP.NET Core: substitua `aspnetcore-runtime-2.0` no comando anterior por `dotnet-runtime-2.0` .

```bash
sudo dnf install dotnet-runtime-2.0
```
