---
description: 'Saiba mais sobre: LINQ to SQL N camadas com serviços Web'
title: LINQ to SQL de n camadas com serviços da Web
ms.date: 03/30/2017
ms.assetid: 9cb10eb8-957f-4beb-a271-5f682016fed2
ms.openlocfilehash: 7c97cc80f071ae964f329265f5c3d0e68e12b84f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99663099"
---
# <a name="linq-to-sql-n-tier-with-web-services"></a>LINQ to SQL de n camadas com serviços da Web

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o é projetado especialmente para uso na camada intermediária em uma DAL (camada de acesso a dados de acoplamento flexível), como um serviço Web. Se a camada de apresentação é uma página da Web ASP.NET, então você usa o controle de servidor Web de <xref:System.Web.UI.WebControls.LinqDataSource> para gerenciar a transferência de dados entre a interface do usuário e [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] na camada intermediária. Se a camada de apresentação não é uma página ASP.NET, então a camada intermediária e a camada de apresentação devem fazer qualquer trabalho adicional para gerenciar serialização e desserialização de dados.  
  
## <a name="setting-up-linq-to-sql-on-the-middle-tier"></a>Foundation LINQ to SQL na camada intermediária  

 Em um serviço Web ou em um aplicativo de n camadas, a camada intermediária contém o contexto de dados e classes de entidade. Você pode criar essas classes manualmente ou usando SQLMetal.exe ou a Object Relational Designer conforme descrito em outro lugar na documentação. Em tempo de design, você tem a opção fazer as classes de entidade serializável. Para obter mais informações, consulte [como: tornar entidades serializáveis](how-to-make-entities-serializable.md). Outra opção é criar um conjunto separado de classes que encapsulam os dados a serem serializados e, em seguida, projetar nesses tipos serializáveis quando você retornar dados em suas consultas LINQ.  
  
 Você então define a interface com métodos que os clientes chamarão para recuperar, inserir e atualizar dados. Os métodos de interface encapsulam suas consultas LINQ. Você pode usar qualquer tipo de mecanismo de serialização para manipular chamadas remotos do método e serialização de dados. O único requisito é que se você tiver relações cíclicas ou bidirecionais no seu modelo de objeto, tal como aquela entre clientes e pedidos no modelo de objeto padrão do Northwind, então você deve usar um serializador que ofereça. O Windows Communication Foundation (WCF) <xref:System.Runtime.Serialization.DataContractSerializer> dá suporte a relações bidirecionais, mas o XmlSerializer usado com serviços Web não WCF não. Se você optar por usar o XmlSerializer, deverá verificar se o modelo de objeto não tem relações cíclicas.  
  
 Para obter mais informações sobre Windows Communication Foundation, consulte [Windows Communication Foundation Services and WCF Data Services no Visual Studio](/visualstudio/data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio).  
  
 Implemente suas regras comerciais ou outra lógica específica de domínio usando as classes e métodos parciais em <xref:System.Data.Linq.DataContext> e classes de entidade para ligar em eventos em runtime de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] . Para obter mais informações, consulte [implementando a lógica de negócios de N camadas](implementing-business-logic-linq-to-sql.md).  
  
## <a name="defining-the-serializable-types"></a>Definindo tipos Serializable  

 O cliente ou a camada de apresentação devem ter definições de tipo para as classes que será recebendo de camada intermediária. Esses tipos podem ser a entidade classificam-se, ou classes especiais que envolvem apenas determinados campos de entidade classe remoting. Em qualquer caso, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o é completamente inpreocupante sobre como a camada de apresentação adquire essas definições de tipo. Por exemplo, a camada de apresentação pode usar WCF para gerar automaticamente os tipos, ou pode ter uma cópia de uma DLL em que esses tipos são definidos, ou pode apenas definir suas próprias versões de tipos.  
  
## <a name="retrieving-and-inserting-data"></a>Recuperando e inserindo dados  

 A camada intermediária define uma interface que especifica como a camada de apresentação acessa os dados. Por exemplo, `GetProductByID(int productID)` ou `GetCustomers()`. Na camada intermediária, o corpo do método normalmente cria uma nova instância de <xref:System.Data.Linq.DataContext>, executa uma consulta em uma ou mais da tabela. A camada intermediária então retorna o resultado como <xref:System.Collections.Generic.IEnumerable%601>, onde `T` é uma classe de entidade ou outro tipo que é usado para serialização. A camada de apresentação nunca envia ou recebe variáveis de consulta diretamente ou da camada intermediária. Os dois valores de troca de camadas, objetos, e coleções de dados concretos. Depois de receber uma coleção, a camada de apresentação pode usar LINQ to Objects para consultá-la, se necessário.  
  
 Para inserir dados, a camada de apresentação pode criar um novo objeto e enviá-lo para a camada intermediária, ou pode fazer com que a camada intermediária criar o objeto com base nos valores que fornece. Em geral, recuperar e inserir dados em aplicativos n-tier não difere do processo muito 2 em aplicativos de camada. Para obter mais informações, consulte [consultando o banco de](querying-the-database.md) [dados e fazendo e enviando as alterações de dado](making-and-submitting-data-changes.md).  
  
## <a name="tracking-changes-for-updates-and-deletes"></a>Controlar alterações para atualizações e exclusões  

 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] suporta concorrência otimista com base nos carimbos de data/hora (também chamados RowVersions) e valores originais. Se as tabelas de base de dados têm carimbos de data/hora, então atualizações e exclusões exigem vez trabalho adicional na camada intermediária na camada de apresentação. Entretanto, se você deve usar valores originais para verificação de simultaneidade otimista, então a camada de apresentação é responsável para controlar os valores e enviá-los novamente quando fazer atualizações. Isso ocorre porque as alterações que foram feitas às entidades na camada de apresentação não são controladas na camada intermediária. De fato, a recuperação original de uma entidade, e a atualização feita a eventual ele normalmente são executadas por duas instâncias separadas de <xref:System.Data.Linq.DataContext>completamente.  
  
 Maior o número de alterações que a camada de apresentação isso, ele fica mais complexa para controlar as alterações e para empacotar-las de volta para a camada intermediária. A implementação de um mecanismo para alterações de comunicação é completamente até o aplicativo. O único requisito é que [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] deve ser fornecido os valores originais que são necessários para verificação de simultaneidade otimista.  
  
 Para obter mais informações, consulte [operações de recuperação de dados e cud em aplicativos de N camadas (LINQ to SQL)](data-retrieval-and-cud-operations-in-n-tier-applications.md).  
  
## <a name="see-also"></a>Consulte também

- [Aplicativos de n camadas e remoto com LINQ to SQL](n-tier-and-remote-applications-with-linq-to-sql.md)
- [Visão geral do controle de servidor Web LinqDataSource](/previous-versions/aspnet/bb547113(v=vs.100))
