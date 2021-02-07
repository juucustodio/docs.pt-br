---
description: 'Saiba mais sobre: política de proteção estendida'
title: Política de proteção estendida
ms.date: 03/30/2017
ms.assetid: e2616a10-317e-4c34-8023-0c015a80a82f
ms.openlocfilehash: 295b49f3795e60095403dcef98b3d7ecbf29aeb9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99752386"
---
# <a name="extended-protection-policy"></a>Política de proteção estendida

A proteção estendida é uma iniciativa de segurança para proteção contra ataques MITM (Man-in-the-Middle). Um ataque MITM é uma ameaça à segurança em que um MITM Obtém as credenciais de um cliente e as encaminha para um servidor.  
  
## <a name="demonstrates"></a>Demonstra  

 Proteção estendida  
  
## <a name="discussion"></a>Discussão  

 Quando os aplicativos são autenticados usando Kerberos, Digest ou NTLM usando HTTPS, um canal de TLS (segurança de nível de transporte) é estabelecido primeiro e, em seguida, a autenticação ocorre usando o canal seguro. No entanto, não há nenhuma associação entre a chave de sessão gerada pelo SSL e a chave de sessão gerada durante a autenticação. Qualquer MITM pode se estabelecer entre o cliente e o servidor e começar a encaminhar as solicitações do cliente, mesmo quando o canal de transporte em si é seguro, porque o servidor não tem como saber se o canal seguro foi estabelecido do cliente ou de um MITM. A solução neste cenário é associar o canal TLS externo ao canal de autenticação interna, de modo que o servidor possa detectar se há um MITM.  
  
> [!NOTE]
> Este exemplo só funciona quando hospedado no IIS e não funciona no Cassini – Visual Studio Development Server porque o Cassini não oferece suporte a HTTPS.  
  
> [!NOTE]
> No momento, esse recurso está disponível apenas no Windows 7. As etapas a seguir são específicas para o Windows 7.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo  
  
1. Instale o Serviços de Informações da Internet no **painel de controle**, **adicione/remova programas**, recursos do **Windows**.  
  
2. Instale a **autenticação do Windows** em recursos do **Windows**, **serviços de informações da Internet**, **serviços de World Wide Web**, **segurança** e autenticação do **Windows**.  
  
3. Instale **Windows Communication Foundation ativação http** nos **recursos do Windows**, **Microsoft .NET Framework 3.5.1** e **Windows Communication Foundation ativação http**.  
  
4. Este exemplo requer que o cliente estabeleça um canal seguro com o servidor, portanto, ele requer a presença de um certificado de servidor que pode ser instalado do Gerenciador Serviços de Informações da Internet (IIS).  
  
    1. Abra o Gerenciador do IIS. Abra **certificados de servidor**, que aparece na guia **exibição de recurso** quando o nó raiz (nome da máquina) é selecionado.  
  
    2. Para testar esse exemplo, crie um certificado autoassinado. Se você não quiser que o Internet Explorer solicite que o certificado não seja seguro, instale o certificado no repositório de autoridade raiz do certificado confiável.  
  
5. Abra o painel **ações** do site da Web padrão. Clique em **Editar site**, **associações**. Adicione HTTPS como um tipo, se ainda não estiver presente, com o número da porta 443. Atribua o certificado SSL criado na etapa anterior.  
  
6. Crie o serviço. Isso cria um diretório virtual no IIS e copia os arquivos. dll,. svc e. config, conforme necessário para que o serviço seja hospedado na Web.  
  
7. Abra o Gerenciador do IIS. Clique com o botão direito do mouse no diretório virtual (**ExtendedProtection**), que foi criado na etapa anterior. Selecione **converter para aplicativo**.  
  
8. Abra o módulo de **autenticação** no Gerenciador do IIS para este diretório virtual e habilite a **autenticação do Windows**.  
  
9. Abra **Configurações avançadas** em **autenticação do Windows** para este diretório virtual e defina-o como **obrigatório**.  
  
10. Você pode testar o serviço acessando a URL HTTPS de uma janela do navegador (forneça um nome de domínio totalmente qualificado). Se você quiser acessar essa URL de um computador remoto, certifique-se de que o firewall esteja aberto para todas as conexões HTTP e HTTPS de entrada.  
  
11. Abra o arquivo de configuração do cliente e forneça um nome de domínio totalmente qualificado para o atributo de endereço do cliente ou do ponto de extremidade que substitui `<<full_machine_name>>` .  
  
12. Execute o cliente. O cliente se comunica com o serviço, que estabelece um canal seguro e usa a proteção estendida.  
  
> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Security\ExtendedProtection`
