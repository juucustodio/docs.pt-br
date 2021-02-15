---
title: 'Alteração significativa: os aplicativos ASP.NET Core permitem a desserialização de números entre aspas'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que os aplicativos ASP.NET Cores irão desserializar com êxito os números representados como cadeias de caracteres JSON em vez de lançar uma exceção.
ms.date: 10/21/2020
ms.openlocfilehash: fc8a4c6638be391c22c7cfb2fc7c216c88377f29
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760348"
---
# <a name="aspnet-core-apps-allow-deserializing-quoted-numbers"></a>ASP.NET Core aplicativos permitem a desserialização de números entre aspas

A partir do .NET 5,0, os aplicativos ASP.NET Core usam as opções de desserialização padrão conforme especificado por <xref:System.Text.Json.JsonSerializerDefaults.Web?displayProperty=nameWithType> . O <xref:System.Text.Json.JsonSerializerDefaults.Web> conjunto de opções inclui <xref:System.Text.Json.JsonSerializerOptions.NumberHandling> a configuração para <xref:System.Text.Json.Serialization.JsonNumberHandling.AllowReadingFromString?displayProperty=nameWithType> . Essa alteração significa que ASP.NET Core aplicativos desserializarão com êxito os números representados como cadeias de caracteres JSON em vez de lançar uma exceção.

## <a name="change-description"></a>Descrição das alterações

No .NET Core 3,0-3,1, <xref:System.Text.Json.JsonSerializer> lança uma <xref:System.Text.Json.JsonException> durante a desserialização se encontrar um número entre aspas em uma carga JSON. Os números entre aspas são usados para mapear com propriedades de número em grafos de objeto. No .NET Core 3,0-3,1, os números são lidos somente de <xref:System.Text.Json.JsonTokenType.Number?displayProperty=nameWithType> tokens.

A partir do .NET 5,0, os números entre aspas em cargas JSON são considerados válidos, por padrão, para os aplicativos ASP.NET Core. Nenhuma exceção é lançada durante a desserialização de números entre aspas.

> [!TIP]
>
> - Não há nenhuma alteração de comportamento para o padrão, autônomo <xref:System.Text.Json.JsonSerializer> ou <xref:System.Text.Json.JsonSerializerOptions> .
> - Isso tecnicamente não é uma alteração significativa, pois torna um cenário mais permissivo, em vez de mais restritivo (ou seja, ele tem sucesso em impor um número de uma cadeia de caracteres JSON em vez de gerar uma exceção). No entanto, como essa é uma alteração comportamental significativa que afeta muitos aplicativos ASP.NET Core, ele está documentado aqui.
> - Os <xref:System.Net.Http.Json.HttpClientJsonExtensions.GetFromJsonAsync%2A?displayProperty=nameWithType> <xref:System.Net.Http.Json.HttpContentJsonExtensions.ReadFromJsonAsync%2A?displayProperty=nameWithType> métodos de extensão e também usam o <xref:System.Text.Json.JsonSerializerDefaults.Web> conjunto de opções de serialização.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="reason-for-change"></a>Motivo da alteração

Vários usuários solicitaram uma opção para a manipulação de números mais permissivos no <xref:System.Text.Json.JsonSerializer> . Esse comentário indica que muitos produtores JSON (por exemplo, serviços na Web) emitem números entre aspas. Ao permitir que números entre aspas sejam lidos (desserializados), os aplicativos .NET podem analisar com êxito essas cargas, por padrão, em contextos da Web. A configuração é exposta por meio <xref:System.Text.Json.JsonSerializerDefaults.Web?displayProperty=nameWithType> do para que você possa especificar as mesmas opções em diferentes camadas de aplicativo, por exemplo, cliente, servidor e compartilhado.

## <a name="recommended-action"></a>Ação recomendada

Se essa alteração for interrompida, por exemplo, se você depender da manipulação de número estrito para validação, poderá reabilitar o comportamento anterior. Defina a <xref:System.Text.Json.JsonSerializerOptions.NumberHandling?displayProperty=nameWithType> opção como <xref:System.Text.Json.Serialization.JsonNumberHandling.Strict?displayProperty=nameWithType> .

Para os aplicativos de API Web e MVC do ASP.NET Core, você pode configurar a opção no `Startup` usando o seguinte código:

```csharp
services.AddControllers()
   .AddJsonOptions(options.NumberHandling = JsonNumberHandling.Strict);
```

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.DeserializeAsync%2A?displayProperty=fullName>

<!--

### Affected APIs

- `Overload:System.Text.Json.JsonSerializer.Deserialize`
- `Overload:System.Text.Json.JsonSerializer.DeserializeAsync`

### Category

- ASP.NET Core
- Serialization

-->
