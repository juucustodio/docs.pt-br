---
description: 'Saiba mais sobre: funcionalidade sem suporte'
title: Funcionalidade sem suporte
ms.date: 03/30/2017
ms.assetid: e480cfb5-697e-42c8-bed5-9264c945c4f9
ms.openlocfilehash: 5c44dd4aad2d2ee4ec5e00ce42f4de9400cea478
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99680883"
---
# <a name="unsupported-functionality"></a>Funcionalidade sem suporte

Em LINQ to SQL, a seguinte funcionalidade do SQL não pode ser expostas pela conversão do Common Language Runtime existente (CLR) e construtores do.NET Framework:  
  
- `STDDEV`  
  
- `LIKE`  
  
     Embora `LIKE` não é com a conversão direta, a funcionalidade semelhante existido na classe de <xref:System.Data.Linq.SqlClient.SqlMethods> . Para obter mais informações, consulte <xref:System.Data.Linq.SqlClient.SqlMethods.Like%2A?displayProperty=nameWithType>.  
  
- `DATEDIFF`  
  
     LINQ to SQL limitou suporte para `DATEDIFF`. Funcionalidade semelhante existe na classe de <xref:System.Data.Linq.SqlClient.SqlMethods> .  
  
- `ROUND`  
  
     LINQ to SQL limitou suporte para `ROUND`. Para obter mais informações, consulte [métodos System. Math](system-math-methods.md).  
  
## <a name="see-also"></a>Consulte também

- [Tipos de dados e funções](data-types-and-functions.md)
