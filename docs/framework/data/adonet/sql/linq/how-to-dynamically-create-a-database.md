---
description: 'Saiba mais sobre: como criar dinamicamente um banco de dados'
title: 'Como: criar um banco de dados dinamicamente'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fb7f23c4-4572-4c38-9898-a287807d070c
ms.openlocfilehash: b9addce6befc63f91358d6ecae57e40d6123b200
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99738969"
---
# <a name="how-to-dynamically-create-a-database"></a>Como: criar um banco de dados dinamicamente

No LINQ to SQL, um modelo de objeto é mapeado para um banco de dados relacional. O mapeamento é habilitado usando o mapeamento baseado em atributo ou um arquivo de mapeamento externo para descrever a estrutura do banco de dados relacional. Em ambos os cenários, há informações suficientes sobre o banco de dados relacional para que você possa criar uma nova instância do banco de dados usando o método <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType>.  
  
 O método <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> cria uma réplica do banco de dados somente para a extensão das informações codificadas no modelo de objeto. Os arquivos de mapeamento e os atributos no modelo de objeto podem não codificar tudo sobre a estrutura de um banco de dados existente. As informações de mapeamento não representam o conteúdo das funções definidas pelo usuário, dos procedimentos armazenados, dos gatilhos ou das restrições de verificação. Esse comportamento é suficiente para vários bancos de dados.  
  
 Você pode usar o método <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> em diversos cenários, especialmente se um provedor de dados conhecido como o Microsoft SQL Server 2008 estiver disponível. Os cenários comuns são os seguintes:  
  
- Você está criando um aplicativo que se instala automaticamente em um sistema de cliente.  
  
- Você está criando um aplicativo cliente que precisa de um banco de dados local para salvar seu estado offline.  
  
 Você também pode usar o método <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> com o SQL Server usando um arquivo .mdf ou um nome de catálogo, dependendo da cadeia de conexão. O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] usa a cadeia de conexão para definir o banco de dados a ser criado e em qual servidor o banco de dados será criado.  
  
> [!NOTE]
> Sempre que possível, use a Segurança Integrada do Windows para se conectar ao banco de dados, de modo que não sejam necessárias senhas na cadeia de conexão.  
  
## <a name="example"></a>Exemplo  

 O código a seguir fornece um exemplo de como criar um novo banco de dados chamado MyDVDs.mdf.  
  
 [!code-csharp[DLinqSubmittingChanges#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#5)]
 [!code-vb[DLinqSubmittingChanges#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#5)]  
  
## <a name="example"></a>Exemplo  

 Você pode usar o modelo de objeto para criar um banco de dados fazendo o seguinte:  
  
 [!code-csharp[DLinqSubmittingChanges#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#6)]
 [!code-vb[DLinqSubmittingChanges#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#6)]  
  
## <a name="example"></a>Exemplo  

 Ao criar um aplicativo que se instala automaticamente em um sistema de cliente, verifique se o banco de dados já existe e solte-o antes de criar um novo. A classe <xref:System.Data.Linq.DataContext> fornece os métodos <xref:System.Data.Linq.DataContext.DatabaseExists%2A> e <xref:System.Data.Linq.DataContext.DeleteDatabase%2A> para ajudar nesse processo.  
  
 O exemplo a seguir mostra uma maneira de implementar essa abordagem através desses métodos:  
  
 [!code-csharp[DLinqSubmittingChanges#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#7)]
 [!code-vb[DLinqSubmittingChanges#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#7)]  
  
## <a name="see-also"></a>Consulte também

- [Mapeamento baseado em atributos](attribute-based-mapping.md)
- [Mapeamento externo](external-mapping.md)
- [Mapeamento de tipo SQL-CLR](sql-clr-type-mapping.md)
- [Informações gerais](background-information.md)
- [Fazendo e enviando alterações de dados](making-and-submitting-data-changes.md)
