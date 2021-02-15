---
description: 'Saiba mais sobre: isolamento de rede para aplicativos da Windows Store'
title: Isolamento de rede para Aplicativos da Windows Store
ms.date: 03/30/2017
ms.assetid: b064497c-d956-46b8-838d-7a0223c7e200
ms.openlocfilehash: cc805cb5d5d761bb79b6a307caef6c809aabed16
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785713"
---
# <a name="network-isolation-for-windows-store-apps"></a>Isolamento de rede para Aplicativos da Windows Store

As classes nos <xref:System.Net> <xref:System.Net.Http> namespaces,, e <xref:System.Net.Http.Headers> podem ser usadas para desenvolver aplicativos da Windows Store ou aplicativos da área de trabalho. Quando usado em um aplicativo da Windows Store, as classes nesses namespaces são afetadas pelo isolamento de rede, parte do modelo de segurança de aplicativo usado pelo Windows 8. Para que o sistema permita o acesso à rede, os recursos de rede apropriados deverão ser habilitados no manifesto do aplicativo para um aplicativo da Windows Store.  
  
## <a name="checklist-for-network-isolation"></a>Lista de verificação para isolamento de rede  

Use esta lista de verificação para verificar se o isolamento de rede está configurado para o aplicativo da Windows Store.  
  
1. Determine a direção das solicitações de acesso de rede necessárias para o aplicativo. Isso pode ser solicitações de saída iniciadas pelo cliente ou solicitações de entrada não solicitadas ou pode ser ainda uma combinação de ambos esses tipos de solicitação de rede.  
  
2. Determine o tipo de recursos de rede com os quais o aplicativo se comunicará. Um aplicativo pode precisar se comunicar com recursos confiáveis em uma rede doméstica ou corporativa. Um aplicativo pode precisar se comunicar com recursos na Internet. Um aplicativo pode precisar de acesso a ambos os tipos de recursos de rede.  
  
3. Configure as funcionalidades de isolamento de rede mínimas necessárias no manifesto do aplicativo.  
  
4. Implante e execute seu aplicativo para testá-lo usando as ferramentas de isolamento de rede fornecidas para solução de problemas.  
  
Para obter informações mais detalhadas sobre como configurar os recursos de rede e as ferramentas de isolamento usadas para solucionar problemas de isolamento de rede, consulte [como configurar recursos de isolamento de rede](/previous-versions/windows/apps/hh770532(v=win.10)) na documentação do desenvolvedor da loja do Windows 8. x.
  
## <a name="see-also"></a>Consulte também

- [Conectando-se a um serviço Web](/previous-versions/windows/apps/hh761504(v=win.10))
- [Diretrizes e lista de verificação para isolamento de rede](/previous-versions/windows/apps/hh770532(v=win.10))
- [Início Rápido: Conectando-se usando HttpClient](/previous-versions/windows/apps/hh781239(v=win.10))
- [Como usar manipuladores HttpClient](/previous-versions/windows/apps/hh781241(v=win.10))
- [Como proteger conexões HttpClient](/previous-versions/windows/apps/hh781240(v=win.10))
- [Amostra de HttpClient](https://code.msdn.microsoft.com/windowsapps/HttpClient-sample-55700664)
