---
description: 'Saiba mais sobre: como chamar funções de Model-Defined em consultas'
title: 'Como: o chamar funções definidas em consultas'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6c804e4d-f348-4afd-9f63-d3f0f24bc6a9
ms.openlocfilehash: d59ef6edeba1e4b00e0481f8578e9c04735831fa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99748642"
---
# <a name="how-to-call-model-defined-functions-in-queries"></a>Como: o chamar funções definidas em consultas

Este tópico descreve como chamar funções que são definidas no modelo conceitual de dentro de LINQ to Entities consultas.  
  
 O procedimento abaixo fornece uma estrutura de tópicos de alto nível para chamar uma função definida pelo modelo de dentro de uma consulta LINQ to Entities. O exemplo a seguir fornece mais detalhes sobre as etapas no procedimento. O procedimento presume que você definiu uma função no modelo conceitual. Para obter mais informações, consulte [como: definir funções personalizadas no modelo conceitual](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100)).  
  
### <a name="to-call-a-function-defined-in-the-conceptual-model"></a>Para chamar uma função definida no modelo conceitual  
  
1. Adicione um método do Common Language Runtime (CLR) ao seu aplicativo que mapeia função definida no modelo conceitual. Para mapear o método, você deve aplicar <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> para o método. Observe que os parâmetros de <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> e de <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> de atributo é o nome do espaço do modelo conceitual e o nome da função no modelo conceitual respectivamente. A resolução de nomes de função para LINQ diferencia maiúsculas de minúsculas.  
  
2. Chame a função em uma consulta LINQ to Entities.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir demonstra como chamar uma função que é definida no modelo conceitual de dentro de uma consulta LINQ to Entities. O exemplo usa o modelo de escola. Para obter informações sobre o modelo escolar, consulte [criando o banco de dados de exemplo da escola](/previous-versions/dotnet/netframework-4.0/bb399731(v=vs.100)) e [gerando o arquivo School. edmx](/previous-versions/dotnet/netframework-4.0/bb399739(v=vs.100)).  
  
 A função a seguir o modelo conceitual retorna o número de anos como um instrutor foi contratado. Para obter informações sobre como adicionar a função a um modelo conceitual, consulte [como definir funções personalizadas no modelo conceitual](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100)).  
  
 [!code-xml[DP ConceptualModelFunctions#1](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp conceptualmodelfunctions/xml/school.edmx#1)]
  
## <a name="example"></a>Exemplo  

 Em seguida, adicione o seguinte método ao seu aplicativo e usa <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> para mapear-lo à função de modelo conceitual:  
  
 [!code-csharp[DP ConceptualModelFunctions#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp conceptualmodelfunctions/cs/program.cs#2)]
 [!code-vb[DP ConceptualModelFunctions#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp conceptualmodelfunctions/vb/module1.vb#2)]  
  
## <a name="example"></a>Exemplo  

 Agora você pode chamar a função de modelo conceitual de dentro de uma consulta LINQ to Entities. O código a seguir chama o método para exibir todos os instrutores que foram contratados mais de dez anos há:  
  
 [!code-csharp[DP ConceptualModelFunctions#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp conceptualmodelfunctions/cs/program.cs#3)]
 [!code-vb[DP ConceptualModelFunctions#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp conceptualmodelfunctions/vb/module1.vb#3)]  
  
## <a name="see-also"></a>Consulte também

- [Visão geral do arquivo. edmx](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))
- [Consultas no LINQ to Entities](queries-in-linq-to-entities.md)
- [Chamando funções em consultas no LINQ to Entities](calling-functions-in-linq-to-entities-queries.md)
- [Como: o chamar funções definidas como métodos de objeto](how-to-call-model-defined-functions-as-object-methods.md)
