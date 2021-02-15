---
description: 'Saiba mais sobre: considerações sobre a migração (Entity Framework)'
title: Considerações sobre migração (Entity Framework)
ms.date: 03/30/2017
ms.assetid: c85b6fe8-cc32-4642-8f0a-dc0e5a695936
ms.openlocfilehash: 6824d28fecc743e17046c826b887900218c90f3c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739242"
---
# <a name="migration-considerations-entity-framework"></a>Considerações sobre migração (Entity Framework)

O Entity Framework ADO.NET fornece vários benefícios para um aplicativo existente. Um dos mais importantes desses benefícios é a capacidade de usar um modelo conceitual para separar as estruturas de dados usadas pelo aplicativo no esquema da fonte de dados. Isso permite que você faça alterações futuras facilmente no modelo de armazenamento ou na própria fonte de dados sem fazer alterações de compensação no aplicativo. Para obter mais informações sobre os benefícios de usar o Entity Framework, consulte [Entity Framework visão geral](overview.md) e [modelo de dados de entidade](../entity-data-model.md).  
  
 Para aproveitar os benefícios do Entity Framework, você pode migrar um aplicativo existente para o Entity Framework. Algumas tarefas são comuns a todos os aplicativos migrados. Essas tarefas comuns incluem atualizar o aplicativo para usar o .NET Framework a partir da versão 3,5 do SP1 (Service Pack 1), definindo modelos e mapeamento e Configurando o Entity Framework. Quando você migra um aplicativo para o Entity Framework, há considerações adicionais que se aplicam. Essas considerações dependem do tipo do aplicativo que está sendo migrado e da funcionalidade específica do aplicativo. Este tópico fornece informações para ajudá-lo a escolher a melhor abordagem a ser utilizada ao atualizar um aplicativo existente.  
  
## <a name="general-migration-considerations"></a>Considerações gerais sobre migração  

 As seguintes considerações se aplicam ao migrar qualquer aplicativo para o Entity Framework:  
  
- Qualquer aplicativo que usa o .NET Framework a partir da versão 3,5 SP1 pode ser migrado para o Entity Framework, desde que o provedor de dados para a fonte de dados usada pelo aplicativo ofereça suporte ao Entity Framework.  
  
- O Entity Framework não dá suporte a toda a funcionalidade de um provedor de fonte de dados, mesmo que o provedor dê suporte ao Entity Framework.  
  
- Para um aplicativo grande ou complexo, não é necessário migrar todo o aplicativo para o Entity Framework de uma vez. No entanto, qualquer parte do aplicativo que não use o Entity Framework ainda deve ser alterada quando a fonte de dados for alterada.  
  
- A conexão do provedor de dados usada pelo Entity Framework pode ser compartilhada com outras partes do seu aplicativo porque o Entity Framework usa provedores de dados ADO.NET para acessar a fonte de dados. Por exemplo, o provedor SqlClient é usado pelo Entity Framework para acessar um banco de dados SQL Server. Para obter mais informações, consulte [EntityClient Provider para o Entity Framework](entityclient-provider-for-the-entity-framework.md).  
  
## <a name="common-migration-tasks"></a>Tarefas de migração comuns  

 O caminho para migrar um aplicativo existente para a Entity Framework depende do tipo de aplicativo e da estratégia de acesso a dados existente. No entanto, você deve sempre executar as seguintes tarefas ao migrar um aplicativo existente para o Entity Framework.  
  
> [!NOTE]
> Todas essas tarefas são executadas automaticamente quando você usa as ferramentas de Modelo de Dados de Entidade a partir do Visual Studio 2008. Para obter mais informações, consulte [como: usar o assistente de modelo de dados de entidade](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100)).  
  
1. Atualizar o aplicativo.  
  
     Um projeto criado usando uma versão anterior do Visual Studio e o .NET Framework deve ser atualizado para usar o Visual Studio 2008 SP1 e o .NET Framework a partir da versão 3,5 SP1.  
  
