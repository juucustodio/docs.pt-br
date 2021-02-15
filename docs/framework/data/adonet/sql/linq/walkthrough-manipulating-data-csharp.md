---
description: 'Saiba mais sobre: Walkthrough: Manipulando dados (C#)'
title: 'Passo a passo: Manipular dados (C#)'
ms.date: 03/30/2017
ms.assetid: 24adfbe0-0ad6-449f-997d-8808e0770d2e
ms.openlocfilehash: 6176709a2e02d8c06ec54b70cc6e0e4c302509c3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99729582"
---
# <a name="walkthrough-manipulating-data-c"></a>Passo a passo: Manipular dados (C#)

Essa explicação passo a passo fornece um cenário completo fundamental do [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] para adicionar, modificar e excluir dados em um banco de dados. Você usará uma cópia do banco de dados de exemplo Northwind para adicionar um cliente, alterar o nome de um cliente e excluir um pedido.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Esse passo a passo foi escrito usando as configurações de desenvolvimento do Visual C#.  
  
## <a name="prerequisites"></a>Pré-requisitos  

 Este passo a passo requer o seguinte:  
  
- Este passo a passo usa uma pasta dedicada ("c:\linqtest6") para armazenar arquivos. Crie essa pasta antes de iniciar o passo a passo.  
  
- O banco de dados de exemplo Northwind.  
  
     Se você não tiver esse banco de dados no seu computador de desenvolvimento, poderá baixá-lo no site de download da Microsoft. Para obter instruções, consulte [baixar bancos de dados de exemplo](downloading-sample-databases.md). Depois de baixar o banco de dados, copie o arquivo northwnd.mdf para a pasta c:\linqtest6.  
  
- Um arquivo de código C# gerado no banco de dados Northwind.  
  
     Você pode gerar esse arquivo usando o Object Relational Designer ou a ferramenta SqlMetal. Este passo a passo foi escrito usando a ferramenta SQLMetal com a seguinte linha de comando:  
  
     **SqlMetal/Code: "c:\linqtest6\northwind.cs"/Language: CSharp "C:\linqtest6\northwnd.MDF"/Pluralize**  
  
     Para obter mais informações, consulte [SqlMetal.exe (ferramenta de geração de código)](../../../../tools/sqlmetal-exe-code-generation-tool.md).  
  
## <a name="overview"></a>Visão geral  

 Este passo a passo consiste em seis tarefas principais:  
  
- Criando a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] solução no Visual Studio.  
  
- Adicionar o arquivo do código de banco de dados ao projeto.  
  
- Criar um novo objeto do cliente.  
  
- Alterar o nome de contato de um cliente.  
  
- Excluir um pedido.  
  
- Enviar essas alterações para o banco de dados Northwind.  
  
## <a name="creating-a-linq-to-sql-solution"></a>Criando uma solução LINQ to SQL  

 Nesta primeira tarefa, você cria uma solução do Visual Studio que contém as referências necessárias para compilar e executar um [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] projeto.  
  
#### <a name="to-create-a-linq-to-sql-solution"></a>Para criar uma solução LINQ to SQL  
  
1. No menu **arquivo** do Visual Studio, aponte para **novo** e clique em **projeto**.  
  
2. No painel **tipos de projeto** na caixa de diálogo **novo projeto** , clique em **Visual C#**.  
  
3. No painel **Modelos**, clique em **Aplicativo de Console**.  
  
4. Na caixa **nome** , digite **LinqDataManipulationApp**.  
  
5. Na caixa **local** , verifique onde você deseja armazenar os arquivos de projeto.  
  
6. Clique em **OK**.  
  
## <a name="adding-linq-references-and-directives"></a>Adicionando referências e diretivas LINQ  

 Este passo a passo usa assemblies que não podem ser instalados por padrão em seu projeto. Se System.Data.Linq não estiver listado como uma referência em seu projeto, adicione-o, conforme explicado nas seguintes etapas:  
  
#### <a name="to-add-systemdatalinq"></a>Para adicionar System.Data.Linq  
  
1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **referências** e clique em **Adicionar referência**.  
  
2. Na caixa de diálogo **Adicionar referência** , clique em **.net**, clique no assembly System. Data. LINQ e, em seguida, clique em **OK**.  
  
     O assembly é adicionado ao projeto.  
  
