---
description: 'Saiba mais sobre: como criar um serviço de dados usando uma fonte de dados de LINQ to SQL (WCF Data Services)'
title: 'Como: criar um serviço de dados usando uma fonte de dados LINQ to SQL (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, LINQ to SQL
- WCF Data Services, providers
ms.assetid: 3b01c2fd-8c6e-4bf5-b38f-9e61bdc3c328
ms.openlocfilehash: 18c59cc8a067372f2a5c5b4b25d9aec77515ad98
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766230"
---
# <a name="how-to-create-a-data-service-using-a-linq-to-sql-data-source-wcf-data-services"></a>Como: criar um serviço de dados usando uma fonte de dados LINQ to SQL (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

O WCF Data Services expõe os dados da entidade como um serviço de dados. O provedor de reflexão permite que você defina um modelo de dados baseado em qualquer classe que expõe Membros que retornam uma <xref:System.Linq.IQueryable%601> implementação. Para poder fazer atualizações nos dados na fonte de dados, essas classes também devem implementar a <xref:System.Data.Services.IUpdatable> interface. Para obter mais informações, consulte [provedores de serviços de dados](data-services-providers-wcf-data-services.md). Este tópico mostra como criar LINQ to SQL classes que acessam o banco de dados de exemplo Northwind usando o provedor de reflexão, além de como criar o serviço de dado baseado nessas classes de dados.

## <a name="to-add-linq-to-sql-classes-to-a-project"></a>Para adicionar LINQ to SQL classes a um projeto

1. De dentro de um aplicativo Visual Basic ou C#, no menu **projeto** , clique em **Adicionar**  >  **novo item**.

2. Clique no modelo **classes de LINQ to SQL** .

3. Altere o nome para **Northwind. dbml**.

4. Clique em **Adicionar**.

     O arquivo Northwind. dbml é adicionado ao projeto e o Object Relational Designer (O/R Designer) é aberto.

5. Em  / **Gerenciador de banco de dados** do servidor, em Northwind, expanda **tabelas** e arraste a `Customers` tabela para a Object Relational Designer (o/R Designer).

     Uma `Customer` classe de entidade é criada e aparece na superfície de design.

6. Repita a etapa 6 para `Orders` as `Order_Details` tabelas, e `Products` .

7. Clique com o botão direito do mouse no novo arquivo. dbml que representa as classes de LINQ to SQL e clique em **Exibir código**.

     Isso cria uma nova página code-behind chamada Northwind.cs que contém uma definição de classe parcial para a classe que herda da <xref:System.Data.Linq.DataContext> classe, que nesse caso é `NorthwindDataContext` .

8. Substitua o conteúdo do arquivo de código Northwind.cs pelo código a seguir. Esse código implementa o provedor de reflexão estendendo as <xref:System.Data.Linq.DataContext> classes de dados e geradas por LINQ to SQL:

     [!code-csharp[Astoria Linq Provider#Linq2SqlProvider](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_linq_provider/cs/northwind.cs#linq2sqlprovider)]
     [!code-vb[Astoria Linq Provider#Linq2SqlProvider](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_linq_provider/vb/northwind.vb#linq2sqlprovider)]

### <a name="to-create-a-data-service-by-using-a-linq-to-sql-based-data-model"></a>Para criar um serviço de dados usando um modelo de dados baseado em LINQ to SQL

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nome do seu projeto ASP.net e clique em **Adicionar**  >  **novo item**.

2. Na caixa de diálogo **Adicionar novo item** , selecione o modelo do **WCF Data Service** na categoria **Web** .

   ![Modelo de item do WCF Data Service no Visual Studio 2015](./media/wcf-data-service-item-template.png)

   > [!NOTE]
   > O modelo do **WCF Data Service** está disponível no visual Studio 2015, mas não no visual Studio 2017 ou posterior.

3. Forneça um nome para o serviço e clique em **OK**.

     O Visual Studio cria a marcação XML e os arquivos de código do novo serviço. Por padrão, a janela do editor de códigos é aberta.

4. No código do serviço de dados, substitua o comentário `/* TODO: put your data source class name here */` na definição da classe que define o serviço de dados pelo tipo que é o contêiner de entidade do modelo de dados, que, neste caso, é `NorthwindDataContext`.

5. No código para o serviço de dados, substitua o código de espaço reservado na função `InitializeService` pelo seguinte:

     [!code-csharp[Astoria Linq Provider#EnableAccess](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_linq_provider/cs/northwind.svc.cs#enableaccess)]
     [!code-vb[Astoria Linq Provider#EnableAccess](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_linq_provider/vb/northwind.svc.vb#enableaccess)]

     Isso permite que clientes autorizados acessem recursos para os três conjuntos de entidades especificados.

6. Para testar o serviço de dados Northwind. svc usando um navegador da Web, siga as instruções no tópico [acessando o serviço em um navegador da Web](accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md).

## <a name="see-also"></a>Consulte também

- [Como: criar um serviço de dados usando uma fonte de dados do ADO.NET Entity Framework](create-a-data-service-using-an-adonet-ef-data-wcf.md)
- [Como: criar um serviço de dados usando o provedor de reflexão](create-a-data-service-using-rp-wcf-data-services.md)
- [Provedores de serviços de dados](data-services-providers-wcf-data-services.md)
