---
description: 'Saiba mais sobre: extensibilidade de canais'
title: Extensibilidade de canais
ms.date: 03/30/2017
ms.assetid: 4cc3b20b-778a-4ae8-b58c-a3822fb13065
ms.openlocfilehash: 08c93ffa2e7c4645e4c49be619c0cb065ecdbff7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99704063"
---
# <a name="channels-extensibility"></a>Extensibilidade de canais

Esta seção contém exemplos que demonstram canais personalizados.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Canal local](local-channel.md)  
 Demonstra o canal local, um canal de transporte do WCF que é usado para comunicação dentro do mesmo domínio de aplicativo.  
  
 [Perfil seguro confiável](reliable-secure-profile.md)  
 Demonstra como compor o WCF e um perfil seguro confiável (RSP).  
  
 [Distribuidor de canal personalizado](custom-channel-dispatcher.md)  
 Demonstra como criar a pilha de canais de forma personalizada implementando-a <xref:System.ServiceModel.ServiceHostBase> diretamente e como criar um Dispatcher de canal personalizado no ambiente de host da Web.  
  
 [Canal de agrupamento](chunking-channel.md)  
 Demonstra como limitar a quantidade de memória usada para armazenar em buffer mensagens grandes enviadas usando o WCF.
  
 [HttpCookieSession](httpcookiesession.md)  
 Demonstra como criar um canal de protocolo personalizado para usar cookies HTTP para o gerenciamento de sessão.  
  
 [Interceptor de mensagem personalizado](custom-message-interceptor.md)  
 Demonstra como implementar um elemento de ligação personalizado que cria fábricas de canal e ouvintes de canal para interceptar todas as mensagens de entrada e saída em um ponto específico na pilha de tempo de execução.
