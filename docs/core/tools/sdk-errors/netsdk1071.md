---
title: "NETSDK1071: um PackageReference para ' {0} ' especificou uma versão de `{1}` ."
description: Como resolver o problema de um PackageReference para um metapacote incluído com a estrutura com uma versão.
author: Forgind
ms.topic: error-reference
ms.date: 10/09/2020
f1_keywords:
- NETSDK1071
ms.openlocfilehash: 1381fc63941ec04efb31035d13913620a195c236
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95713074"
---
# <a name="netsdk1071-explicitly-versioned-packagereference-to-a-metapackage-that-would-be-included-with-the-framework"></a>NETSDK1071: PackageReference com controle de versão explícito para um metapacote que seria incluído com a estrutura.

**Este artigo aplica-se a:** ✔️ o SDK do .NET 5.0.100 e versões posteriores

Quando o SDK do .NET emite aviso NETSDK1071, ele sugere que pode haver um conflito de versão no futuro entre a versão de um metapacote especificado em um PackageReference e a versão desse metapacote como referenciado implicitamente por meio de uma propriedade TargetFramework:

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp3.1</TargetFramework>
</PropertyGroup>
```

Como o TargetFramework automaticamente coloca em uma versão do metapacote, as versões entrarão em conflito caso sejam diferentes.

Para resolver esse problema:

1. Considere, ao direcionar .NET Core ou .NET Standard, evitando referências explícitas para `Microsoft.NETCore.App` ou `NETStandard.Library` em seu arquivo de projeto.
2. Se você precisar de uma versão específica do tempo de execução ao direcionar para o .NET Core, use a `<RuntimeFrameworkVersion>` propriedade em vez de fazer referência ao metapacote diretamente. Por exemplo, isso pode acontecer se você estiver usando [implantações independentes](../../deploying/index.md#publish-self-contained) e precisar de um patch específico do tempo de execução do 1.0.0 LTS.
3. Se precisar de uma versão específica do `NetStandard.Library` ao direcionar .net Standard, você poderá usar a `<NetStandardImplicitPackageVersion>` propriedade e defini-la para a versão necessária.
4. Não adicione ou atualize explicitamente referências a um `Microsoft.NETCore.App` ou `NETSTandard.Library` em projetos .NET Framework. O NuGet instala automaticamente qualquer versão de `NETStandard.Library` que você precisa ao usar um pacote NuGet baseado em .net Standard.
5. Não especifique uma versão para `Microsoft.AspNetCore.App` o ou `Microsoft.AspNetCore.All` ao usar o .NET Core 2.1 +, pois o SDK do .NET Core seleciona automaticamente a versão apropriada. (Observação: isso só funcionará ao direcionar o .NET Core 2,1 se o projeto também usar `Microsoft.NET.Sdk.Web` . Esse problema foi resolvido no SDK do .NET Core 2,2.
6. Se você quiser que o aviso saia, também poderá desabilitá-lo:

   ```xml
   <PackageReference Include="Microsoft.NetCore.App" Version="2.2.8" >
     <AllowExplicitVersion>true</AllowExplicitVersion>
   </PackageReference>
   ```
