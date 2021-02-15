---
ms.openlocfilehash: 2c1362d6982206b14475f77700add0bae61da173
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032230"
---
### <a name="caching-compactonmemorypressure-property-removed"></a>Caching: Propriedade CompactOnMemoryPressure removida

A versão ASP.NET Core 3,0 removeu as [APIs MemoryCacheOptions obsoletas](https://github.com/dotnet/extensions/blob/dc5c593da7b72c82e6fe85abb91d03818f9b700c/src/Caching/Memory/src/MemoryCacheOptions.cs#L17-L18).

#### <a name="change-description"></a>Descrição das alterações

Essa alteração é um acompanhamento do [ASPNET/Caching # 221](https://github.com/aspnet/Caching/issues/221). Para obter uma discussão, consulte [dotnet/Extensions # 1062](https://github.com/dotnet/extensions/issues/1062).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

`MemoryCacheOptions.CompactOnMemoryPressure` a propriedade estava disponível.

#### <a name="new-behavior"></a>Novo comportamento

A `MemoryCacheOptions.CompactOnMemoryPressure` propriedade foi removida.

#### <a name="reason-for-change"></a>Motivo da alteração

A compactação automática do cache causou problemas. Para evitar um comportamento inesperado, o cache só deve ser compactado quando necessário.

#### <a name="recommended-action"></a>Ação recomendada

Para compactar o cache, downcast `MemoryCache` e chame `Compact` quando necessário.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.Extensions.Caching.Memory.MemoryCacheOptions.CompactOnMemoryPressure%2A?displayProperty=nameWithType>

<!--

#### Affected APIs

`Overload:Microsoft.Extensions.Caching.Memory.MemoryCacheOptions.CompactOnMemoryPressure`

-->
