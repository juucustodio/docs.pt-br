---
description: 'Saiba mais sobre: 1004-WorkflowInstanceAborted'
title: 1004 - WorkflowInstanceAborted
ms.date: 03/30/2017
ms.assetid: edb9ab8c-0b9a-488d-aa96-9c8c7984b53c
ms.openlocfilehash: 4aaa0899da9b0b8510684a13537a8cb8f9117ee1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755610"
---
# <a name="1004---workflowinstanceaborted"></a>1004 - WorkflowInstanceAborted

## <a name="properties"></a>Propriedades

|||
|-|-|
|ID|1004|
|Palavras-chave|WFRuntime|
|Level|Informações|
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|

## <a name="description"></a>Descrição

Indica que uma instância de fluxo de trabalho foi anulada com uma exceção.

## <a name="message"></a>Mensagem

Identificação de WorkflowInstance: “%1 " foi anuladas com uma exceção.

## <a name="details"></a>Detalhes

|Nome do item de dados|Tipo de item de dados|Descrição|
|--------------------|--------------------|-----------------|
|WorkflowInstanceId|`xs:string`|A identificação de instância para o fluxo de trabalho|
|Exceção|`xs:string`|Os detalhes de exceção para a exceção|
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
