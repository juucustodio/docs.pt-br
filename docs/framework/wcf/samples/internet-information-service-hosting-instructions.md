---
description: 'Saiba mais sobre: instruções de hospedagem do serviço de informações da Internet'
title: Instruções de hospedagem de serviço de informação de internet
ms.date: 03/30/2017
ms.assetid: 959a21c8-9d9d-4757-b255-4e57793ae9d6
ms.openlocfilehash: 51f5230ecbb8eaf4a909c5c09366680b8c555165
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99726371"
---
# <a name="internet-information-service-hosting-instructions"></a>Instruções de hospedagem de serviço de informação de internet

Para executar os exemplos hospedados pelo Serviços de Informações da Internet (IIS), você deve verificar se o IIS está instalado corretamente e está em execução.  
  
### <a name="to-install-iis-version-75-on-windows-server-2008-r2"></a>Para instalar o IIS versão 7,5 no Windows Server 2008 R2  
  
1. Em **Gerenciador do servidor**, selecione **funções.** Em **Resumo de funções**, clique em **adicionar funções**.  
  
2. Clique em **Avançar** para exibir a caixa de diálogo **selecionar funções de servidor** .  
  
3. Selecione **servidor de aplicativos** na lista **funções** e clique em **Avançar** duas vezes para exibir a caixa de diálogo **selecionar serviços de função** para a função servidor de aplicativos.  
  
4. Marque a caixa de seleção **servidor Web (IIS)** . Se for solicitado que você instale recursos e serviços de função adicionais, clique em **Adicionar recursos necessários**. Clique em **Avançar** duas vezes para exibir a caixa de diálogo **selecionar serviços de função** para a função do servidor Web (IIS).  
  
5. Expanda **ferramentas de gerenciamento** e, em seguida, expanda **compatibilidade de gerenciamento do IIS 6**. Selecione **ferramentas de script do IIS 6**. Se for solicitado que você instale recursos e serviços de função adicionais, clique em **Adicionar serviços de função necessários**. Clique em **Próximo**.  
  
6. Se o resumo das seleções estiver correto, clique em **instalar**.  
  
7. Quando a instalação for concluída, clique em **fechar**.  
  
### <a name="to-install-iis-version-75-on-windows-7"></a>Para instalar o IIS versão 7,5 no Windows 7  
  
1. Clique em **Iniciar** e em **Painel de Controle**.  
  
2. Abra o grupo **programas** .  
  
3. Em **programas e recursos**, clique em **Ativar ou desativar recursos do Windows**.  
  
4. A caixa de diálogo **controle de conta de usuário** é exibida. Clique em **Continue**.  
  
5. A caixa de diálogo **recursos do Windows** é exibida. Expanda o item rotulado **serviços de informações da Internet**.  
  
6. Expanda o item rotulado **World Wide Web serviços**.  
  
7. Expanda o item rotulado **recursos de desenvolvimento de aplicativos**.  
  
8. Verifique se os seguintes itens estão selecionados:  
  
    1. **Extensibilidade .NET**  
  
    2. **ASP.NET**  
  
    3. **Extensões ISAPI**  
  
    4. **Filtros ISAPI**  
  
9. Sob o item rotulado **World Wide Web serviços**, expanda **recursos http comuns**.  
  
10. Certifique-se de que **conteúdo estático** esteja selecionado.  
  
11. Sob o item rotulado **World Wide Web serviços**, expanda **segurança**.  
  
12. Verifique se a **autenticação do Windows** está selecionada.  
  
13. No diretório **serviços de informações da Internet** , expanda o item rotulado **ferramentas de gerenciamento da Web** e selecione **console de gerenciamento do IIS**.  
  
14. Expanda o item rotulado **compatibilidade de gerenciamento do IIS 6** e, em seguida, selecione **ferramentas de script do IIS 6**.  
  
15. No diretório **serviços de informações da Internet** , expanda o item rotulado **Microsoft .NET Framework 3.5.1** e, em seguida, selecione **Windows Communication Foundation ativação http**.  
  
16. Clique em **OK**.  
  
### <a name="to-install-iis-version-70-on-windows-server-2008"></a>Para instalar o IIS versão 7,0 no Windows Server 2008  
  
1. Em **Gerenciador do servidor**, selecione **funções**. Em **Resumo de funções**, clique em **adicionar funções**.  
  
2. Clique em **Avançar** para exibir a caixa de diálogo **selecionar funções de servidor** .  
  
3. Selecione **servidor de aplicativos** na lista **funções** e clique em **Avançar** duas vezes para exibir a caixa de diálogo **selecionar serviços de função** para a função servidor de aplicativos.  
  
4. Selecione a caixa **de seleção servidor Web (IIS)** . Se for solicitado que você instale recursos e serviços de função adicionais, clique em **Adicionar recursos necessários**. Clique em **Avançar** duas vezes para exibir a caixa de diálogo **selecionar serviços de função** para a função do servidor Web (IIS).  
  
