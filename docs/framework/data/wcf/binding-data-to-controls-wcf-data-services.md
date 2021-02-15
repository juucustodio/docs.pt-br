---
description: 'Saiba mais sobre: vinculação de dados a controles (WCF Data Services)'
title: Associando dados a controles (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- client applications, WCF Data Services
- WCF Data Services, client library
- data binding, WCF Data Services
ms.assetid: b32e1d49-c214-4cb1-867e-88fbb3d08c8d
ms.openlocfilehash: 01ef24c2723bb690a8f441a315085c4312307b03
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766472"
---
# <a name="binding-data-to-controls-wcf-data-services"></a>Associando dados a controles (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Com WCF Data Services, você pode associar controles como os `ComboBox` controles e `ListView` a uma instância da <xref:System.Data.Services.Client.DataServiceCollection%601> classe. Essa coleção, que é herdada da <xref:System.Collections.ObjectModel.ObservableCollection%601> classe, contém os dados de um feed protocolo Open Data (OData). Essa classe representa uma coleção de dados dinâmicos que fornece notificações quando itens são adicionados ou removidos. Quando você usa uma instância do <xref:System.Data.Services.Client.DataServiceCollection%601> para associação de dados, as bibliotecas de cliente do WCF Data Services lidam com esses eventos para garantir que os objetos rastreados pelo <xref:System.Data.Services.Client.DataServiceContext> permaneçam sincronizados com os dados no elemento da interface do usuário associada.  
  
 A classe <xref:System.Data.Services.Client.DataServiceCollection%601> (indiretamente) implementa a interface do <xref:System.Collections.Specialized.INotifyCollectionChanged> para alertar o contexto quando os objetos forem adicionados ou removidos da coleção. Os objetos do tipo de serviço de dados usados com <xref:System.Data.Services.Client.DataServiceCollection%601> também devem implementar a interface de <xref:System.ComponentModel.INotifyPropertyChanged> para alertar <xref:System.Data.Services.Client.DataServiceCollection%601> quando as propriedades dos objetos na coleção de associação forem alterados.  
  
> [!NOTE]
> Quando você usa a caixa de diálogo **Adicionar referência de serviço** ou a ferramenta de [DataSvcUtil.exe](wcf-data-service-client-utility-datasvcutil-exe.md) com a `/dataservicecollection` opção de gerar as classes de serviço de dados do cliente, as classes de dados geradas implementam a <xref:System.ComponentModel.INotifyPropertyChanged> interface. Para obter mais informações, consulte [como: gerar manualmente classes de serviço de dados do cliente](how-to-manually-generate-client-data-service-classes-wcf-data-services.md).  
  
## <a name="creating-the-binding-collection"></a>Criando a coleção de associação  

 Crie uma nova instância da classe <xref:System.Data.Services.Client.DataServiceCollection%601> chamando um dos métodos de construtor de classe com um instância de <xref:System.Data.Services.Client.DataServiceContext> fornecida e, opcionalmente, um <xref:System.Data.Services.Client.DataServiceQuery%601> ou consulta LINQ que, quando executada, retorna uma instância de <xref:System.Collections.Generic.IEnumerable%601>. Isso <xref:System.Collections.Generic.IEnumerable%601> fornece a fonte de objetos para a coleção de associação, que são materializados de um feed OData. Para obter mais informações, consulte [materialização de objeto](object-materialization-wcf-data-services.md). Por padrão, as alterações feitas em objetos e itens associados inseridos na coleção são controlados automaticamente por <xref:System.Data.Services.Client.DataServiceContext>. Se você precisar controlar manualmente essas alterações, chame um dos métodos do construtor que usa um `trackingMode` parâmetro e especifique um valor de <xref:System.Data.Services.Client.TrackingMode.None> .  
  
 O exemplo a seguir mostra como criar uma instância de <xref:System.Data.Services.Client.DataServiceCollection%601> baseada em um <xref:System.Data.Services.Client.DataServiceContext> fornecido e em um <xref:System.Data.Services.Client.DataServiceQuery%601>, que retorna todos os clientes com pedidos relacionados:  
  
 [!code-csharp[Astoria Northwind Client#CustomersOrders2Binding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorders2.cs#customersorders2binding)]
 [!code-vb[Astoria Northwind Client#CustomersOrders2Binding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorders2.vb#customersorders2binding)]  
  
## <a name="binding-data-to-windows-presentation-foundation-elements"></a>Associando dados aos elementos do Windows Presentation Foundation  

 Como a classe <xref:System.Data.Services.Client.DataServiceCollection%601> herda da classe <xref:System.Collections.ObjectModel.ObservableCollection%601>, você pode associar objetos a um elemento ou controle em um aplicativo WPF (Windows Presentation Foundation) como o faria ao usar a classe <xref:System.Collections.ObjectModel.ObservableCollection%601> para associação. Para obter mais informações, consulte [vinculação de dados (Windows Presentation Foundation)](/dotnet/desktop/wpf/data/data-binding-overview). Uma maneira de associar dados do serviço de dados a controles WPF é definir a propriedade `DataContext` do elemento como a instância da classe <xref:System.Data.Services.Client.DataServiceCollection%601> que contém o resultado da consulta. Nesse caso, você usa a propriedade <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> para definir a origem do objeto para o controle. Use a propriedade <xref:System.Windows.Controls.ItemsControl.DisplayMemberPath%2A> para especificar qual propriedade do objeto associado deve ser exibida. Se você estiver associando um elemento a um objeto relacionado que é retornado por uma propriedade de navegação, inclua o caminho na associação definida para a propriedade <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>. Esse caminho é relativo ao objeto raiz definido pela propriedade <xref:System.Windows.FrameworkElement.DataContext%2A> do controle pai. O exemplo a seguir define a propriedade <xref:System.Windows.FrameworkElement.DataContext%2A> de um elemento <xref:System.Windows.Controls.StackPanel> para associar o controle pai a um <xref:System.Data.Services.Client.DataServiceCollection%601> dos objetos de cliente:  
  
 [!code-csharp[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderscustom.xaml.cs#masterdetailbinding)]
 [!code-csharp[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf.xaml.cs#masterdetailbinding)]
 [!code-vb[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom.xaml.vb#masterdetailbinding)]
 [!code-vb[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf.xaml.vb#masterdetailbinding)]
 [!code-vb[Astoria Northwind Client#MasterDetailBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom2.xaml.vb#masterdetailbinding)]  
  
 O exemplo a seguir mostra o definição de associação XAML do <xref:System.Windows.Controls.DataGrid> filho e controles de <xref:System.Windows.Controls.ComboBox>:  
  
 [!code-xaml[Astoria Northwind Client#MasterDetailXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf.xaml#masterdetailxaml)]  
  
 Para obter mais informações, consulte [como associar dados a elementos de Windows Presentation Foundation](bind-data-to-wpf-elements-wcf-data-services.md).  
  
 Quando uma entidade participa de uma relação um-para-muitos ou muitos-para-muitos, a propriedade de navegação da relação retorna uma coleção de objetos relacionados. Quando você usa a caixa de diálogo **Adicionar referência de serviço** ou a ferramenta DataSvcUtil.exe para gerar as classes de serviço de dados do cliente, a propriedade de navegação retorna uma instância do <xref:System.Data.Services.Client.DataServiceCollection%601> . Isso permite que você associe objetos relacionados a um controle e dê suporte a cenários de associação WPF comuns, como o padrão de associação de detalhes mestre para entidades relacionadas. No exemplo anterior de XAML, o código XAML associa o <xref:System.Data.Services.Client.DataServiceCollection%601> mestre ao elemento de dados raiz. O <xref:System.Windows.Controls.DataGrid> do pedido é então associado ao <xref:System.Data.Services.Client.DataServiceCollection%601> dos pedidos retornados do objeto Customers selecionado, que, por sua vez, é associado ao elemento de dados raiz do <xref:System.Windows.Window>.  
  
## <a name="binding-data-to-windows-forms-controls"></a>Associando dados aos controles do Windows Forms  

 Para associar objetos um controle do Windows Form, defina a propriedade `DataSource` do controle à instância da classe <xref:System.Data.Services.Client.DataServiceCollection%601> que contém o resultado da consulta.  
  
> [!NOTE]
> A vinculação de dados é tem suporte apenas para controles que escutam eventos de alteração implementando as interfaces de <xref:System.Collections.Specialized.INotifyCollectionChanged> e <xref:System.ComponentModel.INotifyPropertyChanged>. Quando um controle não dá suporte a esse tipo de notificação de alteração, as alterações que são feitas no <xref:System.Data.Services.Client.DataServiceCollection%601> subjacente não são refletidas no controle associado.  
  
 O exemplo a seguir associa um <xref:System.Data.Services.Client.DataServiceCollection%601> a um controle <xref:System.Windows.Forms.ComboBox>:  
  
 [!code-csharp[Astoria Northwind Client#CustomersOrdersDataBindingSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorders.cs#customersordersdatabindingspecific)]
 [!code-vb[Astoria Northwind Client#CustomersOrdersDataBindingSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorders.vb#customersordersdatabindingspecific)]  
  
 Quando você usa a caixa de diálogo **Adicionar referência de serviço** para gerar as classes de serviço de dados do cliente, uma fonte de dados do projeto também é criada com base no gerado <xref:System.Data.Services.Client.DataServiceContext> . Com essa fonte de dados, você pode criar elementos de interface do usuário ou controles que exibem dados do serviço de dados simplesmente arrastando itens da janela **fontes de dados** para o designer. Esses itens se tornam os elementos na interface do usuário do aplicativo que são associados à fonte de dados. Para obter mais informações, consulte [como associar dados usando uma fonte de dados do projeto](how-to-bind-data-using-a-project-data-source-wcf-data-services.md).  
  
## <a name="binding-paged-data"></a>Associando dados paginados  

 Um serviço de dados pode ser configurado para limitar a quantidade de dados consultados que são retornados em uma única mensagem de resposta. Para obter mais informações, consulte [Configurando o serviço de dados](configuring-the-data-service-wcf-data-services.md). Quando o serviço de dados está paginando dados de resposta, cada resposta contém um link que é usado para retornar a próxima página de resultados. Para obter mais informações, consulte [carregando conteúdo adiado](loading-deferred-content-wcf-data-services.md). Nesse caso, você deve carregar páginas explicitamente chamando o método <xref:System.Data.Services.Client.DataServiceCollection%601.Load%2A> no <xref:System.Data.Services.Client.DataServiceCollection%601> passando o URI obtido na propriedade <xref:System.Data.Services.Client.DataServiceQueryContinuation.NextLinkUri%2A>, como no exemplo a seguir:  
  
 [!code-csharp[Astoria Northwind Client#BindPagedDataSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf3.xaml.cs#bindpageddataspecific)]
 [!code-vb[Astoria Northwind Client#BindPagedDataSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf3.xaml.vb#bindpageddataspecific)]  
  
 Os objetos relacionados são carregados de uma maneira semelhante. Para obter mais informações, consulte [como associar dados a elementos de Windows Presentation Foundation](bind-data-to-wpf-elements-wcf-data-services.md).  
  
## <a name="customizing-data-binding-behaviors"></a>Personalizando comportamentos de vinculação de dados  

 A classe <xref:System.Data.Services.Client.DataServiceCollection%601> permite que você intercepte os eventos disparados quando são feitas alterações na coleção, como a adição ou remoção de um objeto, e quando são feitas alterações nas propriedades do objeto de uma coleção. Você pode alterar os eventos de vinculação de dados para substituir o comportamento padrão, o que inclui as seguintes restrições:  
  
- Nenhuma validação é executada dentro dos representantes.  
  
- A adição de uma entidade adiciona automaticamente as entidades relacionadas.  
  
- A exclusão de uma entidade não exclui as entidades relacionadas.  
  
 Quando cria uma nova instância de <xref:System.Data.Services.Client.DataServiceCollection%601>, você tem a opção de especificar os seguintes parâmetros que definem representantes para métodos que manipulam os eventos gerados quando os objetos associados são alterados:  
  
- `entityChanged` - um método que é chamado quando a propriedade de um objeto associado é alterada. Esse delegado de <xref:System.Func%602> aceita um objeto <xref:System.Data.Services.Client.EntityChangedParams> e retorna um valor booliano que indica se o comportamento padrão, chamar <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> no <xref:System.Data.Services.Client.DataServiceContext>, ainda deve ocorrer.  
  
- `entityCollectionChanged` - um método que é chamado quando um objeto é adicionado ou removido da coleção de associação. Esse delegado de <xref:System.Func%602> aceita um objeto <xref:System.Data.Services.Client.EntityCollectionChangedParams> e retorna um valor booliano que indica se o comportamento padrão, chamar <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> para uma ação <xref:System.Collections.Specialized.NotifyCollectionChangedAction.Add> ou <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> para uma ação <xref:System.Collections.Specialized.NotifyCollectionChangedAction.Remove> no <xref:System.Data.Services.Client.DataServiceContext>, ainda deve ocorrer.  
  
> [!NOTE]
> WCF Data Services não executa nenhuma validação dos comportamentos personalizados que você implementa nesses delegados.  
  
 No exemplo a seguir, a ação <xref:System.Collections.Specialized.NotifyCollectionChangedAction.Remove> é personalizada para chamar o <xref:System.Data.Services.Client.DataServiceContext.DeleteLink%2A> e o método <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> para remover as entidades `Orders_Details` que pertencem a uma entidade `Orders` excluída. Esta ação personalizada é executada porque as entidades dependentes não são excluídas automaticamente quando o objeto pai é excluído.  
  
 [!code-csharp[Astoria Northwind Client#CustomersOrdersDeleteRelated](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderscustom.xaml.cs#customersordersdeleterelated)]
 [!code-vb[Astoria Northwind Client#CustomersOrdersDeleteRelated](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom.xaml.vb#customersordersdeleterelated)]
 [!code-vb[Astoria Northwind Client#CustomersOrdersDeleteRelated](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom2.xaml.vb#customersordersdeleterelated)]  
  
 Para obter mais informações, consulte [How to: Customize Data Binding Behaviors](how-to-customize-data-binding-behaviors-wcf-data-services.md).  
  
 O comportamento padrão quando um objeto é removido de um <xref:System.Data.Services.Client.DataServiceCollection%601> usando o método <xref:System.Collections.ObjectModel.Collection%601.Remove%2A> é que o objeto também é marcado como excluído no <xref:System.Data.Services.Client.DataServiceContext>. Para alterar esse comportamento, você pode especificar um representante para um método no parâmetro `entityCollectionChanged` que é chamado quando o evento <xref:System.Collections.Specialized.INotifyCollectionChanged.CollectionChanged> ocorre.  
  
## <a name="data-binding-with-custom-client-data-classes"></a>Vinculação de dados com classes de dados de cliente personalizadas  

 Para poder carregar objetos em um <xref:System.Data.Services.Client.DataServiceCollection%601>, os próprios objetos devem implementar a interface de <xref:System.ComponentModel.INotifyPropertyChanged>. As classes de cliente do serviço de dados que são geradas quando você usa a caixa de diálogo **Adicionar referência de serviço** ou a ferramenta [DataSvcUtil.exe](wcf-data-service-client-utility-datasvcutil-exe.md) implementam essa interface. Se você fornecer suas próprias classes de dados do cliente, deverá usar outro tipo de coleção para vinculação de dados. Quando os objetos forem alterados, você deverá manipular os eventos nos controles associados por dados para chamar os seguintes métodos da classe <xref:System.Data.Services.Client.DataServiceContext>:  
  
- <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> - quando um novo objeto é adicionado à coleção.  
  
- <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> - quando um objeto é removido da coleção.  
  
- <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> - quando uma propriedade é alterada em um objeto da coleção.  
  
- <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> - quando um objeto é adicionado a uma coleção de objeto relacionado.  
  
- <xref:System.Data.Services.Client.DataServiceContext.SetLink%2A> - quando um objeto é adicionado a uma coleção de objetos relacionados.  
  
 Para obter mais informações, consulte [atualizando o serviço de dados](updating-the-data-service-wcf-data-services.md).  
  
## <a name="see-also"></a>Consulte também

- [Como: gerar manualmente as classes de serviço de dados do cliente](how-to-manually-generate-client-data-service-classes-wcf-data-services.md)
- [Como: adicionar uma referência de serviço de dados](how-to-add-a-data-service-reference-wcf-data-services.md)
