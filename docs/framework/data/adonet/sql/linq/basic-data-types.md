---
description: 'Saiba mais sobre: tipos de dados básicos'
title: Tipos de dados básicos
ms.date: 03/30/2017
ms.assetid: eca2c472-9548-4800-bd31-5d8d9f11752b
ms.openlocfilehash: d0236bc315c884d9e70c3c4a75755c3b66b1f2e4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99712604"
---
# <a name="basic-data-types"></a>Tipos de dados básicos

Porque as consultas LINQ to SQL traduzem a Transact-SQL antes que elas sejam executadas no Microsoft SQL Server. LINQ to SQL suporta grande parte da mesma funcionalidade interna que o SQL Server faz para tipos de dados básicos.  
  
## <a name="casting"></a>Transmissão  

 Conversões implícitas ou explícitas estão ativados de um tipo de CLR de origem para um tipo de CLR de destino se há uma conversão válido semelhante em SQL Server. Para obter mais informações sobre a conversão de CLR, consulte [função CType](../../../../../visual-basic/language-reference/functions/ctype-function.md) (Visual Basic) e [operadores de conversão e teste de tipo](../../../../../csharp/language-reference/operators/type-testing-and-cast.md). Após a conversão, as conversões alteram o comportamento das operações executadas em uma expressão CLR para corresponder ao comportamento de outras expressões CLR que são mapeadas naturalmente para o tipo de destino. As conversões também são traduzível no contexto do mapeamento de herança. Objetos podem ser convertidos em um subtipos mais específicos entidade para que seus dados específicos subtipo- possam ser acessados.  
  
## <a name="equality-operators"></a>Operadores de igualdade  

 LINQ to SQL oferece suporte aos seguintes operadores de igualdade em tipos de dados básicos dentro das consultas LINQ to SQL:  
  
- Operador de igual e desigualdade: há suporte para operadores de igualdade e desigualdade para tipos numéricos,, <xref:System.Boolean> <xref:System.DateTime> e <xref:System.TimeSpan> . Para obter mais informações sobre operadores de Visual Basic `=` e `<>` , consulte [operadores de comparação](../../../../../visual-basic/language-reference/operators/comparison-operators.md). Para obter mais informações sobre operadores de comparação de C# `==` e `!=` , consulte [operadores de igualdade](../../../../../csharp/language-reference/operators/equality-operators.md).
  
- O operador: O operador de `IS` tem uma translação suportado quando o mapeamento de herança está sendo usado. Pode ser usado em vez de diretamente testar a coluna de discriminador para determinar se um objeto é de um tipo específico de entidade, e é convertido para uma verificação na coluna de discriminador. Para obter mais informações sobre o Visual Basic e o C# são operadores, consulte [is Operator](../../../../../visual-basic/language-reference/operators/is-operator.md) and [is](../../../../../csharp/language-reference/operators/type-testing-and-cast.md#is-operator).  
  
## <a name="see-also"></a>Consulte também

- [Mapeamento de tipo SQL-CLR](sql-clr-type-mapping.md)
- [Tipos de dados e funções](data-types-and-functions.md)
