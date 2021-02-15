---
title: Migrar um serviço de solicitação-resposta do WCF para gRPC-gRPC para desenvolvedores do WCF
description: Saiba como migrar um serviço de solicitação-resposta simples do WCF para o gRPC.
ms.date: 12/15/2020
ms.openlocfilehash: 38c6e33e7588dd7c1b263d813d06c088ab484948
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938566"
---
# <a name="migrate-a-wcf-request-reply-service-to-a-grpc-unary-rpc"></a>Migrar um serviço de solicitação-resposta WCF para um RPC unário gRPC

Esta seção aborda como migrar um serviço de solicitação-resposta básico no WCF para um serviço RPC unário no ASP.NET Core gRPC. Esses serviços são os tipos de serviço mais simples no Windows Communication Foundation (WCF) e no gRPC, portanto, é um ótimo lugar para começar. Depois de migrar o serviço, você aprenderá a gerar uma biblioteca de cliente do mesmo `.proto` arquivo para consumir o serviço de um aplicativo cliente .net.

## <a name="the-wcf-solution"></a>A solução WCF

A [solução PortfoliosSample](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/PortfoliosSample/wcf/TraderSys) inclui um serviço de portfólio simples de solicitação-resposta para baixar um único portfólio ou todos os portfólios de um determinado Trader. O serviço é definido na interface `IPortfolioService` com um `ServiceContract` atributo:

```csharp
[ServiceContract]
public interface IPortfolioService
{
    [OperationContract]
    Task<Portfolio> Get(Guid traderId, int portfolioId);

    [OperationContract]
    Task<List<Portfolio>> GetAll(Guid traderId);
}
```

O `Portfolio` modelo é uma classe C# simples marcada com [DataContract](xref:System.Runtime.Serialization.DataContractAttribute) e incluindo uma lista de `PortfolioItem` objetos. Esses modelos são definidos no `TraderSys.PortfolioData` projeto junto com uma classe de repositório que representa uma abstração de acesso a dados.

```csharp
[DataContract]
public class Portfolio
{
    [DataMember]
    public int Id { get; set; }

    [DataMember]
    public Guid TraderId { get; set; }

    [DataMember]
    public List<PortfolioItem> Items { get; set; }
}

[DataContract]
public class PortfolioItem
{
    [DataMember]
    public int Id { get; set; }

    [DataMember]
    public int ShareId { get; set; }

    [DataMember]
    public int Holding { get; set; }

    [DataMember]
    public decimal Cost { get; set; }
}
```

A `ServiceContract` implementação usa uma classe de repositório fornecida por meio de injeção de dependência que retorna instâncias dos `DataContract` tipos:

```csharp
public class PortfolioService : IPortfolioService
{
    private readonly IPortfolioRepository _repository;

    public PortfolioService(IPortfolioRepository repository)
    {
        _repository = repository;
    }

    public async Task<Portfolio> Get(Guid traderId, int portfolioId)
    {
        return await _repository.GetAsync(traderId, portfolioId);
    }

    public async Task<List<Portfolio>> GetAll(Guid traderId)
    {
        return await _repository.GetAllAsync(traderId);
    }
}
```

## <a name="the-portfoliosproto-file"></a>O arquivo portfolios. proto

Se você seguiu as instruções na seção anterior, deve ter um projeto gRPC com um arquivo parecido com `portfolios.proto` este:

```protobuf
syntax = "proto3";

option csharp_namespace = "TraderSys.Portfolios.Protos";

package PortfolioServer;

service Portfolios {
  // RPCs will go here
}
```

A primeira etapa é migrar as `DataContract` classes para seus equivalentes Protobuf.

## <a name="convert-the-datacontract-classes-to-grpc-messages"></a>Converter as classes DataContract em mensagens gRPC

A `PortfolioItem` classe será convertida em uma mensagem Protobuf primeiro, porque a `Portfolio` classe depende dela. A classe é simples e três das propriedades são mapeadas diretamente para os tipos de dados gRPC. A `Cost` propriedade, que representa o preço pago pelos compartilhamentos na compra, é um `decimal` campo. o gRPC dá suporte apenas a `float` números reais ou a um `double` número real, que não são adequados para a moeda. Como os preços de compartilhamento variam em um mínimo de uma centésimo, o custo pode ser expresso como uma `int32` das centavos.

