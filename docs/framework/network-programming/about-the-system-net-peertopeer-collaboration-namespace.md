---
description: 'Saiba mais sobre: sobre o namespace System .net. PeerToPeer. Collaboration'
title: Sobre o namespace System.Net.PeerToPeer.Collaboration
ms.date: 03/30/2017
ms.assetid: b5d8c1c1-6844-4947-9759-c7f1b564bded
ms.openlocfilehash: cb51208b2424b93e963101943652c57f0266baf6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801911"
---
# <a name="about-the-systemnetpeertopeercollaboration-namespace"></a>Sobre o namespace System.Net.PeerToPeer.Collaboration

O namespace <xref:System.Net.PeerToPeer.Collaboration> fornece classes e APIs que são usadas para implementar as atividades de colaboração de pares usando a infraestrutura de Colaboração Ponto a Ponto.  
  
## <a name="classes"></a>Classes  

 As principais classes usadas na implementação de uma atividade de Colaboração Ponto a Ponto são:  
  
- O <xref:System.Net.PeerToPeer.Collaboration.ContactManager>, que pode ser usado para armazenar contatos de pares.  
  
- O <xref:System.Net.PeerToPeer.Collaboration.PeerApplication> no qual a colaboração ocorre, como um jogo, cliente de chat ou solução de conferência.  
  
- Os pares que colaborarão em uma atividade.  Esses pares podem ser representados como objetos <xref:System.Net.PeerToPeer.Collaboration.PeerContact>, <xref:System.Net.PeerToPeer.Collaboration.PeerNearMe> ou <xref:System.Net.PeerToPeer.Collaboration.PeerEndPoint>.  
  
- A classe <xref:System.Net.PeerToPeer.Collaboration.PeerCollaboration> estática em si, que especifica quais aplicativos estão disponíveis e quais pares participam deles.  
  
 Os métodos <xref:System.Net.PeerToPeer.Collaboration.PeerContact.Invite%2A> são usados para convidar pares para uma sessão de colaboração.  Um par de chamada pode assinar outro par para eventos que sinalizam atualizações para informações de aplicativo, objeto ou presença, afiliadas à sessão de colaboração. Classes de presença especificam se um <xref:System.Net.PeerToPeer.Collaboration.Peer> está disponível para colaboração e a classe <xref:System.Net.PeerToPeer.Collaboration.PeerScope> é usada para especificar a quantidade de participação permitida para um par: <xref:System.Net.PeerToPeer.Collaboration.PeerScope.Internet> (global), <xref:System.Net.PeerToPeer.Collaboration.PeerScope.NearMe>, (sub-rede) ou <xref:System.Net.PeerToPeer.Collaboration.PeerScope.None>.  
  
 Uma sessão de colaboração é composta por quatro etapas:  
  
- Descoberta. Descubra ou publique aplicativos, pares e informações de presença.  Por exemplo, encontre outras pessoas na sub-rede local que têm os mesmos jogos instalados.  
  
- Convite. Envie e aceite convites seguros de pares remotos para iniciar ou participar de sessões de <xref:System.Net.PeerToPeer.Collaboration.PeerCollaboration>.  
  
- Gerenciamento de contatos. Adicione pares descobertos como um contato a um <xref:System.Net.PeerToPeer.Collaboration.ContactManager>.  
  
- Comunicação. Quando a comunicação for estabelecida, use as APIs <xref:System.Net>, a API <xref:System.Net.PeerToPeer> ou as classes de Canal Par do Windows Communication Foundation para comunicações com vários participantes.  
  
 Por exemplo, o par de host inicia uma sessão de colaboração e utiliza o método <xref:System.Net.PeerToPeer.Collaboration.ContactManager.CreateContact%2A> para adicionar um par remoto e um de seus pares locais ao Gerenciador de Contatos do par de host.  Em seguida, os três usuários participarão em sua própria sessão de colaboração particular.  
  
 Os aplicativos P2P típicos são: chamadas em conferência para anotações ou quadro de comunicações de colaboração, aplicativos de chat sem servidor, anúncios interativos e sessões de jogos online.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Net.PeerToPeer.Collaboration>
