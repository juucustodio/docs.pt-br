---
ms.openlocfilehash: f6e4c3d5c5fd020562e48515554136e0f8b6785c
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032235"
---
### <a name="data-protection-dataprotectionblobs-uses-new-azure-storage-apis"></a>Proteção de dados: dataprotegetion. BLOBs usa novas APIs de armazenamento do Azure

`Azure.Extensions.AspNetCore.DataProtection.Blobs` depende das [bibliotecas de armazenamento do Azure](https://github.com/Azure/azure-storage-net). Essas bibliotecas renomeam seus assemblies, pacotes e namespaces. A partir do ASP.NET Core 3,0, `Azure.Extensions.AspNetCore.DataProtection.Blobs` o usa as `Azure.Storage.` APIs e os pacotes novos e prefixados.

Para perguntas sobre as APIs de armazenamento do Azure, use <https://github.com/Azure/azure-storage-net> . Para obter uma discussão sobre esse problema, consulte [dotnet/aspnetcore # 19570](https://github.com/dotnet/aspnetcore/issues/19570).

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

O pacote referenciou o `WindowsAzure.Storage` pacote NuGet.
O pacote faz referência ao `Microsoft.Azure.Storage.Blob` pacote NuGet.

#### <a name="new-behavior"></a>Novo comportamento

O pacote faz referência ao `Azure.Storage.Blob` pacote NuGet.

#### <a name="reason-for-change"></a>Motivo da alteração

Essa alteração permite `Azure.Extensions.AspNetCore.DataProtection.Blobs` migrar para os pacotes de armazenamento do Azure recomendados.

#### <a name="recommended-action"></a>Ação recomendada

Se você ainda precisar usar as APIs mais antigas do armazenamento do Azure com o ASP.NET Core 3,0, adicione uma dependência direta ao pacote [WindowsAzure. Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) ou [Microsoft. Azure. Storage](https://www.nuget.org/packages/Microsoft.Azure.Storage.Blob/). Esse pacote pode ser instalado junto com as novas `Azure.Storage` APIs.

Em muitos casos, a atualização envolve apenas a alteração das `using` instruções para usar os novos namespaces:

```diff
- using Microsoft.WindowsAzure.Storage;
- using Microsoft.WindowsAzure.Storage.Blob;
- using Microsoft.Azure.Storage;
- using Microsoft.Azure.Storage.Blob;
+ using Azure.Storage;
+ using Azure.Storage.Blobs;
```

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

Nenhum

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
