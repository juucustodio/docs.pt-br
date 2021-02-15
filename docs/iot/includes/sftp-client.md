---
ms.openlocfilehash: 60e326af0d956ceb63b32e5d3ec2436fe09a7005
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2020
ms.locfileid: "96585603"
---
[Usando um cliente SFTP](https://www.raspberrypi.org/documentation/remote-access/ssh/sftp.md), copie os arquivos do local de publicação no computador de desenvolvimento para uma nova pasta no Raspberry Pi.

Por exemplo, para usar o `scp` comando para copiar arquivos do computador de desenvolvimento para o Raspberry Pi, abra um prompt de comando e execute o seguinte:

```console
scp -r /publish-location/* pi@raspberrypi:/home/pi/deployment-location/
```

Sendo que:

- A `-r` opção instrui `scp` a copiar os arquivos recursivamente.
- */Publish-Location/* é a pasta que você publicou na etapa anterior.
- `pi@raspberypi` é o usuário e os nomes de host no formato `<username>@<hostname>` .
- */Home/PI/Deployment-Location/* é a nova pasta no Raspberry Pi.

> [!TIP]
> As versões recentes do Windows têm o OpenSSH, que inclui o `scp` , pré-instalado.
