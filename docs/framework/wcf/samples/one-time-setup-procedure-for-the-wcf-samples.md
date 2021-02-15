---
description: 'Saiba mais sobre: One-Time procedimento de instalação para os exemplos de Windows Communication Foundation'
title: Procedimento de configuração único para exemplos do Windows Communication Foundation
ms.date: 03/30/2017
ms.assetid: a5848ffd-3eb5-432d-812e-bd948ccb6bca
ms.openlocfilehash: 8d57da5e018a61c6d11c9a9dc319ee74ec19d2ac
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99752087"
---
# <a name="one-time-setup-procedure-for-the-windows-communication-foundation-samples"></a>Procedimento de configuração único para exemplos do Windows Communication Foundation

A maioria dos exemplos de Windows Communication Foundation (WCF) são hospedados no Serviços de Informações da Internet (IIS) e executados a partir de um diretório virtual comum. Este procedimento de configuração única cria uma pasta no disco; Ele também adiciona um diretório virtual ao IIS chamado **ServiceModelSamples**.

O diretório virtual **ServiceModelSamples** é usado para compilar e executar todos os exemplos que usam um serviço hospedado pelo IIS. Esse é o único diretório virtual que é necessário para executar os exemplos. A criação de um exemplo substituirá qualquer serviço implantado anteriormente neste diretório virtual; somente o exemplo criado mais recentemente será implantado e estará disponível neste diretório virtual.

> [!NOTE]
> Você deve executar todos os comandos em uma conta de administrador local. Se você estiver usando o Windows 7, o Windows Vista ou o Windows Server 2008 R2, também deverá executar o prompt de comando com privilégios elevados. Para fazer isso, clique com o botão direito do mouse no ícone do prompt de comando e clique em **Executar como administrador**. Todos os comandos neste tópico devem ser executados em um prompt de comando que tenha as configurações de caminho apropriadas.  A maneira mais fácil de garantir isso é usando o prompt de comando do Visual Studio. Para abrir este prompt, clique em **Iniciar**, **Selecione todos os programas**, role para baixo até o **Visual Studio 2010**, selecione **Ferramentas do Visual Studio**, clique com o botão direito do mouse em prompt de **comando do Visual Studio (2010)** e clique em **Executar como administrador**. Se você tiver uma das edições do Visual Studio Express instaladas, esse prompt de comando não estará disponível e você terá que adicionar "C:\Windows\Microsoft.Net\Framework\v4.0" ao caminho do sistema.

### <a name="one-time-setup-procedure-for-wcf-samples"></a>Procedimento de configuração única para exemplos do WCF

1. Verifique se o ASP.NET está configurado. Para obter mais informações sobre como configurar o ASP.NET, consulte [instruções de hospedagem do serviço de informações da Internet](internet-information-service-hosting-instructions.md).

2. Verifique se o .NET Framework 4 está instalado. Pesquise o seguinte diretório para o v 4.0 (ou posterior): **\Windows\Microsoft.NET\Framework**

3. Verifique se você tem o Visual Studio 2012 ou posterior instalado ou se o seu sistema operacional é o Windows Server 2008 SP2 ou posterior.

4. Execute os seguintes comandos. Para obter mais informações sobre por que esses comandos devem ser executados, consulte [falha do IIS Hosted Service](/previous-versions/dotnet/netframework-3.5/ms752252(v=vs.90)).

    > [!WARNING]
    > Se o IIS for reinstalado, os comandos a seguir precisarão ser executados novamente.

    ```console
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\aspnet_regiis" –i –enable
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\ServiceModelReg.exe" -r
    ```

    > [!WARNING]
    > A execução do comando `aspnet_regiis –i –enable` fará com que o pool de aplicativos padrão seja executado usando .NET Framework 4, o que pode produzir problemas de incompatibilidade para outros aplicativos no mesmo computador.

5. Siga as [instruções de firewall](firewall-instructions.md) para habilitar as portas usadas pelos exemplos.

6. Verifique o seguinte diretório padrão: \<InstallDrive> :**\ WF_WCF_Samples**. Se os exemplos tiverem sido instalados anteriormente, esse será o diretório padrão.

