---
title: Instalar arquivos do IntelliSense localizado
description: Saiba como configurar seu computador de desenvolvimento para usar arquivos do IntelliSense localizados para projetos do .NET 5 + (incluindo o .NET Core) no Visual Studio.
ms.date: 11/06/2020
ms.openlocfilehash: 45eeae12ca79179cacb3d48fca28118de70e0a4f
ms.sourcegitcommit: bc9c63541c3dc756d48a7ce9d22b5583a18cf7fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94506760"
---
# <a name="how-to-install-localized-intellisense-files-for-net"></a>Como instalar arquivos do IntelliSense localizados para .NET

O [IntelliSense](/visualstudio/ide/using-intellisense) é um recurso de conclusão de código que está disponível em ides (ambientes de desenvolvimento integrado) diferentes, como o Visual Studio. Por padrão, quando você está desenvolvendo projetos .NET, o SDK inclui apenas a versão em inglês dos arquivos do IntelliSense. Este artigo explica:

- Como instalar a versão localizada desses arquivos.
- Como modificar a instalação do Visual Studio para usar uma linguagem diferente.

## <a name="prerequisites"></a>Pré-requisitos

- [SDK do .NET Core 3,0](https://dotnet.microsoft.com/download/dotnet-core) ou uma versão posterior, como o [SDK do .NET 5](https://dotnet.microsoft.com/download/dotnet/5.0).
- [Visual Studio 2019 versão 16.3](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) ou uma versão posterior.

## <a name="download-and-install-the-localized-intellisense-files"></a>Baixar e instalar os arquivos do IntelliSense localizado

> [!IMPORTANT]
> Este procedimento requer que você tenha permissão de administrador para copiar os arquivos do IntelliSense para a pasta de instalação do .NET.

1. Acesse a página [Baixar arquivos do IntelliSense](https://dotnet.microsoft.com/download/intellisense).

1. Baixe o arquivo do IntelliSense para a linguagem e a versão que você gostaria de usar.

1. Extraia o conteúdo do arquivo zip.

1. Navegue até a pasta .NET IntelliSense.

   1. Navegue até a pasta de instalação do .NET. Por padrão, ela está em *%ProgramFiles%\dotnet\packs*.
   1. Escolha o SDK para o qual você deseja instalar o IntelliSense e navegue até o caminho associado. Você tem as seguintes opções:

      | Tipo de SDK              | Caminho                               |
      |-----------------------|------------------------------------|
      | .NET 5 + e .NET Core | *Microsoft.NETCore.App.Ref*        |
      | Windows Desktop       | *Microsoft.WindowsDesktop.App.Ref* |
      | .NET Standard         | *NETStandard.Library.Ref*          |

   1. Navegue até a versão para a qual você deseja instalar o IntelliSense localizado. Por exemplo, *5.0.0*.
   1. Abra a pasta *ref*.
   1. Abra a pasta moniker. Por exemplo, *net 5.0*.

   Portanto, o caminho completo que você navegaria seria semelhante a *C:\Program Files\dotnet\packs\Microsoft.NETCore.app.Ref\5.0.0\ref\net5.0*.

1. Crie uma subpasta dentro da pasta moniker que você acabou de abrir. O nome da pasta indica qual linguagem você deseja usar. A tabela a seguir especifica as diferentes opções:

   | Idioma              | Nome da pasta |
   | --------------------- | ----------- |
   | Português (Brasil)  | *pt-br*     |
   | Chinês (simplificado)  | *zh-Hans*   |
   | Chinês (tradicional) | *zh-Hant*   |
   | Francês                | *fr*        |
   | Alemão                | *de*        |
   | Italiano               | *it*        |
   | Japonês              | *ja*        |
   | Coreano                | *ko*        |
   | Russo               | *ru*        |
   | Espanhol               | *es*        |

1. Copie os arquivos *. xml* extraídos na etapa 3 para essa nova pasta. Os arquivos *. xml* são divididos por pastas do SDK, portanto, copie-os para o SDK correspondente que você escolheu na etapa 4.

## <a name="modify-visual-studio-language"></a>Modificar o idioma do Visual Studio

Para que o Visual Studio use um idioma diferente para o IntelliSense, instale o pacote de idiomas apropriado. Isso pode ser feito [durante a instalação](/visualstudio/install/install-visual-studio#step-6---install-language-packs-optional) ou em um momento posterior, modificando a instalação do Visual Studio. Se você já tiver o Visual Studio configurado para o idioma de sua escolha, a instalação do IntelliSense estará pronta.

### <a name="install-the-language-pack"></a>Instalar o pacote de idiomas

Se você não instalou o pacote de idiomas desejado durante a instalação, atualize o Visual Studio da seguinte maneira para instalar o pacote de idiomas:

> [!IMPORTANT]
> Para instalar, atualizar ou modificar o Visual Studio, você deve fazer logon com uma conta que tenha permissão de administrador. Para obter mais informações, consulte [permissões de usuário e Visual Studio](/visualstudio/ide/user-permissions-and-visual-studio).

1. Localize o Instalador do Visual Studio no computador.

   Por exemplo, em um computador que executa o Windows 10, selecione **Iniciar** e, em seguida, role até a letra **I** , onde ele está listado como **Instalador do Visual Studio**.

   ![Abra o Instalador do Visual Studio no Windows](./media/localized-intellisense/vs-installer-windows-start.png)

   > [!NOTE]
   > Também é possível encontrar o Instalador do Visual Studio no seguinte local:
   >
   > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

   Talvez você precise atualizar o instalador antes de continuar. Nesse caso, siga os prompts.

1. No instalador, procure a edição do Visual Studio à qual você deseja adicionar o pacote de idiomas e escolha **Modificar**.

   ![Atualizar ou modificar o Visual Studio](./media/localized-intellisense/vs-installer-modify.png)

   > [!IMPORTANT]
   > Se você não vir um botão **Modificar** , mas vir um **Atualizar** , será necessário atualizar seu Visual Studio antes de poder modificar sua instalação.
   > Depois que a atualização for concluída, o botão **Modificar** deverá ser exibido.

1. Na guia **Pacotes de idiomas** , selecione ou cancele a seleção dos idiomas que você deseja instalar ou desinstalar.

   ![Guia de pacotes de idiomas do Visual Studio](./media/localized-intellisense/vs-modify-language-packs.png)

1. Escolha **Modificar**. A atualização será iniciada.

### <a name="modify-language-settings-in-visual-studio"></a>Modificar as configurações de idioma no Visual Studio

Depois de instalar os pacotes de idiomas desejados, modifique suas configurações do Visual Studio para usar um idioma diferente:

1. Abra o Visual Studio.

1. Na janela de início, escolha **Continuar sem código**.

1. Na barra de menus, selecione **Ferramentas** > **Opções**. A caixa de diálogo Opções é aberta.

1. No nó **ambiente** , escolha **configurações internacionais**.

1. No menu suspenso **Idioma** , selecione o idioma desejado. Selecione **OK**.

1. Uma caixa de diálogo informa que você precisa reiniciar o Visual Studio para que as alterações entrem em vigor. Selecione **OK**.

1. Reinicie o Visual Studio.

Depois disso, o IntelliSense deve funcionar conforme o esperado quando você abre um projeto do .NET que tem como alvo a versão dos arquivos do IntelliSense que você acabou de instalar.

## <a name="see-also"></a>Confira também

- [IntelliSense no Visual Studio](/visualstudio/ide/using-intellisense)
