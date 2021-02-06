---
description: 'Saiba mais sobre: instruções de instalação do certificado do servidor do Serviços de Informações da Internet (IIS)'
title: Instruções da instalação do certificado de servidor dos Serviços de Informações da Internet (IIS)
ms.date: 03/30/2017
ms.assetid: 11281490-d2ac-4324-8f33-e7714611a34b
ms.openlocfilehash: 1ac5209e9ff82911b0631c190e16ff457fea0db6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631847"
---
# <a name="internet-information-services-iis-server-certificate-installation-instructions"></a>Instruções da instalação do certificado de servidor dos Serviços de Informações da Internet (IIS)

Para executar os exemplos que comunicam com segurança com o IIS (Serviços de Informações da Internet), você deverá criar e instalar um certificado do servidor.  
  
## <a name="step-1-creating-certificates"></a>Etapa 1. Criando certificados  

 Para criar um certificado para o computador, abra um Prompt de Comando do Desenvolvedor para o Visual Studio com privilégios de administrador e execute o Setup.bat incluído em cada um dos exemplos que usam comunicação segura com o IIS. Verifique se o caminho inclui a pasta que contém Makecert.exe antes de executar este arquivo em lote. O comando a seguir é usado para criar o certificado em Setup.bat.  
  
```console  
makecert -sr LocalMachine -ss My -n CN=ServiceModelSamples-HTTPS-Server -sky exchange -sk ServiceModelSamples-HTTPS-Key  
```  
  
## <a name="step-2-installing-certificates"></a>Etapa 2. Instalando certificados  

 As etapas necessárias para instalar os certificados que você criou dependem de qual versão do IIS você está usando.  
  
#### <a name="to-install-iis-on-iis-51-windows-xp-and-iis-60-windows-server-2003"></a>Para instalar o IIS no IIS 5.1 (Windows XP) e IIS 6.0 (Windows Server 2003)  
  
1. Abra o snap-in do MMC do Gerenciador dos Serviços de Informações da Internet.  
  
2. Clique com o botão direito do mouse no site da Web padrão e selecione **Propriedades**.  
  
3. Selecione a guia **segurança de diretório** .  
  
4. Clique no botão **certificado do servidor** . O assistente de certificado do servidor Web é iniciado.  
  
5. Conclua o assistente. Selecione a opção para atribuir um certificado. Selecione o certificado ServiceModelSamples-HTTPS-Server da lista de certificados que são exibidos.  
  
     ![Assistente de Certificado IIS](media/iiscertificate-wizard.GIF "IISCertificate_Wizard")  
  
6. Teste o acesso ao serviço em um navegador usando o endereço HTTPS `https://localhost/servicemodelsamples/service.svc` .  
  
#### <a name="if-ssl-was-previously-configured-by-using-httpcfgexe"></a>Se o SSL foi configurado anteriormente usando Httpcfg.exe  
  
1. Use Makecert.exe (ou execute Setup.bat) para criar o certificado do servidor.  
  
2. Execute o Gerenciador do IIS e instale o certificado de acordo com as etapas anteriores.  
  
3. Adicione a seguinte linha de código ao programa cliente.  
  
> [!IMPORTANT]
> Esse código somente é necessário para certificados de teste como os criados por Makecert.exe. Não é recomendável para o código de produção.  
  
```csharp  
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");  
```  
  
#### <a name="to-install-iis-on-iis-70-windows-vista-and-windows-server-2008"></a>Para instalar o IIS no IIS 7.0 (Windows Vista e Windows Server 2008)  
  
1. No menu **Iniciar** , clique em **executar** e digite **inetmgr** para abrir o snap-in do MMC serviços de informações da Internet (IIS).  
  
2. Clique com o botão direito do mouse no **site da Web padrão** e selecione **Editar associações...**  
  
3. Clique no botão **Adicionar** da caixa de diálogo **ligações do site** .  
  
4. Selecione **https** na lista suspensa **tipo** .  
  
5. Selecione o **ServiceModelSamples-https-Server** na lista suspensa **certificado SSL** e clique em **OK**.  
  
6. Teste o acesso ao serviço em um navegador usando o endereço HTTPS `https://localhost/servicemodelsamples/service.svc` .  
  
> [!NOTE]
> Como o certificado de teste que você acabou de instalar não é um certificado confiável, você poderá encontrar avisos de segurança adicionais do Internet Explorer ao navegar em endereços Web locais protegidos por esse certificado.  
  
## <a name="removing-certificates"></a>Removendo certificados  
  
- Use o Gerenciador dos Serviços de Informações da Internet como direcionado anteriormente, mas remova o certificado ou associação em vez de adicionar.  
  
- Remova o certificado do computador usando o comando a seguir.  
  
    ```console  
    httpcfg delete ssl -i 0.0.0.0:443  
    ```
