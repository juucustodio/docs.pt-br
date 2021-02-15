---
description: 'Saiba mais sobre: publicação e resolução de nome de par'
title: Resolução e publicação de nome de par
ms.date: 03/30/2017
ms.assetid: f0370e08-9fa6-4ee5-ab78-9a58a20a7da2
ms.openlocfilehash: cd1d3358c212b1618548422715329eea57452ac3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99747420"
---
# <a name="peer-name-publication-and-resolution"></a>Resolução e publicação de nome de par

## <a name="publishing-a-peer-name"></a>Como publicar um nome de par  

 Para publicar uma nova ID de PNRP, um par executa o seguinte:  
  
- Envia mensagens de publicação PNRP para seus vizinhos de cache (os pares que registraram as IDs de PNRP no nível mais baixo do cache) para propagar os caches deles.  
  
- Escolhe nós aleatórios na nuvem que não são vizinhos dele e envia solicitações de resolução de nome PNRP para sua própria ID de P2P. O processo de determinação do ponto de extremidade resultante propaga os caches de nós aleatórios na nuvem com a ID de PNRP do par que realiza a publicação.  
  
Nós de versão 2 do PNRP não publicam IDs de PNRP se eles estão apenas resolvendo outras IDs de P2P. O valor de Registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\PeerNet\PNRP\IPV6-Global\SearchOnly=1 (tipo REG_DWORD) especifica que os pares só usam PNRP para resolução de nome, nunca para publicação de nome. Esse valor de Registro também pode ser configurado por meio da Política de Grupo.  
  
## <a name="resolving-a-peer-name"></a>Como resolver um nome de par

 Localizar outros pares em uma nuvem ou rede PNRP é um processo composto de duas fases:  
  
1. Determinação do ponto de extremidade  
  
2. Resolução da ID de PNRP  
  
 Na fase de determinação do ponto de extremidade, um par que está tentando resolver a ID de PNRP de um serviço em outro computador determina o endereço IPv6 desse par remoto.  O par remoto é o que publicou ou está associado com a ID de PNRP do computador ou serviço.  
  
 Depois de confirmar que o ponto de extremidade remoto foi registrado na nuvem PNRP, o par solicitante na fase de resolução de ID de PNRP envia ao ponto de extremidade de par uma solicitação da ID de PNRP do serviço desejado. O ponto de extremidade envia uma resposta confirmando a ID de PNRP do serviço, um comentário e até 4 KB de informações adicionais que o par solicitante pode usar para comunicação futura. Por exemplo, se o ponto de extremidade desejado é um servidor de jogos, os dados de registro de nome de par adicionais podem conter informações sobre o jogo, o nível de jogo e o número atual de jogadores.  
  
 Na fase de determinação de ponto de extremidade, o PNRP usa um processo iterativo para localizar o nó que publicou a ID de PNRP, no qual o nó executando a resolução é responsável por entrar em contato com nós que são sucessivamente mais próximos à ID de PNRP de destino.  
  
 Para executar a resolução de nomes PNRP, o par examina as entradas no seu próprio cache em busca de uma entrada que corresponde à ID de PNRP de destino. Se encontra essa entrada, o par envia uma mensagem de solicitação de PNRP para o par e aguarda uma resposta. Se uma entrada para a ID de PNRP não é encontrada, o par envia uma mensagem de solicitação de PNRP para o par que corresponde à entrada que tem uma ID de PNRP que melhor corresponde à ID de PNRP de destino. O nó que recebe a mensagem de solicitação de PNRP examina o seu próprio cache e faz o seguinte:  
  
- Se a ID de PNRP for encontrada, o par do ponto de extremidade solicitado responderá diretamente para o par solicitante.  
  
- Se a ID de PNRP não for encontrada e uma ID de PNRP no cache for mais próxima à ID de PNRP de destino, o par solicitado enviará uma resposta ao par solicitante contendo o endereço IPv6 do par que representa a entrada com uma ID de PNRP que melhor corresponde à ID de PNRP de destino. Usando o endereço IP na resposta, o nó de consulta envia outra mensagem de solicitação de PNRP ao endereço IPv6 para responder ou examinar seu cache.  
  
- Se a ID de PNRP não é encontrada e não há nenhuma ID de PNRP em seu cache que melhor corresponde à ID de PNRP, o par solicitado envia ao par solicitante uma resposta que indica essa condição. O par solicitante escolhe então a próxima ID de PNRP com maior correspondência.  
  
O par solicitante continua esse processo com iterações sucessivas, eventualmente localizando o nó que registrou a ID de PNRP.  
  
 Dentro do namespace <xref:System.Net.PeerToPeer>, há uma relação muitos para muitos entre os registros de <xref:System.Net.PeerToPeer.PeerName> que contêm pontos de extremidade e nuvens PNRP ou malhas nas quais eles se comunicam. Quando há entradas duplicadas ou obsoletas ou vários nós com o mesmo nome de par, nós PNRP podem obter informações atuais usando a classe <xref:System.Net.PeerToPeer.PeerNameResolver>. Os métodos <xref:System.Net.PeerToPeer.PeerNameResolver> usam um único nome de par para simplificar a perspectiva para registros de nome de um par para muitos pares e do mesmo par para muitas nuvens. Isso é semelhante a uma consulta executada usando uma junção de tabela relacional. Após a conclusão bem-sucedida, o objeto resolvedor retorna um <xref:System.Net.PeerToPeer.PeerNameRecordCollection> para o nome de par especificado.  Por exemplo, um nome de par ocorreria em todos os registros de nome de par na coleção, ordenados pela nuvem. Estas são as instâncias do nome do par cujos dados de suporte podem ser solicitados por um aplicativo baseado em PNRP.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Net.PeerToPeer>
