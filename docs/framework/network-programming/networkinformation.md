---
description: 'Saiba mais sobre: NetworkInformation'
title: NetworkInformation
ms.date: 03/30/2017
helpviewer_keywords:
- Network
ms.assetid: 31b44dd3-b903-4a48-8419-40419a3e4038
ms.openlocfilehash: 9092fd0593d9046f419018b882c08066a6bc654c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785699"
---
# <a name="networkinformation"></a>NetworkInformation

O namespace <xref:System.Net.NetworkInformation> permite que você colete informações sobre eventos, alterações, estatísticas e propriedades de rede. Você também pode determinar se um host remoto está acessível usando a classe <xref:System.Net.NetworkInformation.Ping?displayProperty=nameWithType>.  
  
## <a name="network-availability-and-events"></a>Disponibilidade de rede e eventos  

 A classe <xref:System.Net.NetworkInformation.NetworkChange?displayProperty=nameWithType> permite que você determine se o endereço de rede ou a disponibilidade foi alterada. Para usar essa classe, crie um manipulador de eventos para processar a alteração e associe-o a um <xref:System.Net.NetworkInformation.NetworkAddressChangedEventHandler> ou <xref:System.Net.NetworkInformation.NetworkAvailabilityChangedEventHandler>. Para obter mais informações, consulte [Como detectar a disponibilidade de rede e alterações de endereço](how-to-detect-network-availability-and-address-changes.md).  
  
## <a name="network-statistics-and-properties"></a>Propriedades e estatísticas de rede  

 Você pode coletar estatísticas de rede e propriedades por protocolo ou por interface. As classes <xref:System.Net.NetworkInformation.NetworkInterface>, <xref:System.Net.NetworkInformation.NetworkInterfaceType> e <xref:System.Net.NetworkInformation.PhysicalAddress> fornecem informações sobre um adaptador de rede específico, enquanto as classes <xref:System.Net.NetworkInformation.IPInterfaceProperties>, <xref:System.Net.NetworkInformation.IPGlobalProperties>, <xref:System.Net.NetworkInformation.IPGlobalStatistics>, <xref:System.Net.NetworkInformation.TcpStatistics> e <xref:System.Net.NetworkInformation.UdpStatistics> fornecem informações sobre os pacotes de camada 3 e de camada 4. Para obter mais informações, consulte [Como obter informações de interface e de protocolo](how-to-get-interface-and-protocol-information.md).  
  
## <a name="determine-if-a-remote-host-is-reachable"></a>Determinar se um Host remoto é alcançável  

 Você pode usar a classe <xref:System.Net.NetworkInformation.Ping> para determinar se um Host remoto está funcionando, se está na rede e se pode ser acessado. Para obter mais informações, consulte [Como executar ping em um host](how-to-ping-a-host.md).  
  
## <a name="see-also"></a>Consulte também

- [Amostras de programação de rede](network-programming-samples.md)

<!-- to-do: review sample links
- [Network Information Technology Sample](https://archive.msdn.microsoft.com/nclsamples/Wiki/View.aspx?title=Network%20Information)
- [NetStat Tool Technology Sample](https://archive.msdn.microsoft.com/nclsamples/Wiki/View.aspx?title=NetStat%20Tool)
- [Ping Client Technology Sample](https://archive.msdn.microsoft.com/nclsamples/Wiki/View.aspx?title=Ping%20Client)
-->
