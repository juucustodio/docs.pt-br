---
description: 'Saiba mais sobre: Configurando seu aplicativo'
title: Configurando seu aplicativo
ms.date: 03/30/2017
ms.assetid: a2f995b0-669d-4721-b00f-4561ec7eb6a4
ms.openlocfilehash: d28876068f23a67ea1ff005d7d217e09b2854783
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646056"
---
# <a name="configuring-your-application"></a>Configurando seu aplicativo

O Windows Communication Foundation (WCF) usa o sistema de configuração do .NET e permite que você configure serviços no escopo do computador e do aplicativo.  
  
 As definições de configuração definidas pelo WCF estão localizadas no `<system.serviceModel>` grupo de seções. Para obter mais informações sobre como configurar um serviço WCF, consulte os seguintes tópicos:  
  
- [Configurando serviços](../configuring-services.md)  
  
- [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md)  
  
 As definições de configurações definidas pelo aplicativo são definidas no `<appSettings>` grupo de seções. Para obter mais informações sobre configurações de aplicativo em arquivos de configuração do .NET, consulte [\<appSettings>](/previous-versions/dotnet/netframework-4.0/ms228154(v=vs.100)) .  
  
## <a name="using-the-configuration-editor"></a>Usando o editor de configuração  

 A ferramenta do editor de configuração do WCF [(SvcConfigEditor.exe)](../configuration-editor-tool-svcconfigeditor-exe.md) permite que administradores e desenvolvedores criem e modifiquem definições de configuração para serviços WCF usando uma interface gráfica do usuário. Com essa ferramenta, você pode gerenciar configurações para associações, comportamentos, serviços e diagnósticos do WCF sem editar diretamente os arquivos de configuração XML.  
  
## <a name="editing-configuration-files-in-visual-studio"></a>Editando arquivos de configuração no Visual Studio  

 Para editar o arquivo de configuração de um projeto de serviço WCF no Visual Studio, clique com o botão direito do mouse no **Gerenciador de soluções** e escolha o item de menu editar o contexto de **configuração do WCF** . Isso inicia a [ferramenta do editor de configuração (SvcConfigEditor.exe)](../configuration-editor-tool-svcconfigeditor-exe.md).  
  
> [!NOTE]
> Se você editar o arquivo de configuração de um projeto de serviço Web WCF no Visual Studio, clicando com o botão direito do mouse no **Gerenciador de soluções**, observe que o item de menu Editar contexto de **configuração do WCF** está ausente. Para solucionar esse problema, clique no menu **ferramentas** e escolha **Editor de configuração do serviço WCF**. Depois disso, você pode clicar com o botão direito do mouse em um arquivo de configuração e usar o item de menu de contexto **Editar configuração do WCF** .  
  
## <a name="see-also"></a>Consulte também

- [Ferramenta Configuration Editor (SvcConfigEditor.exe)](../configuration-editor-tool-svcconfigeditor-exe.md)
- [Configurando serviços](../configuring-services.md)
- [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md)
