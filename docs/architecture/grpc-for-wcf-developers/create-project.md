---
title: Criar um novo projeto ASP.NET Core gRPC-gRPC para desenvolvedores do WCF
description: Saiba como criar um projeto gRPC usando o Visual Studio ou a linha de comando.
ms.date: 01/06/2021
ms.openlocfilehash: c9d66a773f0633c2ae93c42ce3ce53084032cd17
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970252"
---
# <a name="create-a-new-aspnet-core-grpc-project"></a>Criar um projeto ASP.NET Core gRPC

O SDK do .NET vem com uma poderosa ferramenta CLI, `dotnet` , que permite criar e gerenciar projetos e soluções na linha de comando. O SDK está intimamente integrado ao Visual Studio, de modo que tudo também está disponível por meio da interface gráfica do usuário familiar. Este capítulo mostra as duas maneiras de criar um novo projeto ASP.NET Core gRPC.

## <a name="create-the-project-by-using-visual-studio"></a>Criar o projeto usando o Visual Studio

> [!IMPORTANT]
> Para desenvolver qualquer aplicativo ASP.NET Core 5,0, você precisa do Visual Studio 2019 versão 16,8 ou posterior, com a ASP.NET e a carga de trabalho de **desenvolvimento Web** instaladas.

Crie uma solução vazia chamada **Traders** a partir do modelo de *solução em branco* . Adicione uma pasta de solução chamada `src` . Em seguida, clique com o botão direito do mouse na pasta e escolha **Adicionar**  >  **novo projeto**. Digite `grpc` na caixa de pesquisa de modelo e você deverá ver um modelo de projeto chamado `gRPC Service` .

![Captura de tela da caixa de diálogo Adicionar um novo projeto](media/create-project/new-grpc-project.png)

Selecione **Avançar** para continuar na caixa de diálogo **Configurar o novo projeto** . Nomeie o projeto `TraderSys.Portfolios` e adicione um `src` subdiretório ao **local**.

![Captura de tela da caixa de diálogo Configurar seu novo projeto](media/create-project/configure-project.png)

Selecione **Avançar** para continuar na caixa de diálogo **criar um novo serviço gRPC** .

![Captura de tela da caixa de diálogo criar um novo serviço gRPC](media/create-project/create-new-grpc-service-v2.png)

No momento, você tem opções limitadas para a criação do serviço. O Docker será introduzido posteriormente, por isso, por enquanto, deixe essa opção desmarcada. Basta selecionar **criar**. Seu primeiro projeto ASP.NET Core gRPC 5,0 é gerado e adicionado à solução. Se você não quiser saber sobre como trabalhar com o `dotnet CLI` , pule para a seção [limpar o exemplo de código](#clean-up-the-example-code) .

## <a name="create-the-project-by-using-the-net-cli"></a>Criar o projeto usando a CLI do .NET

Esta seção aborda a criação de soluções e projetos da linha de comando.

Crie a solução, conforme mostrado no comando a seguir. O `-o` sinalizador (ou `--output` ) especifica o diretório de saída, que é criado no diretório atual, caso ele ainda não exista. A solução tem o mesmo nome que o diretório: `TraderSys.sln` . Você pode fornecer um nome diferente usando o `-n` sinalizador (ou `--name` ).

```dotnetcli
dotnet new sln -o TraderSys
cd TraderSys
```

ASP.NET Core 5,0 vem com um modelo de CLI para serviços gRPCs. Crie o novo projeto usando esse modelo, colocando-o em um `src` subdiretório como é convencional para projetos de ASP.NET Core. O projeto é nomeado após o diretório ( `TraderSys.Portfolios.csproj` ), a menos que você especifique um nome diferente com o `-n` sinalizador.

```dotnetcli
dotnet new grpc -o src/TraderSys.Portfolios
```

Por fim, adicione o projeto à solução usando o `dotnet sln` comando:

```dotnetcli
dotnet sln add src/TraderSys.Portfolios
```

> [!TIP]
> Como o diretório específico contém apenas um único `.csproj` arquivo, você pode especificar apenas o diretório, para salvar a digitação.

Agora você pode abrir essa solução no Visual Studio 2019, Visual Studio Code ou em qualquer editor que preferir.

## <a name="clean-up-the-example-code"></a>Limpar o código de exemplo

Agora você criou um serviço de exemplo usando o modelo gRPC, que foi revisado anteriormente no livro. Esse código não é útil em nosso contexto de comércio de ações, portanto, vamos editar as coisas para nosso primeiro projeto.

### <a name="rename-and-edit-the-proto-file"></a>Renomear e editar o arquivo proto

Vá em frente e renomeie o `Protos/greet.proto` arquivo para `Protos/portfolios.proto` e abra-o em seu editor. Exclua tudo após a `package` linha. Em seguida, altere os `option csharp_namespace` nomes, e `package` `service` e remova o `SayHello` serviço padrão. O código agora é semelhante ao seguinte:

```protobuf
syntax = "proto3";

option csharp_namespace = "TraderSys.Portfolios.Protos";

package PortfolioServer;

service Portfolios {
  // RPCs will go here
}
```

> [!TIP]
> O modelo não adiciona a `Protos` parte de namespace por padrão, mas adicioná-la torna mais fácil manter classes gRPC e suas próprias classes claramente separadas em seu código.

Se você renomear o `greet.proto` arquivo em um ambiente de desenvolvimento integrado (IDE) como o Visual Studio, uma referência a esse arquivo será atualizada automaticamente no `.csproj` arquivo. Mas, em algum outro editor, como Visual Studio Code, essa referência não é atualizada automaticamente, portanto, você precisa editar o arquivo de projeto manualmente.

Nos destinos de compilação gRPC, há um `Protobuf` elemento item que permite especificar quais `.proto` arquivos devem ser compilados e qual forma de geração de código é necessária (ou seja, "Server" ou "Client").

```xml
<ItemGroup>
  <Protobuf Include="Protos\portfolios.proto" GrpcServices="Server" />
</ItemGroup>
```

### <a name="rename-the-greeterservice-class"></a>Renomear a `GreeterService` classe

A `GreeterService` classe está na `Services` pasta e herda de `Greeter.GreeterBase` . Renomeie- `PortfolioService` o para e altere a classe base para `Portfolios.PortfoliosBase` . Exclua os `override` métodos.

```csharp
public class PortfolioService : Portfolios.PortfoliosBase
{
}
```

Houve uma referência à `GreeterService` classe no `Configure` método na `Startup` classe. Se você usou a refatoração para renomear a classe, essa referência deverá ter sido atualizada automaticamente. No entanto, se você não tiver, precisará editá-lo manualmente.

```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    app.UseRouting();

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapGrpcService<PortfolioService>();
    });
}
```

Na próxima seção, adicionaremos funcionalidade a esse novo serviço.

>[!div class="step-by-step"]
>[Anterior](migrate-wcf-to-grpc.md) 
> [Avançar](migrate-request-reply.md)