> [!NOTE]
> Lembre-se de usar `snake_case` para nomes de campo em seu `.proto` arquivo. O gerador de código C# irá convertê-los para o `PascalCase` para você e os usuários de outras linguagens lhe agradecerão por respeitar seus diferentes padrões de codificação.

```protobuf
message PortfolioItem {
    int32 id = 1;
    int32 share_id = 2;
    int32 holding = 3;
    int32 cost_cents = 4;
}
```

A `Portfolio` classe é um pouco mais complicada. No código WCF, o desenvolvedor usou um `Guid` para a `TraderId` propriedade e contém um `List<PortfolioItem>` . No Protobuf, que não tem um tipo de primeira classe `UUID` , você deve usar um `string` para o `traderId` campo e analisá-lo em seu próprio código. Para a lista de itens, use a `repeated` palavra-chave no campo.

```protobuf
message Portfolio {
    int32 id = 1;
    string trader_id = 2;
    repeated PortfolioItem items = 3;
}
```

Agora que você tem as mensagens de dados, você pode declarar os pontos de extremidade de RPC do serviço.

## <a name="convert-servicecontract-to-a-grpc-service"></a>Converter o ServiceContract em um serviço gRPC

O `Get` método WCF usa dois parâmetros: `Guid traderId` e `int portfolioId` . os métodos de serviço gRPC podem usar apenas um único parâmetro, portanto, você precisa criar uma mensagem para conter os dois valores. É uma prática comum nomear esses objetos de solicitação com o mesmo nome que o método seguido pelo sufixo `Request` . Novamente, `string` o está sendo usado para o `traderId` campo em vez de `Guid` .

O serviço pode simplesmente retornar uma `Portfolio` mensagem diretamente, mas novamente, isso poderia afetar a compatibilidade com versões anteriores no futuro. É uma prática recomendada definir `Request` mensagens e separadas `Response` para cada método em um serviço, mesmo se muitos deles forem os mesmos no momento. Portanto, declare uma `GetResponse` mensagem com um único `Portfolio` campo.

Este exemplo mostra a declaração do método de serviço gRPC com a `GetRequest` mensagem:

```protobuf
message GetRequest {
    string trader_id = 1;
    int32 portfolio_id = 2;
}

message GetResponse {
    Portfolio portfolio = 1;
}

service Portfolios {
    rpc Get(GetRequest) returns (GetResponse);
}
```

O `GetAll` método WCF usa apenas um único parâmetro, `traderId` , portanto, pode parecer que você pode especificar `string` como o tipo de parâmetro. Mas gRPC requer um tipo de mensagem definido. Esse requisito ajuda a impor a prática de usar mensagens personalizadas para todas as entradas e saídas, para compatibilidade com versões anteriores futuras.

O método WCF também retorna um `List<Portfolio>` , mas, pelo mesmo motivo, ele não permite tipos de parâmetro simples, gRPC não permitirá `repeated Portfolio` como um tipo de retorno. Em vez disso, crie um `GetAllResponse` tipo para encapsular a lista.

> [!WARNING]
> Você pode estar tentado a criar uma `PortfolioList` mensagem ou algo semelhante e usá-lo em vários métodos de serviço, mas deve resistir a essa tentação. É impossível saber como os vários métodos em um serviço irão evoluir, portanto, mantenha suas mensagens específicas e separadas de forma limpa.

```protobuf
message GetAllRequest {
    string trader_id = 1;
}

message PortfolioList {
    repeated Portfolio portfolios = 1;
}

service Portfolios {
    rpc Get(GetRequest) returns (Portfolio);
    rpc GetAll(GetAllRequest) returns (GetAllResponse);
}
```

Se você salvar seu projeto com essas alterações, o destino da compilação gRPC será executado em segundo plano e gerará todos os tipos de mensagem Protobuf e uma classe base que você pode herdar para implementar o serviço.

Abra a `Services/GreeterService.cs` classe e exclua o código de exemplo. Agora você pode adicionar a implementação do serviço de portfólio. A classe base gerada estará no `Protos` namespace e será gerada como uma classe aninhada. gRPC cria uma classe estática com o mesmo nome que o serviço no `.proto` arquivo e uma classe base com o sufixo `Base` dentro dessa classe estática, portanto, o identificador completo para o tipo base é `TraderSys.Portfolios.Protos.Portfolios.PortfoliosBase` .

```csharp
namespace TraderSys.Portfolios.Services
{
    public class PortfolioService : Protos.Portfolios.PortfoliosBase
    {
    }
}
```

