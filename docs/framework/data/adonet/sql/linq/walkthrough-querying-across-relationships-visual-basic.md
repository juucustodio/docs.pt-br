---
description: 'Saiba mais sobre: Walkthrough: consultando entre relações (Visual Basic)'
title: 'Passo a passo: consultar entre relações (Visual Basic)'
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: a7da43e3-769f-4e07-bcd6-552b8bde66f4
ms.openlocfilehash: 002ec53c5a56d988dcd71af658a546d199473425
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99650567"
---
# <a name="walkthrough-querying-across-relationships-visual-basic"></a>Passo a passo: consultar entre relações (Visual Basic)

Este tutorial demonstra o uso de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] *associações* para representar relações de chave estrangeira no banco de dados.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Este passo a passo foi escrito usando as Configurações de Desenvolvimento do Visual Basic.  
  
## <a name="prerequisites"></a>Pré-requisitos  

 Você deve ter concluído [a explicação: modelo de objeto simples e consulta (Visual Basic)](walkthrough-simple-object-model-and-query-visual-basic.md). Este passo a passo é baseado naquele, incluindo a presença do arquivo northwnd.mdf em c:\linqtest.  
  
## <a name="overview"></a>Visão geral  

 Este passo a passo consiste em três tarefas principais:  
  
- Adicionando uma classe de entidade para representar a tabela Orders no banco de dados de exemplo Northwind.  
  
- Suplementando anotações à classe `Customer` para aprimorar a relação entre as classes `Customer` e `Order`.  
  
- Criando e executando uma consulta para testar o processo de obtenção de informações de `Order` usando a classe `Customer`.  
  
## <a name="mapping-relationships-across-tables"></a>Relações de mapeamento entre tabelas  

 Depois de definir a classe `Customer`, crie a definição da classe de entidade `Order` que inclui o código a seguir, que indica que `Orders.Customer` se relaciona como uma chave estrangeira a `Customers.CustomerID`.  
  
#### <a name="to-add-the-order-entity-class"></a>Para adicionar a classe de entidade Order  
  
- Digite ou cole o código a seguir depois da classe `Customer`:  
  
     [!code-vb[DLinqWalk2VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#1)]  
  
## <a name="annotating-the-customer-class"></a>Anotando a classe Customer  

 Nesta etapa, você anota a classe `Customer` para indicar sua relação com a classe `Order`. Essa adição não é estritamente necessária, porque a definição da relação em qualquer direção é suficiente para criar o link. Mas a adição dessa anotação permite que você navegue objetos facilmente em qualquer direção.  
  
#### <a name="to-annotate-the-customer-class"></a>Para anotar a classe Customer  
  
- Digite ou cole o código a seguir na classe `Customer`:  
  
     [!code-vb[DLinqWalk2VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#2)]  
  
## <a name="creating-and-running-a-query-across-the-customer-order-relationship"></a>Criando e executando uma consulta pela relação de Customer-Order  

 Agora você pode acessar objetos `Order` diretamente nos objetos `Customer` ou na ordem oposta. Você não precisa de uma *junção* explícita entre clientes e pedidos.  
  
#### <a name="to-access-order-objects-by-using-customer-objects"></a>Para acessar objetos Order usando objetos Customer  
  
1. Modifique o método `Sub Main` digitando ou colando o seguinte código no método:  
  
     [!code-vb[DLinqWalk2VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#3)]  
  
2. Pressione F5 para depurar seu aplicativo.  
  
     Dois nomes aparecem na caixa de mensagem, e a janela Console mostra o código SQL gerado.  
  
3. Feche a caixa de mensagem para interromper a depuração.  
  
## <a name="creating-a-strongly-typed-view-of-your-database"></a>Criando uma exibição fortemente tipada do seu banco de dados  

 É muito mais fácil começar com uma exibição fortemente tipada do seu banco de dados. Com o objeto <xref:System.Data.Linq.DataContext> fortemente tipado, você não precisa de chamadas para <xref:System.Data.Linq.DataContext.GetTable%2A>. Você pode usar tabelas fortemente tipadas em todas as consultas quando usa o objeto <xref:System.Data.Linq.DataContext> fortemente tipado.  
  
 Nas etapas a seguir, você criará `Customers` como uma tabela fortemente tipada que mapeia para a tabela Customers no banco de dados.  
  
#### <a name="to-strongly-type-the-datacontext-object"></a>Para tornar o objeto DataContext fortemente tipado  
  
1. Adicione o código a seguir acima da declaração da classe `Customer`.  
  
     [!code-vb[DLinqWalk2VB#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#4)]  
  
2. Modifique `Sub Main` para usar o <xref:System.Data.Linq.DataContext> fortemente tipado da seguinte maneira:  
  
     [!code-vb[DLinqWalk2VB#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#5)]  
  
3. Pressione F5 para depurar seu aplicativo.  
  
     A saída da janela Console é:  
  
     `ID=WHITC`  
  
4. Pressione Enter na janela Console para fechar o aplicativo.  
  
5. No menu **arquivo** , clique em **salvar tudo** se desejar salvar este aplicativo.  
  
## <a name="next-steps"></a>Próximas etapas  

 A próxima instrução ([Walkthrough: Manipulando dados (Visual Basic)](walkthrough-manipulating-data-visual-basic.md)) demonstra como manipular dados. Esse passo a passo não requer que você salve os dois tutoriais passo a passo desta série que você já concluiu.  
  
## <a name="see-also"></a>Consulte também

- [Aprendendo com explicações passo a passo](learning-by-walkthroughs.md)
