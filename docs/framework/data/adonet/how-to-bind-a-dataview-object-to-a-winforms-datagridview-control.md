---
description: 'Saiba mais sobre: como associar um objeto DataView a um controle Windows Forms DataGridView'
title: 'Como: associar um objeto de DataView a um controle DataGridView do Windows Forms'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2b73d60a-6049-446a-85a7-3e5a68b183e2
ms.openlocfilehash: 59bc1a0f6b7b2b0d6da4fa6d88e06922d95c9f46
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99723901"
---
# <a name="how-to-bind-a-dataview-object-to-a-windows-forms-datagridview-control"></a>Como: associar um objeto de DataView a um controle DataGridView do Windows Forms

O controle de <xref:System.Windows.Forms.DataGridView> fornece uma maneira poderosa e flexível para exibir dados em um formato de tabela. O controle de <xref:System.Windows.Forms.DataGridView> oferece suporte ao modelo padrão de associação de dados do Windows Forms, portanto associar-se-&amp;z a <xref:System.Data.DataView> e uma variedade de outras fontes de dados. Na maioria das situações, o entanto, você associar-se-&amp;z a um componente de <xref:System.Windows.Forms.BindingSource> que gerencia os detalhes de interagir com a fonte de dados.  
  
 Para obter mais informações sobre o <xref:System.Windows.Forms.DataGridView> controle, consulte [visão geral do controle DataGridView](/dotnet/desktop/winforms/controls/datagridview-control-overview-windows-forms).  
  
### <a name="to-connect-a-datagridview-control-to-a-dataview"></a>Para se conectar a um controle DataGridView em um DataView  
  
1. Implementar um método para manipular os detalhes de recuperar dados de um base de dados. O exemplo de código a seguir implementa um método de `GetData` que inicializa um componente de <xref:System.Data.SqlClient.SqlDataAdapter> e usá-lo para preencher <xref:System.Data.DataSet>. Certifique-se de definir a variável de `connectionString` como um valor que seja apropriada para o base de dados. Você precisa ter acesso a um servidor com o base de dados de exemplo AdventureWorks do SQL Server instalado.  
  
     [!code-csharp[DP DataViewWinForms Sample#LDVSample1GetData](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/CS/Form1.cs#ldvsample1getdata)]
     [!code-vb[DP DataViewWinForms Sample#LDVSample1GetData](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/VB/Form1.vb#ldvsample1getdata)]  
  
2. No manipulador de eventos <xref:System.Windows.Forms.Form.Load> do formulário, associar o controle de <xref:System.Windows.Forms.DataGridView> componente de <xref:System.Windows.Forms.BindingSource> e chame o método de `GetData` para recuperar os dados de base de dados. O <xref:System.Data.DataView> é criado a partir de um LINQ to DataSet consulta sobre o contato <xref:System.Data.DataTable> e, em seguida, é associado ao <xref:System.Windows.Forms.BindingSource> componente.  
  
     [!code-csharp[DP DataViewWinForms Sample#LDVSample1FormLoad](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/CS/Form1.cs#ldvsample1formload)]
     [!code-vb[DP DataViewWinForms Sample#LDVSample1FormLoad](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/VB/Form1.vb#ldvsample1formload)]  
  
## <a name="see-also"></a>Consulte também

- [Associação e LINQ to DataSet de dados](data-binding-and-linq-to-dataset.md)
