---
description: 'Saiba mais sobre: como executar um procedimento armazenado parametrizado usando EntityCommand'
title: 'Como: executar um procedimento armazenado parametrizado usando EntityCommand'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 4f5639bf-bb7f-4982-bb1d-c7caa4348888
ms.openlocfilehash: a45c9a276cc33037a4d353e05d1174c9748aab82
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99650684"
---
# <a name="how-to-execute-a-parameterized-stored-procedure-using-entitycommand"></a>Como: executar um procedimento armazenado parametrizado usando EntityCommand

Este tópico mostra como executar um procedimento armazenado parametrizado usando a classe de <xref:System.Data.EntityClient.EntityCommand> .  
  
### <a name="to-run-the-code-in-this-example"></a>Para executar o código nesse exemplo  
  
1. Adicione o [modelo escolar](/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100)) ao seu projeto e configure seu projeto para usar o Entity Framework. Para obter mais informações, consulte [como: usar o assistente de modelo de dados de entidade](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100)).  
  
2. Na página de código do seu aplicativo, adicione as seguintes instruções `using` (`Imports` no Visual Basic):  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
3. Importar o procedimento armazenado `GetStudentGrades` e especificar entidades de `CourseGrade` como um tipo de retorno. Para obter informações sobre como importar um procedimento armazenado, consulte [como importar um procedimento armazenado](/previous-versions/dotnet/netframework-4.0/bb896231(v=vs.100)).  
  
## <a name="example"></a>Exemplo  

 O código a seguir executa o procedimento armazenado `GetStudentGrades` onde `StudentId` é um parâmetro necessário. Os resultados são lidos em seguida <xref:System.Data.EntityClient.EntityDataReader>.  
  
 [!code-csharp[DP EntityServices Concepts#StoredProcWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#storedprocwithentitycommand)]
 [!code-vb[DP EntityServices Concepts#StoredProcWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#storedprocwithentitycommand)]  
  
## <a name="see-also"></a>Consulte também

- [Provedor EntityClient para Entity Framework](entityclient-provider-for-the-entity-framework.md)
