---
description: 'Saiba mais sobre: cenários de rede ponto a ponto'
title: Cenários de rede ponto a ponto
ms.date: 03/30/2017
ms.assetid: d23b1a64-2e08-4014-882a-c1dd766bdcc2
ms.openlocfilehash: 097b006c5f260a91c1f134a443f7d2f63a1f7866
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99738257"
---
# <a name="peer-to-peer-networking-scenarios"></a>Cenários de rede ponto a ponto

Rede ponto a ponto permite ou aprimora os cenários a seguir:

## <a name="real-time-communications-rtc"></a>RTC (comunicação em tempo real)

- Mensagens instantâneas sem servidor

  A RTC existe atualmente. Atualmente, os usuários do computador podem conversar por chat e ter conversações por voz ou vídeo com seus colegas. No entanto, muitos dos programas existentes e dos respectivos protocolos de comunicação dependem de servidores para funcionar. Se você estiver participando de uma rede sem fio ad hoc ou fizer parte de uma rede isolada, não será possível usar esses recursos RTC. A tecnologia Pessoas ao Meu Redor permite a extensão de tecnologias de RTC para esses ambientes de rede adicionais.

- Jogos e emparelhamento (organizar uma partida) em tempo real

  Semelhante ao RTC, o jogo em tempo real existe nos dias de hoje. Há muitos sites de jogos baseados na Web que atendem à comunidade de jogos através da Internet. Eles oferecem a capacidade de localizar outros jogadores com interesses semelhantes e jogar juntos. O problema é que os sites de jogos existem apenas na Internet e são direcionados para o jogador ávido, que deseja competir com os melhores gamers do mundo. Esses sites acompanham e fornecem as estatísticas para ajudar no processo. No entanto, esses sites não permitem que um jogador configure um jogo ad-hoc entre amigos em uma variedade de ambientes de rede. A rede ponto a ponto pode oferecer essa capacidade.

## <a name="collaboration"></a>Colaboração

- Workspaces de projeto atingindo uma meta

  Aplicativos de workspace compartilhado permitem a criação de grupos de trabalho ad hoc e, em seguida, permitem que os proprietários do grupo de trabalho preencham o workspace compartilhado com as ferramentas e o conteúdo que permitirão que o grupo solucione um problema. Isso pode incluir arquivos, ferramentas de produtividade e quadros de mensagens.

- Compartilhamento de arquivos com outras pessoas

  Um subconjunto do compartilhamento de workspace de projeto é a capacidade de compartilhar arquivos. Embora essa capacidade exista atualmente com a versão atual do Windows, ela pode ser aprimorada por meio da rede ponto a ponto para disponibilizar o conteúdo do arquivo de uma maneira fácil e amigável. Permitir o acesso fácil à incrível riqueza de conteúdo na borda da Internet ou em ambientes de computação ad-hoc aumenta o valor da computação de rede.

- Compartilhando experiências

  Com a conectividade sem fio se tornando mais predominante, a rede ponto a ponto permite que você esteja online em um grupo de pares e seja capaz de compartilhar suas experiências (como um pôr-do-sol, um show de rock ou um cruzeiro de férias) enquanto elas estão ocorrendo.

## <a name="content-distribution"></a>Distribuição de conteúdo

- Mensagens de texto

  A rede ponto a ponto pode permitir a divulgação de informações baseadas em texto na forma de arquivos ou mensagens para um grande grupo de usuários. Um exemplo é uma lista de notícias.

- Áudio e vídeo

  A rede ponto a ponto também pode permitir a divulgação de informações de áudio ou vídeo para um grande grupo de usuários, tal como um grande concerto ou uma reunião da empresa. Para distribuir o conteúdo hoje em dia, você deve configurar servidores de alta capacidade para coletar e distribuir a carga entre centenas ou milhares de usuários. Com a rede ponto a ponto, apenas alguns pares realmente obteriam o conteúdo de servidores centralizados. Esses pares propagariam essas informações para algumas pessoas mais, que por sua vez as enviariam para outras e assim por diante. A carga de distribuir o conteúdo é distribuída para os pares na nuvem. Um par que desejasse receber o conteúdo localizaria o par mais próximo distribuindo o conteúdo e obteria o conteúdo dele.

- Distribuição de atualizações de produtos

  Redes ponto a ponto também pode fornecer um mecanismo eficiente para distribuir software como atualizações de produtos (service packs e atualizações de segurança). Um par que tenha uma conexão a um servidor de distribuição de software pode obter a atualização de produto e propagá-la a outros membros do seu grupo.

## <a name="distributed-processing"></a>Processamento distribuído

- Divisão e distribuição de uma tarefa

  Uma tarefa de computação grande pode primeiro ser dividida em tarefas de computação menores separadas adequadas para os recursos de computação de um par. Um par pode fazer a divisão da tarefa de computação grande. Em seguida, a rede ponto a ponto pode distribuir as tarefas individuais para os pares separados no grupo. Cada par executa sua tarefa de computação e reporta o resultado para um ponto de acúmulo centralizado.

- Agregação de recursos do computador

  Outra maneira de usar a rede ponto a ponto para processamento distribuído é executar programas em cada par que é executado durante tempos de processador ocioso e que faz parte de uma tarefa de computação maior que é coordenada por um servidor central. Agregando os processadores de vários computadores, redes ponto a ponto podem transformar um grupo de computadores de par em um grande processador paralelo para tarefas de computação grandes.

## <a name="see-also"></a>Confira também

- <xref:System.Net.PeerToPeer.Collaboration>
