---
description: 'Saiba mais sobre: colaboração ponto a ponto'
title: Colaboração ponto a ponto
ms.date: 03/30/2017
ms.assetid: b6216d88-bccb-4a59-9f1c-9f751708e811
ms.openlocfilehash: 824ab3152c1ad765c2d19f5c6e719242255f606d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99738273"
---
# <a name="peer-to-peer-collaboration"></a>Colaboração ponto a ponto

A rede ponto a ponto é a utilização dos computadores relativamente poderosos (computadores pessoais) que existem na borda da Internet para mais do que apenas tarefas de computação baseadas no cliente. O PC moderno tem um processador muito rápido, ampla memória e um disco rígido grande, nenhum dos quais está sendo totalmente utilizado ao executar tarefas comuns de computação, como email e navegação na Web. O PC moderno pode facilmente atuar como um cliente e um servidor (um par) para vários tipos de aplicativos.  
  
A infraestrutura de colaboração ponto a ponto é uma implementação simplificada da infraestrutura de ponto a ponto do Microsoft Windows que aproveita o serviço Pessoas ao meu Redor no Windows Vista e em plataformas posteriores. Ele é mais adequado para aplicativos habilitados para par dentro de uma sub-rede para a qual o serviço Pessoas ao meu Redor opera, embora ele também possa atender a pontos de extremidade de Internet ou contatos. Ele incorpora o Gerenciador de Contatos comum que é usado pelo Live Messenger e outros aplicativos que reconhecem o Live para determinar pontos de extremidade de contato, presença e disponibilidade.  
  
## <a name="collaboration-applications"></a>Aplicativos de colaboração

 Um aplicativo de colaboração ponto a ponto típico é composto das seguintes etapas:  
  
- O par determina a identidade de um par que está interessado em hospedar uma sessão de colaboração  
  
- Uma solicitação para hospedar uma sessão é enviada de alguma forma e o par de host concorda em gerenciar a atividade de colaboração.  
  
- O host convida contatos na sub-rede (incluindo o solicitante) para uma sessão.  
  
- Todos os pares que desejam colaborar podem adicionar o host aos respectivos gerenciadores de contatos.  
  
- A maioria dos pares enviará respostas ao convite, aceito ou recusado, de volta para o par de host de maneira oportuna.  
  
- Todos os pares que desejam colaborar assinarão o par de host.  
  
- Enquanto os pares estiverem executando a atividade de colaboração inicial, o par de host poderá adicionar pares remotos a seu gerenciador de contatos. Ele também processa todas as respostas de convite para determinar quem aceitou, quem recusou e que não foi atendido.  Ele pode cancelar convites para aqueles que não responderam ou executar alguma outra atividade.  
  
- Neste ponto, o par de host pode iniciar uma sessão de colaboração com todos os pares convidados ou registrar um aplicativo com a infraestrutura de colaboração.  Aplicativos P2P usam a infraestrutura de colaboração ponto a ponto e o namespace <xref:System.Net.PeerToPeer.Collaboration> para coordenar as comunicações para jogos, BBS, conferência e outros aplicativos de presença sem servidor.  
  
## <a name="peer-to-peer-networking-security"></a>Segurança de rede ponto a ponto  

 Em um domínio do Active Directory, os controladores de domínio fornecem serviços de autenticação usando o Kerberos. Em um ambiente de par sem servidor, os pares devem fornecer sua própria autenticação. Para rede ponto a ponto, qualquer nó pode agir como uma AC, removendo a necessidade de um certificado raiz no repositório de raiz confiável do cada par. A autenticação é fornecida usando certificados autoassinados, formatados como certificados X.509. Esses são os certificados que são criados por cada par, o que gera o par de chaves pública/privada e o certificado é assinado usando a chave privada. O certificado autoassinado é usado para autenticação e para fornecer informações sobre a entidade de par. Assim como a autenticação X.509, a autenticação de rede ponto a ponto depende de uma cadeia de certificados ser rastreada de volta para uma chave pública confiável.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Net.PeerToPeer.Collaboration>
- [Sobre o namespace System.Net.PeerToPeer.Collaboration](about-the-system-net-peertopeer-collaboration-namespace.md)
