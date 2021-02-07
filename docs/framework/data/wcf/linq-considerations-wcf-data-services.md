---
description: 'Saiba mais sobre: considerações sobre LINQ (WCF Data Services)'
title: Considerações sobre o LINQ (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, LINQ
- querying the data service [WCF Data Services]
- WCF Data Services, querying
ms.assetid: cc4ec9e9-348f-42a6-a78e-1cd40e370656
ms.openlocfilehash: 4205fc5c67c5939377e2a964d5a82d8855b03fce
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99764958"
---
# <a name="linq-considerations-wcf-data-services"></a>Considerações sobre o LINQ (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Este tópico fornece informações sobre a maneira como as consultas LINQ são compostas e executadas quando você está usando o cliente WCF Data Services e as limitações de usar o LINQ para consultar um serviço de dados que implementa o Protocolo Open Data (OData). Para obter mais informações sobre como compor e executar consultas em um serviço de dados baseado em OData, consulte [consultando o serviço de dados](querying-the-data-service-wcf-data-services.md).  
  
## <a name="composing-linq-queries"></a>Compondo consultas LINQ  

 O LINQ permite compor consultas em uma coleção de objetos que implementam o <xref:System.Collections.Generic.IEnumerable%601>. A caixa de diálogo **Adicionar referência de serviço** no Visual Studio e a ferramenta de DataSvcUtil.exe são usadas para gerar uma representação de um serviço OData como uma classe de contêiner de entidade que herda de <xref:System.Data.Services.Client.DataServiceContext> , bem como objetos que representam as entidades retornadas em feeds. Essas ferramentas também geram propriedades na classe do contêiner de entidade para as coleções expostas como feeds pelo serviço. Cada uma dessas propriedades da classe que encapsula o retorno do serviço de dados retorna um <xref:System.Data.Services.Client.DataServiceQuery%601>. Como a classe <xref:System.Data.Services.Client.DataServiceQuery%601> implementa a interface do <xref:System.Linq.IQueryable%601> definida pelo LINQ, você pode compor uma consulta LINQ com os feeds expostos pelo serviço de dados, que são traduzidos pela biblioteca de cliente em um URI de solicitação de consulta que é enviado para o serviço de dados em execução.  
  
> [!IMPORTANT]
> O conjunto de consultas que são expressas na sintaxe LINQ é mais amplo do que aquelas habilitadas na sintaxe URI usada pelo OData Data Services. Uma classe <xref:System.NotSupportedException> é gerada quando a consulta não pode ser mapeada para um URI no serviço de dados de destino. Para obter mais informações, consulte [métodos LINQ sem suporte](linq-considerations-wcf-data-services.md#unsupportedMethods) neste tópico.  
  
 O exemplo a seguir é uma consulta LINQ que retorna `Orders` que têm um custo de frete mais que US$ 30 e classifica os resultados por data de envio, começando com a data de envio mais recente:  
  
[!code-csharp[Astoria Northwind Client#AddQueryOptionsLinqSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addqueryoptionslinqspecific)]
[!code-vb[Astoria Northwind Client#AddQueryOptionsLinqSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addqueryoptionslinqspecific)]
  
 Essa consulta LINQ é convertida no seguinte URI de consulta que é executado no serviço de dados de [início rápido](quickstart-wcf-data-services.md) baseado na Northwind:  
  
```http
http://localhost:12345/Northwind.svc/Orders?Orderby=ShippedDate&?filter=Freight gt 30  
```  
  
 Para obter mais informações gerais sobre LINQ, consulte [LINQ (consulta integrada à linguagem)-C#](../../../csharp/programming-guide/concepts/linq/index.md) ou [LINQ (consulta integrada à linguagem)-Visual Basic](../../../visual-basic/programming-guide/concepts/linq/index.md).  
  
 O LINQ permite compor consultas usando tanto a sintaxe de consulta declarativa específica à linguagem, mostrada no exemplo anterior, bem como um conjunto de métodos de consulta conhecidos como operadores de consulta padrão. Uma consulta equivalente ao exemplo anterior pode ser composta usando somente a sintaxe baseada em método, conforme mostrado no exemplo a seguir:  
  
[!code-csharp[Astoria Northwind Client#AddQueryOptionsLinqExpressionSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addqueryoptionslinqexpressionspecific)]
[!code-vb[Astoria Northwind Client#AddQueryOptionsLinqExpressionSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addqueryoptionslinqexpressionspecific)]
  
 O cliente WCF Data Services é capaz de converter os dois tipos de consultas compostas em um URI de consulta, e você pode estender uma consulta LINQ acrescentando métodos de consulta a uma expressão de consulta. Quando você compõe consultas LINQ acrescentando a sintaxe de método a uma expressão de consulta ou a um <xref:System.Data.Services.Client.DataServiceQuery%601>, as operações são adicionadas ao URI de consulta na ordem em que os métodos são chamados. Isso é equivalente a chamar o método <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> para adicionar cada opção de consulta ao URI de consulta.  
  
## <a name="executing-linq-queries"></a>Executando consultas LINQ  

 Determinados métodos de consulta LINQ, como <xref:System.Linq.Enumerable.First%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29> ou <xref:System.Linq.Enumerable.Single%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29>, quando acrescentados à consulta, fazem com que a consulta seja executada. Uma consulta também é executada quando os resultados são enumerados implicitamente, como em um loop `foreach` ou quando a consulta é atribuída a uma coleção `List`. Para obter mais informações, consulte [consultando o serviço de dados](querying-the-data-service-wcf-data-services.md).  
  
 O cliente executa uma consulta LINQ em duas partes. Sempre que possível, as expressões LINQ em uma consulta são avaliadas primeiro no cliente e, em seguida, uma consulta baseada em URI é gerada e enviada ao serviço de dados para avaliação em relação aos dados no serviço. Para obter mais informações, consulte a seção [cliente versus execução do servidor](querying-the-data-service-wcf-data-services.md#executingQueries) ao [consultar o serviço de dados](querying-the-data-service-wcf-data-services.md).  
  
 Quando uma consulta LINQ não pode ser convertida em um URI de consulta compatível com OData, uma exceção é gerada quando a execução é tentada. Para obter mais informações, consulte [consultando o serviço de dados](querying-the-data-service-wcf-data-services.md).  
  
## <a name="linq-query-examples"></a>Exemplos de consulta LINQ  

 Os exemplos nas seções a seguir demonstram os tipos de consultas LINQ que podem ser executadas em um serviço OData.  
  
<a name="filtering"></a>

### <a name="filtering"></a>Filtragem  

 Os exemplos de consulta LINQ desta seção filtram os dados no feed retornado pelo serviço.  
  
 Os exemplos a seguir são consultas equivalentes que filtram as entidades `Orders` retornadas, de forma que somente pedidos com um frete maior que US$ 30 sejam retornados:  
  
- Usando a sintaxe de consulta LINQ:  
  
[!code-csharp[Astoria Northwind Client#LinqWhereClauseSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqwhereclausespecific)]
[!code-vb[Astoria Northwind Client#LinqWhereClauseSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqwhereclausespecific)]
  
- Usando métodos de consulta LINQ:  
  
[!code-csharp[Astoria Northwind Client#LinqWhereMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqwheremethodspecific)]
[!code-vb[Astoria Northwind Client#LinqWhereMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqwheremethodspecific)]
  
- A opção `$filter` de cadeia de caracteres de consulta URI:  
  
[!code-csharp[Astoria Northwind Client#ExplicitQueryWhereMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#explicitquerywheremethodspecific)]
[!code-vb[Astoria Northwind Client#ExplicitQueryWhereMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#explicitquerywheremethodspecific)]
  
 Todos os exemplos anteriores são convertidos no URI de consulta: `http://localhost:12345/northwind.svc/Orders()?$filter=Freight gt 30M`.  
  
<a name="sorting"></a>

### <a name="sorting"></a>Classificação  

 Os exemplos a seguir mostram consultas equivalentes que classificam os dados retornados pelo nome da empresa e o código postal, em ordem decrescente:  
  
- Usando a sintaxe de consulta LINQ:  
  
[!code-csharp[Astoria Northwind Client#LinqOrderByClauseSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqorderbyclausespecific)]
[!code-vb[Astoria Northwind Client#LinqOrderByClauseSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqorderbyclausespecific)]
  
- Usando métodos de consulta LINQ:  
  
[!code-csharp[Astoria Northwind Client#LinqOrderByMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqorderbymethodspecific)]
[!code-vb[Astoria Northwind Client#LinqOrderByMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqorderbymethodspecific)]
  
- Opção `$orderby` de cadeia de caracteres de consulta URI:  
  
[!code-csharp[Astoria Northwind Client#ExplicitQueryOrderByMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#explicitqueryorderbymethodspecific)]
[!code-vb[Astoria Northwind Client#ExplicitQueryOrderByMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#explicitqueryorderbymethodspecific)]
  
 Todos os exemplos anteriores são convertidos no URI de consulta: `http://localhost:12345/northwind.svc/Customers()?$orderby=CompanyName,PostalCode desc`.  
  
<a name="projection"></a>

### <a name="projection"></a>Projeção  

 Os exemplos a seguir mostram consultas equivalentes que projetam os dados no tipo `CustomerAddress` mais restrito:  
  
- Usando a sintaxe de consulta LINQ:  
  
[!code-csharp[Astoria Northwind Client#LinqSelectClauseSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqselectclausespecific)]
[!code-vb[Astoria Northwind Client#LinqSelectClauseSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqselectclausespecific)]
  
- Usando métodos de consulta LINQ:  
  
[!code-csharp[Astoria Northwind Client#LinqSelectMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqselectmethodspecific)]
[!code-vb[Astoria Northwind Client#LinqSelectMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqselectmethodspecific)]

> [!NOTE]
> A opção de consulta `$select` não pode ser adicionada a um URI de consulta usando o método <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A>. Recomendamos usar o método LINQ <xref:System.Linq.Enumerable.Select%2A> para que o cliente gere a opção de consulta `$select` no URI de solicitação.  
  
 Os dois exemplos anteriores são convertidos no URI de consulta: `"http://localhost:12345/northwind.svc/Customers()?$filter=Country eq 'GerGerm'&$select=CustomerID,Address,City,Region,PostalCode,Country"`.  
  
<a name="paging"></a>

### <a name="client-paging"></a>Paginação do cliente  

 Os exemplos a seguir mostram consultas equivalentes que solicitam uma página de entidades de pedidos classificados, que inclua 25 pedidos, ignorando os primeiros 50 pedidos:  
  
- Aplicando métodos de consulta a uma consulta LINQ:  
  
[!code-csharp[Astoria Northwind Client#LinqSkipTakeMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqskiptakemethodspecific)]
[!code-vb[Astoria Northwind Client#LinqSkipTakeMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqskiptakemethodspecific)]
  
- Opções `$skip` e `$top` da cadeia de caracteres da consulta URI:  
  
[!code-csharp[Astoria Northwind Client#ExplicitQuerySkipTakeMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#explicitqueryskiptakemethodspecific)]
[!code-vb[Astoria Northwind Client#ExplicitQuerySkipTakeMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#explicitqueryskiptakemethodspecific)]
  
 Os dois exemplos anteriores são convertidos no URI de consulta: `http://localhost:12345/northwind.svc/Orders()?$orderby=OrderDate desc&$skip=50&$top=25`.  
  
<a name="expand"></a>

### <a name="expand"></a>Expanda  

 Ao consultar um serviço de dados OData, você pode solicitar que as entidades relacionadas à entidade de destino da consulta sejam incluídas no feed retornado. O método <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> é chamado no <xref:System.Data.Services.Client.DataServiceQuery%601> do conjunto de entidades definido pela consulta LINQ, com o nome do conjunto de entidades relacionadas fornecido como o parâmetro `path`. Para obter mais informações, consulte [carregando conteúdo adiado](loading-deferred-content-wcf-data-services.md).  
  
 Os exemplos a seguir mostram maneiras equivalentes de usar o método <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> em uma consulta:  
  
- Na sintaxe de consulta LINQ:  
  
[!code-csharp[Astoria Northwind Client#LinqQueryExpandSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqqueryexpandspecific)]
[!code-vb[Astoria Northwind Client#LinqQueryExpandSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqqueryexpandspecific)]  
  
- Com métodos de consulta LINQ:  

[!code-csharp[Astoria Northwind Client#LinqQueryExpandMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqqueryexpandmethodspecific)]
[!code-vb[Astoria Northwind Client#LinqQueryExpandMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqqueryexpandmethodspecific)]

 Os dois exemplos anteriores são convertidos no URI de consulta: `http://localhost:12345/northwind.svc/Orders()?$filter=CustomerID eq 'ALFKI'&$expand=Order_Details`.  
  
<a name="unsupportedMethods"></a>

## <a name="unsupported-linq-methods"></a>Métodos LINQ sem suporte  

 A tabela a seguir contém as classes de métodos LINQ sem suporte e não pode ser incluída em uma consulta executada em um serviço OData:  
  
|Tipo de operação|Método sem suporte|  
|--------------------|------------------------|  
|Operador de conjunto|Todos os operadores de conjunto não são suportados em um <xref:System.Data.Services.Client.DataServiceQuery%601>, que incluem os seguintes:<br /><br /> -   <xref:System.Linq.Enumerable.All%2A><br />-   <xref:System.Linq.Enumerable.Any%2A><br />-   <xref:System.Linq.Enumerable.Concat%2A><br />-   <xref:System.Linq.Enumerable.DefaultIfEmpty%2A><br />-   <xref:System.Linq.Enumerable.Distinct%2A><br />-   <xref:System.Linq.Enumerable.Except%2A><br />-   <xref:System.Linq.Enumerable.Intersect%2A><br />-   <xref:System.Linq.Enumerable.Union%2A><br />-   <xref:System.Linq.Enumerable.Zip%2A>|  
|Operadores de ordenação|Os seguintes operadores de ordenação que exigem o <xref:System.Collections.Generic.IComparer%601> não são suportados no <xref:System.Data.Services.Client.DataServiceQuery%601>:<br /><br /> -   <xref:System.Linq.Enumerable.OrderBy%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29><br />-   <xref:System.Linq.Enumerable.OrderByDescending%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29><br />-   <xref:System.Linq.Enumerable.ThenBy%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29><br />-   <xref:System.Linq.Enumerable.ThenByDescending%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29>|  
|Operadores de operação e de filtragem|Os seguintes operadores de projeção e de filtragem que aceitam um argumento posicional não são suportados em um <xref:System.Data.Services.Client.DataServiceQuery%601>:<br /><br /> -   <xref:System.Linq.Enumerable.Join%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%603%7D%2CSystem.Collections.Generic.IEqualityComparer%7B%60%602%7D%29><br />-   <xref:System.Linq.Enumerable.Select%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2C%60%601%7D%29><br />-   <xref:System.Linq.Enumerable.SelectMany%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%29><br />-   <xref:System.Linq.Enumerable.SelectMany%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%29><br />-   <xref:System.Linq.Enumerable.SelectMany%60%603%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%602%7D%29><br />-   <xref:System.Linq.Enumerable.SelectMany%60%603%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%602%7D%29><br />-   <xref:System.Linq.Enumerable.Where%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2CSystem.Boolean%7D%29>|  
|Operadores de agrupamento|Todos os operadores de agrupamento não são suportados em um <xref:System.Data.Services.Client.DataServiceQuery%601>, incluindo os seguintes:<br /><br /> -   <xref:System.Linq.Enumerable.GroupBy%2A><br />-   <xref:System.Linq.Enumerable.GroupJoin%2A><br /><br /> As operações de agrupamento devem ser executadas no cliente.|  
|Operadores de agregação|Todos os operadores de agregação não são suportados em um <xref:System.Data.Services.Client.DataServiceQuery%601>, incluindo os seguintes:<br /><br /> -   <xref:System.Linq.Enumerable.Aggregate%2A><br />-   <xref:System.Linq.Enumerable.Average%2A><br />-   <xref:System.Linq.Enumerable.Count%2A><br />-   <xref:System.Linq.Enumerable.LongCount%2A><br />-   <xref:System.Linq.Enumerable.Max%2A><br />-   <xref:System.Linq.Enumerable.Min%2A><br />-   <xref:System.Linq.Enumerable.Sum%2A><br /><br /> As operações de agregação devem ser executadas no cliente ou ser encapsuladas por uma operação de serviço.|  
|Operadores de paginação|Os seguintes operadores de paginação não são suportados em um <xref:System.Data.Services.Client.DataServiceQuery%601>:<br /><br /> -   <xref:System.Linq.Enumerable.ElementAt%2A><br />-   <xref:System.Linq.Enumerable.Last%2A><br />-   <xref:System.Linq.Enumerable.LastOrDefault%2A><br />-   <xref:System.Linq.Enumerable.SkipWhile%2A><br />-   <xref:System.Linq.Enumerable.TakeWhile%2A><br/><br/>**Observação:**  Os operadores de paginação executados em uma sequência vazia retornam NULL.|  
|Outros operadores|Os operadores a seguir também não têm suporte em um <xref:System.Data.Services.Client.DataServiceQuery%601> :<br /><br /> - <xref:System.Linq.Enumerable.Empty%2A><br />- <xref:System.Linq.Enumerable.Range%2A><br />- <xref:System.Linq.Enumerable.Repeat%2A><br />- <xref:System.Linq.Enumerable.ToDictionary%2A><br />- <xref:System.Linq.Enumerable.ToLookup%2A>|  
  
<a name="supportedExpressions"></a>

## <a name="supported-expression-functions"></a>Funções de expressão suportadas  

 Há suporte para os seguintes métodos e propriedades do CLR (Common Language Runtime) porque eles podem ser convertidos em uma expressão de consulta para inclusão no URI de solicitação para um serviço OData:  
  
|Membro <xref:System.String>|Função OData com suporte|  
|-----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.String.Concat%28System.String%2CSystem.String%29>|`string concat(string p0, string p1)`|  
|<xref:System.String.Contains%28System.String%29>|`bool substringof(string p0, string p1)`|  
|<xref:System.String.EndsWith%28System.String%29>|`bool endswith(string p0, string p1)`|  
|<xref:System.String.IndexOf%28System.String%2CSystem.Int32%29>|`int indexof(string p0, string p1)`|  
|<xref:System.String.Length>|`int length(string p0)`|  
|<xref:System.String.Replace%28System.String%2CSystem.String%29>|`string replace(string p0, string find, string replace)`|  
|<xref:System.String.Substring%28System.Int32%29>|`string substring(string p0, int pos)`|  
|<xref:System.String.Substring%28System.Int32%2CSystem.Int32%29>|`string substring(string p0, int pos, int length)`|  
|<xref:System.String.ToLower>|`string tolower(string p0)`|  
|<xref:System.String.ToUpper>|`string toupper(string p0)`|  
|<xref:System.String.Trim>|`string trim(string p0)`|  
  
|<xref:System.DateTime> Membro<sup>1</sup>|Função OData com suporte|  
|-------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.DateTime.Day>|`int day(DateTime p0)`|  
|<xref:System.DateTime.Hour>|`int hour(DateTime p0)`|  
|<xref:System.DateTime.Minute>|`int minute(DateTime p0)`|  
|<xref:System.DateTime.Month>|`int month(DateTime p0)`|  
|<xref:System.DateTime.Second>|`int second(DateTime p0)`|  
|<xref:System.DateTime.Year>|`int year(DateTime p0)`|  
  
 <sup>1</sup> Também há suporte para as propriedades de data e hora equivalentes do <xref:Microsoft.VisualBasic.DateAndTime?displayProperty=nameWithType> e do <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A> método em Visual Basic.  
  
|Membro <xref:System.Math>|Função OData com suporte|  
|---------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.Math.Ceiling%28System.Decimal%29>|`decimal ceiling(decimal p0)`|  
|<xref:System.Math.Ceiling%28System.Double%29>|`double ceiling(double p0)`|  
|<xref:System.Math.Floor%28System.Decimal%29>|`decimal floor(decimal p0)`|  
|<xref:System.Math.Floor%28System.Double%29>|`double floor(double p0)`|  
|<xref:System.Math.Round%28System.Decimal%29>|`decimal round(decimal p0)`|  
|<xref:System.Math.Round%28System.Double%29>|`double round(double p0)`|  
  
|Membro <xref:System.Linq.Expressions.Expression>|Função OData com suporte|  
|---------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.Linq.Expressions.Expression.TypeIs%28System.Linq.Expressions.Expression%2CSystem.Type%29>|`bool isof(type p0)`|  
  
 O cliente também pode avaliar funções de CLR adicionais no cliente. Um <xref:System.NotSupportedException> é gerado para qualquer expressão que não possa ser avaliada no cliente e não possa ser convertida em um URI de solicitação válido para avaliação no servidor.  
  
## <a name="see-also"></a>Consulte também

- [Consultar o serviço de dados](querying-the-data-service-wcf-data-services.md)
- [Projeções de consulta](query-projections-wcf-data-services.md)
- [Materialização de objetos](object-materialization-wcf-data-services.md)
- [OData: convenções de URI](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/)
