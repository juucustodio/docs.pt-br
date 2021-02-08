---
description: 'Saiba mais sobre: caches PNRP'
title: Caches PNRP
ms.date: 03/30/2017
ms.assetid: 270068d9-1b6b-4eb9-9e14-e02326bb88df
ms.openlocfilehash: a9e64cd647be2fe33863e014ee4c22d1752f56f8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794904"
---
# <a name="pnrp-caches"></a>Caches PNRP

Caches de protocolo PNRP são coleções locais de pontos de extremidade de par selecionados de maneira algorítmica mantidos no par.  
  
## <a name="pnrp-cache-initialization"></a>Inicialização do cache PNRP  

 Para inicializar o cache PNRP ou a coleção de registro de nome de nó par, quando um nó par é iniciado, um nó pode usar os seguintes métodos:  
  
- Entradas de cache persistente que estavam presentes quando o nó foi desligado são carregadas do armazenamento de disco rígido.  
  
- Se um aplicativo usa a infraestrutura de colaboração P2P, informações de colaboração estão disponíveis no Gerenciador de Contatos desse nó.  
  
## <a name="scaling-peer-name-resolution-with-a-multi-level-cache"></a>Colocação em escala da resolução de nomes de par com um cache multinível  

 Para manter os tamanhos dos caches PNRP pequenos, nós pares usam um cache multinível, em que cada nível contém um número máximo de entradas. Cada nível no cache representa uma parte menor equivalente a um décimo do espaço do número de identificação de PNRP (2<sup>256</sup>). O nível mais baixo no cache contém uma ID de PNRP registrada localmente e outras IDs de PNRP numericamente próximas a ela. Conforme um nível de cache é preenchido com um máximo de 20 entradas, um novo nível inferior é criado. O número máximo de níveis no cache é na ordem de log10(número total de IDs de PNRP na nuvem). Por exemplo, para uma nuvem global com 100 milhões de IDs de PNRP, há não mais do que 8 (=log10(100.000.000)) níveis em cache e um número semelhante de saltos para resolver uma ID de PNRP durante a resolução de nome. Esse mecanismo permite uma tabela de hash distribuída para a qual uma ID de PNRP arbitrária pode ser resolvida pelo encaminhamento de mensagens de solicitação PNRP para o par mais próximo até o par com o CPA correspondente ser encontrado.  
  
 Para garantir que a resolução possa ser concluída, cada vez que um nó adiciona uma entrada para o nível mais baixo de seu cache, ele sobrecarrega uma cópia da entrada para todos os nós contidos no último nível do cache.  
  
 As entradas de cache são atualizadas ao longo do tempo. Entradas de cache obsoletas são removidas do cache. O resultado é que a tabela de hash distribuída de IDs de PNRP é baseada em pontos de extremidade ativos, ao contrário do DNS em que os registros de endereços e o protocolo DNS não fornecem nenhuma garantia de que o nó associado ao endereço esteja ativamente na rede.  
  
## <a name="other-pnrp-caches"></a>Outros caches PNRP  

 Um outro armazenamento de dados persistente é o cache local.  Além dos outros objetos necessários para a atividade de PNRP, ele pode incluir os registros associados a uma sessão de colaboração ou de nuvem PNRP que é publicada com segurança e sincronizada entre todos os membros da nuvem. Esse repositório replicado representa a exibição dos dados do grupo, que devem ser os mesmos para todos os membros do grupo. Tecnicamente, esses objetos não são registros propriamente ditos mas, em vez disso, são dados de aplicativos, de presença e de objeto destinados a um cache local. O uso da nuvem PNRP garante que os objetos sejam propagados para todos os nós na sessão de colaboração ou nuvem PNRP.  O registro de replicação entre os membros da nuvem usa SSL para fornecer criptografia e integridade dos dados.  
  
 Quando um par ingressa em uma nuvem, ele não recebe automaticamente dados de cache local do par de host ao qual ele se conecta; ele precisa assinar o par de host para receber atualizações de dados de aplicativos, de presença de objeto. Após a sincronização inicial, pares ressincronizam periodicamente seus repositórios replicados para garantir que todos os membros do grupo tenham a mesma exibição, de maneira consistente.  A sessão de colaboração ou aplicativos dentro da sessão de colaboração também podem executar a mesma função.  
  
 Depois de iniciada uma sessão de colaboração para uma nuvem, os aplicativos podem registrar pares e começar a publicar suas informações usando a segurança definida pelo escopo de nuvem. Quando um par ingressa em uma nuvem, os mecanismos de segurança para a nuvem são aplicados ao par, dando a ele um escopo no qual participar.  Os registros dele, em seguida, podem ser publicados com segurança dentro do escopo da nuvem. Observe que o escopo da nuvem pode não ser o mesmo que o escopo do aplicativo de colaboração.  
  
 Pares podem registrar interesse em receber objetos de outros pares. Quando um objeto é atualizado, o aplicativo de colaboração é notificado e o novo objeto é passado para todos os assinantes do aplicativo. Por exemplo, um par em um aplicativo de chat de grupo pode registrar interesse em receber informações do aplicativo, que ele envie todos os registros de chat como dados de aplicativo.  Isso permite monitorar a atividade de chat dentro da nuvem.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Net.PeerToPeer>
