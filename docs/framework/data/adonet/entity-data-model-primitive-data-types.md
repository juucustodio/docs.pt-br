---
description: 'Saiba mais sobre: Modelo de Dados de Entidade: tipos de dados primitivos'
title: 'Modelo de Dados de Entidade: Tipos de dados primitivos'
ms.date: 03/30/2017
ms.assetid: 7635168e-0566-4fdd-8391-7941b0d9f787
ms.openlocfilehash: bdc34f3232e78d29e6c2ce25d8f159d7f5238f2f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724460"
---
# <a name="entity-data-model-primitive-data-types"></a>Modelo de Dados de Entidade: Tipos de dados primitivos

O Modelo de Dados de Entidade (EDM) dá suporte a um conjunto de tipos de dados primitivos abstratos (como cadeia de caracteres, booliano, Int32 e assim por diante) que são usados para definir [Propriedades](property.md) em um modelo conceitual. Esses tipos de dados primitivos são proxies para os tipos de dados primitivos reais que são suportados no armazenamento ou no ambiente de hospedagem, como um base de dados SQL Server ou Common Language Runtime (CLR). EDM não define a semântica das operações ou das conversões sobre tipos de dados primitivos; essa semântica é definida pelo armazenamento ou pelo ambiente de hospedagem. Normalmente, os tipos de dados primitivos em EDM são mapeados para os tipos de dados primitivos no armazenamento ou no ambiente de hospedagem. Para obter informações sobre como o Entity Framework mapeia tipos primitivos no EDM para SQL Server tipos de dados, consulte [SqlClient para Entity FrameworkTypes](./ef/sqlclient-for-ef-types.md).  
  
> [!NOTE]
> EDM não suporta coleções de tipos de dados primitivos.  
  
 Para obter informações sobre tipos de dados estruturados no EDM, consulte [tipo de entidade](entity-type.md) e [tipo complexo](complex-type.md).  
  
## <a name="primitive-data-types-supported-in-the-entity-data-model"></a>Tipos de dados primitivos suportados em Modelo de Dados de Entidade  

 A tabela abaixo lista os tipos de dados primitivos suportados por EDM. A tabela também lista as [facetas](facet.md) que podem ser aplicadas a cada tipo de dados primitivo.  
  
|Tipo de dados primitivo|Descrição|Facetas aplicáveis|  
|-------------------------|-----------------|-----------------------|  
|Binário|Contém dados binários.|MaxLength, FixedLength, anulável, opção|  
|Boolean|Contém o valor `true` ou `false`.|Anulável, opção|  
|Byte|Contém um valor inteiro de 8 bits sem sinal.|Precisão, anulável, opção|  
|Datetime|Representa uma data e hora.|Precisão, anulável, opção|  
|DateTimeOffset|Contém uma data e hora como um deslocamento em minutos GMT.|Precisão, anulável, opção|  
|Decimal|Contém um valor numérico com precisão e escala fixa.|Precisão, anulável, opção|  
|Double|Contém um número de ponto flutuante com precisão de 15 dígitos.|Precisão, anulável, opção|  
|Float|Contém um número de ponto flutuante com precisão de sete dígitos.|Precisão, anulável, opção|  
|Guid|Contém um identificador exclusivo de 16 bytes.|Precisão, anulável, opção|  
|Int16|Contém um valor inteiro de 16 bits assinado.|Precisão, anulável, opção|  
|Int32|Contém um valor inteiro de 32 bits assinado.|Precisão, anulável, opção|  
|Int64|Contém um valor inteiro de 64 bits assinado.|Precisão, anulável, opção|  
|SByte|Contém um valor inteiro de 8 bits com sinal.|Precisão, anulável, opção|  
|String|Contém dados de caractere.|Unicode, FixedLength, MaxLength, ordenação, precisão, anulável, opção|  
|Hora|Contém uma hora.|Precisão, anulável, opção|  
  
## <a name="see-also"></a>Consulte também

- [Conceitos chave do Modelo de Dados de Entidade](entity-data-model-key-concepts.md)
- [Modelo de Dados de Entidade](entity-data-model.md)
