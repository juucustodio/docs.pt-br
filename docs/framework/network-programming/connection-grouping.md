---
description: 'Saiba mais sobre: agrupamento de conexões'
title: Agrupamento de conexão
ms.date: 03/30/2017
helpviewer_keywords:
- Internet, connections
- connections [.NET Framework], grouping
- WebRequest class, connection grouping
- network resources, connections
- connection pooling
ms.assetid: 2ec502e8-4ba0-4c22-9410-f28eaf4eee63
ms.openlocfilehash: 08e917b555da918ad4386a77938aeb57bc4e4ced
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791563"
---
# <a name="connection-grouping"></a>Agrupamento de conexão

O agrupamento de conexão associa solicitações específicas em um único aplicativo a um pool de conexão definido. Isso pode ser necessário para um aplicativo de camada intermediária que se conecta a um servidor back-end em nome de um usuário e usa um protocolo de autenticação que dá suporte à delegação, como o Kerberos ou para um aplicativo de camada intermediária que fornece suas próprias credenciais, como no exemplo abaixo. Por exemplo, suponha que um usuário, Julio, visite um site interno que exibe suas informações de folha de pagamento. Depois de autenticar Julio, o servidor de aplicativos de camada intermediária usa as credenciais de Julio para se conectar ao servidor back-end para recuperar suas informações de folha de pagamento. Em seguida, Sara visita o site e solicita suas informações de folha de pagamento. Como o aplicativo de camada intermediária já fez uma conexão usando as credenciais de Julio, o servidor back-end responde com as informações de Julio. No entanto, se o aplicativo atribuir cada solicitação enviada para o servidor back-end a um grupo de conexão formado com base no nome de usuário, cada usuário pertencerá a um pool de conexão separado e não poderá compartilhar informações de autenticação acidentalmente com outro usuário.  
  
 Para atribuir uma solicitação a um grupo de conexão específico, é necessário atribuir um nome à propriedade <xref:System.Net.WebRequest.ConnectionGroupName%2A> da <xref:System.Net.WebRequest> antes de fazer a solicitação.  
  
## <a name="see-also"></a>Consulte também

- [Gerenciando conexões](managing-connections.md)
- [Como: Atribuir informações de usuário a conexões de grupo](how-to-assign-user-information-to-group-connections.md)
