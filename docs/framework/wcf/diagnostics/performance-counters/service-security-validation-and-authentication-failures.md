---
description: 'Saiba mais sobre: serviço: falhas de validação e autenticação de segurança'
title: 'Serviço: falhas de autenticação e validação de segurança'
ms.date: 03/30/2017
ms.assetid: 55c98268-b1ad-459d-851b-25ef52248187
ms.openlocfilehash: 8938c74e706526a02bf2ea5885951d067d6ebae9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99759478"
---
# <a name="service-security-validation-and-authentication-failures"></a>Serviço: falhas de autenticação e validação de segurança

Nome do contador: falhas de validação e autenticação de segurança  
  
## <a name="description"></a>Descrição  

 Esse contador é incrementado sempre que uma mensagem é rejeitada devido a um problema de segurança não coberto pelo contador "chamadas de segurança não autorizadas". Esses problemas incluem:  
  
- O token do cliente não pode ser lido a partir da mensagem.  
  
- Falha na autenticação do token do cliente (por exemplo, senha inadequada).  
  
- Falha na verificação da assinatura (por exemplo, a mensagem foi violada).  
  
- A mensagem é uma duplicata de uma anterior, o que pode ocorrer durante um ataque de repetição.  
  
- Ocorreu uma falha de descriptografia.  
  
- Alguns elementos necessários (por exemplo, carimbo de data/hora ausente ou bloco de dados criptografados) estão ausentes da mensagem.  
  
- Ocorreram erros durante o handshake TLSNEGO/SPNEGO.
