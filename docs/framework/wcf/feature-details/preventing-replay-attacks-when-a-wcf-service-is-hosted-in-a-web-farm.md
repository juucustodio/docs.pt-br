---
description: 'Saiba mais sobre: impedindo ataques de repetição quando um serviço WCF é hospedado em um Web farm'
title: Prevenindo ataques por repetição quando um serviço do WCF é hospedado em uma Web Farm
ms.date: 03/30/2017
ms.assetid: 1c2ed695-7a31-4257-92bd-9e9731b886a5
ms.openlocfilehash: 015059ef650b3ec213c54b89763bac7d46dd218f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99793604"
---
# <a name="preventing-replay-attacks-when-a-wcf-service-is-hosted-in-a-web-farm"></a>Prevenindo ataques por repetição quando um serviço do WCF é hospedado em uma Web Farm

Ao usar a segurança de mensagem, o WCF impede ataques de repetição criando um NONCE fora da mensagem de entrada e verificando o interno `InMemoryNonceCache` para ver se o nonce gerado está presente. Se for, a mensagem será descartada como uma reprodução. Quando um serviço WCF é hospedado em um web farm, como o `InMemoryNonceCache` não é compartilhado entre os nós na Web farm, o serviço é vulnerável a ataques de repetição.  Para atenuar esse cenário, o WCF 4,5 fornece um ponto de extensibilidade que permite que você implemente seu próprio cache de NONCE compartilhado derivando uma classe da classe abstrata <xref:System.ServiceModel.Security.NonceCache> .  
  
## <a name="noncecache-implementation"></a>Implementação de NonceCache  

 Para implementar seu próprio cache NONCE compartilhado, derive uma classe de <xref:System.ServiceModel.Security.NonceCache> e substitua <xref:System.ServiceModel.Security.NonceCache.CheckNonce%2A> os <xref:System.ServiceModel.Security.NonceCache.TryAddNonce%2A> métodos e. <xref:System.ServiceModel.Security.NonceCache.CheckNonce%2A> verificará se o NONCE especificado existe no cache. <xref:System.ServiceModel.Security.NonceCache.TryAddNonce%2A> tentará adicionar um NONCE ao cache. Depois que a classe é implementada, você a conecta instanciando uma instância do e atribuindo-a à <xref:System.ServiceModel.Channels.LocalClientSecuritySettings.NonceCache%2A> detecção de reprodução do lado do cliente e à <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.NonceCache%2A> detecção de reprodução do lado do servidor. Não há suporte para configuração pronto para esse recurso.  
  
## <a name="see-also"></a>Consulte também

- [Segurança de mensagem](message-security-in-wcf.md)
- [SymmetricSecurityBindingElement](../diagnostics/wmi/symmetricsecuritybindingelement.md)
