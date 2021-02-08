---
description: 'Saiba mais sobre: Walkthrough: usando somente procedimentos armazenados (Visual Basic)'
title: 'Passo a passo: usar somente procedimentos armazenados (Visual Basic)'
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: 5a736a30-ba66-4adb-b87c-57d19476e862
ms.openlocfilehash: b368bdd5717c0f424192c3eabb8058d633cac61e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791758"
---
# <a name="walkthrough-using-only-stored-procedures-visual-basic"></a>Passo a passo: usar somente procedimentos armazenados (Visual Basic)

Essa explicação passo a passo fornece um cenário de ponta a ponta básico de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] para acessar dados usando somente procedimentos armazenados. Essa abordagem é frequentemente usada por administradores de banco de dados para limitar como o repositório de dados é acessado.  
  
> [!NOTE]
> Você também pode usar procedimentos armazenados nos aplicativos do [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] para substituir o comportamento padrão, especialmente para os processos `Create`, `Update` e `Delete`. Para obter mais informações, consulte [Personalizando as operações de inserção, atualização e exclusão](customizing-insert-update-and-delete-operations.md).  
  
 Neste passo a passo, você usará dois métodos que foram mapeados para os procedimentos armazenados no banco de dados de exemplo Northwind: CustOrdersDetail e CustOrderHist. O mapeamento ocorre quando você executa a ferramenta de linha de comando SqlMetal para gerar um arquivo de Visual Basic. Para obter mais informações, consulte a seção Pré-requisitos posteriormente neste passo a passo.  
  
 Este tutorial não depende do Object Relational Designer. Os desenvolvedores que usam o Visual Studio também podem usar o o/R Designer para implementar a funcionalidade de procedimento armazenado. Consulte [LINQ to SQL Tools no Visual Studio](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2).  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Este passo a passo foi escrito usando as Configurações de Desenvolvimento do Visual Basic.  
  
## <a name="prerequisites"></a>Pré-requisitos  

 Este passo a passo requer o seguinte:  
  
- Essa explicação passo a passo usa uma pasta c:\linqtest3 dedicada (“") para armazenar arquivos. Crie essa pasta antes de iniciar o passo a passo.  
  
- O banco de dados de exemplo Northwind.  
  
     Se você não tiver esse banco de dados no seu computador de desenvolvimento, poderá baixá-lo no site de download da Microsoft. Para obter instruções, consulte [baixar bancos de dados de exemplo](downloading-sample-databases.md). Depois que você baixou o base de dados, copie o arquivo de northwnd.mdf para a pasta de c:\linqtest3.  
  
- Um arquivo de código do Visual Basic gerado do banco de dados Northwind.  
  
     Este passo a passo foi escrito usando a ferramenta SqlMetal com a seguinte linha de comando:  
  
     **SqlMetal/Code: "c:\linqtest3\northwind.vb"/Language: vb "c:\linqtest3\northwnd.MDF"/sprocs/Functions/Pluralize**  
  
     Para obter mais informações, consulte [SqlMetal.exe (ferramenta de geração de código)](../../../../tools/sqlmetal-exe-code-generation-tool.md).  
  
## <a name="overview"></a>Visão geral  

 Este passo a passo consiste em seis tarefas principais:  
  
- Configurando a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] solução no Visual Studio.  
  
- Adicionar o assembly System.Data.Linq ao projeto.  
  
- Adicionar o arquivo do código de banco de dados ao projeto.  
  
- Criando uma conexão a base de dados.  
  
- Configurar a interface do usuário.  
  
- Executar e testar o aplicativo.  
  
## <a name="creating-a-linq-to-sql-solution"></a>Criando uma solução LINQ to SQL  

 Nesta primeira tarefa, você cria uma solução do Visual Studio que contém as referências necessárias para compilar e executar um [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] projeto.  
  
### <a name="to-create-a-linq-to-sql-solution"></a>Para criar uma solução LINQ to SQL  
  
1. No menu **arquivo** do Visual Studio, clique em **novo projeto**.  
  
2. No painel **tipos de projeto** na caixa de diálogo **novo projeto** , expanda **Visual Basic** e clique em **Windows**.  
  
3. No painel **modelos** , clique em **Windows Forms aplicativo**.  
  
4. Na caixa **nome** , digite **SprocOnlyApp**.  
  
5. Clique em **OK**.  
  
     O Designer de Formulários do Windows é aberto.  
  
