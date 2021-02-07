---
description: 'Saiba mais sobre: como criar um serviço de dados usando uma fonte de dados do ADO.NET Entity Framework (WCF Data Services)'
title: Como criar um serviço de dados usando uma fonte de dados do ADO.NET Entity Framework (WCF Data Services)
ms.date: 08/24/2018
helpviewer_keywords:
- WCF Data Services, providers
- WCF Data Services, Entity Framework
ms.assetid: 6d11fec8-0108-42f5-8719-2a7866d04428
ms.openlocfilehash: aea96c3953ec990b5f70a9702961512332330c6e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766189"
---
# <a name="how-to-create-a-data-service-using-an-adonet-entity-framework-data-source-wcf-data-services"></a>Como criar um serviço de dados usando uma fonte de dados do ADO.NET Entity Framework (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

O WCF Data Services expõe os dados da entidade como um serviço de dados. Esses dados de entidade são fornecidos pelo ADO. NETEntity Framework quando a fonte de dados é um banco de dado relacional. Este tópico mostra como criar um modelo de dados baseado em Entity Framework em um aplicativo Web do Visual Studio com base em um banco de dados existente e usar esse modelo para criar um novo serviço de dados.

O Entity Framework também fornece uma ferramenta de linha de comando que pode gerar um modelo de Entity Framework fora de um projeto do Visual Studio. Para obter mais informações, consulte [como: usar EdmGen.exe para gerar o modelo e os arquivos de mapeamento](../adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md).

## <a name="to-add-an-entity-framework-model-that-is-based-on-an-existing-database-to-an-existing-web-application"></a>Para adicionar um modelo do Entity Framework que está baseado em um banco de dados existente para um aplicativo da Web existente

1. No menu **projeto** , clique em **Adicionar**  >  **novo item**.

2. No painel **modelos** , clique na categoria **dados** e selecione **ADO.NET modelo de dados de entidade**.

3. Insira o nome do modelo e clique em **Adicionar**.

     A primeira página do assistente de Modelo de Dados de Entidade é exibida.

4. Na caixa de diálogo **escolher conteúdo do modelo** , selecione **gerar do banco de dados**. Em seguida, clique em **Próximo**.

5. Clique no botão **nova conexão** .

6. Na caixa de diálogo **Propriedades da conexão** , digite o nome do servidor, selecione o método de autenticação, digite o nome do banco de dados e clique em **OK**.

     A caixa de diálogo **escolher sua conexão de dados** é atualizada com as configurações de conexão do banco de dado.

7. Verifique se a caixa de seleção **salvar configurações de conexão de entidade no App.Config como:** está marcada. Em seguida, clique em **Próximo**.

8. Na caixa de diálogo **escolher seu objeto de banco** de dados, selecione todos os objetos de banco de dados que você planeja expor no Data Service.

    > [!NOTE]
    > Os objetos incluídos no modelo de dados não são expostos automaticamente pelo serviço de dados. Eles devem ser explicitamente expostos pelo próprio serviço. Para obter mais informações, consulte [Configurando o serviço de dados](configuring-the-data-service-wcf-data-services.md).

9. Clique em **Concluir** para finalizar o assistente.

     Isso cria um modelo de dados padrão com base no banco de dados específico. O Entity Framework permite personalizar o modelo de dados. Para obter mais informações, consulte [tarefas de ferramentas de modelo de dados de entidade](/previous-versions/dotnet/netframework-4.0/bb738480(v=vs.100)).

## <a name="to-create-the-data-service-by-using-the-new-data-model"></a>Para criar o serviço de dados usando o novo modelo de dados

1. No Visual Studio, abra o arquivo. edmx que representa o modelo de dados.

2. No **navegador de modelos**, clique com o botão direito do mouse no modelo, clique em **Propriedades** e observe o nome do contêiner de entidade.

3. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nome do seu projeto ASP.net e clique em **Adicionar**  >  **novo item**.

4. Na caixa de diálogo **Adicionar novo item** , selecione o modelo do **WCF Data Service** na categoria **Web** .

   ![Modelo de item do WCF Data Service no Visual Studio 2015](./media/wcf-data-service-item-template.png)

   > [!NOTE]
   > O modelo do **WCF Data Service** está disponível no visual Studio 2015, mas não no visual Studio 2017 ou posterior.

5. Forneça um nome para o serviço e clique em **OK**.

     O Visual Studio cria a marcação XML e os arquivos de código do novo serviço. Por padrão, a janela do editor de códigos é aberta.

6. No código para o serviço de dados, substitua o comentário `/* TODO: put your data source class name here */` na definição de classe que define o serviço de dados com o tipo que herda da classe <xref:System.Data.Objects.ObjectContext> e que é o contêiner de entidade do modelo de dados, que foi observado na etapa 2.

7. No código para o serviço de dados, permita que os clientes autorizados acessem os conjuntos de entidades que o serviço de dados expõe. Para obter mais informações, consulte [criando o serviço de dados](creating-the-data-service.md).

8. Para testar o serviço de dados Northwind. svc usando um navegador da Web, siga as instruções no tópico [acessando o serviço em um navegador da Web](accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md).

## <a name="see-also"></a>Consulte também

- [Configurando WCF Data Services](defining-wcf-data-services.md)
- [Provedores de serviços de dados](data-services-providers-wcf-data-services.md)
- [Como: criar um serviço de dados usando o provedor de reflexão](create-a-data-service-using-rp-wcf-data-services.md)
- [Como: criar um serviço de dados usando uma fonte de dados LINQ to SQL](create-a-data-service-using-linq-to-sql-wcf.md)