3. Adicione as seguintes diretivas na parte superior de Program.cs:  
  
     [!code-csharp[DLinqWalk3CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#1)]  
  
## <a name="adding-the-northwind-code-file-to-the-project"></a>Adicionando o arquivo do código Northwind ao projeto  

 Estas etapas presumem que você tenha usado a ferramenta SQLMetal para gerar um arquivo de código do banco de dados de exemplo Northwind. Para obter mais informações, consulte a seção de pré-requisitos anteriormente neste passo a passo.  
  
#### <a name="to-add-the-northwind-code-file-to-the-project"></a>Para adicionar o arquivo do código Northwind ao projeto  
  
1. No menu **Projeto** , clique em **Adicionar Item Existente**.  
  
2. Na caixa de diálogo **Adicionar item existente** , navegue até c:\linqtest6\northwind.cs e clique em **Adicionar**.  
  
     O arquivo northwind.cs é adicionado ao projeto.  
  
## <a name="setting-up-the-database-connection"></a>Configurando a conexão de banco de dados  

 Primeiro, teste sua conexão com o banco de dados. Observe especialmente se o banco de dados, Northwnd, não tem nenhum caractere i. Se você gerar erros nas próximas etapas, revise o arquivo northwind.cs para determinar como a classe parcial do Northwind é soletrada.  
  
#### <a name="to-set-up-and-test-the-database-connection"></a>Para configurar e testar a conexão com o banco de dados  
  
1. Digite ou cole o código a seguir no método `Main` na classe Program:  
  
     [!code-csharp[DLinqWalk3CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#2)]  
  
2. Pressione F5 para testar o aplicativo neste ponto.  
  
     Uma janela de **console** é aberta.  
  
     Você pode fechar o aplicativo pressionando ENTER na janela do **console** ou clicando em **parar depuração** no menu **depurar** do Visual Studio.  
  
## <a name="creating-a-new-entity"></a>Criando uma nova entidade  

 Criar uma nova entidade é simples. Você pode criar objetos (como `Customer`) usando a palavra-chave `new`.  
  
 Nessa seção e nas seguintes, você está fazendo alterações somente no cache local. Nenhuma alteração será enviada para o banco de dados até que você chame <xref:System.Data.Linq.DataContext.SubmitChanges%2A> no final dessa explicação passo a passo.  
  
#### <a name="to-add-a-new-customer-entity-object"></a>Para adicionar um novo objeto de entidade de cliente  
  
1. Crie um novo `Customer` adicionando o seguinte código antes de `Console.ReadLine();` no método `Main`:  
  
     [!code-csharp[DLinqWalk3CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#3)]  
  
2. Pressione F5 para depurar a solução.  
  
3. Pressione Enter na janela do **console** para parar a depuração e continuar o passo a passos.  
  
## <a name="updating-an-entity"></a>Atualizar uma entidade  

 Nas etapas a seguir, você recuperará um objeto `Customer` e alterará uma de suas propriedades.  
  
#### <a name="to-change-the-name-of-a-customer"></a>Para alterar o nome de um cliente  
  
- Adicione o seguinte código acima de `Console.ReadLine();`:  
  
     [!code-csharp[DLinqWalk3CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#4)]  
  
## <a name="deleting-an-entity"></a>Excluindo uma entidade  

 Usando o mesmo objeto de cliente, você poderá excluir o primeiro pedido.  
  
 O código a seguir demonstra como separar relações entre linhas, e como excluir uma linha do banco de dados. Adicione o seguinte código antes de `Console.ReadLine` para ver como os objetos podem ser excluídos:  
  
#### <a name="to-delete-a-row"></a>Para excluir uma linha  
  
- Adicione o seguinte código bem acima de `Console.ReadLine();`:  
  
     [!code-csharp[DLinqWalk3CS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#5)]  
  
## <a name="submitting-changes-to-the-database"></a>Enviando alterações para o banco de dados  

 A etapa final necessária para criar, atualizar e excluir objetos é realmente enviar as alterações para o banco de dados. Sem esta etapa, suas alterações serão somente locais e não aparecerão nos resultados da consulta.  
  
#### <a name="to-submit-changes-to-the-database"></a>Para enviar alterações para o banco de dados  
  
1. Insira o seguinte código bem acima de `Console.ReadLine`:  
  
     [!code-csharp[DLinqWalk3CS#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#6)]  
  
2. Insira o código a seguir (após `SubmitChanges`) para mostrar os efeitos de antes e depois de enviar as alterações:  
  
     [!code-csharp[DLinqWalk3CS#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#7)]  
  
3. Pressione F5 para depurar a solução.  
  
4. Pressione Enter na janela do **console** para fechar o aplicativo.  
  
> [!NOTE]
> Depois de adicionar o novo cliente enviando as alterações, você não poderá executar esta solução novamente como está. Para executar novamente a solução, altere o nome do cliente e a ID do cliente a ser adicionada.  
  
## <a name="see-also"></a>Consulte também

- [Aprendendo com explicações passo a passo](learning-by-walkthroughs.md)
