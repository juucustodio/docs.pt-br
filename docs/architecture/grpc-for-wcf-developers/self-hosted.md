---
title: Aplicativos gRPC de hospedagem interna – gRPC para desenvolvedores do WCF
description: Implantando ASP.NET Core aplicativos gRPC como serviços hospedados internamente.
ms.date: 12/15/2020
ms.openlocfilehash: a5e2316b8d76593f4eb53760d2609b5bbbc9d2c5
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938527"
---
# <a name="self-hosted-grpc-applications"></a>Aplicativos gRPC auto-hospedados

Embora ASP.NET Core aplicativos 5,0 possam ser hospedados no IIS no Windows Server, atualmente não é possível hospedar um aplicativo gRPC no IIS porque não há suporte para algumas das funcionalidades HTTP/2. Essa funcionalidade é uma meta para uma atualização futura do Windows Server.

Você pode executar seu aplicativo como um serviço do Windows. Ou você pode executá-lo como um serviço do Linux controlado pelo [sistema](https://en.wikipedia.org/wiki/Systemd), devido aos novos recursos nas extensões de hospedagem do .NET 5,0.

## <a name="run-your-app-as-a-windows-service"></a>Executar seu aplicativo como um serviço do Windows

Para configurar seu aplicativo ASP.NET Core para ser executado como um serviço do Windows, instale o pacote [Microsoft. Extensions. Hosting. WindowsServices](https://www.nuget.org/packages/Microsoft.Extensions.Hosting.WindowsServices) do NuGet. Em seguida, adicione uma chamada para `UseWindowsService` para o `CreateHostBuilder` método em `Program.cs` .

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .UseWindowsService() // Enable running as a Windows service
        .ConfigureWebHostDefaults(webBuilder =>
        {
            webBuilder.UseStartup<Startup>();
        });
```

> [!NOTE]
> Se o aplicativo não estiver sendo executado como um serviço do Windows, o `UseWindowsService` método não fará nada.

Agora, publique seu aplicativo usando um destes métodos:

* No Visual Studio, clicando com o botão direito do mouse no projeto e selecionando **publicar** no menu de atalho.
* Da CLI do .NET.

Ao publicar um aplicativo .NET, você pode optar por criar uma implantação *dependente da estrutura* ou uma implantação *independente* . As implantações dependentes da estrutura exigem que o tempo de execução compartilhado do .NET seja instalado no host onde eles são executados. As implantações independentes são publicadas com uma cópia completa do tempo de execução e da estrutura do .NET e podem ser executadas em qualquer host. Para obter mais informações, incluindo as vantagens e desvantagens de cada abordagem, consulte a documentação de [implantação de aplicativos .net](../../core/deploying/index.md) .

Para publicar uma compilação independente do aplicativo que não exige que o tempo de execução do .NET 5,0 seja instalado no host, especifique o tempo de execução a ser incluído no aplicativo. Use o `-r` sinalizador (ou `--runtime` ).

```dotnetcli
dotnet publish -c Release -r win-x64 -o ./publish
```

Para publicar uma compilação dependente de estrutura, omita o `-r` sinalizador.

```dotnetcli
dotnet publish -c Release -o ./publish
```

Copie todo o conteúdo do `publish` diretório para uma pasta de instalação. Em seguida, use a [ferramenta SC](/windows/desktop/services/controlling-a-service-using-sc) para criar um serviço do Windows para o arquivo executável.

```console
sc create MyService binPath=C:\MyService\MyService.exe
```

### <a name="log-to-the-windows-event-log"></a>Registrar no log de eventos do Windows

O `UseWindowsService` método adiciona automaticamente um provedor de [log](/aspnet/core/fundamentals/logging/) que grava mensagens de log no log de eventos do Windows. Você pode configurar o log para esse provedor adicionando uma `EventLog` entrada à `Logging` seção de `appsettings.json` ou outra fonte de configuração.

Você pode substituir o nome de origem usado no log de eventos definindo uma `SourceName` Propriedade nessas configurações. Se você não especificar um nome, o nome do aplicativo padrão (normalmente, o nome do assembly executável) será usado.

Mais informações sobre o registro em log estão no final deste capítulo.

## <a name="run-your-app-as-a-linux-service-with-systemd"></a>Execute seu aplicativo como um serviço Linux com o sistema

Para configurar seu aplicativo ASP.NET Core para ser executado como um serviço do Linux (ou *daemon* na linguagem Linux), instale o pacote [Microsoft.Extensions.Hosting.Systemd](https://www.nuget.org/packages/Microsoft.Extensions.Hosting.Systemd) do NuGet. Em seguida, adicione uma chamada para `UseSystemd` para o `CreateHostBuilder` método em `Program.cs` .

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .UseSystemd() // Enable running as a Systemd service
        .ConfigureWebHostDefaults(webBuilder =>
        {
            webBuilder.UseStartup<Startup>();
        });
```

> [!NOTE]
> Se o aplicativo não estiver sendo executado como um serviço do Linux, o `UseSystemd` método não fará nada.

Agora, publique seu aplicativo. O aplicativo pode ser dependente da estrutura ou independente para o tempo de execução do Linux relevante (por exemplo, `linux-x64` ). Você pode publicar usando um destes métodos:

* No Visual Studio, clicando com o botão direito do mouse no projeto e selecionando **publicar** no menu de atalho.
* Na CLI do .NET, usando o seguinte comando:

  ```dotnetcli
  dotnet publish -c Release -r linux-x64 -o ./publish
  ```
  
Copie todo o conteúdo do `publish` diretório para uma pasta de instalação no host do Linux. O registro do serviço requer um arquivo especial, chamado *arquivo de unidade*, a ser adicionado ao `/etc/systemd/system` diretório. Você precisará de permissão de raiz para criar um arquivo nessa pasta. Nomeie o arquivo com o identificador que você deseja `systemd` usar e a `.service` extensão. Por exemplo, use `/etc/systemd/system/myapp.service`.

O arquivo de serviço usa o formato INI, conforme mostrado neste exemplo:

```ini
[Unit]
Description=My gRPC Application

[Service]
Type=notify
ExecStart=/usr/sbin/myapp

[Install]
WantedBy=multi-user.target
```

A `Type=notify` propriedade informa `systemd` que o aplicativo irá notificá-lo na inicialização e no desligamento. A `WantedBy=multi-user.target` configuração fará com que o serviço seja iniciado quando o sistema Linux atingir "runlevel 2", o que significa que um shell de vários usuários não gráficas está ativo.

Antes que `systemd` o reconheça o serviço, ele precisa recarregar sua configuração. Você controla `systemd` usando o `systemctl` comando. Após o recarregamento, use o `status` subcomando para confirmar se o aplicativo foi registrado com êxito.

```console
sudo systemctl daemon-reload
sudo systemctl status myapp
```

Se você tiver configurado o serviço corretamente, obterá a seguinte saída:

```text
myapp.service - My gRPC Application
 Loaded: loaded (/etc/systemd/system/myapp.service; disabled; vendor preset: enabled)
 Active: inactive (dead)
```

Use o `start` comando para iniciar o serviço.

```console
sudo systemctl start myapp.service
```

> [!TIP]
> A `.service` extensão é opcional quando você está usando o `systemctl start` .

Para saber `systemd` como iniciar o serviço automaticamente na inicialização do sistema, use o `enable` comando.

```console
sudo systemctl enable myapp
```

### <a name="log-to-journald"></a>Log no diário

O equivalente do Linux do log de eventos do Windows é `journald` um serviço de sistema de registro em log estruturado que faz parte do `systemd` . As mensagens de log gravadas na saída padrão por um daemon do Linux são gravadas automaticamente no `journald` . Para configurar os níveis de log, use a `Console` seção da configuração de log. O `UseSystemd` método do host Builder configura automaticamente o formato de saída do console para se adequar ao diário.

Como `journald` o é o padrão para logs do Linux, uma variedade de ferramentas integra-se a ele. Você pode facilmente rotear logs do `journald` para um sistema de log externo. Trabalhando localmente no host, você pode usar o `journalctl` comando para exibir os logs da linha de comando.

```console
sudo journalctl -u myapp
```

> [!TIP]
> Se você tiver um ambiente de GUI disponível em seu host, alguns visualizadores de log gráficos estarão disponíveis para Linux, como *QJournalctl* e *logs GNOME*.

Para saber mais sobre como consultar o `systemd` diário na linha de comando usando `journalctl` , consulte [o manpages](https://manpages.debian.org/buster/systemd/journalctl.1).

## <a name="https-certificates-for-self-hosted-applications"></a>Certificados HTTPS para aplicativos de hospedagem interna

Quando você estiver executando um aplicativo gRPC em produção, deverá usar um certificado TLS de uma autoridade de certificação confiável (CA). Essa autoridade de certificação pode ser uma CA pública ou uma interna para sua organização.

Em hosts do Windows, você pode carregar o certificado de um [repositório de certificados](/windows/win32/seccrypto/managing-certificates-with-certificate-stores) seguro usando a <xref:System.Security.Cryptography.X509Certificates.X509Store> classe. Você também pode usar a `X509Store` classe com o armazenamento de chaves OpenSSL em alguns hosts Linux.

Você também pode criar certificados usando um dos [construtores X509Certificate2](xref:System.Security.Cryptography.X509Certificates.X509Certificate2.%23ctor%2A), de:

* Um arquivo, como um `.pfx` arquivo protegido por uma senha forte
* Dados binários recuperados de um serviço de armazenamento seguro, como [Azure Key Vault](https://azure.microsoft.com/services/key-vault/)

Você pode configurar o Kestrel para usar um certificado de duas maneiras: da configuração ou no código.

### <a name="set-https-certificates-by-using-configuration"></a>Definir certificados HTTPS usando a configuração

A abordagem de configuração requer a definição do caminho para o arquivo de certificado `.pfx` e a senha na seção de configuração Kestrel. No `appsettings.json` , isso teria a seguinte aparência:

```json
{
  "Kestrel": {
    "Certificates": {
      "Default": {
        "Path": "cert.pfx",
        "Password": "DO NOT STORE PLAINTEXT PASSWORDS IN APPSETTINGS FILES"
      }
    }
  }
}
```

Forneça a senha usando uma fonte de configuração segura, como o Azure Key Vault ou o cofre Hashicorp.

> [!IMPORTANT]
> Não armazene senhas não criptografadas em arquivos de configuração.

### <a name="set-https-certificates-in-code"></a>Definir certificados HTTPS no código

Para configurar o HTTPS em Kestrel no código, use o `ConfigureKestrel` método em `IWebHostBuilder` na `Program` classe.

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .ConfigureWebHostDefaults(webBuilder =>
        {
            webBuilder.UseStartup<Startup>();
            webBuilder.ConfigureKestrel(kestrel =>
            {
                kestrel.ConfigureHttpsDefaults(https =>
                {
                    https.ServerCertificate = new X509Certificate2("mycert.pfx", "password");
                });
            });
        });
```

Novamente, certifique-se de armazenar a senha do `.pfx` arquivo em e recuperá-la de uma fonte de configuração segura.

>[!div class="step-by-step"]
>[Anterior](grpc-in-production.md) 
> [Avançar](docker.md)
