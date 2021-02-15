---
description: 'Saiba mais sobre: Walkthrough: Manipulando dados (Visual Basic)'
title: 'Passo a passo: manipular dados (Visual Basic)'
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: 1f6a54f6-ec33-452a-a37d-48122207bf14
ms.openlocfilehash: 22bef61c294a92984446402063bf14b06f5b2b2d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99729517"
---
# <a name="walkthrough-manipulating-data-visual-basic"></a>Passo a passo: manipular dados (Visual Basic)

Essa explicação passo a passo fornece um cenário completo fundamental do [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] para adicionar, modificar e excluir dados em um banco de dados. Você usará uma cópia do banco de dados de exemplo Northwind para adicionar um cliente, alterar o nome de um cliente e excluir um pedido.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Este passo a passo foi escrito usando as Configurações de Desenvolvimento do Visual Basic.  
  
## <a name="prerequisites"></a>Pré-requisitos  

 Este passo a passo requer o seguinte:  
  
- Este passo a passo usa uma pasta dedicada ("c:\linqtest2") para armazenar arquivos. Crie essa pasta antes de iniciar o passo a passo.  
  
- O banco de dados de exemplo Northwind.  
  
     Se você não tiver esse banco de dados no seu computador de desenvolvimento, poderá baixá-lo no site de download da Microsoft. Para obter instruções, consulte [baixar bancos de dados de exemplo](downloading-sample-databases.md). Depois de baixar o banco de dados, copie o arquivo northwnd.mdf para a pasta c:\linqtest2.  
  
- Um arquivo de código do Visual Basic gerado do banco de dados Northwind.  
  
     Você pode gerar esse arquivo usando o Object Relational Designer ou a ferramenta SqlMetal. Este passo a passo foi escrito usando a ferramenta SQLMetal com a seguinte linha de comando:  
  
     **SqlMetal/Code: "c:\linqtest2\northwind.vb"/Language: vb "C:\linqtest2\northwnd.MDF"/Pluralize**  
  
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
  
1. No menu **arquivo** do Visual Studio, clique em **novo projeto**.  
  
2. No painel **tipos de projeto** na caixa de diálogo **novo projeto** , clique em **Visual Basic**.  
  
3. No painel **Modelos**, clique em **Aplicativo de Console**.  
  
4. Na caixa **nome** , digite **LinqDataManipulationApp**.  
  
5. Clique em **OK**.  
  
## <a name="adding-linq-references-and-directives"></a>Adicionando referências e diretivas LINQ  

 Este passo a passo usa assemblies que não podem ser instalados por padrão em seu projeto. Se `System.Data.Linq` não estiver listado como uma referência em seu projeto (clique em **Mostrar todos os arquivos** em **Gerenciador de soluções** e expanda o nó **referências** ), adicione-o, conforme explicado nas etapas a seguir.  
  
#### <a name="to-add-systemdatalinq"></a>Para adicionar System.Data.Linq  
  
1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **referências** e clique em **Adicionar referência**.  
  
2. Na caixa de diálogo **Adicionar referência** , clique em **.net**, clique no assembly System. Data. LINQ e, em seguida, clique em **OK**.  
  
     O assembly é adicionado ao projeto.  
  
