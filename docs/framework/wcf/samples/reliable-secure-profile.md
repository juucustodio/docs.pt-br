---
description: 'Saiba mais sobre: perfil seguro confiável'
title: Perfil seguro confiável
ms.date: 03/30/2017
ms.assetid: 921edc41-e91b-40f9-bde9-b6148b633e61
ms.openlocfilehash: 6e9552b3a6e715f6eac6742f89b2e70a34f926a6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99703816"
---
# <a name="reliable-secure-profile"></a>Perfil seguro confiável

Este exemplo demonstra como compor o WCF e um [perfil seguro confiável (RSP)](http://www.ws-i.org/Profiles/ReliableSecureProfile-1.0.html). Este exemplo demonstra a implementação de um canal de [conexão de make](http://docs.oasis-open.org/ws-rx/wsmc/200702/wsmc-1.0-spec-cs-01.pdf) , que pode ser composto junto com mensagens confiáveis e, opcionalmente, um canal seguro para criar uma associação segura confiável com base na especificação rsp.  
  
> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Channels\ReliableSecureProfile`  
  
## <a name="discussion"></a>Discussão  

 Este exemplo demonstra um cenário de troca de mensagens bidirecional assíncrona confiável. O serviço tem um contrato duplex e o cliente implementa o contrato de retorno de chamada duplex. O cliente inicia uma solicitação para um serviço, para a qual uma resposta é esperada em uma conexão separada. A mensagem de solicitação é enviada de forma confiável. O cliente não deseja abrir um ponto de extremidade de escuta em seu final. Portanto, ele sonda o serviço com as solicitações ' make Connection ' para que o serviço envie a resposta no canal traseiro dessa solicitação ' make Connection '. Este exemplo demonstra como ter uma comunicação duplex confiável em HTTP sem o cliente expondo um ponto de extremidade de escuta (e criando uma exceção de firewall).  
  
## <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo  
  
1. Abra a solução **ReliableSecureProfile** .  
  
2. Clique com o botão direito do mouse no projeto de **serviço** no **Gerenciador de soluções**, selecione **depurar**, **Iniciar nova instância** no menu de contexto. Isso inicia o host de serviço.  
  
3. Clique com o botão direito do mouse no projeto **cliente** no **Gerenciador de soluções**, selecione **depurar**, **Iniciar nova instância** no menu de contexto. Isso inicia o cliente.  
  
4. Digite qualquer cadeia de caracteres no prompt na janela do console do cliente e clique em ENTER. Isso envia a cadeia de caracteres de entrada para o serviço, que computa um hash dessa cadeia de caracteres.  
  
5. Exiba o resultado nas janelas do cliente quando o serviço chamar de volta a operação de contrato de retorno de chamada duplex para exibir o resultado na janela do console do cliente. Há um atraso intencional no serviço para simular uma operação de execução longa do processamento dos dados.  
  
6. O monitoramento do tráfego HTTP (por qualquer uma das ferramentas de monitoramento de rede online, como Monitor de Rede, Fiddler e assim por diante) mostra que uma sequência de comunicação é estabelecida entre o cliente e o serviço conforme disposto pelo perfil seguro confiável e como o cliente sonda o serviço com as solicitações ' fazer conexão '. Quando o serviço fica pronto para enviar de volta a resposta processada, ele usa o canal traseiro da última solicitação "fazer conexão" para enviar de volta os resultados.  
  
7. Pressione ENTER na janela do console de serviço para fechar o serviço. Pressione ENTER na janela do console do cliente para fechar o cliente.
