---
title: Implementando leituras/consultas em um microsserviço CQRS
description: Arquitetura de Microsserviços do .NET para aplicativos .NET em contêineres | Entenda a implementação do lado de consultas do CQRS no microsserviço de ordenação no eShopOnContainers usando o Dapper.
ms.date: 01/13/2021
ms.openlocfilehash: 047fc3893dcaf72a17d29f5560c928879757d024
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188914"
---
# <a name="implement-readsqueries-in-a-cqrs-microservice"></a>Implementando leituras/consultas em um microsserviço CQRS

Para leituras/consultas, o microsserviço de ordenação do aplicativo de referência eShopOnContainers implementa as consultas independentemente do modelo DDD e da área transacional. Essa implementação foi feita principalmente porque as demandas de consultas e de transações são drasticamente diferentes. Grava transações de execução que devem estar em conformidade com a lógica do domínio. Consultas, por outro lado, são idempotentes e podem ser separadas das regras de domínio.

A abordagem é simples, conforme mostra a Figura 7-3. A interface de API é implementada pelos controladores de API da Web usando qualquer infraestrutura, como um micro ORM (Mapeador Relacional de Objeto) como Dapper e retornando ViewModels dinâmicos dependendo das necessidades dos aplicativos de interface do usuário.

![Diagrama mostrando consultas de alto nível no CQRS simplificado.](./media/cqrs-microservice-reads/simple-approach-cqrs-queries.png)

**Figura 7-3**. A abordagem mais simples para consultas em um microsserviço CQRS

A abordagem mais simples para as consultas no lado de uma abordagem de CQRS simplificada pode ser implementada consultando o banco de dados com um micro ORM como Dapper, retornando ViewModels dinâmicos. As definições de consulta consultam o banco de dados e retornam um ViewModel dinâmico criado dinamicamente para cada consulta. Uma vez que as consultas são idempotentes, elas não alteram os dados, não importa quantas vezes você execute uma consulta. Portanto, você não precisa estar restrito por nenhum padrão DDD usado no lado do transacional, como agregações e outros padrões, e é por isso que as consultas são separadas da área de trabalho transacional. Você consulta o banco de dados em busca de quais são as necessidades da interface do usuário e retorna um ViewModel dinâmico que não precisa ser definido estaticamente em qualquer lugar (nenhuma classe para ViewModels), exceto nas próprias instruções SQL.

