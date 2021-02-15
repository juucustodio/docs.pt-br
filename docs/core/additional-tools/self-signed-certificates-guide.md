---
title: Gerar visão geral de certificados de Self-Signed
description: Uma visão geral da ferramenta de desenvolvimento/certificados do Microsoft dotnet que adiciona funcionalidade para projetos do .NET Core e ASP.NET Core e outras opções para usar certificados autoassinados.
author: angee
ms.date: 11/19/2020
ms.openlocfilehash: d1675abb7d584b72d981f9db739e02269abe662c
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189135"
---
# <a name="generate-self-signed-certificates-with-the-net-cli"></a>Gerar certificados autoassinados com a CLI do .NET

Ao usar certificados autoassinados, há diferentes maneiras de criá-los e usá-los para cenários de desenvolvimento e teste.  Neste guia, você abordará o uso de certificados autoassinados com o e `dotnet dev-certs` outras opções como `PowerShell` e `OpenSSL` .

Em seguida, você pode validar que o certificado será carregado usando um exemplo, como um [aplicativo ASP.NET Core](https://github.com/dotnet/dotnet-docker/blob/master/samples/run-aspnetcore-https-development.md) hospedado em um contêiner.

## <a name="prerequisites"></a>Pré-requisitos

No exemplo, você pode utilizar o .NET Core 3,1 ou o .NET 5.

Para `dotnet dev-certs` o, certifique-se de ter a versão apropriada do .net instalada:

* [Instalar o .NET no Windows](../install/windows.md)
* [Instalar o .NET no Linux](../install/linux.md)
* [Instalar o .NET no macOS](../install/macos.md)

Este exemplo requer o [docker 17, 6](https://docs.docker.com/release-notes/docker-ce) ou posterior do [cliente do Docker](https://www.docker.com/products/docker).

## <a name="prepare-sample-app"></a>Preparar aplicativo de exemplo

Você precisará preparar o aplicativo de exemplo dependendo do tempo de execução que você gostaria de usar para o teste, [.NET Core 3,1](#net-core-31-sample-app) ou [.NET 5](#net-5-sample-app).

Para este guia, você usará um [aplicativo de exemplo](https://hub.docker.com/_/microsoft-dotnet-samples) e fará alterações quando apropriado.

### <a name="net-core-31-sample-app"></a>Aplicativo de exemplo do .NET Core 3,1

Obter o aplicativo de exemplo.

```console
git clone https://github.com/dotnet/dotnet-docker/
```

Navegue até o repositório localmente e abra o espaço de trabalho em um editor.

> [!NOTE]
> Se você pretende usar dotnet publish parâmetros para *cortar* a implantação, certifique-se de que as dependências apropriadas estejam incluídas para dar suporte a certificados SSL.
Atualize o [dotnet-docker\samples\aspnetapp\aspnetapp.csproj](https://github.com/dotnet/dotnet-docker/blob/master/samples/aspnetapp/aspnetapp/aspnetapp.csproj) para garantir que os assemblies apropriados sejam incluídos no contêiner. Para referência, verifique como atualizar o arquivo. csproj para [dar suporte a certificados SSL](../deploying/trim-self-contained.md#support-for-ssl-certificates) ao usar o corte para implantações independentes.

Certifique-se de que o `aspnetapp.csproj` inclui a estrutura de destino apropriada:

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>.netcoreapp3.1</TargetFramework>
    <!--Other Properties-->
  </PropertyGroup>

</Project>
```

Modifique o Dockerfile para verificar se o tempo de execução aponta para o .NET Core 3,1:

```Dockerfile
# https://hub.docker.com/_/microsoft-dotnet-core
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /source

# copy csproj and restore as distinct layers
COPY *.sln .
COPY aspnetapp/*.csproj ./aspnetapp/
RUN dotnet restore

# copy everything else and build app
COPY aspnetapp/. ./aspnetapp/
WORKDIR /source/aspnetapp
RUN dotnet publish -c release -o /app --no-restore

# final stage/image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["dotnet", "aspnetapp.dll"]
```

Verifique se você está apontando para o aplicativo de exemplo.

```console
cd .\dotnet-docker\samples\aspnetapp
```

Crie o contêiner para teste local.

```console
docker build -t aspnetapp:my-sample -f Dockerfile .
```

### <a name="net-5-sample-app"></a>Aplicativo de exemplo do .NET 5

Para este guia, o [exemplo de aspnetapp](https://hub.docker.com/_/microsoft-dotnet-samples) deve ser verificado para o .NET 5.

Verifique se o aplicativo de exemplo [Dockerfile](https://github.com/dotnet/dotnet-docker/blob/master/samples/aspnetapp/Dockerfile) está usando o .NET 5.

Dependendo do sistema operacional do host, o tempo de execução do ASP.NET pode precisar ser atualizado. Por exemplo, alterar de `mcr.microsoft.com/dotnet/aspnet:5.0-nanoservercore-2009 AS runtime` para `mcr.microsoft.com/dotnet/aspnet:5.0-windowsservercore-ltsc2019 AS runtime` no Dockerfile ajudará a direcionar o tempo de execução do Windows apropriado.

Por exemplo, isso ajudará no teste dos certificados no Windows:

```Dockerfile
# https://hub.docker.com/_/microsoft-dotnet
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /source

# copy csproj and restore as distinct layers
COPY *.sln .
COPY aspnetapp/*.csproj ./aspnetapp/
RUN dotnet restore -r win-x64

# copy everything else and build app
COPY aspnetapp/. ./aspnetapp/
WORKDIR /source/aspnetapp
RUN dotnet publish -c release -o /app -r win-x64 --self-contained false --no-restore

# final stage/image
# Uses the 2009 release; 2004, 1909, and 1809 are other choices
FROM mcr.microsoft.com/dotnet/aspnet:5.0-windowsservercore-ltsc2019 AS runtime
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["aspnetapp"]

```

Se estiver testando os certificados no Linux, você poderá usar o Dockerfile existente.

Certifique-se de que o `aspnetapp.csproj` inclui a estrutura de destino apropriada:

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    <!--Other Properties-->
  </PropertyGroup>

</Project>
```

> [!NOTE]
> Se você quiser usar `dotnet publish` parâmetros para *cortar* a implantação, verifique se as dependências apropriadas estão incluídas para dar suporte a certificados SSL.
Atualize o [dotnet-docker\samples\aspnetapp\aspnetapp.csproj](https://github.com/dotnet/dotnet-docker/blob/master/samples/aspnetapp/aspnetapp/aspnetapp.csproj) para garantir que os assemblies apropriados sejam incluídos no contêiner. Para referência, verifique como atualizar o arquivo. csproj para [dar suporte a certificados SSL](../deploying/trim-self-contained.md#support-for-ssl-certificates) ao usar o corte para implantações independentes.

Verifique se você está apontando para o aplicativo de exemplo.

```console
cd .\dotnet-docker\samples\aspnetapp
```

Crie o contêiner para teste local.

```console
docker build -t aspnetapp:my-sample -f Dockerfile .
```

## <a name="create-a-self-signed-certificate"></a>Criará um certificado autoassinado

Você pode criar um certificado autoassinado:

- [Com o dotnet dev-certs](#with-dotnet-dev-certs)
- [Com o PowerShell](#with-powershell)
- [Com OpenSSL](#with-openssl)

### <a name="with-dotnet-dev-certs"></a>Com o dotnet dev-certs

Você pode usar o `dotnet dev-certs` para trabalhar com certificados autoassinados. Este exemplo usa um console do PowerShell.

```console
dotnet dev-certs https -ep $env:USERPROFILE\.aspnet\https\aspnetapp.pfx -p crypticpassword
dotnet dev-certs https --trust
```

> [!NOTE]
> O nome do certificado, nesse caso, *aspnetapp*. pfx, deve corresponder ao nome do assembly do projeto. `crypticpassword` é usado como um substituto para uma senha de sua escolha. Se o console retornar "um certificado HTTPS válido já está presente.", um certificado confiável já existe em seu repositório. Ele pode ser exportado usando o console do MMC.

Configure os segredos do aplicativo para o certificado:

```console
dotnet user-secrets -p aspnetapp\aspnetapp.csproj set "Kestrel:Certificates:Development:Password" "crypticpassword"
```

> [!NOTE]
> Observação: a senha deve corresponder à senha usada para o certificado.

Execute a imagem de contêiner com ASP.NET Core configurado para HTTPS:

```console
docker run --rm -it -p 8000:80 -p 8001:443 -e ASPNETCORE_URLS="https://+;http://+" -e ASPNETCORE_HTTPS_PORT=8001 -e ASPNETCORE_ENVIRONMENT=Development -v $env:APPDATA\microsoft\UserSecrets\:C:\Users\ContainerUser\AppData\Roaming\microsoft\UserSecrets -v $env:USERPROFILE\.aspnet\https:C:\Users\ContainerUser\AppData\Roaming\ASP.NET\Https mcr.microsoft.com/dotnet/samples:aspnetapp
```

Depois que o aplicativo for iniciado, navegue até `https://localhost:8001` no navegador da Web.

#### <a name="clean-up"></a>Limpeza

Se os segredos e certificados não estiverem em uso, certifique-se de limpá-los.

```console
dotnet user-secrets remove "Kestrel:Certificates:Development:Password" -p aspnetapp\aspnetapp.csproj
dotnet dev-certs https --clean
```

### <a name="with-powershell"></a>Com o PowerShell

Você pode usar o PowerShell para gerar certificados autoassinados. O [cliente PKI](/powershell/module/pkiclient/new-selfsignedcertificate?preserve-view=true&view=win10-ps) pode ser usado para gerar um certificado autoassinado.

```powershell
$cert = New-SelfSignedCertificate -DnsName @("contoso.com", "www.contoso.com") -CertStoreLocation "cert:\LocalMachine\My"
```

O certificado será gerado, mas, para fins de teste, deve ser colocado em um repositório de certificados para teste em um navegador.

```powershell
$certKeyPath = "c:\certs\contoso.com.pfx"
$password = ConvertTo-SecureString 'password' -AsPlainText -Force
$cert | Export-PfxCertificate -FilePath $certKeyPath -Password $password
$rootCert = $(Import-PfxCertificate -FilePath $certKeyPath -CertStoreLocation 'Cert:\LocalMachine\Root' -Password $password)
```

Neste ponto, os certificados devem ser exibidos em um [snap-in do MMC](../../framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md).

Você pode executar o contêiner de exemplo no subsistema do Windows para Linux (WSL):

```console
docker run --rm -it -p 8000:80 -p 8001:443 -e ASPNETCORE_URLS="https://+;http://+" -e ASPNETCORE_HTTPS_PORT=8001 -e ASPNETCORE_ENVIRONMENT=Development -e ASPNETCORE_Kestrel__Certificates__Default__Password="password" -e ASPNETCORE_Kestrel__Certificates__Default__Path=/https/contoso.com.pfx -v /c/certs:/https/ mcr.microsoft.com/dotnet/samples:aspnetapp
```

> [!NOTE]
> Observe que, com a montagem de volume, o caminho do arquivo poderia ser tratado diferentemente com base no host.  Por exemplo, em WSL, poderemos substituir */c/certs* por */mnt/c/certs*.

Se você estiver usando o contêiner criado anteriormente para o Windows, o comando executar será semelhante ao seguinte:

```console
docker run --rm -it -p 8000:80 -p 8001:443 -e ASPNETCORE_URLS="https://+;http://+" -e ASPNETCORE_HTTPS_PORT=8001 -e ASPNETCORE_ENVIRONMENT=Development -e ASPNETCORE_Kestrel__Certificates__Default__Password="password" -e ASPNETCORE_Kestrel__Certificates__Default__Path=c:\https\contoso.com.pfx -v c:\certs:C:\https aspnetapp:my-sample
```

Quando o aplicativo estiver ativo, navegue até contoso.com:8001 em um navegador.

Certifique-se de que as entradas de host sejam atualizadas para `contoso.com` que respondam no endereço IP apropriado (por exemplo, 127.0.0.1). Se o certificado não for reconhecido, verifique se o certificado carregado com o contêiner também é confiável no host e se há entradas apropriadas de SAN/DNS para o `contoso.com` .

#### <a name="clean-up"></a>Limpeza

```powershell
$cert | Remove-Item
Get-ChildItem $certFilePath | Remove-Item
$rootCert | Remove-item
```

### <a name="with-openssl"></a>Com OpenSSL

Você pode usar o [OpenSSL](https://www.openssl.org/) para criar certificados autoassinados. Este exemplo usará o WSL/Ubuntu e um shell bash com `OpenSSL` .

Isso irá gerar um. CRT e uma. Key.

```bash
PARENT="contoso.com"
openssl req \
-x509 \
-newkey rsa:4096 \
-sha256 \
-days 365 \
-nodes \
-keyout $PARENT.key \
-out $PARENT.crt \
-subj "/CN=${PARENT}" \
-extensions v3_ca \
-extensions v3_req \
-config <( \
  echo '[req]'; \
  echo 'default_bits= 4096'; \
  echo 'distinguished_name=req'; \
  echo 'x509_extension = v3_ca'; \
  echo 'req_extensions = v3_req'; \
  echo '[v3_req]'; \
  echo 'basicConstraints = CA:FALSE'; \
  echo 'keyUsage = nonRepudiation, digitalSignature, keyEncipherment'; \
  echo 'subjectAltName = @alt_names'; \
  echo '[ alt_names ]'; \
  echo "DNS.1 = www.${PARENT}"; \
  echo "DNS.2 = ${PARENT}"; \
  echo '[ v3_ca ]'; \
  echo 'subjectKeyIdentifier=hash'; \
  echo 'authorityKeyIdentifier=keyid:always,issuer'; \
  echo 'basicConstraints = critical, CA:TRUE, pathlen:0'; \
  echo 'keyUsage = critical, cRLSign, keyCertSign'; \
  echo 'extendedKeyUsage = serverAuth, clientAuth')

openssl x509 -noout -text -in $PARENT.crt
```

Para obter um. pfx, use o seguinte comando:

```bash
openssl pkcs12 -export -out $PARENT.pfx -inkey $PARENT.key -in $PARENT.crt
```

> [!NOTE]
> O exemplo. aspnetcore 3,1 usará `.pfx` e uma senha. Começando com o `.net 5` tempo de execução, o Kestrel também pode pegar `.crt` arquivos codificados por PEM `.key` .

Dependendo do sistema operacional do host, o certificado precisará ser confiável. Em um host Linux, ' confiar ' o certificado é diferente e distribuição dependente.

Para os fins deste guia, veja um exemplo no Windows usando o PowerShell:

```powershell
Import-Certificate -FilePath $certFilePath -CertStoreLocation 'Cert:\LocalMachine\Root'
```

Para o .NET Core 3,1, execute o seguinte comando em WSL:

```bash
docker run --rm -it -p 8000:80 -p 8001:443 -e ASPNETCORE_URLS="https://+;http://+" -e ASPNETCORE_HTTPS_PORT=8001 -e ASPNETCORE_ENVIRONMENT=Development -e ASPNETCORE_Kestrel__Certificates__Default__Password="password" -e ASPNETCORE_Kestrel__Certificates__Default__Path=/https/contoso.com.pfx -v /c/path/to/certs/:/https/ mcr.microsoft.com/dotnet/samples:aspnetapp
```

A partir do .NET 5, o Kestrel pode pegar os `.crt` arquivos codificados por PEM `.key` . Você pode executar o exemplo com o seguinte comando para o .NET 5:

```bash
docker run --rm -it -p 8000:80 -p 8001:443 -e ASPNETCORE_URLS="https://+;http://+" -e ASPNETCORE_HTTPS_PORT=8001 -e ASPNETCORE_ENVIRONMENT=Development -e ASPNETCORE_Kestrel__Certificates__Default__Path=/https/contoso.com.crt -e ASPNETCORE_Kestrel__Certificates__Default__KeyPath=/https/contoso.com.key -v /c/path/to/certs:/https/ mcr.microsoft.com/dotnet/samples:aspnetapp
```

> [!NOTE]
> Observe que no WSL, o caminho de montagem do volume pode ser alterado dependendo da configuração.

Para o .NET Core 3,1 no Windows, execute o seguinte comando no `Powershell` :

```powershell
docker run --rm -it -p 8000:80 -p 8001:443 -e ASPNETCORE_URLS="https://+;http://+" -e ASPNETCORE_HTTPS_PORT=8001 -e ASPNETCORE_ENVIRONMENT=Development -e ASPNETCORE_Kestrel__Certificates__Default__Password="password" -e ASPNETCORE_Kestrel__Certificates__Default__Path=c:\https\contoso.com.pfx -v c:\certs:C:\https aspnetapp:my-sample
```

Para o .NET 5 no Windows, execute o seguinte comando no PowerShell:

```powershell
docker run --rm -it -p 8000:80 -p 8001:443 -e ASPNETCORE_URLS="https://+;http://+" -e ASPNETCORE_HTTPS_PORT=8001 -e ASPNETCORE_ENVIRONMENT=Development -e ASPNETCORE_Kestrel__Certificates__Default__Path=c:\https\contoso.com.crt -e ASPNETCORE_Kestrel__Certificates__Default__KeyPath=c:\https\contoso.com.key -v c:\certs:C:\https aspnetapp:my-sample
```

Quando o aplicativo estiver ativo, navegue até contoso.com:8001 em um navegador.

Certifique-se de que as entradas de host sejam atualizadas para `contoso.com` que respondam no endereço IP apropriado (por exemplo, 127.0.0.1). Se o certificado não for reconhecido, verifique se o certificado carregado com o contêiner também é confiável no host e se há entradas apropriadas de SAN/DNS para o `contoso.com` .

#### <a name="clean-up"></a>Limpeza

Certifique-se de limpar os certificados autoassinados depois de fazer o teste.

```powershell
Get-ChildItem $certFilePath | Remove-Item
```