A classe base declara `virtual` métodos para `Get` e `GetAll` que podem ser substituídos para implementar o serviço. Os métodos são `virtual` em vez de `abstract` que, se você não implementá-los, o serviço poderá retornar um código de status gRPC explícito `Unimplemented` , assim como você pode lançar um `NotImplementedException` em um código C# regular.

A assinatura para todos os métodos de serviço unário gRPC no ASP.NET Core é consistente. Há dois parâmetros: o primeiro é o tipo de mensagem declarado no `.proto` arquivo e o segundo é um `ServerCallContext` que funciona de forma semelhante ao `HttpContext` de ASP.NET Core. Na verdade, há um método de extensão chamado `GetHttpContext` na `ServerCallContext` classe que você pode usar para obter o subjacente `HttpContext` , embora você não precise usá-lo com frequência. Vamos examinar `ServerCallContext` mais adiante neste capítulo e também no capítulo que aborda a autenticação.

O tipo de retorno do método é um `Task<T>` , em que `T` é o tipo de mensagem de resposta. Todos os métodos de serviço gRPC são assíncronos.

## <a name="migrate-the-portfoliodata-library-to-net"></a>Migrar a biblioteca PortfolioData para o .NET

Neste ponto, o projeto precisa do repositório de portfólio e dos modelos contidos na `TraderSys.PortfolioData` biblioteca de classes na solução do WCF. A maneira mais fácil de trazê-los é criar uma nova biblioteca de classes usando a caixa de diálogo **novo projeto** do Visual Studio com o modelo biblioteca de classes (.net Standard) ou na linha de comando usando o CLI do .NET Core, executando esses comandos do diretório que contém o `TraderSys.sln` arquivo:

```dotnetcli
dotnet new classlib -o src/TraderSys.PortfolioData
dotnet sln add src/TraderSys.PortfolioData
```

Depois de criar a biblioteca e adicioná-la à solução, exclua o `Class1.cs` arquivo gerado e copie os arquivos da biblioteca da solução WCF para a pasta da nova biblioteca de classes, mantendo a estrutura de pastas:

```
Models
  Portfolio.cs
  PortfolioItem.cs
IPortfolioRepository.cs
PortfolioRepository.cs
```

Os projetos do estilo SDK do .NET incluem automaticamente todos os `.cs` arquivos no ou em seu próprio diretório, de modo que você não precisa adicioná-los explicitamente ao projeto. A única etapa restante é remover os `DataContract` atributos e `DataMember` das `Portfolio` `PortfolioItem` classes e para que eles sejam classes C# simples e antigas:

```csharp
public class Portfolio
{
    public int Id { get; set; }
    public Guid TraderId { get; set; }
    public List<PortfolioItem> Items { get; set; }
}

public class PortfolioItem
{
    public int Id { get; set; }
    public int ShareId { get; set; }
    public int Holding { get; set; }
    public decimal Cost { get; set; }
}
```

## <a name="use-aspnet-core-dependency-injection"></a>Usar ASP.NET Core injeção de dependência

Agora você pode adicionar uma referência a essa biblioteca para o projeto de aplicativo gRPC e consumir a `PortfolioRepository` classe usando a injeção de dependência na implementação do serviço gRPC. No aplicativo WCF, a injeção de dependência foi fornecida pelo contêiner Autofac IoC. ASP.NET Core tem injeção de dependência inclusas em. Você pode registrar o repositório no `ConfigureServices` método na `Startup` classe:

```csharp
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        // Register the repository class as a scoped service (instance per request)
        services.AddScoped<IPortfolioRepository, PortfolioRepository>();

        services.AddGrpc();
    }

    // ...
}
```

A `IPortfolioRepository` implementação agora pode ser especificada como um parâmetro de Construtor na `PortfolioService` classe, da seguinte maneira:

```csharp
public class PortfolioService : Protos.Portfolios.PortfoliosBase
{
    private readonly IPortfolioRepository _repository;

    public PortfolioService(IPortfolioRepository repository)
    {
        _repository = repository;
    }
}
```

## <a name="implement-the-grpc-service"></a>Implementar o serviço gRPC

Agora que você declarou suas mensagens e seu serviço no `portfolios.proto` arquivo, precisará implementar os métodos de serviço na `PortfolioService` classe que herda da classe gerada pelo gRPC `Portfolios.PortfoliosBase` . Os métodos são declarados como `virtual` na classe base. Se você não substituí-los, eles retornarão um código de status gRPC "não implementado" por padrão.

