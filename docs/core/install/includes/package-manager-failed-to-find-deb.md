---
ms.openlocfilehash: 3275865cf7f4669ba7deaacea320136d02f64dda
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99804244"
---

Se você receber uma mensagem de erro semelhante a **não é possível localizar o pacote {dotnet-Package}** ou **não foi possível instalar alguns pacotes**, execute os comandos a seguir.

Há dois espaços reservados no seguinte conjunto de comandos.

- `{dotnet-package}`\
Isso representa o pacote .NET que você está instalando, como `aspnetcore-runtime-3.1` . Isso é usado no comando a seguir `sudo apt-get install` .

- `{os-version}`\
Isso representa a versão de distribuição em que você está. Isso é usado no `wget` comando a seguir. A versão de distribuição é o valor numérico, como `20.04` no Ubuntu ou `10` no Debian.

Primeiro, tente limpar a lista de pacotes:

```bash
sudo dpkg --purge packages-microsoft-prod && sudo dpkg -i packages-microsoft-prod.deb
sudo apt-get update
```

Em seguida, tente instalar o .NET novamente. Se isso não funcionar, você poderá executar uma instalação manual com os seguintes comandos:
