---
description: 'Saiba mais sobre: interação de política de cache — idade máxima e atualização mínima'
title: Interação da política de cache – idade máxima e atualização mínima
ms.date: 03/30/2017
helpviewer_keywords:
- time-based cache policies
- Revalidate policy
- cache [.NET Framework], time-based policies
- freshness of cached resources
- maximum age policy
- minimum freshness policy
- age of cached resources
ms.assetid: 6567d451-ecec-496c-95a3-a415b99ba52a
ms.openlocfilehash: 882df93d44c0d745fcf30a7d9be3152797df4844
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791641"
---
# <a name="cache-policy-interactionmaximum-age-and-minimum-freshness"></a>Interação da política de cache – idade máxima e atualização mínima

Para ajudar a garantir que o conteúdo mais atualizado é retornado para o aplicativo cliente, a interação dos requisitos de revalidação do servidor e da política de cache de cliente sempre resulta na política de cache mais conservadora. Todos os exemplos deste tópico ilustram a política de cache para um recurso que é armazenado em cache em 1º de janeiro e expira em 4 de janeiro.  
  
 Os exemplos a seguir ilustram a política de cache que resulta da interação dos valores de idade máxima (`maxAge`) e atualização mínima (`minFresh`).  
  
- Se a política de cache definir `maxAge` = 2 dias e `minFresh` não for especificado, o conteúdo será revalidado em 3 de janeiro.  
  
- Se a política de cache definir `maxAge` = 2 dias e `minFresh` = 1 dia, de acordo com `maxAge`, o conteúdo ficará atualizado até 3 de janeiro. De acordo com `minFresh`, o conteúdo ficará atualizado até 3 de janeiro. Portanto, o conteúdo deverá ser revalidado em 3 de janeiro.  
  
- Se a política de cache definir `maxAge` = 2 dias e `minFresh` = 2 dias, de acordo com `maxAge`, o conteúdo ficará atualizado até 3 de janeiro. De acordo com `minFresh`, o conteúdo ficará atualizado até 2 de janeiro. Portanto, o conteúdo deverá ser revalidado em 2 de janeiro.  
  
## <a name="see-also"></a>Consulte também

- [Gerenciamento de cache para aplicativos de rede](cache-management-for-network-applications.md)
- [Política de cache](cache-policy.md)
- [Políticas de cache baseadas na localização](location-based-cache-policies.md)
- [Políticas de cache baseadas em tempo](time-based-cache-policies.md)
- [Configurando o cache em aplicativos de rede](configuring-caching-in-network-applications.md)
- [Interação da política de cache – idade máxima e desatualização máxima](cache-policy-interaction-maximum-age-and-maximum-staleness.md)
