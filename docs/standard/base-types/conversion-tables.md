---
title: Tabelas de conversão de tipos em .NET
ms.date: 03/30/2017
ms.topic: reference
helpviewer_keywords:
- widening conversions
- narrowing conversions
- type conversion, table
- converting types, narrowing conversions
- converting types, widening conversions
- base types, converting
- tables [.NET], type conversions
- data types [.NET], converting
ms.assetid: 0ea65c59-85eb-4a52-94ca-c36d3bd13058
ms.openlocfilehash: ecfa0841ea6335ce1d7148d21b076af9dbe91a13
ms.sourcegitcommit: 4313614f57690f9a5119a37314f0a1fd738ebda2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2021
ms.locfileid: "98692988"
---
# <a name="type-conversion-tables-in-net"></a>Tabelas de conversão de tipos em .NET

Conversões de expansão ocorrem quando um valor de um tipo é convertido em outro tipo de tamanho igual ou maior. Conversões de redução ocorrem quando um valor de um tipo é convertido em um valor de outro tipo de tamanho menor. As tabelas neste tópico ilustram os comportamentos exibidos por ambos os tipos de conversões.  
  
## <a name="widening-conversions"></a>Conversões de expansão  

 A tabela a seguir descreve as conversões de expansão que podem ser executadas sem perda de informações.  
  
|Digite|Pode ser convertido sem perda de dados para|  
|----------|-------------------------------------------|  
|<xref:System.Byte>|<xref:System.UInt16>, <xref:System.Int16>, <xref:System.UInt32>, <xref:System.Int32>, <xref:System.UInt64>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.SByte>|<xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Int16>|<xref:System.Int32>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.UInt16>|<xref:System.UInt32>, <xref:System.Int32>, <xref:System.UInt64>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Char>|<xref:System.UInt16>, <xref:System.UInt32>, <xref:System.Int32>, <xref:System.UInt64>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Int32>|<xref:System.Int64>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.UInt32>|<xref:System.Int64>, <xref:System.UInt64>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Int64>|<xref:System.Decimal>|  
|<xref:System.UInt64>|<xref:System.Decimal>|  
|<xref:System.Single>|<xref:System.Double>|  
  
 Algumas conversões de expansão para <xref:System.Single> ou <xref:System.Double> podem causar perda de precisão. A tabela a seguir descreve as conversões de expansão que, às vezes, resultam em perda de informações.  
  
|Digite|Pode ser convertido para|  
|----------|-------------------------|  
|<xref:System.Int32>|<xref:System.Single>|  
|<xref:System.UInt32>|<xref:System.Single>|  
|<xref:System.Int64>|<xref:System.Single>, <xref:System.Double>|  
|<xref:System.UInt64>|<xref:System.Single>, <xref:System.Double>|  
|<xref:System.Decimal>|<xref:System.Single>, <xref:System.Double>|  
  
## <a name="narrowing-conversions"></a>Conversões de redução  

 Uma conversão de redução para <xref:System.Single> ou <xref:System.Double> pode causar perda de informações. Se o tipo de destino não puder expressar corretamente a magnitude da origem, o tipo resultante será definido como a constante `PositiveInfinity` ou `NegativeInfinity`. `PositiveInfinity` resulta da divisão de um número positivo por zero, e também é retornado quando o valor de um <xref:System.Single> ou <xref:System.Double> ultrapassar o valor do campo `MaxValue`. `NegativeInfinity` resulta da divisão de um número negativo por zero, e também é retornado quando o valor de um <xref:System.Single> ou <xref:System.Double> fica abaixo do valor do campo `MinValue`. Uma conversão de um <xref:System.Double> em um <xref:System.Single> pode resultar em `PositiveInfinity` ou `NegativeInfinity`.  
  
 Uma conversão de redução também pode resultar em perda de informações para outros tipos de dados. No entanto, <xref:System.OverflowException> será lançada se o valor de um tipo que está sendo convertido ficar fora do intervalo especificado pelos campos `MaxValue` e `MinValue` do tipo de destino, e a conversão será verificada pelo runtime para garantir que o valor do tipo de destino não ultrapasse `MaxValue` ou `MinValue`. Conversões executadas com a classe <xref:System.Convert?displayProperty=nameWithType> sempre são verificadas dessa maneira.  
  
 A tabela a seguir lista conversões que lançam <xref:System.OverflowException> usando <xref:System.Convert?displayProperty=nameWithType> ou qualquer conversão selecionada se o valor do tipo que está sendo convertido estiver fora do intervalo definido pelo tipo resultante.  
  
|Digite|Pode ser convertido para|  
|----------|-------------------------|  
|<xref:System.Byte>|<xref:System.SByte>|  
|<xref:System.SByte>|<xref:System.Byte>, <xref:System.UInt16>, <xref:System.UInt32>, <xref:System.UInt64>|  
|<xref:System.Int16>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.UInt16>|  
|<xref:System.UInt16>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>|  
|<xref:System.Int32>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>,<xref:System.UInt32>|  
|<xref:System.UInt32>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>|  
|<xref:System.Int64>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>,<xref:System.UInt32>,<xref:System.UInt64>|  
|<xref:System.UInt64>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>|  
|<xref:System.Decimal>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>, <xref:System.UInt64>|  
|<xref:System.Single>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>, <xref:System.UInt64>|  
|<xref:System.Double>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>, <xref:System.UInt64>|  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Convert?displayProperty=nameWithType>
- [Conversão de tipo no .NET](type-conversion.md)
