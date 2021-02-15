---
description: 'Saiba mais sobre: Proteção Estendida para Autenticação visão geral'
title: Proteção estendida para visão geral de autenticação
ms.date: 03/30/2017
ms.assetid: 3d2ceffe-a7bf-4bd9-a5a2-9406423bd7f8
ms.openlocfilehash: 5f79092d71266176af3916e919be0018793959ad
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99780265"
---
# <a name="extended-protection-for-authentication-overview"></a>Proteção estendida para visão geral de autenticação

Proteção Estendida para Autenticação ajuda a proteger contra ataques MITM (Man-in-the-Middle), nos quais um invasor intercepta as credenciais de um cliente e as encaminha para um servidor.  
  
 Considere um cenário com três participantes: um cliente, servidor e invasor. O servidor tem a URL `https://server` , enquanto o invasor tem a URL `https://attacker` . O invasor vaza o cliente para acessar o invasor como se fosse o servidor. Em seguida, o invasor envia uma solicitação ao servidor. Se o invasor estiver tentando acessar um recurso seguro, o servidor responderá ao invasor com um cabeçalho WWW-Authenticate. O invasor não tem as informações de autenticação e, portanto, envia o cabeçalho de WWW-Authenticate para o cliente. O cliente envia o cabeçalho de autorização para o invasor, e o invasor envia o cabeçalho para o servidor e obtém acesso aos recursos seguros usando as credenciais do cliente.  
  
 Atualmente, quando um aplicativo cliente se autentica no servidor usando Kerberos, Digest ou NTLM usando HTTPS, um canal de TLS (segurança de nível de transporte) é estabelecido primeiro e a autenticação ocorre usando esse canal. No entanto, não há nenhuma associação entre a chave de sessão gerada por protocolo SSL (SSL) e a chave de sessão que é gerada durante a autenticação. Portanto, no cenário anterior, se a comunicação assumir o lugar de um TLS (como um canal HTTPS), há dois canais SSL criados: um entre o cliente e o invasor e outro entre o invasor e o servidor. As credenciais do cliente são enviadas do cliente para o servidor primeiro por meio do canal SSL entre o cliente e o invasor e, em seguida, pelo canal entre o invasor e o servidor. Depois que as credenciais do cliente chegarem ao servidor, o servidor verificará as credenciais sem detectar que o canal pelo qual essas credenciais foram enviadas foi originado com o invasor e não o cliente.  
  
 A solução é usar um canal externo protegido por TLS e um canal interno autenticado pelo cliente e passar um token de associação de canal (CBT) para o servidor. O CBT é uma propriedade do canal externo protegido por TLS e é usado para associar o canal externo a uma conversa no canal interno autenticado pelo cliente.  
  
 No cenário anterior, o CBT do canal do cliente-invasor TLS é mesclado com as informações de autorização que são enviadas para o servidor. Um servidor com reconhecimento de CBT compara o CBT contido nas informações de autenticação do cliente, que corresponde ao canal do invasor do cliente, para o CBT conectado ao canal do servidor do invasor. Um CBT é específico para o destino de um canal, portanto, o CBT do invasor do cliente não corresponde ao invasor-servidor CBT. Isso permite que o servidor detecte o ataque MITM e recuse a solicitação de autenticação.  
  
 O lado do cliente não requer nenhuma definição de configuração. Depois que o cliente tiver sido atualizado para passar o CBT para o servidor, ele sempre fará isso. Se o servidor também tiver sido atualizado, ele poderá ser configurado para usar o CBT ou ignorá-lo. Se ele não tiver sido atualizado, ele o ignorará.  
  
 O servidor pode ter os seguintes níveis de proteção:  
  
- Nenhum. Nenhuma validação de associação de canal é executada. Esse é o comportamento de todos os servidores que não foram atualizados.  
  
- Parcial. Todos os clientes que foram atualizados devem fornecer informações de associação de canal para o servidor. Os clientes que não foram atualizados não precisam fazer isso. Essa é uma opção intermediária que permite a compatibilidade de aplicativos.  
  
- Completa. Todos os clientes devem fornecer informações de associação de canal. O servidor rejeita solicitações de autenticação de clientes que não fazem isso.  
  
 Para obter mais informações, consulte o exemplo de proteção do Win7 CBT/Extended.  
  
## <a name="see-also"></a>Consulte também

- [Modelo de segurança para o Windows Server app Fabric](/previous-versions/appfabric/ee677202(v=azure.10))