7. Se os exemplos não estiverem instalados, instale-os nos [exemplos de Windows Communication Foundation (WCF) e Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459).

8. Depois de instalar os exemplos, acesse: \<InstallDrive> :**\ WF_WCF_Samples \\ \wcf\setup**

9. Execute o arquivo em lotes **Setupvroot.bat** . As seguintes etapas são executadas:

    - Um diretório virtual é criado no IIS chamado ServiceModelSamples.

    - Novos diretórios de disco são criados com o nome%SystemDrive%\Inetpub\wwwroot\ServiceModelSamples e%SystemDrive%\Inetpub\wwwroot\ServiceModelSamples\bin.

    Se preferir configurar esses diretórios manualmente, consulte as [instruções de instalação do diretório virtual](virtual-directory-setup-instructions.md). Para reverter todas as alterações feitas nesta etapa, execute cleanupvroot.bat depois de terminar de usar os exemplos.

    > [!NOTE]
    > Esse procedimento deve ser executado apenas uma vez em um computador, a menos que cleanupvroot.bat seja executado.

10. Você deve conceder permissão para modificar para%SystemDrive%\inetpub\wwwroot para a conta sob a qual você está criando os exemplos e o usuário de serviço de rede. Durante a criação, alguns exemplos hospedados na Web podem tentar copiar os binários compilados para o local mencionado anteriormente e, se você não tiver definido as permissões apropriadas, a compilação será interrompida. Como alternativa, você pode deixar as permissões como estão e executar o prompt de comando do SDK ou o prompt de comando do Visual Studio (2012) como administrador ou criar os exemplos no Visual Studio 2012, também executar como administrador.

    > [!NOTE]
    > Se essa etapa não for concluída, todos os exemplos hospedados pelo IIS falharão durante a compilação. Verifique se você definiu as permissões corretamente ou execute o prompt de comando do SDK e o prompt de comando do Visual Studio (2012) como administrador.

11. Criar um diretório do C:\Logs no computador; alguns exemplos podem estar esperando. Certifique-se de que a conta apropriada tenha acesso de gravação concedido a esta pasta. Para o Windows 7, o Windows Vista e o Windows Server 2008 R2, essa conta é **serviço de rede**. Para o Windows Server 2008, a conta é NT Authority\Network Service. Para o Windows XP e o Windows Server 2003, a conta é ASPNET.

12. Execute o arquivo Setupcerttool.bat. Esse arquivo está localizado na  \<InstallPath> pasta \ WF_WCF_Samples \wcf\setup\  Esse script executará as seguintes tarefas:

    - Crie a ferramenta FindPrivateKey.

    - Crie um diretório chamado%ProgramFiles%\ServiceModelSampleTools.

    - Copie a nova ferramenta FindPrivateKey para esse diretório.

    Essa ferramenta é exigida por exemplos que usam certificados e são hospedadas no IIS.

    > [!NOTE]
    > Para fins de segurança, lembre-se de remover a definição de diretório virtual e as permissões concedidas nas etapas de configuração acima, executando o arquivo em lotes chamado Cleanupvroot.bat depois de concluir os exemplos.

13. Exemplos que são auto-hospedados (não hospedados no IIS) exigem permissão para registrar endereços HTTP no computador para escuta. A permissão para uma reserva de namespace HTTP é proveniente da conta de usuário usada para executar o exemplo. Por padrão, as contas de administrador têm a permissão para registrar qualquer endereço HTTP. As contas que não são de administrador devem receber permissão para os namespaces HTTP usados pelos exemplos. Para obter mais informações sobre como configurar reservas de namespace, confira [Configurando HTTP e HTTPS](../feature-details/configuring-http-and-https.md).

14. Alguns exemplos exigem o enfileiramento de mensagens. Consulte [instalando o MSMQ (enfileiramento de mensagens)](installing-message-queuing-msmq.md) para obter instruções de instalação.

    > [!NOTE]
    > Certifique-se de iniciar o serviço MSMQ antes de executar qualquer amostra que exija o enfileiramento de mensagens.

15. Alguns exemplos exigem certificados. Consulte [as instruções de instalação do certificado do servidor serviços de informações da Internet (IIS)](iis-server-certificate-installation-instructions.md).
