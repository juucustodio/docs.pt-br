---
description: 'Saiba mais sobre: usando as ferramentas de desenvolvimento do WCF'
title: Utilizando as ferramentas de desenvolvimento do WCF
ms.date: 03/30/2017
ms.assetid: 054adb87-c244-4d5a-83d1-0b2b44bd454b
ms.openlocfilehash: c96644fb66006447f6a05f6c08ea84fe2ed99ce8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631691"
---
# <a name="using-the-wcf-development-tools"></a>Utilizando as ferramentas de desenvolvimento do WCF

Esta seção descreve as ferramentas de desenvolvimento do Visual Studio que podem ajudá-lo a desenvolver seu WCFservice.  
  
 Você pode usar os modelos do Visual Studio como uma base para criar rapidamente seu próprio serviço e, em seguida, usar o cliente de host automático do serviço WCF e de teste do WCF para depurar e testar seu serviço. Essas ferramentas juntas fornecem um ciclo de depuração e teste rápido e contínuo e impedem a necessidade de se comprometer com um modelo de hospedagem em um estágio inicial.  

 > [!NOTE]
 > A partir do Visual Studio 2017, as ferramentas de desenvolvimento do WCF não são instaladas por padrão. Para usar esses recursos, você deve garantir que o componente Windows Communication Foundation esteja selecionado no instalador do Visual Studio.
  
## <a name="the-wcf-developer-tools"></a>O WCF Ferramentas para Desenvolvedores  

 [Modelos do Visual Studio do WCF](wcf-vs-templates.md)  
  
 Você pode usar os modelos de projeto e item predefinidos do Visual Studio no Visual Studio para criar rapidamente serviços WCF e aplicativos adjacentes.  
  
 [Host de serviço do WCF (WcfSvcHost.exe)](wcf-service-host-wcfsvchost-exe.md)  
  
 O host automático do serviço WCF (WcfSvcHost.exe) permite que você inicie o depurador do Visual Studio (F5) para hospedar e testar automaticamente um serviço que você implementou. Em seguida, você pode testar o serviço usando o cliente de teste do WCF (wcfTestClient.exe) ou seu próprio cliente para localizar e corrigir quaisquer erros potenciais.  
  
 [Cliente de Teste do WCF (WcfTestClient.exe)](wcf-test-client-wcftestclient-exe.md)  
  
 O cliente de teste do WCF (WcfTestClient.exe) é uma ferramenta de GUI que permite que você insira parâmetros de tipos arbitrários, envie essa entrada para o serviço e exiba a resposta que o serviço envia de volta. Ele fornece uma experiência de teste de serviço sem interrupção quando combinado com o host automático do serviço WCF.  
  
 [Gerando classes de tipo de dados por meio de XML](generating-data-type-classes-from-xml.md)  
  
 Os dados XML armazenados na área de transferência podem ser colados em uma página de código. As classes definidas nos dados serão convertidas em tipos de código.  
  
## <a name="using-the-tools-without-administrator-privilege"></a>Usando o privilégio ferramentas sem administrador  

 Para permitir que os usuários sem privilégios de administrador desenvolvam serviços WCF, uma ACL (lista de controle de acesso) é criada para o namespace " http://+:8731/Design_Time_Addresses " durante a instalação do Visual Studio. A ACL é definida como (UI), que inclui todos os usuários interativos conectados à máquina. Os administradores podem adicionar ou remover usuários dessa ACL ou abrir portas adicionais. Essa ACL permite que os modelos WCF ou WF enviem e recebam dados em sua configuração padrão. Ele também permite que os usuários usem o host automático do serviço WCF (wcfSvcHost.exe) sem conceder a eles privilégios de administrador.  
  
 Você pode modificar o acesso usando a ferramenta de Netsh.exe no Windows Vista na conta de administrador elevado. Veja a seguir um exemplo de como usar Netsh.exe.  
  
```console  
netsh http add urlacl url=http://+:8001/MyService user=<domain>\<user>  
```  
  
 Para obter mais informações sobre Netsh.exe, consulte [como usar a ferramenta de Netsh.exe e Command-Line opções](/previous-versions/tn-archive/bb490939(v=technet.10)).  
  
## <a name="see-also"></a>Consulte também

- [Modelos do Visual Studio do WCF](wcf-vs-templates.md)
- [Host de serviço do WCF (WcfSvcHost.exe)](wcf-service-host-wcfsvchost-exe.md)
- [Cliente de Teste do WCF (WcfTestClient.exe)](wcf-test-client-wcftestclient-exe.md)
