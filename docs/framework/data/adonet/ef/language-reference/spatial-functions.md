---
description: 'Saiba mais sobre: funções espaciais'
title: Funções espaciais
ms.date: 03/30/2017
ms.assetid: 90cb177d-88a0-45be-97e8-3b306283c6e0
ms.openlocfilehash: cde8f1b0fcf5904eb33fe061de69e566da2804dd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99767876"
---
# <a name="spatial-functions"></a>Funções espaciais

Não há nenhum formato literal para tipos espaciais. Entretanto, você pode usar funções canônicas do Entity Framework que você chama usando cadeias de caracteres no formato de texto bem conhecido. Por exemplo, a chamada de função a seguir cria um ponto geométrico:  
  
```sql  
GeometryFromText('POINT (43 -73)')  
```  
  
 Os <xref:System.Data.Common.CommandTrees.ExpressionBuilder.Spatial.SpatialEdmFunctions> métodos têm todos os métodos de Entity Framework canônicos espaciais. Clique em um método de interesse ver quais parâmetros devem ser passados para uma função.
