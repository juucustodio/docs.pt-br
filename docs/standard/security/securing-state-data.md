---
title: Protegendo dados de estado
description: Declare os dados de estado como variáveis privadas ou internas para limitar o acesso a ele. Esses dados ainda podem ser acessados por meio de reflexão, serialização e depuração.
ms.date: 03/30/2017
helpviewer_keywords:
- security [.NET], state data
- code security, state data
- secure coding, state data
- state data security
ms.assetid: 12671309-2877-43fe-a3df-6863507e712d
ms.openlocfilehash: 849ed993befaceda1b04becbb7fb2530c5c62a77
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94824155"
---
# <a name="securing-state-data"></a>Protegendo dados de estado

Os aplicativos que lidam com dados confidenciais ou que fazem qualquer tipo de decisões de segurança precisam manter esses dados sob seu próprio controle e não podem permitir que outros códigos potencialmente mal-intencionados acessem os dados diretamente. A melhor maneira de proteger os dados na memória é declarar os dados como privados ou internos (com escopo limitado às variáveis do mesmo assembly). No entanto, mesmo esses dados estão sujeitos ao acesso que você deve estar ciente:  
  
- Usando mecanismos de reflexão, um código altamente confiável que pode fazer referência a seu objeto pode obter e definir membros privados.  
  
- Usar o código de serialização e altamente confiável pode efetivamente obter e definir membros privados se puder acessar os dados correspondentes na forma serializada do objeto.  
  
- Em depuração, esses dados podem ser lidos.  
  
 Certifique-se de que nenhum de seus próprios métodos ou Propriedades exponha esses valores involuntariamente.  
  
## <a name="see-also"></a>Confira também

- [Diretrizes de codificação segura](secure-coding-guidelines.md)
- [Segurança de ASP.NET Core](/aspnet/core/security/)
