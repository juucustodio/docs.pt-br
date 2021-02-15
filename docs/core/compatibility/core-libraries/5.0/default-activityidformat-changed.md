---
title: 'Alteração significativa: o ActivityIdFormat padrão é W3C'
description: Saiba mais sobre a alteração significativa do .NET 5,0 nas principais bibliotecas do .NET em que o ActivityIdFormat padrão agora é W3C.
ms.date: 11/01/2020
ms.openlocfilehash: 77ee705ac18065c84ddeab3127e01b6a40c3b84d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760418"
---
# <a name="default-activityidformat-is-w3c"></a>O ActivityIdFormat padrão é W3C

O formato de identificador padrão para atividade ( <xref:System.Diagnostics.Activity.DefaultIdFormat?displayProperty=nameWithType> ) agora é <xref:System.Diagnostics.ActivityIdFormat.W3C?displayProperty=nameWithType> .

## <a name="change-description"></a>Descrição das alterações

O formato da ID da atividade W3C foi introduzido no .NET Core 3,0 como uma alternativa ao formato de ID hierárquica. No entanto, para preservar a compatibilidade, o formato W3C não foi tornado o padrão até o .NET 5,0. O padrão foi alterado no .NET 5,0 porque o [formato W3C foi ratificado](https://www.w3.org/TR/trace-context/) e ganhou força em várias implementações de idioma.

Se seu aplicativo for destinado a uma plataforma diferente do .NET 5,0 ou posterior, ele passará pelo comportamento antigo, em que <xref:System.Diagnostics.ActivityIdFormat.Hierarchical> é o formato padrão. Esse padrão se aplica às plataformas Net45 +, netstandard 1.1 + e netcoreapp (1. x, 2. x e 3. x). No .NET 5,0 e posterior, <xref:System.Diagnostics.Activity.DefaultIdFormat?displayProperty=nameWithType> é definido como <xref:System.Diagnostics.ActivityIdFormat.W3C?displayProperty=nameWithType> .

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Se seu aplicativo for independente do identificador usado para o rastreamento distribuído, nenhuma ação será necessária. Bibliotecas como ASP.NET Core e <xref:System.Net.Http.HttpClient> podem consumir ou propagar ambas as versões do <xref:System.Diagnostics.ActivityIdFormat> .

Se você precisar de interoperabilidade com sistemas existentes ou se os sistemas atuais dependem do formato do identificador, você pode preservar o comportamento antigo definindo <xref:System.Diagnostics.Activity.DefaultIdFormat> como <xref:System.Diagnostics.ActivityIdFormat.Hierarchical?displayProperty=nameWithType> . Como alternativa, você pode definir uma opção AppContext de uma das três maneiras:

- No arquivo de projeto.

  ```xml
  <ItemGroup>
    <RuntimeHostConfigurationOption Include="System.Diagnostics.DefaultActivityIdFormatIsHierarchial" Value="true" />
  </ItemGroup>
  ```

- Na *runtimeconfig.jsno* arquivo.

  ```json
  {
      "runtimeOptions": {
          "configProperties": {
              "System.Diagnostics.DefaultActivityIdFormatIsHierarchial": true
          }
      }
  }
  ```

- Por meio de uma variável de ambiente.

  Defina `DOTNET_SYSTEM_DIAGNOSTICS_DEFAULTACTIVITYIDFORMATISHIERARCHIAL` como `true` ou 1.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Diagnostics.Activity.DefaultIdFormat?displayProperty=fullName>

<!--

### Category

Core .NET libraries

### Affected APIs

- `P:System.Diagnostics.Activity.DefaultIdFormat`

-->
