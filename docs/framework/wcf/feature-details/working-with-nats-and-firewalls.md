---
description: 'Saiba mais sobre: trabalhando com NATs e firewalls'
title: Trabalhando com NATs e firewalls
ms.date: 03/30/2017
helpviewer_keywords:
- firewalls [WCF]
- NATs [WCF]
ms.assetid: 74db0632-1bf0-428b-89c8-bd53b64332e7
ms.openlocfilehash: 6d5adb25ebe77e237a3456d450e8f59c65043bfc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99704258"
---
# <a name="working-with-nats-and-firewalls"></a>Trabalhando com NATs e firewalls

O cliente e o servidor de uma conexão de rede geralmente não têm um caminho direto e aberto para comunicação. Os pacotes são filtrados, roteados, analisados e transformados nos computadores do ponto de extremidade e por máquinas intermediárias na rede. As NATs (conversões de endereço de rede) e os firewalls são exemplos comuns de aplicativos intermediários que podem participar da comunicação de rede.  
  
 Os transportes Windows Communication Foundation (WCF) e os padrões de troca de mensagens (MEPs) reagem de forma diferente ao, à presença de NATs e firewalls. Este tópico descreve como os NATs e os firewalls funcionam em topologias de rede comuns. As recomendações para combinações específicas de transportes do WCF e MEPs são dadas para ajudar a tornar seus aplicativos mais robustos para NATs e firewalls na rede.  
  
## <a name="how-nats-affect-communication"></a>Como os NATs afetam a comunicação  

 O NAT foi criado para permitir que vários computadores compartilhem um único endereço IP externo. Um NAT de remapeamento de porta mapeia um endereço IP interno e uma porta para uma conexão com um endereço IP externo com um novo número de porta. O novo número de porta permite que o NAT Correlacione o tráfego de retorno com a comunicação original. Muitos usuários domésticos agora têm um endereço IP que só é roteável de forma privada e contam com um NAT para fornecer roteamento global de pacotes.  
  
 Um NAT não fornece um limite de segurança. No entanto, as configurações comuns de NAT impedem que as máquinas internas sejam endereçadas diretamente. Isso protege as máquinas internas de algumas conexões indesejadas e dificulta a gravação de aplicativos de servidor que devem enviar dados de forma assíncrona de volta ao cliente. O NAT reescreve os endereços nos pacotes para que pareçam que as conexões se originam no computador NAT. Isso faz com que o servidor falhe ao tentar abrir uma conexão de volta ao cliente. Se o servidor usar o endereço percebido do cliente, ele falhará porque o endereço do cliente não pode ser roteado publicamente. Se o servidor usar o endereço NAT, ele não se conectará porque nenhum aplicativo está escutando nesse computador.  
  
 Alguns NATs dão suporte à configuração de regras de encaminhamento para permitir que computadores externos se conectem a um determinado computador interno. As instruções para configurar regras de encaminhamento variam entre NATs diferentes, e solicitar que os usuários finais alterem sua configuração NAT não é recomendável para a maioria dos aplicativos. Muitos usuários finais não podem ou não querem alterar a configuração de NAT para um aplicativo específico.  
  
## <a name="how-firewalls-affect-communication"></a>Como os firewalls afetam a comunicação  

 Um *Firewall* é um dispositivo de software ou hardware que aplica regras ao tráfego que passa para decidir se deseja permitir ou negar a passagem. Você pode configurar firewalls para examinar fluxos de entrada e/ou saída de tráfego. O firewall fornece um limite de segurança para a rede na borda da rede ou no host do ponto de extremidade. Os usuários empresariais tradicionalmente mantiveram seus servidores atrás de um firewall para evitar ataques mal-intencionados. Desde a introdução do firewall pessoal no Windows XP SP2, o número de usuários domésticos atrás de um firewall também aumentou consideravelmente. Isso torna provável que uma ou ambas as extremidades de uma conexão tenham um firewall examinando os pacotes.  
  
 Os firewalls variam muito em termos de complexidade e capacidade para examinar os pacotes. Firewalls simples aplicam regras com base nos endereços de origem e de destino e portas em pacotes. Os firewalls inteligentes também podem examinar o conteúdo dos pacotes para tomar decisões. Esses firewalls vêm em muitas configurações diferentes e geralmente são usados para aplicativos especializados.  
  
 Uma configuração comum para um firewall de usuário inicial é proibir conexões de entrada, a menos que uma conexão de saída tenha sido feita anteriormente para esse computador. Uma configuração comum para um firewall de usuário de negócios é proibir conexões de entrada em todas as portas, exceto um grupo identificado especificamente. Um exemplo é um firewall que proíbe conexões em todas as portas, exceto as portas 80 e 443 para fornecer o serviço HTTP e HTTPS. Existem firewalls gerenciados para usuários domésticos e empresariais que permitem que um usuário ou processo confiável no computador altere a configuração do firewall. Os firewalls gerenciados são mais comuns para usuários domésticos em que não há nenhuma política corporativa controlando o uso da rede.  
  
## <a name="using-teredo"></a>Usando Teredo  

 O Teredo é uma tecnologia de transição IPv6 que permite a endereçamento direto de computadores por trás de um NAT. O Teredo conta com o uso de um servidor que pode ser roteado de forma pública e global para anunciar possíveis conexões. O servidor Teredo fornece ao cliente de aplicativo e ao servidor um ponto de reunião comum no qual eles podem trocar informações de conexão. Em seguida, os computadores solicitam um endereço Teredo temporário e os pacotes são encapsulados por meio da rede existente. O suporte a Teredo no WCF requer a habilitação do suporte a IPv6 e Teredo no sistema operacional. Os sistemas operacionais Windows XP e posteriores dão suporte a Teredo. O Windows Vista e sistemas operacionais posteriores dão suporte a IPv6 por padrão e só exigem que o usuário habilite o Teredo. O Windows XP SP2 e o Windows Server 2003 exigem que o usuário habilite o IPv6 e o Teredo. Para obter mais informações, consulte a [visão geral do Teredo](/previous-versions/windows/it-pro/windows-xp/bb457011(v=technet.10)).  
  
