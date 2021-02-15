---
description: 'Saiba mais sobre: agilidade de criptografia na segurança do WCF'
title: Agilidade de criptografia na segurança do WCF
ms.date: 03/30/2017
ms.assetid: c2c549e5-ac19-40c5-b686-8f67f52b6dbf
ms.openlocfilehash: ab46034b16a846f7399220480fc928655d931be0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99778341"
---
# <a name="cryptographic-agility-in-wcf-security"></a>Agilidade de criptografia na segurança do WCF

Este exemplo mostra como especificar em um algoritmo padrão/personalizado para fornecer uma implementação ágil de criptografia em um cliente e serviço do Windows Communication Foundation (WCF). O exemplo é composto pelos seguintes projetos:

**Serviço**

Este é um serviço WCF auto-hospedado que implementa a `ICalculator` interface e protege o ponto de extremidade usando a sessão <xref:System.ServiceModel.WSHttpBinding> segura e a sessão confiável desabilitada. O serviço define uma `SecurityAlgorithmSuite` classe personalizada para especificar os algoritmos criptográficos a serem usados para segurança de mensagens.

**Cliente**

Esse é um cliente WCF que acessa o serviço após a autenticação bem-sucedida. Ele invoca as operações expostas pela `ICalculator` interface e implementadas pelo serviço. O cliente também define a mesma `SecurityAlgorithmSuite` classe personalizada para especificar os algoritmos de criptografia a serem usados para a segurança da mensagem.

## <a name="to-use-this-sample"></a>Para usar este exemplo

1. Abra a solução CryptoAgility. sln no Visual Studio 2012.

2. Pressione CTRL+SHIFT+B para criar a solução.

3. Abra o explorador de arquivos e navegue até o diretório \WCF\Basic\Security\CryptoAgility\Service\bin e execute o arquivo de service.exe com privilégios de administrador clicando com o botão direito do mouse em service.exe e selecionando **Executar como administrador**.

4. Navegue até o diretório \WCF\Basic\Security\CryptoAgility\Client\bin e execute o arquivo client.exe normalmente.

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Security\CryptoAgility`

## <a name="see-also"></a>Consulte também

- [Segurança do Windows Communication Foundation](../feature-details/security.md)
