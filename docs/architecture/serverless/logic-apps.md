---
title: Aplicativos lógicos do Azure-aplicativos sem servidor
description: Os aplicativos lógicos do Azure permitem a criação de fluxos de trabalho escalonáveis automatizados que integram aplicativos e dados entre serviços de nuvem e sistemas locais.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 11fdf5b5f176eb0d66eee6dde7638d3eae1e1f55
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91171839"
---
# <a name="azure-logic-apps"></a>Aplicativos Lógicos do Azure

O [aplicativo lógico do Azure](/azure/logic-apps) fornece um mecanismo sem servidor para criar fluxos de trabalho automatizados para integrar aplicativos e dados entre serviços de nuvem e sistemas locais. Você cria fluxos de trabalho usando um designer visual. Você pode disparar fluxos de trabalho com base em eventos ou temporizadores e aproveitar os conectores para aplicativos de integração e facilitar a comunicação entre empresas (B2B). Os aplicativos lógicos se integram perfeitamente com Azure Functions.

![Logotipo do aplicativo lógico do Azure](./media/logic-apps-logo.png)

Os aplicativos lógicos podem fazer mais do que apenas conectar seus serviços de nuvem (como funções) com recursos de nuvem (como filas e bancos de dados). Você também pode orquestrar fluxos de trabalho locais com o gateway local. Por exemplo, você pode usar o aplicativo lógico para disparar um procedimento armazenado SQL local em resposta a um evento baseado em nuvem ou lógica condicional em seu fluxo de trabalho. Saiba mais sobre como [se conectar a fontes de dados locais com o gateway de dados local do Azure](/azure/analysis-services/analysis-services-gateway).

![Arquitetura de aplicativos lógicos](./media/logic-apps-architecture.png)

Assim como Azure Functions, você inicia fluxos de trabalho de aplicativo lógico com um gatilho. Há muitos disparadores para sua escolha. A captura a seguir mostra apenas alguns dos mais populares de centenas que estão disponíveis.

![Gatilhos de Aplicativos Lógicos](./media/logic-app-triggers.png)

Depois que o aplicativo é disparado, você pode usar o designer visual para criar etapas, loops, condições e ações. Todos os dados ingeridos em uma etapa anterior estão disponíveis para uso nas etapas subsequentes. O fluxo de trabalho a seguir carrega URLs de um banco de dados CosmosDB. Ele localiza aqueles com um host de `t.co` e, em seguida, pesquisa-os no Twitter. Se encontrar tweets correspondentes, ele atualizará os documentos com os tweets relacionados chamando uma função.

![Fluxo de trabalho do aplicativo lógico](./media/logic-app-workflow.png)

O painel aplicativos lógicos mostra o histórico da execução de seus fluxos de trabalho e se cada execução foi concluída com êxito ou não. Você pode navegar para qualquer execução específica e inspecionar os dados usados por cada etapa para solução de problemas. Os aplicativos lógicos também fornecem modelos existentes que você pode editar e são adequados para fluxos de trabalho empresariais complexos.

Para saber mais, consulte [aplicativos lógicos do Azure](/azure/logic-apps).

>[!div class="step-by-step"]
>[Anterior](application-insights.md) 
> [Avançar](event-grid.md)