2. Definir os modelos e o mapeamento.  
  
     O modelo e os arquivos de mapeamento definem entidades no modelo conceitual; estruturas na fonte de dados, como tabelas, procedimentos armazenados e modos de exibição; e o mapeamento entre as entidades e estruturas da fonte de dados. Para obter mais informações, consulte [como definir manualmente o modelo e os arquivos de mapeamento](/previous-versions/dotnet/netframework-4.0/bb399785(v=vs.100)).  
  
     Os tipos definidos no modelo de armazenamento devem corresponder ao nome dos objetos na fonte de dados. Se o aplicativo existente expuser dados como objetos, você deverá garantir que as entidades e as propriedades definidas no modelo conceitual correspondam aos nomes dessas classes e propriedades de dados existentes. Para obter mais informações, consulte [como: personalizar a modelagem e o mapeamento de arquivos para trabalhar com objetos personalizados](/previous-versions/dotnet/netframework-4.0/bb738625(v=vs.100)).  
  
    > [!NOTE]
    > O Designer de Modelo de Dados de Entidade pode ser usado para renomear entidades no modelo conceitual para que correspondam aos objetos existentes. Para obter mais informações, consulte [modelo de dados de entidade designer](/previous-versions/dotnet/netframework-4.0/cc716685(v=vs.100)).  
  
3. Definir a cadeia de conexão.  
  
     O Entity Framework usa uma cadeia de conexão especialmente formatada ao executar consultas em um modelo conceitual. Essa cadeia de conexão encapsula informações sobre o modelo e arquivos de mapeamento e a conexão com a fonte de dados. Para obter mais informações, consulte [como: definir a cadeia de conexão](how-to-define-the-connection-string.md).  
  
4. Configure o projeto do Visual Studio.  
  
     As referências a Entity Framework assemblies e ao modelo e aos arquivos de mapeamento devem ser adicionadas ao projeto do Visual Studio. Você pode adicionar esses arquivos de mapeamento ao projeto para garantir que sejam implantados com o aplicativo no local indicado na cadeia de conexão. Para obter mais informações, consulte [como: configurar manualmente um projeto de Entity Framework](/previous-versions/dotnet/netframework-4.0/bb738546(v=vs.100)).  
  
## <a name="considerations-for-applications-with-existing-objects"></a>Considerações para aplicativos com objetos existentes  

 A partir do .NET Framework 4, o Entity Framework dá suporte a objetos CLR "Plain Old" (POCO), também chamados de objetos Persistence-que desconhecem. Na maioria dos casos, os objetos existentes podem trabalhar com o Entity Framework fazendo pequenas alterações. Para obter mais informações, consulte [trabalhando com entidades POCO](/previous-versions/dotnet/netframework-4.0/dd456853(v=vs.100)). Você também pode migrar um aplicativo para o Entity Framework e usar as classes de dados que são geradas pelas ferramentas de Entity Framework. Para obter mais informações, consulte [como: usar o assistente de modelo de dados de entidade](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100)).  
  
## <a name="considerations-for-applications-that-use-adonet-providers"></a>Considerações para aplicativos que usam provedores ADO.NET  

 Os provedores de ADO.NET, como o SqlClient, permitem consultar uma fonte de dados para retornar dados tabulares. Também podem ser carregados em um conjunto de dados ADO.NET. A lista a seguir descreve as considerações para atualizar um aplicativo que usa um provedor de ADO.NET existente:  
  
- Exibindo dados tabulares usando um leitor de dados.  

  Você pode considerar a execução de uma [!INCLUDE[esql](../../../../../includes/esql-md.md)] consulta usando o provedor EntityClient e a enumeração por meio do <xref:System.Data.EntityClient.EntityDataReader> objeto retornado. Faça isso somente se seu aplicativo exibir dados tabulares usando um leitor de dados e não exigir os recursos fornecidos pelo Entity Framework para materializar dados em objetos, controlar alterações e fazer atualizações. Você pode continuar a usar o código de acesso a dados existente que faz atualizações na fonte de dados, mas você pode usar a conexão existente acessada da <xref:System.Data.EntityClient.EntityConnection.StoreConnection%2A> propriedade de <xref:System.Data.EntityClient.EntityConnection> . Para obter mais informações, consulte [EntityClient Provider para o Entity Framework](entityclient-provider-for-the-entity-framework.md).  
  
- Trabalhando com DataSets.  

  O Entity Framework fornece muitas das mesmas funcionalidades fornecidas pelo conjunto de dados, incluindo a persistência na memória, controle de alterações, vinculação e serialização de objetos como dados XML. Para obter mais informações, consulte [trabalhando com objetos](working-with-objects.md).  
  
  Se o Entity Framework não fornecer a funcionalidade do conjunto de aplicativos necessário para seu aplicativo, você ainda poderá aproveitar os benefícios das consultas LINQ usando LINQ to DataSet. Para obter mais informações, consulte [LINQ to DataSet](../linq-to-dataset.md).  
  
