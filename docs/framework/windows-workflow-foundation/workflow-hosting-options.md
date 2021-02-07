---
description: 'Saiba mais sobre: opções de Hospedagem de fluxo de trabalho'
title: Opções de hospedagem de fluxo de trabalho
ms.date: 03/30/2017
ms.assetid: 37bcd668-9c5c-4e7c-81da-a1f1b3a16514
ms.openlocfilehash: 64d02decd3a096b4c83555729826c5fc07b13cbf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754882"
---
# <a name="workflow-hosting-options"></a>Opções de hospedagem de fluxo de trabalho

A maioria dos exemplos de Windows Workflow Foundation (WF) usam fluxos de trabalho hospedados em um aplicativo de console, mas esse não é um cenário realista para fluxos de trabalho do mundo real. Os fluxos de trabalho em aplicativos de negócios reais serão hospedados em processos persistentes – um serviço do Windows criado pelo desenvolvedor ou um aplicativo de servidor como o IIS 7,0 ou AppFabric. As diferenças entre essas abordagens são as seguintes.

## <a name="hosting-workflows-in-iis-with-windows-appfabric"></a>Fluxos de trabalho de hospedagem no IIS com o Windows AppFabric

Usar o IIS com AppFabric é o host preferido para fluxos de trabalho. O aplicativo de host para fluxos de trabalho que usam AppFabric é o WAS (Serviços de Ativação do Windows), que remove a dependência de HTTP em IIS somente.

## <a name="hosting-workflows-in-iis-alone"></a>Fluxos de trabalho de hospedagem apenas no IIS

Usar o IIS 7,0 sozinho não é recomendado, pois há ferramentas de gerenciamento e monitoramento disponíveis com o AppFabric que facilitam a manutenção de aplicativos em execução. Os fluxos de trabalho só devem ser hospedados no IIS 7,0 se houver preocupações com a infraestrutura com a mudança para o AppFabric.

> [!WARNING]
> O IIS 7,0 recicla os pools de aplicativos periodicamente por vários motivos. Quando um pool de aplicativos é reciclado, o IIS para de aceitar mensagens para o pool antigo e cria uma instância de um pool de aplicativos para aceitar novas solicitações. Se um fluxo de trabalho continuar funcionando depois de enviar uma resposta, o IIS 7,0 não saberá que o trabalho está sendo feito e poderá reciclar o pool de aplicativos de hospedagem. Se isso acontecer, o fluxo de trabalho será anulado e os serviços de rastreamento gravarão uma mensagem [1004-WorkflowInstanceAborted](1004-workflowinstanceaborted.md) com um campo de motivo vazio.
>
> Se a persistência for usada, o host deverá reiniciar explicitamente as instâncias anuladas a partir do último ponto de persistência.
>
> Se o AppFabric for usado, o serviço de gerenciamento de fluxo de trabalho finalmente retomará o fluxo de trabalho a partir do último ponto de persistência bem-sucedido se a persistência tiver sido usada. Se nenhuma persistência tiver sido usada e o fluxo de trabalho executar operações fora de um padrão de solicitação/resposta, os dados serão perdidos quando o fluxo de trabalho for anulado.

## <a name="hosting-a-workflow-in-a-custom-windows-service"></a>Hospedando um fluxo de trabalho em um serviço do Windows personalizado

Criar um serviço de fluxo de trabalho personalizado para hospedar o fluxo de trabalho exigirá que o desenvolvedor duplique muito da funcionalidade fornecida pronta pelo AppFabric, mas permitirá mais flexibilidade com funcionalidade personalizada. Essa opção somente deverá ser considerada se o AppFabric provar não ser uma opção.
