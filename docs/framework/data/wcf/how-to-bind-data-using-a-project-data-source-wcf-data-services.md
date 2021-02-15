---
description: 'Saiba mais sobre: como associar dados usando uma fonte de dados do projeto (WCF Data Services)'
title: Como associar dados usando uma fonte de dados do projeto (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding, WCF Data Services
- WCF Data Services, data binding
ms.assetid: 2477af0a-676f-44f7-b73d-e66208785509
ms.openlocfilehash: 42efbfcd241487e9e729c0d0bf2eba1f8f20d996
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765705"
---
# <a name="how-to-bind-data-using-a-project-data-source-wcf-data-services"></a>Como associar dados usando uma fonte de dados do projeto (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Você pode criar fontes de dados que se baseiam nos objetos de dados gerados em um aplicativo cliente WCF Data Services. Quando você adiciona uma referência a um serviço de dados usando a caixa de diálogo **Adicionar referência de serviço** , uma fonte de dados do projeto é criada junto com as classes de dados do cliente geradas. Uma fonte de dados é criada para cada conjunto de entidades que o serviço de dados expõe. Você pode criar formulários que exibem dados do serviço arrastando esses itens de fonte de dados da janela **fontes de dados** para o designer. Esses itens tornam-se controles associados à fonte de dados. Durante a execução, essa fonte de dados é associada a uma instância da <xref:System.Data.Services.Client.DataServiceCollection%601> classe, que é preenchida com objetos que são retornados por uma consulta ao serviço de dados. Para obter mais informações, consulte [associando dados a controles](binding-data-to-controls-wcf-data-services.md).

 Os exemplos neste tópico usam o serviço de dados de exemplo Northwind e as classes de serviço de dados do cliente geradas automaticamente. Esse serviço e as classes de dados do cliente são criados quando você conclui o guia de [início rápido do WCF Data Services](quickstart-wcf-data-services.md).

## <a name="use-a-project-data-source-in-a-wpf-window"></a>Usar uma fonte de dados do projeto em uma janela do WPF

1. No Visual Studio, em um projeto do WPF, adicione uma referência ao serviço de dados Northwind. Para obter mais informações, consulte [como: adicionar uma referência de serviço de dados](how-to-add-a-data-service-reference-wcf-data-services.md).

2. Na janela **fontes de dados** , expanda o `Customers` nó na fonte de dados do projeto **NorthwindEntities** .

3. Clique no item **CustomerID** , selecione **ComboBox** na lista e arraste o item **CustomerID** do nó **Customers** para o designer.

     Isso cria os seguintes elementos de objeto no arquivo XAML para a janela:

    - Um <xref:System.Windows.Data.CollectionViewSource> elemento chamado `customersViewSource` . A <xref:System.Windows.FrameworkElement.DataContext%2A> Propriedade do elemento de objeto de nível superior <xref:System.Windows.Controls.Grid> é definida como esta nova <xref:System.Windows.Data.CollectionViewSource> .

    - Um associado a dados <xref:System.Windows.Controls.ComboBox> denominado `CustomerID` .

    - Um <xref:System.Windows.Controls.Label>.

4. Arraste a propriedade de navegação **Orders** para o designer.

     Isso cria os seguintes elementos de objeto adicionais no arquivo XAML para a janela:

    - Um segundo <xref:System.Windows.Data.CollectionViewSource> elemento chamado `customersOrdersViewSource` , a fonte do qual é o `customerViewSource` .

    - Um controle associado a dados <xref:System.Windows.Controls.DataGrid> denominado `ordersDataGrid` .

5. Adicional Arraste itens adicionais do nó **clientes** para o designer.

6. Abra a página de código do formulário e adicione as seguintes `using` instruções ( `Imports` em Visual Basic):

     [!code-csharp[Astoria Northwind Client#CustomersOrdersUsingWpf](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf2.xaml.cs#customersordersusingwpf)]

7. Na classe parcial que define o formulário, adicione o código a seguir que cria uma <xref:System.Data.Objects.ObjectContext> instância e define a `customerID` constante.

     [!code-csharp[Astoria Northwind Client#CustomersOrdersDefinitionWpf](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf2.xaml.cs#customersordersdefinitionwpf)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDefinitionWpf](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf2.xaml.vb#customersordersdefinitionwpf)]

8. No designer, selecione a janela.

    > [!NOTE]
    > Certifique-se de selecionar a janela em si, em vez de selecionar o conteúdo que está dentro da janela. Se a janela for selecionada, a caixa de texto **nome** próxima à parte superior da janela **Propriedades** deverá conter o nome da janela.

9. Na janela **Propriedades** , selecione o botão **eventos** .

10. Localize o evento **Loaded** e clique duas vezes na lista suspensa ao lado desse evento.

     O Visual Studio abre o arquivo code-behind para a janela e gera um <xref:System.Windows.FrameworkElement.Loaded> manipulador de eventos.

11. No <xref:System.Windows.FrameworkElement.Loaded> manipulador de eventos recém-criado, copie e cole o código a seguir.

     [!code-csharp[Astoria Northwind Client#CustomersOrdersDataBindingWpf](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf2.xaml.cs#customersordersdatabindingwpf)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDataBindingWpf](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf2.xaml.vb#customersordersdatabindingwpf)]

12. Esse código cria uma instância do <xref:System.Data.Services.Client.DataServiceCollection%601> para o `Customers` tipo com base na execução de uma consulta LINQ que retorna um <xref:System.Collections.Generic.IEnumerable%601> de `Customers` juntamente com `Orders` objetos relacionados do serviço de dados Northwind e os associa ao `customersViewSource` .

## <a name="use-a-project-data-source-in-a-windows-form"></a>Usar uma fonte de dados do projeto em um Windows Form

1. Na janela **fontes de dados** , expanda o nó **clientes** na fonte de dados do projeto **NorthwindEntities** .

2. Clique no item **CustomerID** , selecione **ComboBox** na lista e arraste o item **CustomerID** do nó **Customers** para o designer.

     Isso cria os seguintes controles no formulário:

    - Uma instância do <xref:System.Windows.Forms.BindingSource> denominada `customersBindingSource` .

    - Uma instância do <xref:System.Windows.Forms.BindingNavigator> denominada `customersBindingNavigator` . Você pode excluir esse controle, pois ele não será necessário.

    - Um associado a dados <xref:System.Windows.Forms.ComboBox> denominado `CustomerID` .

    - Um <xref:System.Windows.Forms.Label>.

3. Arraste a propriedade de navegação **Orders** para o formulário.

4. Isso cria o `ordersBindingSource` controle com a <xref:System.Windows.Forms.BindingSource.DataSource%2A> Propriedade do conjunto de controle como o `customersBindingSource` e a <xref:System.Windows.Forms.BindingSource.DataMember%2A> propriedade definida como `Customers` . Ele também cria o `ordersDataGridView` controle de vinculação de dados no formulário, acompanhado por um controle de rótulo adequadamente intitulado.

5. Adicional Arraste itens adicionais do nó **clientes** para o designer.

6. Abra a página de código do formulário e adicione as seguintes `using` instruções ( `Imports` em Visual Basic):

     [!code-csharp[Astoria Northwind Client#CustomersOrdersUsing](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorders.cs#customersordersusing)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersUsing](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorders.vb#customersordersusing)]

7. Na classe parcial que define o formulário, adicione o código a seguir que cria uma <xref:System.Data.Objects.ObjectContext> instância e define a `customerID` constante.

     [!code-csharp[Astoria Northwind Client#CustomersOrdersDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorders.cs#customersordersdefinition)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorders.vb#customersordersdefinition)]

8. No designer de formulário, clique duas vezes no formulário.

     Isso abre a página de código para o formulário e cria o método que manipula o `Load` evento para o formulário.

9. No manipulador de eventos `Load`, copie e cole o código a seguir.

     [!code-csharp[Astoria Northwind Client#CustomersOrdersDataBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorders.cs#customersordersdatabinding)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDataBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorders.vb#customersordersdatabinding)]

10. Esse código cria uma instância do <xref:System.Data.Services.Client.DataServiceCollection%601> para o `Customers` tipo com base na execução de um <xref:System.Data.Services.Client.DataServiceQuery%601> que retorna um <xref:System.Collections.Generic.IEnumerable%601> de um do `Customers` serviço de dados Northwind e o associa ao `customersBindingSource` .

## <a name="see-also"></a>Consulte também

- [Biblioteca de cliente do WCF Data Services](wcf-data-services-client-library.md)
- [Como: associar dados aos elementos do Windows Presentation Foundation](bind-data-to-wpf-elements-wcf-data-services.md)
