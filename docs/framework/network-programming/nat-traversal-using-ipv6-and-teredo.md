---
description: 'Saiba mais sobre: passagem NAT usando IPv6 e Teredo'
title: Passagem de NAT usando IPv6 e Teredo
ms.date: 03/30/2017
ms.assetid: 568cd245-3300-49ef-a995-d81bf845d961
ms.openlocfilehash: 4ff7f273c01ef52f4d307cbd3e0698c5cc2ead4d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785738"
---
# <a name="nat-traversal-using-ipv6-and-teredo"></a>Passagem de NAT usando IPv6 e Teredo

Foram feitas melhorias que dão suporte para a passagem de NAT (conversão de endereços de rede). Essas alterações são projetadas para uso com o IPv6 e Teredo, mas elas também são aplicáveis a outras tecnologias de túnel IP. Essas melhorias afetam as classes no <xref:System.Net> e nos namespaces relacionados.  
  
 Essas alterações podem afetar os aplicativos cliente e aplicativos para servidores que planejam usar tecnologias de túnel IP.  
  
 As alterações para dar suporte à passagem NAT estão disponíveis somente para aplicativos que usam o .NET Framework versão 4. Esses recursos não estão disponíveis em versões anteriores do .NET Framework.  
  
## <a name="overview"></a>Visão geral  

 O protocolo IP versão 4 (IPv4) definiu um endereço IPv4 como tendo 32 bits de comprimento. Como resultado, o IPv4 dá suporte a aproximadamente 4 bilhões endereços IP exclusivos (2^32). Conforme o número de computadores e dispositivos de rede na Internet se expandiu na década de 1990, os limites do espaço de endereço IPv4 tornou-se aparente.  
  
 Uma das várias técnicas usadas para estender o tempo de vida do IPv4 foi implantar o NAT para permitir que um único endereço IP público exclusivo representasse um grande número de endereços IP privados (Intranet privada). Os endereços IP privados subjacentes ao dispositivo NAT compartilham um único endereço IPv4 público. O dispositivo NAT pode ser um dispositivo de hardware dedicado (um ponto de acesso sem fio e roteador de baixo custo, por exemplo) ou um computador que executa um serviço para fornecer NAT. Um dispositivo ou serviço para esse endereço IP público converte os pacotes de rede IP entre a Internet pública e a Intranet privada.  
  
 Esse esquema funciona bem para aplicativos de cliente em execução na Intranet privada que enviam solicitações para outros endereços IP (geralmente servidores) na Internet. O dispositivo NAT ou servidor pode manter um mapeamento de solicitações de cliente de modo que quando uma resposta é retornada, ele sabe para que local enviar a resposta. Mas esse esquema apresenta problemas para aplicativos executados em uma Intranet privada subjacente ao dispositivo NAT que deseja fornecer serviços, escutar em busca de pacotes e responder. Isso é especialmente o caso para aplicativos de ponto a ponto.  
  
 O protocolo IPv6 definiu um endereço IPv4 como tendo 128 bits de comprimento. Como resultado, o IPv6 dá suporte a um espaço de endereço IP muito grande de 3,2 x 10^38 endereços exclusivos (2^128). Com um espaço de endereço desse tamanho, é possível que cada dispositivo conectado à Internet receba um endereço exclusivo. No entanto, há problemas. Grande parte do mundo ainda está usando somente IPv4. Em particular, muitos dos roteadores e pontos de acesso sem fio usados por residências, organizações e empresas de pequeno porte não dão suporte a IPv6. Além disso, alguns provedores de serviços de Internet que atendem esses clientes não dão suporte ou não configuraram o suporte a IPv6.  
  
 Várias tecnologias de transição para IPv6 foram desenvolvidas para realização de túnel de endereços IPv6 em um pacote IPv4. Essas tecnologias incluem túneis 6to4, ISATAP e Teredo que fornecem a atribuição de endereço e túnel automático host a host para unicast de tráfego IPv6 quando os hosts IPv6 devem fazer a passagem por redes IP4 para alcançar outras redes IPv6. Os pacotes IPv6 são enviados em túnel como pacotes IPv4. Várias técnicas de túnel estão sendo usadas que permitir a passagem de NAT para endereços IPv6 por meio de um dispositivo NAT.  
  
 Teredo é uma das tecnologias de transição para IPv6 que oferece conectividade IPv6 em redes IPv4. Teredo está documentado em RFC 4380 publicado pela IETF (Internet Engineering Task Force). O Windows XP SP2 e posteriores dão suporte a um adaptador virtual Teredo que pode fornecer um endereço IPv6 público no intervalo 2001:0::/32. Esse endereço IPv6 pode ser usado para escutar conexões de entrada da Internet e pode ser fornecido aos clientes habilitados para IPv6 que desejam se conectar ao serviço de escuta. Isso libera um aplicativo da preocupação sobre como endereçar um computador subjacente a um dispositivo NAT, já que o aplicativo pode se conectar a ele apenas usando seu endereço IPv6 Teredo.  
  
