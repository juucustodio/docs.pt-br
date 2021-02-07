---
description: 'Saiba mais sobre: métodos System. String'
title: Métodos de System.String
ms.date: 03/30/2017
ms.assetid: ce307f14-87e6-4816-8694-8a4147f6b784
ms.openlocfilehash: 68ade8c3d8f47749dcea9cdaad2a19d28c7032c3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99681299"
---
# <a name="systemstring-methods"></a>Métodos de System.String

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não oferece suporte aos seguintes métodos de <xref:System.String> .  
  
## <a name="unsupported-systemstring-methods-in-general"></a>Métodos sem suporte de System.String em geral  

 Métodos sem suporte de <xref:System.String> geralmente:  
  
- Sobrecargas com reconhecimento de cultura (métodos que usam um `CultureInfo`  /  `StringComparison`  /  `IFormatProvider` ).  
  
- Métodos que usam ou gerenciar uma matriz de `char` .  
  
## <a name="unsupported-systemstring-static-methods"></a>Métodos sem suporte estático de System.String  
  
|Métodos sem suporte estático de System.String|  
|----------------------------------------------|  
|<xref:System.String.Copy%28System.String%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.Boolean%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.CompareOrdinal%28System.String%2CSystem.String%29?displayProperty=nameWithType>|  
|<xref:System.String.CompareOrdinal%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType>|  
|<xref:System.String.Format%2A?displayProperty=nameWithType>|  
|<xref:System.String.Join%2A?displayProperty=nameWithType>|  
  
## <a name="unsupported-systemstring-non-static-methods"></a>Métodos sem suporte de não estático de System.String  
  
|Métodos sem suporte de não estático de System.String|  
|---------------------------------------------------|  
|<xref:System.String.IndexOfAny%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
|<xref:System.String.Split%2A?displayProperty=nameWithType>|  
|<xref:System.String.ToCharArray?displayProperty=nameWithType>|  
|<xref:System.String.ToUpper%28System.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.TrimEnd%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
|<xref:System.String.TrimStart%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
  
## <a name="differences-from-net"></a>Diferenças do .NET  
  
- Consultas não esclarecem as ordenações do SQL Server que podem ser aplicadas no servidor, e portanto fornecerão comparações que levam confidenciais, sem diferenciação de maiúsculas e minúsculas por padrão. Esse comportamento difere de opção, semântica maiúsculas de minúsculas do .NET Framework.  
  
- Quando `LastIndexOf` retorna 0, a cadeia de caracteres é `NULL` ou a posição encontrada é 0.  
  
- Os resultados inesperados podem ser retornados de concatenação ou outras operações em cadeias de caracteres de comprimento fixo (`CHAR`, `NCHAR`), porque esses tipos têm automaticamente o preenchimento aplicado ao base de dados.  
  
- Porque muitos métodos, como `Replace`, `ToLower`, `ToUpper`, e o indexador de caracteres, não têm nenhuma conversão válido para `TEXT` ou colunas e XML de `NTEXT` , `SqlExceptions` ocorre se traduzido normalmente. Esse comportamento é considerado aceitável para esses tipos. No entanto, todas as operações de cadeia de caracteres devem corresponder a semântica do Common Language Runtime (CLR) para `VARCHAR`, `NVARCHAR`, `VARCHAR(max)`, e `NVARCHAR(max)`.  
  
## <a name="see-also"></a>Consulte também

- [Tipos de dados e funções](data-types-and-functions.md)
