---
description: 'Saiba mais sobre: rastreamento de atividade na segurança da mensagem'
title: Rastreamento de atividades em segurança de mensagens
ms.date: 03/30/2017
ms.assetid: 68862534-3b2e-4270-b097-8121b12a2c97
ms.openlocfilehash: 94fb6f60539465dd16e09a968679567e94d6cd24
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99770853"
---
# <a name="activity-tracing-in-message-security"></a>Rastreamento de atividades em segurança de mensagens

Este tópico descreve o rastreamento de atividades para o processamento de segurança, que ocorre nas três fases a seguir.  
  
- Negociação/SCT do Exchange. Isso pode acontecer no transporte posteriormente (por meio de troca de dados binária) ou camada de mensagem (por meio de trocas de mensagens SOAP).  
  
- Criptografia/descriptografia de mensagens, com verificação de assinatura e autenticação. Os rastreamentos aparecem na atividade ambiente, normalmente "ação do processo".  
  
- Autorização e verificação. Isso pode acontecer localmente ou durante a comunicação entre pontos de extremidade.  
  
## <a name="negotiationsct-exchange"></a>Negociação/SCT de intercâmbio  

 Na fase de negociação/SCT Exchange, dois tipos de atividade são criados no cliente: "configurar sessão segura" e "fechar sessão segura". "Configurar sessão segura" abrange rastreamentos para as trocas de mensagens RST/RSTR/SCT, enquanto "fechar sessão segura" inclui rastreamentos para a mensagem de cancelamento.  
  
 No servidor, cada solicitação/resposta para o RST/RSTR/SCT aparece em sua própria atividade. Se estiver `propagateActivity` = `true` no servidor e no cliente, as atividades no servidor terão a mesma ID e aparecerão juntas na "sessão segura de instalação" quando visualizadas por meio do Visualizador de rastreamento de serviço.  
  
 Esse modelo de rastreamento de atividade é válido para autenticação de nome de usuário/senha, autenticação de certificado e autenticação NTLM.  
  
 A tabela a seguir lista as atividades e os rastreamentos para negociação e SCT do Exchange.  
  
||Tempo em que a negociação/SCT ocorre no Exchange|Atividades|Rastreamentos|  
|-|-------------------------------------------------|----------------|------------|  
|Transporte seguro<br /><br /> (HTTPS, SSL)|Na primeira mensagem recebida.|Os rastreamentos são emitidos na atividade ambiente.|-Rastreamentos do Exchange<br />-Canal seguro estabelecido<br />-Compartilhe segredos obtidos.|  
|Camada de mensagem segura<br /><br /> (WSHTTP)|Na primeira mensagem recebida.|No cliente:<br /><br /> -"Configurar sessão segura" fora da "ação do processo" da primeira mensagem, para cada solicitação/resposta para RST/RSTR/SCT.<br />-"Fechar sessão segura" para o cancelamento do Exchange, fora da "atividade fechar proxy". Essa atividade pode ocorrer fora de alguma outra atividade de ambiente, dependendo de quando a sessão segura é fechada.<br /><br /> No servidor:<br /><br /> -Uma atividade de "processar ação" para cada solicitação/resposta para RST/SCT/Cancel no servidor. `propagateActivity` = `true` As atividades se, RST/RSTR/SCT são mescladas com "configurar a sessão de segurança" e o cancelamento é mesclado com a atividade de "fechamento" do cliente.<br /><br /> Há dois estágios para "configurar sessão segura":<br /><br /> 1. negociação de autenticação. Isso é opcional se o cliente já tiver as credenciais apropriadas. Essa fase pode ser feita por meio de transporte seguro ou por trocas de mensagens. No último caso, podem ocorrer trocas de 1 ou 2 RST/RSTR. Para essas trocas, os rastreamentos são emitidos em novas atividades de solicitação/resposta, conforme projetado anteriormente.<br />2. o SCT (estabelecimento de sessão segura), no qual uma troca de RST/RSTR acontece aqui. Isso tem as mesmas atividades de ambiente descritas anteriormente.|-Rastreamentos do Exchange<br />-Canal seguro estabelecido<br />-Compartilhe segredos obtidos.|  
  
> [!NOTE]
> No modo de segurança mista, a autenticação de negociação ocorre em intercâmbios binários, mas o SCT acontece na troca de mensagens. No modo de transporte puro, a negociação ocorre apenas no transporte sem atividades adicionais.  
  
## <a name="message-encryption-and-decryption"></a>Criptografia e descriptografia de mensagens  

 A tabela a seguir lista as atividades e os rastreamentos para criptografia/descriptografia de mensagens, bem como autenticação de assinatura.  
  
||Transporte seguro<br /><br /> (HTTPS, SSL) e camada de mensagem segura<br /><br /> (WSHTTP)|  
|-|---------------------------------------------------------------------------------|  
|Tempo em que a criptografia/descriptografia de mensagens, bem como a autenticação de assinatura ocorre|Na mensagem recebida|  
|Atividades|Os rastreamentos são emitidos na atividade processAction no cliente e no servidor.|  
|Rastreamentos|-sendSecurityHeader (remetente):<br />-Assinar mensagem<br />-Criptografar dados de solicitação<br />-receiveSecurityHeader (destinatário):<br />-Verificar assinatura<br />-Descriptografar dados de resposta<br />-Autenticação|  
  
> [!NOTE]
> No modo de transporte puro, a criptografia/descriptografia de mensagens ocorre apenas no transporte sem atividades adicionais.  
  
## <a name="authorization-and-verification"></a>Autorização e verificação  

 A tabela a seguir lista as atividades e os rastreamentos para autorização.  
  
||Hora em que a autorização ocorre|Atividades|Rastreamentos|  
|-|-------------------------------------|----------------|------------|  
|Local (padrão)|Depois que a mensagem é descriptografada no servidor|Os rastreamentos são emitidos na atividade processAction no servidor.|Autorizado pelo usuário.|  
|Remoto|Depois que a mensagem é descriptografada no servidor|Os rastreamentos são emitidos em uma nova atividade chamada pela atividade processAction.|Autorizado pelo usuário.|