## <a name="enhancements-to-support-nat-traversal-and-teredo"></a>Melhorias para suporte a passagem NAT e Teredo  

 Descreve as melhorias adicionadas aos namespaces <xref:System.Net>, <xref:System.Net.NetworkInformation> e <xref:System.Net.Sockets> para dar suporte à passagem NAT usando o IPv6 e o Teredo.  
  
 Vários métodos foram adicionados à classe <xref:System.Net.NetworkInformation.IPGlobalProperties?displayProperty=nameWithType> para obter a lista de endereços IP unicast no host. O método <xref:System.Net.NetworkInformation.IPGlobalProperties.BeginGetUnicastAddresses%2A> começa uma solicitação assíncrona para recuperar a tabela de endereços IP unicast estáveis no computador local. O método <xref:System.Net.NetworkInformation.IPGlobalProperties.EndGetUnicastAddresses%2A> envia uma solicitação assíncrona pendente para recuperar a tabela de endereços IP unicast estáveis no computador local. O método <xref:System.Net.NetworkInformation.IPGlobalProperties.GetUnicastAddresses%2A> é uma solicitação síncrona para recuperar a tabela de endereços IP unicast estáveis no computador local, aguardando até que a tabela de endereços se estabilize se necessário.  
  
 A propriedade <xref:System.Net.IPAddress.IsIPv6Teredo%2A?displayProperty=nameWithType> pode ser usada para determinar se um <xref:System.Net.IPAddress> é um endereço Teredo IPv6.  
  
 Usar esses novos métodos de classe <xref:System.Net.NetworkInformation.IPGlobalProperties> em combinação com a propriedade <xref:System.Net.IPAddress.IsIPv6Teredo%2A> permite que um aplicativo localize facilmente o endereço Teredo. Um aplicativo normalmente só precisará saber o endereço Teredo local se ele estiver se comunicando essas informações para aplicativos remotos. Por exemplo, um aplicativo ponto a ponto pode enviar todos os seus endereços IPv6 em um servidor de emparelhamento que pode, em seguida, encaminhá-las a outros pares para permitir a comunicação direta.  
  
 Um aplicativo normalmente deve definir seu serviço de escuta para escutar em <xref:System.Net.IPAddress.IPv6Any?displayProperty=nameWithType> em vez de no endereço Teredo local. Portanto, se um par ou cliente remoto tem uma rota IPv6 direta para o host do serviço de escuta, o cliente ou par pode se conectar diretamente usando IPv6 e não precisa usar o Teredo para fazer túnel de pacotes.  
  
 Para aplicativos de TCP, a classe <xref:System.Net.Sockets.TcpListener?displayProperty=nameWithType> tem um método <xref:System.Net.Sockets.TcpListener.AllowNatTraversal%2A> para habilitar a passagem NAT. Para aplicativos de UDP, a classe <xref:System.Net.Sockets.UdpClient?displayProperty=nameWithType> tem um método <xref:System.Net.Sockets.UdpClient.AllowNatTraversal%2A> para habilitar a passagem NAT.  
  
 Para aplicativos que usam o <xref:System.Net.Sockets.Socket?displayProperty=nameWithType> e classes relacionadas, os métodos <xref:System.Net.Sockets.Socket.GetSocketOption%2A> e <xref:System.Net.Sockets.Socket.SetSocketOption%2A> podem ser usados com a opção de soquete <xref:System.Net.Sockets.SocketOptionName.IPProtectionLevel?displayProperty=nameWithType> para consultar, habilitar ou desabilitar a passagem NAT.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Net.IPAddress.IsIPv6Teredo%2A?displayProperty=nameWithType>
- <xref:System.Net.NetworkInformation.IPGlobalProperties.BeginGetUnicastAddresses%2A?displayProperty=nameWithType>
- <xref:System.Net.NetworkInformation.IPGlobalProperties.EndGetUnicastAddresses%2A?displayProperty=nameWithType>
- <xref:System.Net.NetworkInformation.IPGlobalProperties.GetUnicastAddresses%2A?displayProperty=nameWithType>
- <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=nameWithType>
- <xref:System.Net.Sockets.Socket.SetIPProtectionLevel%2A?displayProperty=nameWithType>
- <xref:System.Net.Sockets.TcpListener.AllowNatTraversal%2A?displayProperty=nameWithType>
- <xref:System.Net.Sockets.UdpClient.AllowNatTraversal%2A?displayProperty=nameWithType>
