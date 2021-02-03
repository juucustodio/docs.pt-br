---
title: 'Tutorial: Colocar em contêiner um aplicativo com o Docker'
description: Neste tutorial, você aprenderá a colocar em contêiner um aplicativo .NET Core com o Docker.
ms.date: 04/27/2020
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 32ac736daa4d6cdebb6d4bdeccf3f8ba954a5721
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505407"
---
# <a name="tutorial-containerize-a-net-core-app"></a>Tutorial: Colocar um aplicativo .NET Core em contêineres

Neste tutorial, você aprenderá a colocar em contêiner um aplicativo .NET Core com o Docker. Os contêineres têm muitos recursos e benefícios, como uma infraestrutura imutável, fornecendo uma arquitetura portátil e habilitando a escalabilidade. A imagem pode ser usada para criar contêineres para seu ambiente de desenvolvimento local, nuvem privada ou nuvem pública.

Neste tutorial, você:

> [!div class="checklist"]
>
> - Criar e publicar um aplicativo .NET Core simples
> - Criar e configurar um Dockerfile para .NET Core
> - Compilar uma imagem do docker
> - Criar e executar um contêiner do Docker

Você aprenderá as tarefas de build e implantação de contêiner do Docker para um aplicativo .NET Core. A *plataforma Docker* usa o *Mecanismo do Docker* para criar e empacotar aplicativos como *imagens do Docker* com agilidade. Essas imagens são gravadas no formato *Dockerfile* para serem implantadas e executadas em um contêiner em camadas.

> [!NOTE]
> Este tutorial **não é** para aplicativos ASP.NET Core. Se você estiver usando ASP.NET Core, consulte o tutorial [saiba como colocar um aplicativo em contêineres de ASP.NET Core](/aspnet/core/host-and-deploy/docker/building-net-docker-images) .

## <a name="prerequisites"></a>Pré-requisitos

Instale os seguintes pré-requisitos:

- [SDK do .NET Core 5,0](https://dotnet.microsoft.com/download)\
Se você tiver o .NET Core instalado, use o comando `dotnet --info` para determinar qual SDK está usando.
- [Docking Community Edition](https://www.docker.com/products/docker-desktop)
- Uma pasta de trabalho temporária para o *Dockerfile* e o aplicativo de exemplo do .NET Core. Neste tutorial, o nome *Docker – Working* é usado como a pasta de trabalho.

## <a name="create-net-core-app"></a>Criar aplicativo .NET Core

Você precisa de um aplicativo .NET Core que o contêiner do Docker irá executar. Abra seu terminal, crie uma pasta de trabalho se você ainda não fez isso e entre nela. Na pasta de trabalho, execute o seguinte comando para criar um novo projeto em um subdiretório chamado *app*:

```dotnetcli
dotnet new console -o App -n NetCore.Docker
```

A árvore de pastas terá aparência semelhante à seguinte:

```
docker-working
    └──App
        ├──NetCore.Docker.csproj
        ├──Program.cs
        └──obj
            ├──NetCore.Docker.csproj.nuget.dgspec.json
            ├──NetCore.Docker.csproj.nuget.g.props
            ├──NetCore.Docker.csproj.nuget.g.targets
            ├──project.assets.json
            └──project.nuget.cache
```

O `dotnet new` comando cria uma nova pasta chamada *app* e gera um aplicativo de console "Olá, mundo". Altere os diretórios e navegue até a pasta do *aplicativo* de sua sessão de terminal. Use o `dotnet run` comando para iniciar o aplicativo. O aplicativo será executado e imprimirá `Hello World!` abaixo do comando:

```dotnetcli
dotnet run
Hello World!
```

O modelo padrão cria um aplicativo que é impresso no terminal e, em seguida, termina imediatamente. Neste tutorial, você usará um aplicativo que faz um loop indefinidamente. Abra o arquivo *Program.cs* em um editor de texto.

> [!TIP]
> Se você estiver usando Visual Studio Code, na sessão de terminal anterior, digite o seguinte comando:
>
> ```console
> code .
> ```
>
> Isso abrirá a pasta do *aplicativo* que contém o projeto no Visual Studio Code.

O *Program.cs* deve ser semelhante ao seguinte código C#:

```csharp
using System;

namespace NetCore.Docker
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

Substitua o arquivo pelo seguinte código que conta os números a cada segundo:

```csharp
using System;
using System.Threading.Tasks;

namespace NetCore.Docker
{
    class Program
    {
        static async Task Main(string[] args)
        {
            var counter = 0;
            var max = args.Length != 0 ? Convert.ToInt32(args[0]) : -1;
            while (max == -1 || counter < max)
            {
                Console.WriteLine($"Counter: {++counter}");
                await Task.Delay(1000);
            }
        }
    }
}
```

Salve o arquivo e teste o programa novamente com `dotnet run`. Lembre-se de que esse aplicativo é executado indefinidamente. Use o comando Cancel <kbd>Ctrl + C</kbd> para interrompê-lo. Veja a seguir um exemplo de saída:

```dotnetcli
dotnet run
Counter: 1
Counter: 2
Counter: 3
Counter: 4
^C
```

Se você passar um número na linha de comando para o aplicativo, ele apenas contará até tal valor e, em seguida, sairá. Experimente com `dotnet run -- 5` para contar até cinco.

> [!IMPORTANT]
> Quaisquer parâmetros após `--` não são passados para o comando `dotnet run` e, em vez disso, são passados para o aplicativo.

## <a name="publish-net-core-app"></a>Publicar um aplicativo .NET Core

Antes de adicionar o aplicativo .NET Core à imagem do Docker, primeiro ele deve ser publicado. É melhor fazer com que o contêiner execute a versão publicada do aplicativo. Para publicar o aplicativo, execute o seguinte comando:

```dotnetcli
dotnet publish -c Release
```

Esse comando compila seu aplicativo para a pasta *publish*. O caminho para a pasta *publish* da pasta de trabalho deve ser `.\App\bin\Release\netcoreapp5.0\publish\`

#### <a name="windows"></a>[Windows](#tab/windows)

Na pasta do *aplicativo* , obtenha uma listagem de diretório da pasta de publicação para verificar se o arquivo de *NetCore.Docker.dll* foi criado.

```powershell
dir .\bin\Release\netcoreapp5.0\publish\

    Directory: C:\Users\dapine\App\bin\Release\netcoreapp5.0\publish

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        4/27/2020   8:27 AM            434 NetCore.Docker.deps.json
-a----        4/27/2020   8:27 AM           6144 NetCore.Docker.dll
-a----        4/27/2020   8:27 AM         171520 NetCore.Docker.exe
-a----        4/27/2020   8:27 AM            860 NetCore.Docker.pdb
-a----        4/27/2020   8:27 AM            154 NetCore.Docker.runtimeconfig.json
```

#### <a name="linux"></a>[Linux](#tab/linux)

Use o `ls` comando para obter uma listagem de diretório e verificar se o arquivo de *NetCore.Docker.dll* foi criado.

```bash
me@DESKTOP:/docker-working/app$ ls bin/Release/netcoreapp5.0/publish
NetCore.Docker.deps.json  NetCore.Docker.dll  NetCore.Docker.pdb  NetCore.Docker.runtimeconfig.json
```

---

## <a name="create-the-dockerfile"></a>Criar o Dockerfile

O arquivo *Dockerfile* é usado pelo comando `docker build` para criar uma imagem de contêiner. Esse arquivo é um arquivo de texto chamado *Dockerfile* que não tem uma extensão.

Crie um arquivo chamado *Dockerfile* no diretório que contém o *. csproj* e abra-o em um editor de texto. Este tutorial usará a imagem do ASP.NET Core Runtime (que contém a imagem do tempo de execução do .NET Core) e corresponde ao aplicativo de console do .NET Core.

```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:5.0
```

> [!NOTE]
> A imagem de tempo de execução ASP.NET Core é usada intencionalmente aqui, embora a `mcr.microsoft.com/dotnet/runtime:5.0` imagem possa ter sido usada.

A `FROM` palavra-chave requer um nome de imagem de contêiner do Docker totalmente qualificado. O registro de contêiner da Microsoft (MCR, mcr.microsoft.com) é uma agregação do Hub do Docker, que hospeda contêineres publicamente acessíveis. O `dotnet/core` segmento é o repositório de contêiner, onde o `aspnet` segmento é o nome da imagem de contêiner. A imagem é marcada com `5.0` , que é usada para controle de versão. Portanto, `mcr.microsoft.com/dotnet/aspnet:5.0` é o tempo de execução do .NET Core 5,0. Certifique-se de extrair a versão de tempo de execução que corresponde ao tempo de execução direcionado pelo seu SDK. Por exemplo, o aplicativo criado na seção anterior usava o SDK do .NET Core 5,0 e a imagem base mencionada no *Dockerfile* é marcada com **5,0**.

Salve o arquivo *Dockerfile*. A estrutura de diretório da pasta de trabalho deve ser semelhante à mostrada a seguir. Alguns arquivos e pastas de nível mais profundo foram omitidos para economizar espaço no artigo:

```
docker-working
    └──App
        ├──Dockerfile
        ├──NetCore.Docker.csproj
        ├──Program.cs
        ├──bin
        │   └──Release
        │       └──netcoreapp5.0
        │           └──publish
        │               ├──NetCore.Docker.deps.json
        │               ├──NetCore.Docker.exe
        │               ├──NetCore.Docker.dll
        │               ├──NetCore.Docker.pdb
        │               └──NetCore.Docker.runtimeconfig.json
        └──obj
            └──...
```

Do terminal, execute o seguinte comando:

```console
docker build -t counter-image -f Dockerfile .
```

O Docker processará cada linha no *Dockerfile*. O `.` no comando `docker build` instrui o Docker a usar a pasta atual para encontrar um *Dockerfile*. Esse comando cria a imagem e cria um repositório local chamado **Counter-Image** que aponta para essa imagem. Após a conclusão desse comando, execute `docker images` para ver uma lista de imagens instaladas:

```console
docker images
REPOSITORY                              TAG                 IMAGE ID            CREATED             SIZE
counter-image                           latest              e6780479db63        4 days ago          190MB
mcr.microsoft.com/dotnet/aspnet         5.0                 e6780479db63        4 days ago          190MB
```

Observe que as duas imagens compartilham o mesmo valor de **ID DA IMAGEM**. O valor é o mesmo entre as duas imagens porque o único comando no *Dockerfile* era basear a nova imagem em uma imagem existente. Vamos adicionar três comandos ao *Dockerfile*. Cada comando cria uma nova camada de imagem com o comando final que representa os pontos de entrada do repositório de **imagem de contador** para.

```dockerfile
COPY bin/Release/netcoreapp5.0/publish/ App/
WORKDIR /App
ENTRYPOINT ["dotnet", "NetCore.Docker.dll"]
```

O comando `COPY` informa ao Docker para copiar a pasta especificada em seu computador para uma pasta no contêiner. Neste exemplo, a pasta de *publicação* é copiada para uma pasta chamada *aplicativo* no contêiner.

O `WORKDIR` comando altera o **diretório atual** dentro do contêiner para o *aplicativo*.

O comando seguinte, `ENTRYPOINT`, informa ao Docker para configurar o contêiner para ser executado como um executável. Quando o contêiner é iniciado, o comando `ENTRYPOINT` é executado. Quando esse comando terminar, o contêiner será interrompido automaticamente.

No seu terminal, execute `docker build -t counter-image -f Dockerfile .` e, quando o comando terminar, execute `docker images`.

```console
docker build -t counter-image -f Dockerfile .
Sending build context to Docker daemon  1.117MB
Step 1/4 : FROM mcr.microsoft.com/dotnet/aspnet:5.0
 ---> e6780479db63
Step 2/4 : COPY bin/Release/netcoreapp5.0/publish/ App/
 ---> d1732740eed2
Step 3/4 : WORKDIR /App
 ---> Running in b1701a42f3ff
Removing intermediate container b1701a42f3ff
 ---> 919aab5b95e3
Step 4/4 : ENTRYPOINT ["dotnet", "NetCore.Docker.dll"]
 ---> Running in c12aebd26ced
Removing intermediate container c12aebd26ced
 ---> cd11c3df9b19
Successfully built cd11c3df9b19
Successfully tagged counter-image:latest

docker images
REPOSITORY                              TAG                 IMAGE ID            CREATED             SIZE
counter-image                           latest              cd11c3df9b19        41 seconds ago      190MB
mcr.microsoft.com/dotnet/aspnet         5.0                 e6780479db63        4 days ago          190MB
```

Cada comando no *Dockerfile* gerou uma camada e criou uma **ID DA IMAGEM**. A **ID da imagem** final (a sua será diferente) é **cd11c3df9b19** e, em seguida, você criará um contêiner com base nessa imagem.

## <a name="create-a-container"></a>Criar um contêiner

Agora que você tem uma imagem que contém o seu aplicativo, você pode criar um contêiner. Você pode criar um contêiner de duas maneiras. Primeiro, criar um novo contêiner que foi interrompido.

```console
docker create --name core-counter counter-image
0f281cb3af994fba5d962cc7d482828484ea14ead6bfe386a35e5088c0058851
```

O `docker create` comando acima criará um contêiner com base na imagem do **contador-imagem** . A saída desse comando mostra a **ID DO CONTÊINER** (a sua será diferente) do contêiner criado. Para ver uma lista de *todos* os contêineres, use o comando `docker ps -a`:

```console
docker ps -a
CONTAINER ID    IMAGE            COMMAND                   CREATED           STATUS     PORTS    NAMES
0f281cb3af99    counter-image    "dotnet NetCore.Dock…"    40 seconds ago    Created             core-counter
```

### <a name="manage-the-container"></a>Gerenciar o contêiner

O contêiner foi criado com um nome específico `core-counter` , esse nome é usado para gerenciar o contêiner. O exemplo a seguir usa o comando `docker start` para iniciar o contêiner e, em seguida, usa o comando `docker ps` para mostrar apenas os contêineres em execução:

```console
docker start core-counter
core-counter

docker ps
CONTAINER ID    IMAGE            COMMAND                   CREATED          STATUS          PORTS    NAMES
2f6424a7ddce    counter-image    "dotnet NetCore.Dock…"    2 minutes ago    Up 11 seconds            core-counter
```

Da mesma forma, o comando `docker stop` interromperá o contêiner. O exemplo a seguir usa o `docker stop` comando para parar o contêiner e, em seguida, usa o `docker ps` comando para mostrar que nenhum contêiner está em execução:

```console
docker stop core-counter
core-counter

docker ps
CONTAINER ID    IMAGE    COMMAND    CREATED    STATUS    PORTS    NAMES
```

### <a name="connect-to-a-container"></a>Conectar-se a um contêiner

Depois que um contêiner estiver em execução, você poderá se conectar a ele para ver a saída. Use os comandos `docker start` e `docker attach` para iniciar o contêiner e inspecionar o fluxo de saída. Neste exemplo, a tecla <kbd>Ctrl + C</kbd> é usada para desanexar do contêiner em execução. Esse pressionamento de teclas encerrará o processo no contêiner, a menos que especificado de outra forma, o que interromperia o contêiner. O `--sig-proxy=false` parâmetro garante que <kbd>Ctrl + C</kbd> não pare o processo no contêiner.

Depois de desanexar do contêiner, reanexe para verificar se ele ainda está em execução e contando.

```console
docker start core-counter
core-counter

docker attach --sig-proxy=false core-counter
Counter: 7
Counter: 8
Counter: 9
^C

docker attach --sig-proxy=false core-counter
Counter: 17
Counter: 18
Counter: 19
^C
```

### <a name="delete-a-container"></a>Excluir um contêiner

Para os fins desse artigo, você não quer contêineres sem função alguma. Exclua o contêiner que você criou anteriormente. Se o contêiner estiver em execução, interrompa-o.

```console
docker stop core-counter
```

O exemplo a seguir lista todos os contêineres. Em seguida, ele usa o comando `docker rm` para excluir o contêiner e, em seguida, verifica uma segunda vez para verificar qualquer contêiner em execução.

```console
docker ps -a
CONTAINER ID    IMAGE            COMMAND                   CREATED          STATUS                        PORTS    NAMES
2f6424a7ddce    counter-image    "dotnet NetCore.Dock…"    7 minutes ago    Exited (143) 20 seconds ago            core-counter

docker rm core-counter
core-counter

docker ps -a
CONTAINER ID    IMAGE    COMMAND    CREATED    STATUS    PORTS    NAMES
```

### <a name="single-run"></a>Execução única

O Docker fornece o comando `docker run` para criar e executar o contêiner como um único comando. Este comando elimina a necessidade de executar `docker create` e, em seguida, `docker start`. Você também pode definir esse comando para excluir automaticamente o contêiner quando o contêiner for interrompido. Por exemplo, use `docker run -it --rm` para fazer duas coisas: primeiro, use automaticamente o terminal atual para se conectar ao contêiner e, quando o contêiner terminar, remova-o:

```console
docker run -it --rm counter-image
Counter: 1
Counter: 2
Counter: 3
Counter: 4
Counter: 5
^C
```

O contêiner também passa parâmetros para a execução do aplicativo .NET Core. Para instruir o aplicativo .NET Core a contar apenas a 3 passagens 3.

```console
docker run -it --rm counter-image 3
Counter: 1
Counter: 2
Counter: 3
```

Com `docker run -it` o, o comando <kbd>Ctrl + C</kbd> interromperá o processo que está sendo executado no contêiner, o que, por sua vez, interromperá o contêiner. Como o parâmetro `--rm` foi fornecido, o contêiner é automaticamente excluído quando o processo é interrompido. Verifique se ele não existe:

```console
docker ps -a
CONTAINER ID    IMAGE    COMMAND    CREATED    STATUS    PORTS    NAMES
```

### <a name="change-the-entrypoint"></a>Alterar o ENTRYPOINT

O comando `docker run` também permite modificar o comando `ENTRYPOINT` do *Dockerfile* e executar outra coisa, mas apenas para esse contêiner. Por exemplo, use o seguinte comando para executar `bash` ou `cmd.exe`. Edite o comando conforme necessário.

#### <a name="windows"></a>[Windows](#tab/windows)

Neste exemplo, `ENTRYPOINT` é alterado para `cmd.exe`. <kbd>Ctrl + C</kbd> é pressionado para encerrar o processo e parar o contêiner.

```console
docker run -it --rm --entrypoint "cmd.exe" counter-image

Microsoft Windows [Version 10.0.17763.379]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\>dir
 Volume in drive C has no label.
 Volume Serial Number is 3005-1E84

 Directory of C:\

04/09/2019  08:46 AM    <DIR>          app
03/07/2019  10:25 AM             5,510 License.txt
04/02/2019  01:35 PM    <DIR>          Program Files
04/09/2019  01:06 PM    <DIR>          Users
04/02/2019  01:35 PM    <DIR>          Windows
               1 File(s)          5,510 bytes
               4 Dir(s)  21,246,517,248 bytes free

C:\>^C
```

#### <a name="linux"></a>[Linux](#tab/linux)

Neste exemplo, `ENTRYPOINT` é alterado para `bash`. O comando `exit` é executado, o que encerra o processo e interrompe o contêiner.

```bash
docker run -it --rm --entrypoint "bash" counter-image
root@b735b9799abf:/App# ls
NetCore.Docker.deps.json  NetCore.Docker.dll  NetCore.Docker.exe  NetCore.Docker.pdb  NetCore.Docker.runtimeconfig.json
root@b735b9799abf:/App# dotnet NetCore.Docker.dll 3
Counter: 1
Counter: 2
Counter: 3
root@b735b9799abf:/App# exit
exit
```

---

## <a name="essential-commands"></a>Comandos essenciais

O Docker tem muitos comandos diferentes que criam, gerenciam e interagem com contêineres e imagens. Esses comandos do Docker são essenciais para gerenciar seus contêineres:

- [docker build](https://docs.docker.com/engine/reference/commandline/build/)
- [docker run](https://docs.docker.com/engine/reference/commandline/run/)
- [docker ps](https://docs.docker.com/engine/reference/commandline/ps/)
- [docker stop](https://docs.docker.com/engine/reference/commandline/stop/)
- [docker rm](https://docs.docker.com/engine/reference/commandline/rm/)
- [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/)
- [imagem do Docker](https://docs.docker.com/engine/reference/commandline/image/)

## <a name="clean-up-resources"></a>Limpar os recursos

Durante este tutorial, você criou contêineres e imagens. Se quiser, exclua esses recursos. Use os seguintes comandos para:

01. Listar todos os contêineres

    ```console
    docker ps -a
    ```

02. Interrompa os contêineres que estão sendo executados por seu nome.

    ```console
    docker stop counter-image
    ```

03. Excluir o contêiner

    ```console
    docker rm counter-image
    ```

Em seguida, exclua todas as imagens que você não deseja mais em seu computador. Exclua a imagem criada pelo seu *Dockerfile* e exclua a imagem do .NET Core na qual o *Dockerfile* teve base. Você pode usar a **ID DA IMAGEM** ou a cadeia de caracteres formatada **REPOSITÓRIO:TAG**.

```console
docker rmi counter-image:latest
docker rmi mcr.microsoft.com/dotnet/aspnet:5.0
```

Use o comando `docker images` para ver uma lista de imagens instaladas.

> [!TIP]
> Arquivos de imagem podem ser grandes. Normalmente, você removeria contêineres temporários criados durante o teste e o desenvolvimento de seu aplicativo. Em geral, mantenha as imagens de base com o runtime instalado se você planeja construir outras imagens com base nesse runtime.

## <a name="next-steps"></a>Próximas etapas

- [Aprenda a colocar em contêiner um aplicativo ASP.NET Core.](/aspnet/core/host-and-deploy/docker/building-net-docker-images)
- [Experimentar o Tutorial de Microsserviço do ASP.NET Core.](https://dotnet.microsoft.com/learn/web/aspnet-microservice-tutorial/intro)
- [Revisar os serviços do Azure que oferecem suporte a contêineres.](https://azure.microsoft.com/overview/containers/)
- [Ler mais sobre os comandos do Dockerfile.](https://docs.docker.com/engine/reference/builder/)
- [Explore as Ferramentas de Contêiner para Visual Studio](/visualstudio/containers/overview)
