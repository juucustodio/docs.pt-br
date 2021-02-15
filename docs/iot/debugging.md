---
title: Depurar aplicativos .NET no Raspberry Pi
description: Saiba como depurar aplicativos .NET no Raspberry Pi e dispositivos semelhantes.
author: camsoper
ms.author: casoper
ms.date: 11/13/2020
ms.topic: how-to
ms.prod: dotnet
zone_pivot_groups: ide-set-one
ms.openlocfilehash: 7b9872304ee53071452772e3da02081a7def4d80
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2020
ms.locfileid: "96585602"
---
# <a name="debug-net-apps-on-raspberry-pi"></a>Depurar aplicativos .NET no Raspberry Pi

A depuração de aplicativos .NET executados em dispositivos IoT baseados em ARM como o Raspberry Pi apresenta um desafio exclusivo. É possível desenvolver aplicativos .NET em dispositivos ARM. No entanto, OmniSharp, que é necessário para depurar aplicativos .NET fora do Visual Studio, não é compatível com dispositivos ARM. Como resultado, os aplicativos devem ser depurados remotamente de uma plataforma compatível.

::: zone pivot="vscode"

## <a name="debug-from-visual-studio-code-cross-platform"></a>Depurar de Visual Studio Code (plataforma cruzada)

A depuração do .NET no Raspberry Pi de Visual Studio Code requer etapas de configuração no Raspberry Pi e nalaunch.jsdo projeto *no* arquivo.

### <a name="enable-ssh-on-the-raspberry-pi"></a>Habilitar o SSH no Raspberry Pi