## <a name="choosing-a-transport-and-message-exchange-pattern"></a>Escolhendo um padrão de troca de mensagens e transporte  

 Selecionar um transporte e MEP é um processo de três etapas:  
  
1. Analise a Endereçabilidade dos computadores do ponto de extremidade. Os servidores corporativos normalmente têm endereçamento direto, enquanto os usuários finais normalmente têm sua Endereçabilidade bloqueada por NATs. Se ambos os pontos de extremidade estiverem atrás de um NAT, como em cenários ponto a ponto entre os usuários finais, talvez você precise de uma tecnologia como o Teredo para fornecer Endereçabilidade.  
  
2. Analise as restrições de protocolo e porta dos computadores do ponto de extremidade. Os servidores corporativos são geralmente protegidos por firewalls fortes que bloqueiam muitas portas. No entanto, a porta 80 é frequentemente aberta para permitir o tráfego HTTP, e a porta 443 está aberta para permitir o tráfego HTTPS. Os usuários finais têm menos probabilidade de ter restrições de porta, mas podem estar atrás de um firewall que permita somente conexões de saída. Alguns firewalls permitem o gerenciamento por aplicativos no ponto de extremidade para abrir conexões seletivamente.  
  
3. Computar os transportes e MEPs que a endereçamento e as restrições de porta da permissão de rede.  
  
 Uma topologia comum para aplicativos cliente-servidor é ter clientes que estão por trás de um NAT sem Teredo com um firewall somente de saída e um servidor que é diretamente endereçável com um firewall forte. Nesse cenário, o transporte TCP com um MEP duplex e um transporte HTTP com uma solicitação-resposta MEP funcionam bem. Uma topologia comum para aplicativos ponto a ponto é ter os dois pontos de extremidade por trás de NATs e firewalls. Nesse cenário, e em cenários em que a topologia de rede é desconhecida, considere as seguintes recomendações:  
  
- Não use transportes duplos. Um transporte duplo abre mais conexões, o que reduz a possibilidade de conexão bem-sucedida.  
  
- Suporte ao estabelecimento de canais de back-up na conexão de origem. O uso de canais traseiros, como em duplex TCP, abre menos conexões, o que aumenta a chance de conexão bem-sucedida.  
  
- Empregue um serviço acessível para registrar pontos de extremidade ou retransmitir o tráfego. Usar um serviço de conexão acessível globalmente, como um servidor Teredo, aumenta muito a chance de se conectar com êxito quando a topologia de rede é restritiva ou desconhecida.  
  
 As tabelas a seguir examinam o MEPs unidirecional, solicitação-resposta e duplex, e os transportes padrão TCP, TCP com Teredo e HTTP duplo no WCF.  
  
|Endereçabilidade|Servidor direto|Servidor direto com passagem NAT|NAT do servidor|NAT de servidor com passagem NAT|  
|--------------------|-------------------|--------------------------------------|----------------|-----------------------------------|  
|Cliente direto|Qualquer transporte e MEP|Qualquer transporte e MEP|Não há suporte.|Não há suporte.|  
|Cliente direto com passagem NAT|Qualquer transporte e MEP.|Qualquer transporte e MEP.|Não há suporte.|TCP com Teredo e qualquer MEP. O Windows Vista tem uma opção de configuração de todo o computador para dar suporte a HTTP com Teredo.|  
|NAT de cliente|Qualquer transporte não duplo e MEP. O duplex MEP requer transporte TCP.|Qualquer transporte não duplo e MEP. O duplex MEP requer transporte TCP.|Não há suporte.|Não há suporte.|  
|NAT de cliente com passagem NAT|Qualquer transporte não duplo e MEP. O duplex MEP requer transporte TCP.|Todos, exceto HTTP duplo e qualquer MEP. O duplex MEP requer transporte TCP. O transporte TCP duplo requer Teredo. O Windows Vista tem uma opção de configuração de todo o computador para dar suporte a HTTP com Teredo.|Não há suporte.|TCP com Teredo e qualquer MEP. O Windows Vista tem uma opção de configuração de todo o computador para dar suporte a HTTP com Teredo.|  
  
|Restrições de firewall|Servidor aberto|Servidor com Firewall gerenciado|Servidor com firewall somente HTTP|Servidor com firewall somente de saída|  
|---------------------------|-----------------|----------------------------------|-------------------------------------|-----------------------------------------|  
|Cliente aberto|Qualquer transporte e MEP.|Qualquer transporte e MEP.|Qualquer transporte HTTP e MEP.|Não há suporte.|  
|Cliente com Firewall gerenciado|Qualquer transporte não duplo e MEP. O duplex MEP requer transporte TCP.|Qualquer transporte não duplo e MEP. O duplex MEP requer transporte TCP.|Qualquer transporte HTTP e MEP.|Não há suporte.|  
|Cliente com firewall somente HTTP|Qualquer transporte HTTP e MEP.|Qualquer transporte HTTP e MEP.|Qualquer transporte HTTP e MEP.|Não há suporte.|  
|Cliente com firewall somente de saída|Qualquer transporte não duplo e MEP. O duplex MEP requer transporte TCP.|Qualquer transporte não duplo e MEP. O duplex MEP requer transporte TCP.|Qualquer transporte HTTP e qualquer MEP não duplex.|Não há suporte.|
