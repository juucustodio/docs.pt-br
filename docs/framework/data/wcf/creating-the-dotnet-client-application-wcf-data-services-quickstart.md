---
description: 'Saiba mais sobre: criando o aplicativo cliente do .NET Framework (WCF Data Services início rápido)'
title: Criando o aplicativo cliente do .NET Framework (Início rápido do WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 41ade767-eeab-437d-9121-9797e8fb8045
ms.openlocfilehash: 6a397726b0680d4091f7cefd8928e43c74dc08bf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766201"
---
# <a name="creating-the-net-framework-client-application-wcf-data-services-quickstart"></a>Criando o aplicativo cliente do .NET Framework (Início rápido do WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Esta é a tarefa final do guia de início rápido do WCF Data Services. Nesta tarefa, você adicionará um aplicativo de console à solução, adicionará uma referência ao feed Protocolo Open Data (OData) nesse novo aplicativo cliente e acessará o feed OData do aplicativo cliente usando as classes de serviço de dados do cliente geradas e as bibliotecas de cliente.

> [!NOTE]
> Um aplicativo cliente baseado no .NET framework não é necessário para acessar um feed de dados. O serviço de dados pode ser acessado por qualquer componente de aplicativo que consuma um feed OData. Para obter mais informações, consulte [usando um serviço de dados em um aplicativo cliente](using-a-data-service-in-a-client-application-wcf-data-services.md).

## <a name="to-create-the-client-application-by-using-visual-studio"></a>Para criar o aplicativo cliente usando Visual Studio

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse na solução, clique em **Adicionar** e em **novo projeto**.

2. No painel esquerdo, selecione **instalado** > [**Visual C#** ou **Visual Basic**] > área de **trabalho do Windows** e, em seguida, selecione o modelo aplicativo do **WPF** .

3. Insira `NorthwindClient` para o nome do projeto e clique em **OK**.

4. Abra o arquivo MainWindow.xaml e substitua o XAML pelo seguinte código:

     [!code-xaml[Astoria Quickstart Client#Window1Xaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_client/vb/window1.xaml#window1xaml)]

## <a name="to-add-a-data-service-reference-to-the-project"></a>Para adicionar uma referência de serviço de dados ao projeto

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto NorthwindClient, clique em **Adicionar**  >  **referência de serviço** e clique em **descobrir**.

     Isso exibe o serviço de dados Northwind que você criou na primeira tarefa.

2. Na caixa de texto **namespace** , digite `Northwind` e clique em **OK**.

     Isso adiciona um novo arquivo de código ao projeto, que contém classes de dados que são usadas para acessar e interagir com os recursos do serviço de dados como objetos. As classes de dados são criadas no namespace `NorthwindClient.Northwind`.

## <a name="to-access-data-service-data-in-the-wpf-application"></a>Para acessar dados do serviço de dados no aplicativo WPF

1. Em **Gerenciador de soluções** em **NorthwindClient**, clique com o botão direito do mouse no projeto e clique em **Adicionar referência**.

2. Na caixa de diálogo **Adicionar referência** , clique na guia **.net** , selecione o assembly System.Data.Services.Client.dll e clique em **OK**.

3. Em **Gerenciador de soluções** em **NorthwindClient**, abra a página de código do arquivo MainWindow. XAML e adicione a instrução a seguir `using` ( `Imports` em Visual Basic).

    [!code-csharp[Astoria Quickstart Client#Using](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_client/cs/window1.xaml.cs#using)]
    [!code-vb[Astoria Quickstart Client#Using](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_client/vb/window1.xaml.vb#using)]

4. Insira o código a seguir que consulta esse serviço de dados e associa o resultado a uma classe <xref:System.Data.Services.Client.DataServiceCollection%601> na classe `MainWindow`:

    > [!NOTE]
    > Você deve substituir o nome de host `localhost:12345` pelo servidor e a porta que está hospedando sua instância do serviço de dados Northwind.

     [!code-csharp[Astoria Quickstart Client#QueryCode](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_client/cs/window1.xaml.cs#querycode)]
     [!code-vb[Astoria Quickstart Client#QueryCode](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_client/vb/window1.xaml.vb#querycode)]

5. Insira o seguinte código que salvar as alterações na classe `MainWindow`:

     [!code-csharp[Astoria Quickstart Client#SaveChanges](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_client/cs/window1.xaml.cs#savechanges)]
     [!code-vb[Astoria Quickstart Client#SaveChanges](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_client/vb/window1.xaml.vb#savechanges)]

## <a name="to-build-and-run-the-northwindclient-application"></a>Para compilar e executar o aplicativo NorthwindClient

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto NorthwindClient e selecione **definir como projeto de inicialização**.

2. Pressione **F5** para iniciar o aplicativo.

     Isso compila a solução e inicia o aplicativo cliente. Os dados são solicitados do serviço e exibidos no console.

3. Edite um valor na coluna **quantidade** da grade de dados e, em seguida, clique em **salvar**.

     As alterações são salvas no serviço de dados.

    > [!NOTE]
    > Esta versão do aplicativo NorthwindClient não dá suporte a adição e exclusão de entidades.

## <a name="next-steps"></a>Próximas etapas

Você criou com êxito o aplicativo cliente que acessa o feed OData de exemplo Northwind. Você também concluiu o guia de início rápido WCF Data Services!

Para obter mais informações sobre como acessar um feed OData de um aplicativo .NET Framework, consulte [WCF Data Services biblioteca de cliente](wcf-data-services-client-library.md).

## <a name="see-also"></a>Consulte também

- [Introdução](getting-started-with-wcf-data-services.md)
- [Recursos](wcf-data-services-resources.md)