O SSH é necessário para a depuração remota. Para habilitar o SSH, [consulte *habilitar o ssh* na documentação do Raspberry Pi](https://www.raspberrypi.org/documentation/remote-access/ssh/) <span class="docon docon-navigate-external x-hidden-focus"></span> .

### <a name="install-the-visual-studio-remote-debugger-on-the-raspberry-pi"></a>Instalar o Depurador Remoto do Visual Studio no Raspberry Pi

Em um console bash no Raspberry Pi (localmente ou via SSH), conclua as seguintes etapas:

1. Execute o comando a seguir para baixar e instalar o Depurador Remoto do Visual Studio no Raspberry Pi:

    ```bash
    curl -sSL https://aka.ms/getvsdbgsh | /bin/sh /dev/stdin -v latest -l ~/vsdbg
    ```

1. O depurador requer a execução de as `root` . Por padrão, o `root` não tem senha no Raspberry Pi. Defina uma senha para `root` executando o comando a seguir e seguindo os prompts.

    ```bash
    sudo passwd root
    ```

1. Visual Studio Code usa o protocolo SSH para depurar remotamente. Para fins de segurança, o `root` não tem permissão para fazer logon via SSH por padrão. Para habilitar `root` o logon via SSH, conclua as seguintes etapas:

    1. Execute o seguinte comando para abrir */etc/ssh/sshd_config* no [nano](https://www.nano-editor.org/docs.php) <span class="docon docon-navigate-external x-hidden-focus"></span> .

        ```bash
        sudo nano /etc/ssh/sshd_config
        ```

    1. Pressione <kbd>Ctrl + W</kbd> e procure por **PermitRootLogin**.
    1. Remova a marca de comentário da linha com **PermitRootLogin** , se necessário.
    1. Altere a linha para ler da seguinte maneira:

        ```console
        PermitRootLogin yes
        ```

        > [!NOTE]
        > Se não houver nenhuma linha **PermitRootLogin** no */etc/ssh/sshd_config*, adicione uma nova linha com o valor mostrado acima.

    1. Pressione <kbd>Ctrl + X</kbd> para sair e salvar suas chances. Quando solicitado, **salve o buffer modificado?**, pressione <kbd>Y</kbd> para confirmar. Pressione <kbd>Enter</kbd> para confirmar a substituição do arquivo original.
    1. Reinicialize o Raspberry Pi executando o seguinte comando:

        ```bash
        sudo reboot
        ```

### <a name="setup-launchjson-in-visual-studio-code"></a>launch.jsde instalação no Visual Studio Code

Adicione uma configuração de inicialização àlaunch.jsdo projeto *em*. Se o projeto não tiver um *launch.jsno* arquivo, adicione um, alternando para a guia **executar** , selecionando **criar um launch.jsno arquivo** e selecionando **.net** ou **.NET Core** na caixa de diálogo.

A nova configuração no *launch.jsem* deve ser semelhante a esta:

```json
"configurations": [
    {
        "name": ".NET Core Launch (remote console)",
        "type": "coreclr",
        "request": "launch",
        "preLaunchTask": "build",
        "program": "/home/pi/.dotnet/dotnet",
        "args": ["/home/pi/sample/Sample.dll"],
        "cwd": "/home/pi/sample",
        "stopAtEntry": false,
        "console": "internalConsole",
        "pipeTransport": {
            "pipeCwd": "${workspaceFolder}",
            "pipeProgram": "C:\\Program Files\\PuTTY\\PLINK.EXE",
            "pipeArgs": [
                "-pw",
                "P@ssw0rd",
                "root@raspberrypi"
            ],
            "debuggerPath": "/home/pi/vsdbg/vsdbg"
        }
    },
```

Observe o seguinte:

- `program` é o caminho para o tempo de execução do .NET no PI.
- `args` é o caminho para o assembly a ser depurado no PI.
- `cwd` é o diretório de trabalho a ser usado ao iniciar o aplicativo no PI.
- `pipeProgram` é o caminho para um cliente SSH no computador local.
- `pipeArgs` são os parâmetros a serem passados para o cliente SSH. Certifique-se de especificar o parâmetro de senha, bem como o `root` usuário no formato `<user>@<hostname>` .

> [!IMPORTANT]
> O exemplo acima usa *plink*, um componente do cliente SSH [de saída](https://www.ssh.com/ssh/putty/) <span class="docon docon-navigate-external x-hidden-focus"></span> . O [OpenSSH](https://www.openssh.com/) <span class="docon docon-navigate-external x-hidden-focus"></span> , que está incluído nas versões recentes do Windows e do Linux, pode ser usado em vez disso. No entanto, o OpenSSH não dá suporte ao envio de senhas como um parâmetro de linha de comando. Para usar o OpenSSH, [configure seu Raspberry Pi para acesso de SSH com senha](https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md) <span class="docon docon-navigate-external x-hidden-focus"></span> .

### <a name="deploy-the-app"></a>Implantar o aplicativo

Implante o aplicativo conforme descrito em [implantar aplicativos .net no Raspberry Pi](deployment.md). Verifique se o caminho de implantação é o mesmo caminho especificado no `cwd` parâmetro no *launch.jsna* configuração.

### <a name="launch-the-debugger"></a>Iniciar o depurador

Na guia **executar** , selecione a configuração **inicialização do .NET Core (console remoto)** e selecione **Iniciar Depuração**. O aplicativo é iniciado no Raspberry Pi. O depurador pode ser usado para definir pontos de interrupção, inspecionar locais e muito mais.

## <a name="references"></a>Referências

[Depuração remota com vs Code no Windows para um Raspberry Pi usando o .NET Core no ARM](https://www.hanselman.com/blog/remote-debugging-with-vs-code-on-windows-to-a-raspberry-pi-using-net-core-on-arm)<span class="docon docon-navigate-external x-hidden-focus"></span>

::: zone-end

::: zone pivot="visualstudio"

## <a name="debug-from-visual-studio-on-windows"></a>Depurar do Visual Studio no Windows

O Visual Studio pode depurar aplicativos .NET em dispositivos remotos via SSH. Nenhuma configuração especializada é necessária no dispositivo. Para obter detalhes sobre como usar o Visual Studio para depurar o .NET remotamente, consulte [depuração remota do .net no Linux usando SSH](/visualstudio/debugger/remote-debugging-dotnet-core-linux-with-ssh?view=vs-2019).

::: zone-end
