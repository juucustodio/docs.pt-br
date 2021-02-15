---
description: 'Saiba mais sobre: funções de User-Defined'
title: Funções definidas pelo usuário
ms.date: 03/30/2017
ms.assetid: 3304c9b2-5c7a-4a95-9d45-4f260dcb606e
ms.openlocfilehash: d27abd78e15ad6cb5ce4e9440ac425159a0b5bdc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99680935"
---
# <a name="user-defined-functions"></a>Funções definidas pelo usuário

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] usa métodos no seu modelo de objeto para representar funções definidas pelo usuário. Você designa métodos como funções aplicando o atributo de <xref:System.Data.Linq.Mapping.FunctionAttribute> e, quando for necessário, o atributo de <xref:System.Data.Linq.Mapping.ParameterAttribute> . Para obter mais informações, consulte [o modelo de objeto LINQ to SQL](the-linq-to-sql-object-model.md).  
  
 Para evitar <xref:System.InvalidOperationException>, funções definidas pelo usuário em [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] devem estar em um das seguintes formas:  
  
- Uma função empacotada como um chamada de método que tem os atributos corretos de mapeamento. Para obter mais informações, consulte [mapeamento baseado em atributo](attribute-based-mapping.md).  
  
- Um específico do método SQL estático a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
- Uma função com suporte de um método .NET Framework.  
  
 Os tópicos nesta seção de apresentação como formar e chamar esses métodos em seu aplicativo se você escreve o código que você mesmo. Os desenvolvedores que usam o Visual Studio normalmente usariam o Object Relational Designer para mapear funções definidas pelo usuário.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Como: usar funções definidas pelo usuário com valor escalar](how-to-use-scalar-valued-user-defined-functions.md)  
 Descreve como implementar uma função que retorna valores escalares.  
  
 [Como: usar funções definidas pelo usuário com valor de tabela](how-to-use-table-valued-user-defined-functions.md)  
 Descreve como implementar uma função que retorna apresentam valores.  
  
 [Como: chamar funções embutidas definidas pelo usuário](how-to-call-user-defined-functions-inline.md)  
 Descreve como fazer chamadas a funções embutidas e as diferenças em execução quando o chamada é feita embutido.
