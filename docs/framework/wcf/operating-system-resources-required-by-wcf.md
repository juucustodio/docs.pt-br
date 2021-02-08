---
description: 'Saiba mais sobre: recursos do sistema operacional exigidos pelo WCF'
title: Recursos do sistema operacional exigidos pelo WCF
ms.date: 03/30/2017
ms.assetid: cdd9a331-53fe-4e0d-bdfe-782264aec5c9
ms.openlocfilehash: 717ab2074c0dcf840919c2bd8afa2641e106ac11
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99779212"
---
# <a name="operating-system-resources-required-by-wcf"></a>Recursos do sistema operacional exigidos pelo WCF

O Windows Communication Foundation (WCF) depende de vários recursos que são fornecidos pelo sistema operacional para funcionar. A tabela a seguir lista esses recursos:

|Recurso|Descrição|
|--------------|-----------------|
|Coordenador de Transações Distribuídas da Microsoft (MSDTC)|Necessário para dar suporte a transações OleTx.|
|Serviços de Informações da Internet (IIS)|Obrigatório se você quiser usar o IIS para hospedar seu aplicativo.|
|Serviço de Ativação de Processos do Windows (WAS)|Obrigatório se você quiser usar o WAS para hospedar seu aplicativo.|