## <a name="considerations-for-applications-that-bind-data-to-controls"></a>Considerações para aplicativos que associam dados a controles  

 O .NET Framework permite que você encapsula dados em uma fonte de dados, como um conjunto de dados ou um controle da fonte do ASP.NET, e, em seguida, associa os elementos da interface do usuário a esses controles de dados. A lista a seguir descreve as considerações para associar controles aos dados do Entity Framework.  
  
- Associando dados a controles  

  Quando você consulta o modelo conceitual, o Entity Framework retorna os dados como objetos que são instâncias de tipos de entidade. Esses objetos podem ser vinculados diretamente a controles e essa associação dá suporte a atualizações. Isso significa que as alterações nos dados em um controle, como uma linha em um <xref:System.Windows.Forms.DataGridView> , são salvas automaticamente no banco de dado quando o <xref:System.Data.Objects.ObjectContext.SaveChanges%2A> método é chamado.  
  
  Se seu aplicativo enumerar os resultados de uma consulta para exibir dados em um <xref:System.Windows.Forms.DataGridView> ou em outro tipo de controle que dê suporte a vinculação de dados, você poderá alterar seu aplicativo para associar o controle ao resultado de um <xref:System.Data.Objects.ObjectQuery%601>.  
  
  Para obter mais informações, consulte [associando objetos a controles](/previous-versions/dotnet/netframework-4.0/bb738469(v=vs.100)).  
  
- Controles de fonte de dados ASP.NET.  

  O Entity Framework inclui um controle da fonte de dados projetado para simplificar a vinculação de dados em aplicativos Web do ASP.NET. Para obter mais informações, consulte [visão geral do controle de servidor Web de EntityDataSource](/previous-versions/aspnet/cc488502(v=vs.100)).  
  
## <a name="other-considerations"></a>Outras considerações  

 A seguir estão as considerações que podem se aplicar quando você migra tipos específicos de aplicativos para o Entity Framework.  
  
- Aplicativos que expõem serviços de dados.  

  Os serviços e aplicativos Web baseados no WCF (Windows Communication Foundation) expõem dados de uma fonte de dados subjacente usando um formato de mensagem XML de solicitação/resposta. O Entity Framework dá suporte à serialização de objetos de entidade usando a serialização de contrato de dados Binary, XML ou WCF. A serialização binária e do WCF dão suporte à serialização completa de gráficos de objetos. Para obter mais informações, consulte [criando aplicativos de N camadas](/previous-versions/dotnet/netframework-4.0/bb896304(v=vs.100)).  
  
- Aplicativos que usam dados XML.  

  A serialização de objeto permite que você crie Entity Framework Data Services. Esses serviços fornecem dados a aplicativos que consomem dados XML, como aplicativos de Internet baseados em AJAX. Nesses casos, considere o uso de WCF Data Services. Esses serviços de dados são baseados no Modelo de Dados de Entidade e fornecem acesso dinâmico a dados de entidade usando ações HTTP REST (Representational State Transfer), como GET, PUT e POST. Para obter mais informações, consulte [WCF Data Services 4,5](../../wcf/index.md).  
  
  O Entity Framework não oferece suporte a um tipo de dados XML nativo. Isso significa que quando uma entidade é mapeada para uma tabela com uma coluna XML, a propriedade equivalente da entidade para a coluna XML é uma cadeia de caracteres. Os objetos podem ser desconectados e serializados como XML. Para obter mais informações, consulte [serializando objetos](/previous-versions/dotnet/netframework-4.0/bb738446(v=vs.100)).  
  
  Se seu aplicativo exigir a capacidade de consultar dados XML, você ainda poderá tirar proveito dos benefícios de consultas LINQ usando o LINQ to XML. Para obter mais informações, consulte [LINQ to XML (C#)](../../../../standard/linq/linq-xml-overview.md) ou [LINQ to XML (Visual Basic)](../../../../standard/linq/linq-xml-overview.md).  
  
- Aplicativos que mantêm o estado.  

  Os aplicativos Web ASP.NET devem manter com frequência o estado de uma página da Web ou de uma sessão de usuário. Os objetos em uma <xref:System.Data.Objects.ObjectContext> instância podem ser armazenados no estado de exibição do cliente ou no estado da sessão no servidor e, posteriormente, recuperados e anexados novamente a um novo contexto de objeto. Para obter mais informações, consulte [anexando e desanexando objetos](/previous-versions/dotnet/netframework-4.0/bb896271(v=vs.100)).  
  
## <a name="see-also"></a>Consulte também

- [Considerações sobre implantação](deployment-considerations.md)
- [Terminologia do Entity Framework](terminology.md)
