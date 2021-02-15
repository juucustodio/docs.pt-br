---
description: 'Saiba mais sobre: ação de conclusão de instância'
title: Ação de conclusão da instância
ms.date: 03/30/2017
ms.assetid: 90cc99d2-9fef-42fd-bcbf-a56917993721
ms.openlocfilehash: 84405ca9869369e4fe00b0049d628671a79a9f68
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792681"
---
# <a name="instance-completion-action"></a>Ação de conclusão da instância

A propriedade **ação de conclusão da instância** do repositório da instância do fluxo de trabalho SQL permite especificar se os dados e os metadados das instâncias de fluxo de trabalho são excluídos do banco de dados de persistência depois que as instâncias são concluídas. Os valores permitidos para essa propriedade são **DeleteAll** e **DeleteNothing**. A lista a seguir descreve as opções:

- **DeleteAll (padrão).** Se o valor da propriedade é definido como DeleteAll, os dados e os metadados de instâncias de fluxo de trabalho são excluídos de base de dados de persistência depois que as instâncias são concluídas.

- **DeleteNothing.** Se o valor da propriedade é definida como DeleteNothing, os dados e os metadados de instâncias de fluxo de trabalho são mantidos na base de dados de persistência mesmo após as instâncias são concluídas.

  > [!CAUTION]
  > Mantendo informações de estado da instância depois que as instâncias são causas concluídas o base de dados de persistência crescer em tamanho. Como o tamanho de base de dados cresce as operações de base de dados que o subsistema de persistência executa levam mais tempo, portanto você precisa limpar periodicamente informações de estado da instância de base de dados de persistência para que os serviços executar a nível que satisfazem às suas necessidades de desempenho.
