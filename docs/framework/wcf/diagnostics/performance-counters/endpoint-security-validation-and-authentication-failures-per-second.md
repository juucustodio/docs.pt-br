---
description: 'Saiba mais sobre: ponto de extremidade: falhas de validação e autenticação de segurança por segundo'
title: 'Ponto de extremidade: falhas de autenticação e validação de segurança por segundo'
ms.date: 03/30/2017
ms.assetid: 89a70b90-d7e4-4b03-9b84-4dc88ce3d605
ms.openlocfilehash: aa5ccc4049dc81a7c2d545cfc70e9078ac72d87a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99655428"
---
# <a name="endpoint-security-validation-and-authentication-failures-per-second"></a>Ponto de extremidade: falhas de autenticação e validação de segurança por segundo

Nome do contador: falhas de validação e autenticação de segurança por segundo  
  
## <a name="description"></a>Descrição  

 Esse contador é incrementado sempre que uma mensagem é rejeitada devido a um problema de segurança não coberto pelo contador "chamadas de segurança não autorizadas". Esses problemas incluem:  
  
- O token do cliente não pode ser lido a partir da mensagem.  
  
- Falha na autenticação do token do cliente (por exemplo, senha inadequada).  
  
- Falha na verificação da assinatura (por exemplo, a mensagem foi violada).  
  
- A mensagem é uma duplicata de uma anterior, o que pode ocorrer durante um ataque de repetição.  
  
- Ocorreu uma falha de descriptografia.  
  
- Alguns elementos necessários (por exemplo, carimbo de data/hora ausente ou bloco de dados criptografados) estão ausentes da mensagem.  
  
- Ocorreram erros durante o handshake TLSNEGO/SPNEGO.  
  
 Este contador é do tipo de contador de desempenho [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), cujo valor é calculado usando a seguinte fórmula:  
  
 (N1-N0)/((D1-D0)/F)
