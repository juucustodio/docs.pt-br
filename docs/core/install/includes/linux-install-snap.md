---
ms.openlocfilehash: 83808f2f3a05333ed5d9e3809cbc2fd6e230d02c
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96031744"
---

[O .NET Core está disponível no repositório de snap.](https://snapcraft.io/dotnet-sdk)

Um snap é um pacote de um aplicativo e suas dependências que funcionam sem modificação em várias distribuições do Linux diferentes. Os snaps são detectáveis e instaláveis no repositório de instantâneos. Para obter mais informações sobre o snap, consulte [introdução ao snap](https://snapcraft.io/docs/getting-started).

Somente as versões com suporte do .NET Core estão disponíveis por meio do snap.

### <a name="install-the-sdk"></a>Instalar o SDK

Pacotes snap para SDK do .NET são todos publicados sob o mesmo identificador: `dotnet-sdk` . Uma versão específica do SDK pode ser instalada especificando o canal. O SDK inclui o tempo de execução correspondente. A tabela a seguir lista os canais:

| Versão do .NET | Ajustar pacote             |
|--------------|--------------------------|
| 5.0          | `5.0` ou `latest/stable` |
| 3,1 (LTS)    | `3.1` ou `lts/stable`    |
| 2,1 (LTS)    | `2.1`                    |

Use o `snap install` comando para instalar um pacote de snap do SDK do .net. Use o `--channel` parâmetro para indicar qual versão deve ser instalada. Se esse parâmetro for omitido, `latest/stable` será usado. Neste exemplo, `5.0` é especificado:

```bash
sudo snap install dotnet-sdk --classic --channel=5.0
```

Em seguida, registre o `dotnet` comando para o sistema com o `snap alias` comando:

```bash
sudo snap alias dotnet-sdk.dotnet dotnet
```

Este comando é formatado como: `sudo snap alias {package}.{command} {alias}` . Você pode escolher qualquer `{alias}` nome que desejar. Por exemplo, você pode nomear o comando após a versão específica instalada pelo snap: `sudo snap alias dotnet-sdk.dotnet dotnet50` . Ao usar o comando `dotnet50` , você invocará essa versão específica do .net. Mas isso é incompatível com a maioria dos tutoriais e exemplos, pois eles esperam que um `dotnet` comando esteja disponível.

### <a name="install-the-runtime"></a>Instalar o runtime

Os pacotes snap para o tempo de execução do .NET Core são publicados em seu próprio identificador de pacote. A tabela a seguir lista os identificadores de pacote:

| Versão do .NET      | Ajustar pacote        |
|-------------------|---------------------|
| 5.0               | `dotnet-runtime-50` |
| 3,1 (LTS)         | `dotnet-runtime-31` |
| 3.0               | `dotnet-runtime-30` |
| 2.2               | `dotnet-runtime-22` |
| 2,1 (LTS)         | `dotnet-runtime-21` |

Use o `snap install` comando para instalar um pacote de snap do tempo de execução .net. Neste exemplo, o .NET 5,0 está instalado:

```bash
sudo snap install dotnet-runtime-50 --classic
```

Em seguida, registre o `dotnet` comando para o sistema com o `snap alias` comando:

```bash
sudo snap alias dotnet-runtime-50.dotnet dotnet
```

Este comando é formatado como: `sudo snap alias {package}.{command} {alias}` . Você pode escolher qualquer `{alias}` nome que desejar. Por exemplo, você pode nomear o comando após a versão específica instalada pelo snap: `sudo snap alias dotnet-runtime-50.dotnet dotnet50` . Ao usar o comando `dotnet50` , você invocará essa versão específica do .net. Mas isso é incompatível com a maioria dos tutoriais e exemplos, pois eles esperam que um `dotnet` comando esteja disponível.

### <a name="ssl-certificate-errors"></a>Erros de certificado SSL

Quando o .NET é instalado por meio do snap, é possível que, em alguns distribuições, os certificados SSL do .NET possam não ser encontrados e você receba um erro semelhante ao seguinte durante `restore` :

```bash
Processing post-creation actions...
Running 'dotnet restore' on /home/myhome/test/test.csproj...
  Restoring packages for /home/myhome/test/test.csproj...
/snap/dotnet-sdk/27/sdk/2.2.103/NuGet.targets(114,5): error : Unable to load the service index for source https://api.nuget.org/v3/index.json. [/home/myhome/test/test.csproj]
/snap/dotnet-sdk/27/sdk/2.2.103/NuGet.targets(114,5): error :   The SSL connection could not be established, see inner exception. [/home/myhome/test/test.csproj]
/snap/dotnet-sdk/27/sdk/2.2.103/NuGet.targets(114,5): error :   The remote certificate is invalid according to the validation procedure. [/home/myhome/test/test.csproj]
```

Para resolver esse problema, defina algumas variáveis de ambiente:

```bash
export SSL_CERT_FILE=[path-to-certificate-file]
export SSL_CERT_DIR=/dev/null
```

O local do certificado variará de acordo com distribuição. Aqui estão os locais para o distribuições onde tivemos o problema.

* Fedora `/etc/pki/ca-trust/extracted/pem/tls-ca-bundle.pem`
* OpenSUSE `/etc/ssl/ca-bundle.pem`
* Solus - `/etc/ssl/certs/ca-certificates.crt`
