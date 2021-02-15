---
title: Diferenças de log entre ASP.NET MVC e ASP.NET Core
description: Como o registro em log é diferente entre o ASP.NET MVC e os aplicativos de API Web e os aplicativos ASP.NET Core?
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: a364f761699428967b7c7b79d3f9e5103a59da14
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488372"
---
# <a name="logging-differences-between-aspnet-mvc-and-aspnet-core"></a>Diferenças de log entre ASP.NET MVC e ASP.NET Core

O log de aplicativo fornece informações de diagnóstico importantes, especialmente para aplicativos em execução na produção. ASP.NET Core introduz um novo sistema para adicionar o registro em log padronizado a qualquer aplicativo. Os aplicativos de API Web e MVC existentes ASP.NET provavelmente usam soluções de registro em log de terceiros, o que provavelmente continuará a ter suporte em ASP.NET Core.

## <a name="aspnet-mvc-logging"></a>Log MVC do ASP.NET

Não há uma solução de registro em log interna no ASP.NET MVC e em aplicativos de API Web. Em vez disso, a maioria dos aplicativos usa soluções de registro em log de terceiros como [log4net](https://www.nuget.org/packages/log4net/), [NLog](https://www.nuget.org/packages/NLog/)ou [Serilog](https://www.nuget.org/packages/Serilog). Muitas equipes também optam por lançar sua própria solução de registro em log. As estruturas de registro em log normalmente dão suporte a vários "coletores" (ou destinos ou acrescentadores) para a saída do log, como arquivos de texto, bancos de dados ou até mesmo emails. Eles usam a configuração para determinar quais níveis de mensagens de log de quais partes do sistema são roteadas para coletores diferentes. Ao considerar como migrar o log de um aplicativo para o .NET Core, examine como o log é executado e [configurado](configuration-differences.md) no aplicativo.

## <a name="aspnet-core-logging"></a>Registro em log de ASP.NET Core

No ASP.NET Core, [o registro em log é um recurso interno](https://docs.microsoft.com/aspnet/core/fundamentals/logging/) que pode ser configurado e estendido quando o aplicativo é iniciado. Agentes de terceiros, incluindo aqueles mencionados acima, podem ser integrados com ASP.NET Core para aprimorar sua funcionalidade.

O log de ASP.NET Core usa categorias e níveis para controlar o que é registrado e como. Normalmente, as classes usam instâncias da `ILogger<T>` interface, com o tipo da classe usado como o `T` tipo genérico. Nesse cenário, o nome totalmente qualificado da classe é usado como a categoria. Os agentes de log também podem ser criados com uma categoria personalizada usando um `ILoggerFactory` . Os níveis de log variam do mais detalhado, `Trace` , para o mais importante, `Critical` . Usando a configuração, os aplicativos podem especificar qual nível mínimo de log deve ser incluído em uma base por categoria (com curingas).

Uma configuração de log típica poderia registrar `Information` as informações acima por padrão, mas apenas `Warning` ou acima das `Microsoft` categorias prefixadas:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning"
    }
  }
}
```

O suporte para registro em log no ASP.NET Core é extensivo e flexível. Para obter informações mais detalhadas, [consulte os documentos](https://docs.microsoft.com/aspnet/core/fundamentals/logging/).

## <a name="migrate-logging"></a>Migrar log

A maneira como você migra o log do seu aplicativo .NET Framework para o .NET Core depende de como o aplicativo está fazendo logon agora. Se ele estiver usando um pacote NuGet de terceiros, consulte a documentação de atualização para esse pacote. Provavelmente, o caminho de atualização será bem simples. Se você estiver usando sua própria solução de registro em log, execute uma das seguintes ações:

1. Migre a solução de log por conta própria
1. Migrar para uma solução de registro em log de terceiros
1. Use o suporte de log interno no ASP.NET Core

Você pode fazer referência ao `Microsoft.Extensions.Logging` pacote de .NET Framework aplicativos contanto que estejam usando o NuGet 4,3 ou posterior e que estejam no .NET Framework 4.6.1 ou posterior. Depois que seu aplicativo tiver referenciado esse pacote, você poderá converter suas instruções de registro em log para usar as novas extensões antes de migrar o aplicativo para o .NET Core. Isso pode fornecer uma etapa de depuração para a migração completa, já que o aplicativo pode continuar sendo executado em .NET Framework durante o registro em log usando o pacote de extensões mais recente.

## <a name="references"></a>Referências

- [Log no .NET Core e no ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging/)
- [Pacote NuGet Microsoft. Extensions. Logging](https://www.nuget.org/packages/microsoft.extensions.logging/)

>[!div class="step-by-step"]
>[Anterior](middleware-modules-handlers.md) 
> [Avançar](routing-differences.md)