Como essa abordagem é simples, o código necessário para o lado das consultas (como código usando um micro ORM como [Dapper](https://github.com/StackExchange/Dapper)) pode ser implementado [dentro do mesmo projeto de API da Web](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Application/Queries/OrderQueries.cs). A Figura 7-4 mostra essa abordagem. As consultas são definidas no projeto de microsserviço **Ordering.API** dentro da solução eShopOnContainers.

![Captura de tela da pasta de consultas do projeto de classificação. API.](./media/cqrs-microservice-reads/ordering-api-queries-folder.png)

**Figura 7-4**. Consultas no microsserviço de Ordenação em eShopOnContainers

## <a name="use-viewmodels-specifically-made-for-client-apps-independent-from-domain-model-constraints"></a>Usar ViewModels feitos especificamente para aplicativos cliente, independentemente de restrições do modelo de domínio

Uma vez que as consultas são executadas para obter os dados necessários para os aplicativos cliente, o tipo retornado pode ser feito especificamente para os clientes com base nos dados retornados pelas consultas. Esses modelos ou DTOs (Objetos de Transferência de Dados) são chamados de ViewModels.

Os dados retornados (ViewModel) podem ser o resultado da associação de dados de várias entidades ou tabelas no banco de dados, ou mesmo entre várias agregações definidas no modelo de domínio para a área transacional. Nesse caso, como você está criando consultas independentes do modelo de domínio, os limites e restrições de agregações são ignorados e você pode consultar qualquer tabela e coluna que você possa precisar. Essa abordagem fornece grande flexibilidade e produtividade para os desenvolvedores criarem ou atualizarem as consultas.

Os ViewModels podem ser tipos estáticos definidos em classes (como é implementado no microserviço de ordenação). Ou podem ser criados dinamicamente com base nas consultas executadas, o que é ágil para os desenvolvedores.

## <a name="use-dapper-as-a-micro-orm-to-perform-queries"></a>Usar o Dapper como um micro ORM para executar consultas

Você pode usar qualquer micro ORM, Entity Framework Core ou até mesmo ADO.NET simples para a consulta. O aplicativo de exemplo, o Dapper foi selecionado para o microsserviço de ordenação em eShopOnContainers como um bom exemplo de um micro ORM popular. Ele pode executar consultas SQL simples com ótimo desempenho, pois é uma estrutura leve. Usando o Dapper, você pode escrever uma consulta SQL que pode acessar e unir várias tabelas.

O Dapper é um projeto de software livre (original criado por Sam Saffron) e faz parte dos blocos de construção usado no [Stack Overflow](https://stackoverflow.com/). Para usar o Dapper, basta instalá-lo por meio do [pacote Dapper NuGet](https://www.nuget.org/packages/Dapper), conforme mostra a figura a seguir:

![Captura de tela do pacote Dapper na exibição de pacotes NuGet.](./media/cqrs-microservice-reads/drapper-package-nuget.png)

Você também precisa adicionar uma `using` diretiva para que seu código tenha acesso aos métodos de extensão Dapper.

Quando você usa o Dapper em seu código, usa diretamente a classe <xref:System.Data.SqlClient.SqlConnection> disponível no namespace <xref:System.Data.SqlClient>. Por meio do método QueryAsync e de outros métodos de extensão que estendem a <xref:System.Data.SqlClient.SqlConnection> classe, você pode executar consultas de uma maneira simples e de alto desempenho.

## <a name="dynamic-versus-static-viewmodels"></a>ViewModels dinâmicos versus estáticos

Ao retornar ViewModels do lado do servidor para aplicativos cliente, você pode pensar sobre esses ViewModels como DTOs (Objetos de Transferência de Dados) que podem ser diferentes para as entidades de domínio internas do seu modelo de entidade porque a os ViewModels contêm os dados da maneira como o aplicativo cliente precisa. Portanto, em muitos casos, você pode agregar dados provenientes de várias entidades de domínio e compor os ViewModels exatamente de acordo com a maneira como o aplicativo cliente precisa daqueles dados.

Esses ViewModels ou DTOs podem ser definidos explicitamente (como classes de portador de dados), como a `OrderSummary` classe mostrada em um trecho de código posterior. Ou, você poderia simplesmente retornar ViewModels dinâmicos ou DTOs dinâmicos com base nos atributos retornados por suas consultas como um tipo dinâmico.

### <a name="viewmodel-as-dynamic-type"></a>ViewModel como tipo dinâmico

Conforme mostrado no código a seguir, um `ViewModel` pode ser diretamente retornado pelas consultas retornando um tipo *dinâmico* internamente baseado nos atributos retornados por uma consulta. Isso significa que o subconjunto de atributos a serem retornados é baseado na própria consulta. Portanto, se você adicionar uma nova coluna à consulta ou junção, esses dados serão adicionados dinamicamente ao `ViewModel` retornado.

```csharp
using Dapper;
using Microsoft.Extensions.Configuration;
using System.Data.SqlClient;
using System.Threading.Tasks;
using System.Dynamic;
using System.Collections.Generic;

public class OrderQueries : IOrderQueries
{
    public async Task<IEnumerable<dynamic>> GetOrdersAsync()
    {
        using (var connection = new SqlConnection(_connectionString))
        {
            connection.Open();
            return await connection.QueryAsync<dynamic>(
                @"SELECT o.[Id] as ordernumber,
                o.[OrderDate] as [date],os.[Name] as [status],
                SUM(oi.units*oi.unitprice) as total
                FROM [ordering].[Orders] o
                LEFT JOIN[ordering].[orderitems] oi ON o.Id = oi.orderid
                LEFT JOIN[ordering].[orderstatus] os on o.OrderStatusId = os.Id
                GROUP BY o.[Id], o.[OrderDate], os.[Name]");
        }
    }
}
```

O ponto importante é que, ao usar um tipo dinâmico, a coleção de dados retornada é montada dinamicamente como o ViewModel.

**Prós:** Essa abordagem reduz a necessidade de modificar classes ViewModel estáticas sempre que você atualiza a frase SQL de uma consulta, tornando essa abordagem de design ágil durante a codificação, a simples e a rápida evolução em relação às alterações futuras.

**Contras:** no longo prazo, tipos dinâmicos podem afetar negativamente a clareza e a compatibilidade de um serviço com aplicativos cliente. Além disso, o software middleware como Swashbuckle não poderá fornecer o mesmo nível de documentação em tipos retornados ao usar tipos dinâmicos.

### <a name="viewmodel-as-predefined-dto-classes"></a>ViewModel como classes DTO predefinidas

**Prós**: ter classes ViewModel estáticas e predefinidas, como "contratos" com base em classes de DTO explícitas, é definitivamente melhor para APIs públicas, mas também para microserviços de longo prazo, mesmo se elas forem usadas apenas pelo mesmo aplicativo.

Se você quiser especificar os tipos de resposta para o Swagger, precisará usar as classes DTO explícitas como o tipo de retorno. Portanto, classes DTO predefinidas permitem que você ofereça informações mais sofisticadas do Swagger. Isso melhora a documentação da API e a compatibilidade ao consumir uma API.

**Contras:** conforme mencionado anteriormente, ao atualizar o código, serão necessárias mais algumas etapas para atualizar as classes DTO.

*Dica com base em nossa experiência*: nas consultas implementadas no microserviço de pedidos no eShopOnContainers, começamos a desenvolver usando ViewModels dinâmicos, pois era simples e ágil nos estágios de desenvolvimento antecipados. Mas, depois que o desenvolvimento foi estabilizado, optamos por refatorar as APIs e usar os DTOs estáticos ou predefinidos para os ViewModels, porque ele é mais claro para que os consumidores do microserviço saibam tipos de DTO explícitos, usados como "contratos".

No exemplo a seguir, você pode ver como a consulta está retornando dados usando uma classe DTO ViewModel explícita: a classe OrderSummary.

```csharp
using Dapper;
using Microsoft.Extensions.Configuration;
using System.Data.SqlClient;
using System.Threading.Tasks;
using System.Dynamic;
using System.Collections.Generic;

public class OrderQueries : IOrderQueries
{
  public async Task<IEnumerable<OrderSummary>> GetOrdersAsync()
    {
        using (var connection = new SqlConnection(_connectionString))
        {
            connection.Open();
            return await connection.QueryAsync<OrderSummary>(
                  @"SELECT o.[Id] as ordernumber,
                  o.[OrderDate] as [date],os.[Name] as [status],
                  SUM(oi.units*oi.unitprice) as total
                  FROM [ordering].[Orders] o
                  LEFT JOIN[ordering].[orderitems] oi ON  o.Id = oi.orderid
                  LEFT JOIN[ordering].[orderstatus] os on o.OrderStatusId = os.Id
                  GROUP BY o.[Id], o.[OrderDate], os.[Name]
                  ORDER BY o.[Id]");
        }
    }
}
```

#### <a name="describe-response-types-of-web-apis"></a>Descrever os tipos de resposta de APIs da Web

Os desenvolvedores que consomem APIs e microserviços da Web estão mais preocupados com o que é retornado — especificamente tipos de resposta e códigos de erro (se não padrão). Os tipos de resposta são tratados nos comentários de XML e nas anotações de dados.

Sem a documentação adequada na interface do usuário do Swagger, o consumidor não tem conhecimento de quais tipos estão sendo retornados ou quais códigos HTTP podem ser retornados. Esse problema é corrigido adicionando o <xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute?displayProperty=nameWithType>, portanto, o Swashbuckle pode gerar informações mais avançadas sobre o modelo e os valores de retorno de API, conforme mostra o código a seguir:

```csharp
namespace Microsoft.eShopOnContainers.Services.Ordering.API.Controllers
{
    [Route("api/v1/[controller]")]
    [Authorize]
    public class OrdersController : Controller
    {
        //Additional code...
        [Route("")]
        [HttpGet]
        [ProducesResponseType(typeof(IEnumerable<OrderSummary>),
            (int)HttpStatusCode.OK)]
        public async Task<IActionResult> GetOrders()
        {
            var userid = _identityService.GetUserIdentity();
            var orders = await _orderQueries
                .GetOrdersFromUserAsync(Guid.Parse(userid));
            return Ok(orders);
        }
    }
}
```

No entanto, o atributo `ProducesResponseType` não pode usar dinâmica como um tipo, mas requer o uso de tipos explícitos, como o `OrderSummary` ViewModel DTO, mostrado no exemplo a seguir:

```csharp
public class OrderSummary
{
    public int ordernumber { get; set; }
    public DateTime date { get; set; }
    public string status { get; set; }
    public double total { get; set; }
}
```

Essa é outra razão pela qual tipos retornados explícitos são melhores que tipos dinâmicos no longo prazo. Ao usar o `ProducesResponseType` atributo, você também pode especificar qual é o resultado esperado em relação a possíveis erros/códigos http, como 200, 400, etc.

Na imagem a seguir, você pode ver como a interface do usuário Swagger mostra as informações de ResponseType.

![Captura de tela da página da interface do usuário do Swagger para a API de ordenação.](./media/cqrs-microservice-reads/swagger-ordering-http-api.png)

**Figura 7-5**. Interface do usuário do Swagger mostrando os tipos de resposta e possíveis códigos de status HTTP de uma API da Web

A imagem mostra alguns valores de exemplo com base nos tipos ViewModel e os possíveis códigos de status HTTP que podem ser retornados.

## <a name="additional-resources"></a>Recursos adicionais

- **Dapper**  
 <https://github.com/StackExchange/dapper-dot-net>

- **Julie Lerman. Pontos de dados – Dapper, Entity Framework e aplicativos híbridos (artigo da MSDN Magazine)**  
  <https://docs.microsoft.com/archive/msdn-magazine/2016/may/data-points-dapper-entity-framework-and-hybrid-apps>

- **ASP.NET Core páginas de ajuda da API Web usando o Swagger**  
  <https://docs.microsoft.com/aspnet/core/tutorials/web-api-help-pages-using-swagger?tabs=visual-studio>

>[!div class="step-by-step"]
>[Anterior](eshoponcontainers-cqrs-ddd-microservice.md) 
> [Avançar](ddd-oriented-microservice.md)