5. Expanda **ferramentas de gerenciamento** e, em seguida, expanda **compatibilidade de gerenciamento do IIS 6**. Selecione **ferramentas de script do IIS 6**. Se for solicitado que você instale recursos e serviços de função adicionais, clique em **Adicionar serviços de função necessários**. Clique em **Próximo**.  
  
6. Se o resumo das seleções estiver correto, clique em **instalar**.  
  
7. Quando a instalação for concluída, clique em **fechar**.  
  
### <a name="to-install-iis-version-70-on-windows-vista"></a>Para instalar o IIS versão 7,0 no Windows Vista  
  
1. Clique em Iniciar e em Painel de Controle.  
  
2. Selecione o grupo **programas** .  
  
3. Em **programas e recursos**, clique em **Ativar ou desativar recursos do Windows**.  
  
4. A caixa de diálogo **controle de conta de usuário** é exibida. Clique em **Continue**.  
  
5. A caixa de diálogo **recursos do Windows** é exibida. Expanda o item rotulado **serviços de informações da Internet**.  
  
6. Expanda o item rotulado **World Wide Web serviços**.  
  
7. Expanda o item rotulado **recursos de desenvolvimento de aplicativos**.  
  
8. Verifique se os seguintes itens estão selecionados:  
  
    1. **Extensibilidade .NET**  
  
    2. **ASP.NET**  
  
    3. **Extensões ISAPI**  
  
    4. **Filtros ISAPI**  
  
9. Expanda o item rotulado **ferramentas de gerenciamento da Web** e selecione **console de gerenciamento do IIS**.  
  
10. Sob o item rotulado **World Wide Web serviços**, expanda **recursos http comuns**.  
  
11. Certifique-se de que **conteúdo estático** esteja selecionado.  
  
12. Sob o item rotulado **World Wide Web serviços**, expanda **segurança**.  
  
13. Verifique se a **autenticação do Windows** está selecionada.  
  
14. Expanda o item rotulado **compatibilidade de gerenciamento do IIS 6** e, em seguida, selecione **ferramentas de script do IIS 6**.  
  
15. Expanda o item rotulado **Microsoft .NET Framework 3,0** e, em seguida, selecione **Windows Communication Foundation ativação http**.  
  
16. Clique em **OK**.  
  
### <a name="to-install-iis-version-60-on-windows-server-2003"></a>Para instalar o IIS versão 6,0 no Windows Server 2003  
  
1. Em **gerenciar seu servidor**, clique em **Adicionar ou remover uma função** e, em seguida, clique em **Avançar**.  
  
2. Selecione **servidor de aplicativos (IIS, ASP.net)** na lista **função de servidor** e clique em **Avançar**.  
  
3. Marque a caixa de seleção **habilitar ASP.net** e clique em **Avançar**.  
  
4. Se o resumo das seleções estiver correto, clique em Avançar.  
  
### <a name="to-install-iis-version-51-on-windows-xp-with-service-pack-2-and-service-pack-3-installed"></a>Para instalar o IIS versão 5,1 no Windows XP com Service Pack 2 e Service Pack 3 instalados  
  
1. No Painel de Controle, clique em **Adicionar ou Remover Programas**.  
  
2. Na caixa de diálogo **Adicionar ou Remover Programas**, clique em **Adicionar/Remover Componentes do Windows**.  
  
3. No **Assistente de componentes do Windows**, marque a caixa de seleção **serviços de informações da Internet (IIS)** e clique em **Avançar**.  
  
4. Se a caixa de diálogo **arquivos necessários** for exibida, insira o disco de instalação do sistema operacional, navegue até a pasta i386 e clique em **OK**.  
  
5. Quando a instalação for concluída, clique em **concluir**.  
  
6. Feche a caixa de diálogo **Adicionar ou remover programas** e, em seguida, feche o **painel de controle**.  
  
### <a name="to-verify-the-installation-of-iis-and-aspnet"></a>Para verificar a instalação do IIS e do ASP.NET  
  
1. Salve o arquivo HTML encontrado no final deste tópico no diretório root \InetPub\wwwroot e nomeie-o como default. aspx.  
  
2. Abra uma janela do navegador.  
  
3. Digite `http://localhost/Default.aspx` na caixa endereço e pressione Enter.  
  
4. Uma página da Web com o texto "Olá, Mundo" deve aparecer.  
  
> [!NOTE]
> Sempre que você instalar uma nova versão do .NET Framework, deverá registrar novamente aspnet_isapi como uma extensão de serviço da Web para o IIS. Para fazer isso, emita o `aspnet_regiis –I –enable` comando.  
  
## <a name="sample-code"></a>Exemplo de código  
  
```xml  
<html>  
   <body>  
       <form >  
           <h3> Hello World  
           </h3>  
       </form>  
   </body>  
</html>  
```