3. No editor de código, adicione as seguintes diretivas acima do **Module1**:  
  
     [!code-vb[DLinqWalk3VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#1)]  
  
## <a name="adding-the-northwind-code-file-to-the-project"></a>Adicionando o arquivo do código Northwind ao projeto  

 Estas etapas presumem que você tenha usado a ferramenta SQLMetal para gerar um arquivo de código do banco de dados de exemplo Northwind. Para obter mais informações, consulte a seção de pré-requisitos anteriormente neste passo a passo.  
  
#### <a name="to-add-the-northwind-code-file-to-the-project"></a>Para adicionar o arquivo do código Northwind ao projeto  
  
1. No menu **Projeto** , clique em **Adicionar Item Existente**.  
  
2. Na caixa de diálogo **Adicionar item existente** , navegue até c:\linqtest2\northwind.vb e clique em **Adicionar**.  
  
     O arquivo northwind.vb é adicionado ao projeto.  
  
## <a name="setting-up-the-database-connection"></a>Configurando a conexão de banco de dados  

 Primeiro, teste sua conexão com o banco de dados. Observe especialmente se o nome do banco de dados, Northwnd, não tem nenhum caractere i. Se você gerar erros nas próximas etapas, revise o arquivo northwind.vb para determinar como a classe parcial do Northwind é soletrada.  
  
#### <a name="to-set-up-and-test-the-database-connection"></a>Para configurar e testar a conexão com o banco de dados  
  
1. Digite ou cole o seguinte código em `Sub Main`:  
  
     [!code-vb[DLinqWalk3VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#2)]  
  
2. Pressione F5 para testar o aplicativo neste ponto.  
  
     Uma janela de **console** é aberta.  
  
     Feche o aplicativo pressionando ENTER na janela do **console** ou clicando em **parar depuração** no menu **depurar** do Visual Studio.  
  
## <a name="creating-a-new-entity"></a>Criando uma nova entidade  

 Criar uma nova entidade é simples. Você pode criar objetos (como `Customer`) usando a palavra-chave `New`.  
  
 Nessa seção e nas seguintes, você está fazendo alterações somente no cache local. Nenhuma alteração será enviada para o banco de dados até que você chame <xref:System.Data.Linq.DataContext.SubmitChanges%2A> no final dessa explicação passo a passo.  
  
#### <a name="to-add-a-new-customer-entity-object"></a>Para adicionar um novo objeto de entidade de cliente  
  
1. Crie um novo `Customer` adicionando o seguinte código antes de `Console.ReadLine` em `Sub Main`:  
  
     [!code-vb[DLinqWalk3VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#3)]  
  
2. Pressione F5 para depurar a solução.  
  
     Os resultados mostrados na janela do console são:  
  
     `Customers matching CA before insert:`  
  
     `Customer ID: CACTU`  
  
     `Customer ID: RICAR`  
  
     Observe que a nova linha não aparece nos resultados. Os novos dados ainda não foram enviados para o banco de dados.  
  
3. Pressione Enter na janela do **console** para parar a depuração.  
  
## <a name="updating-an-entity"></a>Atualizar uma entidade  

 Nas etapas a seguir, você recuperará um objeto `Customer` e alterará uma de suas propriedades.  
  
#### <a name="to-change-the-name-of-a-customer"></a>Para alterar o nome de um cliente  
  
- Adicione o seguinte código acima de `Console.ReadLine()`:  
  
     [!code-vb[DLinqWalk3VB#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#4)]  
  
## <a name="deleting-an-entity"></a>Excluindo uma entidade  

 Usando o mesmo objeto de cliente, você poderá excluir o primeiro pedido.  
  
 O código a seguir demonstra como separar relações entre linhas, e como excluir uma linha do banco de dados.  
  
#### <a name="to-delete-a-row"></a>Para excluir uma linha  
  
- Adicione o seguinte código bem acima de `Console.ReadLine()`:  
  
     [!code-vb[DLinqWalk3VB#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#5)]  
  
## <a name="submitting-changes-to-the-database"></a>Enviando alterações para o banco de dados  

 A etapa final necessária para criar, atualizar e excluir objetos é realmente enviar as alterações para o banco de dados. Sem esta etapa, suas alterações serão somente locais e não aparecerão nos resultados da consulta.  
  
#### <a name="to-submit-changes-to-the-database"></a>Para enviar alterações para o banco de dados  
  
1. Insira o seguinte código bem acima de `Console.ReadLine`:  
  
     [!code-vb[DLinqWalk3VB#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#6)]  
  
2. Insira o código a seguir (após `SubmitChanges`) para mostrar os efeitos de antes e depois de enviar as alterações:  
  
     [!code-vb[DLinqWalk3VB#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk3VB/vb/Module1.vb#7)]  
  
3. Pressione F5 para depurar a solução.  
  
     A janela do console aparece da seguinte maneira:  
  
    ```console
    Customers matching CA before update:  
    Customer ID: CACTU  
    Customer ID: RICAR  
  
    The Order Detail to be deleted is: OrderID = 10643  
  
    Customers matching CA after update:  
    Customer ID: A3VCA  
    Customer ID: CACTU  
    Customer ID: RICAR  
    ```  
  
4. Pressione Enter na janela do **console** para parar a depuração.  
  
> [!NOTE]
> Depois de você ter adicionado o novo cliente enviando as alterações, você não poderá executar esta solução novamente desta forma, porque não poderá adicionar o mesmo cliente novamente. Para executar novamente a solução, altere o valor da identificação do cliente a ser adicionado.  
  
## <a name="see-also"></a>Consulte também

- [Aprendendo com explicações passo a passo](learning-by-walkthroughs.md)
