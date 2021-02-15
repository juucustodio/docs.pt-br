---
description: 'Saiba mais sobre: malhas de pares'
title: Malhas ponto a ponto
ms.date: 03/30/2017
ms.assetid: d93e312e-ac04-40f8-baea-5da1cacb546e
ms.openlocfilehash: bedb8931c4ed4c4f62cb3556699d7f9f07f6f022
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99733379"
---
# <a name="peer-meshes"></a>Malhas ponto a ponto

Uma *malha* é uma coleção nomeada (um gráfico interconectado) de nós pares que podem se comunicar entre si e que são identificados por uma ID de malha exclusiva. Cada nó é conectado a vários outros nós. Em uma malha bem conectada, há um caminho entre dois nós, com relativamente poucos saltos entre os nós nas bordas mais distantes da malha, e a malha permanecerá conectada mesmo que alguns nós ou conexões sejam cancelados. Os nós ativos na malha publicam suas informações de ponto de extremidade com uma ID de malha correspondente para que outros pontos possam encontrá-las.  
  
## <a name="characteristics-of-a-mesh-created-using-peer-channel"></a>Características de uma malha criada usando o canal de mesmo nível  
  
#### <a name="uniquely-identified"></a>Identificado exclusivamente  
  
- Uma ID exclusiva identifica cada malha. O nome da malha (ou ID de malha) está no mesmo formato que um nome de host DNS (sistema de nomes de domínio). Dessa forma, essa ID de malha deve ser exclusiva para o cliente pretendido do aplicativo dentro do escopo do resolvedor que está sendo usado. Um nome comum, como "MyFamilysPeers" ou "KevinsPokerTable", pode Colider facilmente com outros nomes de usuário e pode retornar informações de ponto de extremidade não pretendidas, o que pode resultar em problemas de privacidade ou aumentar a latência de conexão. Uma maneira de evitar esses problemas pode ser adicionar uma ID exclusiva como um sufixo ao apelido para a malha (por exemplo, "KevinsPokerTable90210").  
  
#### <a name="message-flooding"></a>Inundação de mensagem  
  
- A malha permite que as mensagens sejam propagadas de um ou mais remetentes para todos os outros nós de mesmo nível na mesma malha. As mensagens inundadas por nós pares usam cabeçalhos especificados no namespace em `http://schemas.microsoft.com/net/2006/05/peer` .  
  
#### <a name="optimized-connections"></a>Conexões otimizadas  
  
- Uma malha de canal de mesmo nível é ajustada automaticamente quando os nós entram e saem, garantindo que todos os nós tenham boa conectividade com pouca chance de criar partições (grupos de nós isolados uns dos outros). As conexões na malha também são otimizadas dinamicamente com base nos padrões de tráfego atuais para que a latência de mensagem do remetente para o destinatário seja a menor possível.  
  
#### <a name="popular-network-features-that-peer-channel-does-not-provide"></a>Recursos de rede populares que o canal de mesmo nível não fornece  

 É importante estar ciente dos recursos de rede populares que o canal de mesmo nível não fornece. Esses recursos, que podem todos ser criados com base no canal de pares, incluem o seguinte:  
  
- **Ordenação de mensagens:** As mensagens provenientes de uma única fonte podem não chegar a todas as outras partes na mesma ordem ou na ordem em que a origem foi enviada. Aplicativos que exigem mensagens são entregues em uma determinada ordem devem ser compilados em seus aplicativos (por exemplo, incluindo uma ID de aumento monotônico com todas as mensagens).  
  
- **Mensagens confiáveis:** O canal par não inclui um mecanismo para garantir a recepção de mensagens por todos os pares. Para garantir a entrega de mensagens, você deve gravar uma camada de confiabilidade na parte superior do canal par.
