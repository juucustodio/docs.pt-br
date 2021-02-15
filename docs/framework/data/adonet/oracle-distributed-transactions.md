---
description: 'Saiba mais sobre: transações distribuídas Oracle'
title: Transações distribuídas do Oracle
ms.date: 03/30/2017
ms.assetid: c340ca81-ef79-402f-b204-c5156b890fe5
ms.openlocfilehash: d0c41920f18e0f56ebdf57e3cb82cf829a59c450
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786167"
---
# <a name="oracle-distributed-transactions"></a>Transações distribuídas do Oracle

O <xref:System.Data.OracleClient.OracleConnection> objeto será automaticamente inscrito em uma transação distribuída existente se determinar que uma transação está ativa. A inscrição de transação automática ocorre quando a conexão é aberta ou recuperada do pool de conexões. Você pode desabilitar a inscrição automática em transações existentes especificando  
  
```csharp  
Enlist=false  
```  
  
 como um parâmetro de cadeia de conexão para um <xref:System.Data.OracleClient.OracleConnection> .  
  
## <a name="see-also"></a>Consulte também

- [Oracle e ADO.NET](oracle-and-adonet.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
