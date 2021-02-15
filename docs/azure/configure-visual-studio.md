---
title: Configurar o Visual Studio para desenvolvimento do Azure com o .NET
description: Este artigo ajuda você a configurar o Visual Studio para desenvolvimento do Azure, incluindo a obtenção das cargas de trabalho corretas instaladas e a conexão do Visual Studio à sua conta do Azure
ms.date: 11/30/2020
ms.topic: conceptual
ms.custom: devx-track-dotnet
ms.author: daberry
author: daberry
ms.openlocfilehash: 986469bd07657d968045465803047dc21d76dd62
ms.sourcegitcommit: 3d6d6595a03915f617349781f455f838a44b0f44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97701076"
---
# <a name="configure-visual-studio-for-azure-development-with-net"></a>Configurar o Visual Studio para desenvolvimento do Azure com o .NET

O Visual Studio inclui ferramentas para ajudar no desenvolvimento e na implantação de aplicativos no Azure.  Este guia o ajudará a garantir que você tenha o Visual Studio configurado corretamente para o desenvolvimento do Azure.

### <a name="download-visual-studio-2019"></a>Baixar o Visual Studio 2019

Se você já tiver o Visual Studio 2019 instalado, poderá ignorar esta etapa.

> [!div class="nextstepaction"]
> [Baixar o Visual Studio 2019](https://www.visualstudio.com/downloads/)

### <a name="install-azure-workloads"></a>Instalar cargas de trabalho do Azure

Inicie o **instalador do Visual Studio** e valide se você tem as cargas de trabalho **desenvolvimento do Azure** e **ASP.net e desenvolvimento da Web** estão instalados.  Se nenhuma dessas cargas de trabalho não estiver instalada, selecione essas cargas de trabalho para instalá-las.

![Captura de tela da Instalador do Visual Studio mostrando as cargas de trabalho de desenvolvimento do Azure e ASP.NET e desenvolvimento da Web selecionadas](./media/visual-studio-installer-azure-development.png)

### <a name="authenticate-visual-studio-with-azure"></a>Autenticar o Visual Studio com o Azure

Ao depurar aplicativos por meio do Visual Studio, o Visual Studio pode usar sua conta do Azure para autenticar e acessar recursos do Azure com o.  Essa conta também é usada quando você publica aplicativos diretamente do Visual Studio para o Azure.

Para autenticar sua conta do Azure do Visual Studio, selecione o menu opções de **ferramentas**  >   para iniciar a caixa de diálogo **Opções** . Navegue até as `Azure Service Authentication` Opções e entre usando sua conta do Azure.

![Captura de tela da caixa de diálogo opções do Visual Studio mostrando o logon do Azure](./media/visual-studio-azure-login-dialog.png)

### <a name="next-steps"></a>Próximas etapas

Se você também usar [Visual Studio Code](https://code.visualstudio.com/) para desenvolvimento no .net ou em qualquer outra linguagem, também deverá [Configurar o Visual Studio Code para o desenvolvimento do Azure](./configure-vs-code.md). Caso contrário, vá para a [instalação do CLI do Azure](./install-azure-cli.md).