## <a name="adding-the-linq-to-sql-assembly-reference"></a>Adicionando a referência do assembly do LINQ to SQL  

 O assembly do [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não é incluído no modelo padrão do Aplicativo do Windows Forms. Você mesmo precisará adicionar o assembly, conforme explicado nas etapas a seguir:  
  
### <a name="to-add-systemdatalinqdll"></a>Para adicionar o System.Data.Linq.dll  
  
1. Em **Gerenciador de soluções**, clique em **Mostrar todos os arquivos**.  
  
2. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **referências** e clique em **Adicionar referência**.  
  
3. Na caixa de diálogo **Adicionar referência** , clique em **.net**, clique no assembly System. Data. LINQ e, em seguida, clique em **OK**.  
  
     O assembly é adicionado ao projeto.  
  
## <a name="adding-the-northwind-code-file-to-the-project"></a>Adicionando o arquivo do código Northwind ao projeto  

 Esta etapa presume que você usou a ferramenta SqlMetal para gerar um arquivo de código do banco de dados de exemplo Northwind. Para obter mais informações, consulte a seção de pré-requisitos anteriormente neste passo a passo.  
  
### <a name="to-add-the-northwind-code-file-to-the-project"></a>Para adicionar o arquivo do código Northwind ao projeto  
  
1. No menu **Projeto** , clique em **Adicionar Item Existente**.  
  
2. Na caixa de diálogo **Adicionar item existente** , vá para c:\linqtest3\northwind.vb e clique em **Adicionar**.  
  
     O arquivo northwind.vb é adicionado ao projeto.  
  
## <a name="creating-a-database-connection"></a>Criando uma conexão de banco de dados  

 Nesta etapa, você define a conexão com o banco de dados de exemplo Northwind. Essa explicação passo a passo usa “c:\linqtest3\northwnd.mdf” como o caminho.  
  
### <a name="to-create-the-database-connection"></a>Par criar a conexão de banco de dados  
  
1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **Form1. vb** e clique em **Exibir código**.  
  
     `Class Form1` aparece no editor de códigos.  
  
2. Digite o seguinte código no bloco de código de `Form1` :  
  
     [!code-vb[DLinqWalk4VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#1)]  
  
## <a name="setting-up-the-user-interface"></a>Configurando a interface do usuário  

 Nesta tarefa você cria uma interface de modo que os usuários podem executar procedimentos armazenados para acessar dados na base de dados. No aplicativo que você está desenvolvendo com este passo-a-passo, os usuários podem acessar dados na base de dados usando somente os procedimentos armazenados inseridos no aplicativo.  
  
### <a name="to-set-up-the-user-interface"></a>Para configurar a interface do usuário  
  
1. Retorne ao Designer de Formulários do Windows (**Form1. vb [Design]**).  
  
2. No menu **Exibir** , clique em **Caixa de Ferramentas**.  
  
     A caixa de ferramentas é aberta.  
  
    > [!NOTE]
    > Clique na anotação de **AutoOcultar** para manter a caixa de ferramentas aberta enquanto você executa as etapas restantes nesta seção.  
  
3. Arraste dois botões, duas caixas de texto e dois rótulos da caixa de ferramentas para o **Form1**.  
  
     Organize os controles conforme mostrado na ilustração de acompanhamento. Expanda **Form1** para que os controles caibam facilmente.  
  
4. Clique com o botão direito do mouse em **Label1** e clique em **Propriedades**.  
  
5. Altere a propriedade **Text** de **Label1** para **Enter OrderID:**.  
  
6. Da mesma forma para o **Label2**, altere a propriedade **Text** de **Label2** para **Enter CustomerID:**.  
  
7. Da mesma forma, altere a propriedade **Text** de **Button1** para **Order Details**.  
  
8. Altere a propriedade **Text** de **Button2** para **histórico de pedidos**.  
  
     Amplie os controles de botão de modo que todo o texto fique visível.  
  
### <a name="to-handle-button-clicks"></a>Para manipular cliques de botão  
  
1. Clique duas vezes em **Order Details** no **Form1** para criar o `Button1` manipulador de eventos e abrir o editor de código.  
  
2. Digite o código a seguir no manipulador `Button1`:  
  
     [!code-vb[DLinqWalk4VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#2)]  
  
3. Agora, clique duas vezes em **Button2** no Form1 para criar o `Button2` manipulador de eventos e abrir o editor de código.  
  
4. Digite o código a seguir no manipulador `Button2`:  
  
     [!code-vb[DLinqWalk4VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk4VB/vb/Form1.vb#3)]  
  
## <a name="testing-the-application"></a>Testando o aplicativo  

 Agora é hora de testar o aplicativo. Observe que o contato com o repositório de dados limita-se a qualquer ação que os dois procedimentos armazenados podem executar. Essas ações retornarão os produtos para qualquer orderID inserida ou retornarão um histórico do produtos solicitados para qualquer CustomerID inserida.  
  
### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1. Pressione F5 para iniciar a depuração.  
  
     Form1 aparecerá.  
  
2. Na caixa **Inserir NúmeroDoPedido** , digite **10249** e clique em **detalhes do pedido**.  
  
     Uma caixa de mensagem lista os produtos incluídos no pedido 10249.  
  
     Clique em **OK** para fechar a caixa de mensagens.  
  
3. Na caixa **Inserir CustomerID** , digite e, em `ALFKI` seguida, clique em **histórico do pedido**.  
  
     Uma caixa de mensagem lista o histórico de pedidos para o cliente ALFKI.  
  
     Clique em **OK** para fechar a caixa de mensagens.  
  
4. Na caixa **Inserir NúmeroDoPedido** , digite `123` e clique em detalhes do **pedido**.  
  
     Uma caixa de mensagem não exibe “nenhum” resultado.  
  
     Clique em **OK** para fechar a caixa de mensagens.  
  
5. No menu **depurar** , clique em **parar depuração**.  
  
     A sessão de depuração é fechada.  
  
6. Se você concluiu o experimento, pode clicar em **fechar projeto** no menu **arquivo** e salvar seu projeto quando solicitado.  
  
## <a name="next-steps"></a>Próximas etapas  

 Você pode aprimorar esse projeto fazendo algumas alterações. Por exemplo, você pode listar os procedimentos armazenados disponíveis em uma caixa de listagem e fazer com que o usuário selecione os procedimentos que serão executados. Você também pode transmitir a saída dos relatórios para um arquivo de texto.  
  
## <a name="see-also"></a>Consulte também

- [Aprendendo com explicações passo a passo](learning-by-walkthroughs.md)
- [Procedimentos armazenados](stored-procedures.md)
