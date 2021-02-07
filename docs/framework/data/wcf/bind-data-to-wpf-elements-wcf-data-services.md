---
description: 'Saiba mais sobre: como associar dados a elementos de Windows Presentation Foundation (WCF Data Services)'
title: Como associar dados aos elementos do Windows Presentation Foundation (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding, WCF Data Services
- WCF Data Services, data binding
ms.assetid: d6538ab0-0abe-426a-b9d9-e6f3a5ca2016
ms.openlocfilehash: 57ad03770681fbedf9b0d5afae82a0a2590f0bc6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766524"
---
# <a name="how-to-bind-data-to-windows-presentation-foundation-elements-wcf-data-services"></a>Como associar dados aos elementos do Windows Presentation Foundation (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Com WCF Data Services, você pode associar elementos de Windows Presentation Foundation (WPF), como um <xref:System.Windows.Controls.ListBox> ou <xref:System.Windows.Controls.ComboBox> a uma instância do <xref:System.Data.Services.Client.DataServiceCollection%601> , que manipula os eventos gerados pelos controles para manter o <xref:System.Data.Services.Client.DataServiceContext> sincronizado com as alterações feitas nos dados nos controles. Para obter mais informações, consulte [associando dados a controles](binding-data-to-controls-wcf-data-services.md).  
  
 O exemplo deste tópico usa o serviço de dados de exemplo Northwind e as classes de serviço de dados do cliente geradas automaticamente. Esse serviço e as classes de dados do cliente são criados quando você conclui o guia de [início rápido do WCF Data Services](quickstart-wcf-data-services.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir é da página code-behind de uma página da linguagem XAML que define a janela `SalesOrders` no WPF. Quando a janela é carregada, uma <xref:System.Data.Services.Client.DataServiceCollection%601> é criada com base no resultado de uma consulta que retorna clientes, filtrados por país/região. Todas as páginas deste resultado paginado são carregadas, juntamente com os pedidos relacionados, e associadas à propriedade <xref:System.Windows.FrameworkElement.DataContext%2A> do <xref:System.Windows.Controls.StackPanel> que é o controle do layout raiz da janela WPF. Para obter mais informações, consulte [carregando conteúdo adiado](loading-deferred-content-wcf-data-services.md).  
  
 [!code-csharp[Astoria Northwind Client#BindPagedData](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf3.xaml.cs#bindpageddata)]
 [!code-vb[Astoria Northwind Client#BindPagedData](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf3.xaml.vb#bindpageddata)]  
  
## <a name="example"></a>Exemplo  

 O XAML a seguir define a janela `SalesOrders` no WPF do exemplo anterior.  
  
 [!code-xaml[Astoria Northwind Client#BindPagedDataXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf3.xaml#bindpageddataxaml)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir é da página code-behind de uma página da linguagem XAML que define a janela `SalesOrders` no WPF. Quando a janela é carregada, uma <xref:System.Data.Services.Client.DataServiceCollection%601> é criada com base no resultado de uma consulta que retorna clientes com objetos relacionados, filtrados por país/região. Esse resultado é associado à propriedade <xref:System.Windows.FrameworkElement.DataContext%2A> do <xref:System.Windows.Controls.StackPanel> que é o controle de layout raiz da janela WPF.  
  
 [!code-csharp[Astoria Northwind Client#WpfDataBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderswpf.xaml.cs#wpfdatabinding)]
 [!code-vb[Astoria Northwind Client#WpfDataBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf.xaml.vb#wpfdatabinding)]  
  
## <a name="example"></a>Exemplo  

 O XAML a seguir define a janela `SalesOrders` no WPF do exemplo anterior.  
  
 [!code-xaml[Astoria Northwind Client#WpfDataBindingXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderswpf.xaml#wpfdatabindingxaml)]
