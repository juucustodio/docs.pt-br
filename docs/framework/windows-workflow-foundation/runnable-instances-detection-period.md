---
description: 'Saiba mais sobre: período de detecção de instâncias executáveis'
title: Período viável de detecção de instâncias
ms.date: 03/30/2017
ms.assetid: 4ea5c787-b638-47fd-bfc8-ede8c2898ce6
ms.openlocfilehash: fc4305c11361a3d9ccf7079f4f1b639fb507c469
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99720014"
---
# <a name="runnable-instances-detection-period"></a>Período viável de detecção de instâncias

A instância Store de fluxo de trabalho do SQL executa uma tarefa periodicamente interna que acorde e detecte instâncias praticáveis ou activatable na base de dados de persistência. A propriedade **período de detecção de instâncias executáveis** do repositório da instância do fluxo de trabalho SQL especifica o período após o qual o armazenamento da instância do fluxo de trabalho SQL executa uma tarefa de detecção para detectar qualquer instância de fluxo de trabalho executável ou ativável no banco de dados de persistência após o ciclo de detecção anterior.  
  
 Definir um intervalo menor para essa propriedade reduz o tempo entre a validade de um timer associado com uma instância de fluxo de trabalho e a sinalização de evento e de carregamento de instância subsequente. No entanto, também aumenta a carga de processamento em um host e não pode ser desejável em situações onde timers e/ou falhas duráveis host são incomuns. O tipo de propriedade é período e o valor da propriedade segue o formato: hh:mm:ss. O valor mínimo para essa propriedade é 00:00:01. O valor padrão para a propriedade é 00:00:05.  
  
 Para obter mais informações sobre como detectar e ativar instâncias de fluxo de trabalho executáveis e ativáveis, consulte [ativação de instância](instance-activation.md).