Comece implementando o `Get` método. A substituição padrão é semelhante a este exemplo:

```csharp
public override Task<GetResponse> Get(GetRequest request, ServerCallContext context)
{
    return base.Get(request, context);
}
```

O primeiro problema é `request.TraderId` uma cadeia de caracteres, e o serviço requer um `Guid` . Embora o formato esperado para a cadeia de caracteres seja `UUID` , o código precisa lidar com a possibilidade de um chamador ter enviado um valor inválido e responder adequadamente. O serviço pode responder com erros ao lançar um `RpcException` e usar o `InvalidArgument` código de status padrão para expressar o problema:

```csharp
public override Task<GetResponse> Get(GetRequest request, ServerCallContext context)
{
    if (!Guid.TryParse(request.TraderId, out var traderId))
    {
        throw new RpcException(new Status(StatusCode.InvalidArgument, "traderId must be a UUID"));
    }

    return base.Get(request, context);
}
```

Depois que houver um `Guid` valor adequado para o `traderId` , você poderá usar o repositório para recuperar o portfólio e retorná-lo ao cliente:

```csharp
    var response = new GetResponse
    {
        Portfolio = await _repository.GetAsync(request.TraderId, request.PortfolioId)
    };
```

### <a name="map-internal-models-to-grpc-messages"></a>Mapear modelos internos para mensagens gRPC

O código anterior não funciona realmente porque o repositório está retornando seu próprio modelo POCO `Portfolio` , mas gRPC precisa de sua própria mensagem Protobuf `Portfolio` . Como quando você mapeia tipos de Entity Framework para tipos de transferência de dados, a melhor solução é fornecer uma conversão entre os dois. Um bom local para colocar o código para essa conversão é na classe gerada pelo Protobuf, que é declarada como uma `partial` classe para que possa ser estendida:

```csharp
namespace TraderSys.Portfolios.Protos
{
    public partial class PortfolioItem
    {
        public static PortfolioItem FromRepositoryModel(PortfolioData.Models.PortfolioItem source)
        {
            if (source is null) return null;

            return new PortfolioItem
            {
                Id = source.Id,
                ShareId = source.ShareId,
                Holding = source.Holding,
                CostCents = (int)(source.Cost * 100)
            };
        }
    }

    public partial class Portfolio
    {
        public static Portfolio FromRepositoryModel(PortfolioData.Models.Portfolio source)
        {
            if (source is null) return null;

            var target = new Portfolio
            {
                Id = source.Id,
                TraderId = source.TraderId.ToString(),
            };

            target.Items.AddRange(source.Items.Select(PortfolioItem.FromRepositoryModel));

            return target;
        }
    }
}
```

