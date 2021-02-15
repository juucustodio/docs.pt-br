---
title: Diferenças de inicialização de aplicativo entre ASP.NET MVC e ASP.NET Core
description: O ASP.NET MVC e o ASP.NET Core diferem significativamente em como os aplicativos são inicializados. Aprenda as diferenças importantes e como migrar do ASP.NET MVC para o ASP.NET Core.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 4f40bb9cf616ea67b9826ff6a9dfe1c21cd1ea07
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488422"
---
# <a name="app-startup-differences-between-aspnet-mvc-and-aspnet-core"></a>Diferenças de inicialização de aplicativo entre ASP.NET MVC e ASP.NET Core

Os aplicativos MVC ASP.NET são totalmente dentro do Internet Information Server (IIS), o servidor Web primário disponível em sistemas operacionais Windows. Ao contrário do ASP.NET MVC, os aplicativos ASP.NET Core são aplicativos executáveis. Você pode executá-los na linha de comando, usando `dotnet run` . Eles têm um método de ponto de entrada como todos os programas em C#, normalmente `public static void Main()` ou uma variação semelhante (talvez com argumentos ou `async` suporte). Essa é talvez a maior diferença arquitetônica entre ASP.NET Core e o ASP.NET MVC e é uma das várias diferenças que permite que ASP.NET Core seja executado em sistemas não Windows.

## <a name="aspnet-mvc-startup"></a>Inicialização do MVC do ASP.NET

Hospedados no IIS, os aplicativos ASP.NET dependem do IIS para instanciar determinados objetos e chamar determinados métodos quando uma solicitação chega. ASP.NET cria uma instância da classe do arquivo *global. asax* , que deriva de `HttpApplication` . Quando a primeira solicitação é recebida, antes de manipular a solicitação em si, ASP.NET chama o `Application_Start` método na classe do arquivo *global. asax* . Qualquer lógica que precise ser executada quando o aplicativo ASP.NET MVC iniciar pode ser adicionado a esse método.

Muitos pacotes NuGet para ASP.NET MVC e API Web usam o pacote [webactivator](https://github.com/davidebbo/WebActivator) para permitir que eles executem algum código durante a inicialização do aplicativo. Por convenção, esse código normalmente seria adicionado a uma pasta *App_Start* e seria configurado por meio de um atributo para ser executado imediatamente antes ou depois `Application_Start` .

Também é possível usar a [interface da Web aberta para .net (OWIN) e o Project Katana com o ASP.NET MVC](https://docs.microsoft.com/aspnet/aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana). Ao fazer isso, o aplicativo incluirá um arquivo *Startup.cs* que é responsável por configurar o middleware de solicitação de uma forma muito semelhante à ASP.NET Core se comporta.

Se você precisar executar código quando seu aplicativo ASP.NET MVC for iniciado, ele normalmente usará uma dessas abordagens.

## <a name="aspnet-core-startup"></a>Inicialização de ASP.NET Core

Como observado anteriormente, ASP.NET Core aplicativos são programas autônomos. Como tal, eles normalmente incluem um arquivo *Program.cs* que contém o ponto de entrada para o aplicativo. Um exemplo típico desse arquivo é mostrado na Figura 2-1.

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseStartup<Startup>();
            });
}
```

**Figura 2-1**. Um arquivo típico ASP.NET Core *Program.cs* .

O código mostrado na Figura 2-1 cria um *host* para o aplicativo, compila-o e executa-o. O aplicativo ASP.NET Core é executado no host configurado pelo `IHostBuilder` mostrado. Embora seja possível configurar completamente um aplicativo de ASP.NET Core usando o `IHostBuilder` , normalmente a massa desse trabalho é feita em uma `Startup` classe.

A `Startup` classe expõe dois métodos ao host: `ConfigureServices` e `Configure` . O `ConfigureServices` método é usado para definir os serviços que o aplicativo usará e seus respectivos tempos de vida. O `Configure` método é usado para definir como cada solicitação para o aplicativo será manipulada Configurando um pipeline de solicitação composto de middleware.

Além do código relacionado à configuração de serviços ou pipeline de solicitação do aplicativo, os aplicativos podem ter outro código que deve ser executado quando o aplicativo é iniciado. Esse código normalmente é colocado em *Program.cs* ou registrado como um `IHostedService` , que será iniciado pelo [host genérico](https://docs.microsoft.com/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-3.1&preserve-view=true) quando o aplicativo for iniciado.

A `IHostedService` interface apenas expõe dois métodos, `StartAsync` e `StopAsync` . Você registra a interface no `ConfigureServices` e o host faz o resto, chamando o `StartAsync` método antes da inicialização do aplicativo.

## <a name="porting-considerations"></a>Considerações sobre portabilidade

As equipes que procuram migrar seus aplicativos do ASP.NET MVC para ASP.NET Core precisam identificar qual código está sendo executado quando seu aplicativo é iniciado e determinar o local apropriado para esse código em seu aplicativo ASP.NET Core. Para o código personalizado necessário para executar quando o aplicativo é inicializado, especialmente o código assíncrono, a abordagem recomendada normalmente é colocar esse código em `IHostedService` implementações.

## <a name="references"></a>Referências

- [Visão geral do ciclo de vida do aplicativo ASP.NET para o IIS 7](https://docs.microsoft.com/previous-versions/aspnet/bb470252(v=vs.100))
- [Visão geral do ciclo de vida do aplicativo ASP.NET para o IIS 5 e 6](https://docs.microsoft.com/previous-versions/aspnet/ms178473(v=vs.100))
- [Introdução a OWIN e Katana](https://docs.microsoft.com/aspnet/aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana)
- [Webactivator](https://github.com/davidebbo/WebActivator)
- [Inicialização do aplicativo no ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/startup?view=aspnetcore-3.1&preserve-view=true)
- [Host genérico .NET no ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-3.1&preserve-view=true)
- [IHostedService](https://docs.microsoft.com/dotnet/architecture/microservices/multi-container-microservice-net-applications/background-tasks-with-ihostedservice)

>[!div class="step-by-step"]
>[Anterior](architectural-differences.md) 
> [Avançar](hosting-differences.md)
