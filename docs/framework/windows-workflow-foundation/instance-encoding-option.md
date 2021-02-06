---
description: 'Saiba mais sobre: opção de codificação de instância'
title: Padrão de codificação de instância
ms.date: 03/30/2017
ms.assetid: 89e4b029-4f68-438c-8117-9b21fe094ef4
ms.openlocfilehash: 8cca7fd536673ca99b1014173e172508e3d97b7c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631158"
---
# <a name="instance-encoding-option"></a>Padrão de codificação de instância

A propriedade de **opção de codificação de instância** do repositório da instância do fluxo de trabalho SQL permite especificar se o provedor de persistência do SQL deve compactar as informações de estado da instância do fluxo de trabalho usando o algoritmo gzip antes de salvar as informações no banco de dados de persistência. Os valores permitidos para essa propriedade são: GZip e quaisquer. O valor padrão é Nenhum. A lista a seguir descreve as opções.  
  
1. **Gzip**. O provedor de persistência codificação informações de estado usando o algoritmo de GZip antes de manter informações de estado na base de dados de persistência.  
  
2. **None**. O provedor de persistência não codificação informações de estado antes de salvar informações na base de dados de persistência.  
  
 Informações de estado da instância de fluxo de trabalho de codificação que usa o GZip reduz o consumo de memória na base de dados SQL e também reduz o consumo de rede se o base de dados reside em um outro computador na rede do computador no qual o host serviço de fluxo de trabalho está sendo executado. Uma orientação geral é definir a propriedade da **opção de codificação da instância** como **None** se o estado da instância do fluxo de trabalho for pequeno.