> [!NOTE]
> Você pode usar uma biblioteca como o [AutoMapper](https://automapper.org/) para lidar com essa conversão de classes de modelo internas para tipos Protobuf, contanto que configure as conversões de tipo de nível inferior como `string` / `Guid` ou `decimal` / `double` e o mapeamento de lista.

Agora que você tem o código de conversão em vigor, você pode concluir a `Get` implementação do método:

```csharp
public override async Task<GetResponse> Get(GetRequest request, ServerCallContext context)
{
    if (!Guid.TryParse(request.TraderId, out var traderId))
    {
        throw new RpcException(new Status(StatusCode.InvalidArgument, "traderId must be a UUID"));
    }

    var portfolio = await _repository.GetAsync(traderId, request.PortfolioId);

    return new GetResponse
    {
        Portfolio = Portfolio.FromRepositoryModel(portfolio)
    };
}

```

A implementação do `GetAll` método é semelhante. Observe que os `repeated` campos em mensagens Protobuf são gerados como `readonly` Propriedades do tipo `RepeatedField<T>` , portanto, você precisa adicionar itens a eles usando o `AddRange` método, como neste exemplo:

```csharp
public override async Task<GetAllResponse> GetAll(GetAllRequest request, ServerCallContext context)
{
    if (!Guid.TryParse(request.TraderId, out var traderId))
    {
        throw new RpcException(new Status(StatusCode.InvalidArgument, "traderId must be a UUID"));
    }

    var portfolios = await _repository.GetAllAsync(traderId);

    var response = new GetAllResponse();
    response.Portfolios.AddRange(portfolios.Select(Portfolio.FromRepositoryModel));

    return response;
}
```

Tendo migrado com êxito o serviço de solicitação-resposta do WCF para gRPC, vamos examinar a criação de um cliente para ele a partir do `.proto` arquivo.

## <a name="generate-client-code"></a>Gerar código de cliente

Crie um .NET Standard biblioteca de classes na mesma solução para conter o cliente. Isso é basicamente um exemplo de criação de código de cliente, mas você pode empacotar essa biblioteca usando o NuGet e distribuí-la em um repositório interno para que outras equipes do .NET consumam. Vá em frente e adicione uma nova biblioteca de classes .NET Standard chamada `TraderSys.Portfolios.Client` à solução e exclua o `Class1.cs` arquivo.

> [!CAUTION]
> O pacote NuGet do [.net. Client do Grpc](https://www.nuget.org/packages/Grpc.Net.Client) requer o .net Core 3,0 ou posterior (ou outro tempo de execução .net Standard em conformidade com 2,1). As versões anteriores do .NET Framework e do .NET Core são compatíveis com o pacote NuGet [Grpc. Core](https://www.nuget.org/packages/Grpc.Core) .

No Visual Studio 2019, você pode adicionar referências a serviços gRPCs de uma maneira semelhante a como você adicionaria referências de serviço a projetos WCF em versões anteriores do Visual Studio. Referências de serviço e serviços conectados são todos gerenciados na mesma interface do usuário agora. Você pode acessar a interface do usuário clicando com o botão direito do mouse no nó **dependências** no `TraderSys.Portfolios.Client` projeto no Gerenciador de soluções e selecionando **Adicionar serviço conectado**. Na janela de ferramentas exibida, selecione a seção **referências de serviço** e, em seguida, selecione **Adicionar nova referência de serviço gRPC**:

![Interface do usuário de serviços conectados no Visual Studio 2019](media/migrate-request-reply/add-connected-service.png)

Navegue até o `portfolios.proto` arquivo no `TraderSys.Portfolios` projeto, deixe **cliente** em **selecionar o tipo de classe a ser gerado** e, em seguida, selecione **OK**:

![Caixa de diálogo Adicionar nova referência de serviço gRPC no Visual Studio 2019](media/migrate-request-reply/add-new-grpc-service-reference.png)

> [!TIP]
> Observe que essa caixa de diálogo também fornece um campo URL. Se sua organização mantém um diretório de arquivos acessível pela Web `.proto` , você pode criar clientes apenas definindo esse endereço de URL.

Quando você usa o recurso **Adicionar serviço conectado** do Visual Studio, o `portfolios.proto` arquivo é adicionado ao projeto de biblioteca de classes como um *arquivo vinculado* , em vez de copiado, portanto, as alterações no arquivo no projeto de serviço serão aplicadas automaticamente no projeto cliente. O `<Protobuf>` elemento no `csproj` arquivo tem a seguinte aparência:

```xml
<Protobuf Include="..\TraderSys.Portfolios\Protos\portfolios.proto" GrpcServices="Client">
  <Link>Protos\portfolios.proto</Link>
</Protobuf>
```

> [!TIP]
> Se você não estiver usando o Visual Studio ou preferir trabalhar na linha de comando, poderá usar a `dotnet-grpc` ferramenta global para gerenciar referências Protobuf em um projeto .net gRPC. Para obter mais informações, consulte a [ `dotnet-grpc` documentação](/aspnet/core/grpc/dotnet-grpc).

### <a name="use-the-portfolios-service-from-a-client-application"></a>Usar o serviço de portfólios de um aplicativo cliente

O código a seguir é um breve exemplo de como usar o cliente gerado em um aplicativo de console. Uma exploração mais detalhada do código do cliente gRPC está no final deste capítulo.

```csharp
public class Program
{
    public async Task Main(string[] args)
    {
        GetResponse response;

        using (var channel = GrpcChannel.ForAddress("https://localhost:5001"))
        {
            var client = new Protos.Portfolios.PortfoliosClient(channel);

            response = await client.GetAsync(new GetRequest
            {
                TraderId = args[0],
                PortfolioId = int.Parse(args[1])
            });
        }

        foreach (var item in response.Portfolio.Items)
        {
            Console.WriteLine($"Holding {item.Holding} of Share ID {item.ShareId}.");
        }
    }
}
```

Agora você migrou um aplicativo WCF básico para um ASP.NET Core serviço gRPC e criou um cliente para consumir o serviço de um aplicativo .NET. A próxima seção abordará os serviços duplex mais envolvidos.

>[!div class="step-by-step"]
>[Anterior](create-project.md) 
> [Avançar](migrate-duplex-services.md)
