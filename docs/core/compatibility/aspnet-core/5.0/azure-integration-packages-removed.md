---
title: 'Alteração interruptiva: pacotes de integração do Azure prefixados com Microsoft removidos'
description: 'Saiba mais sobre a alteração interruptiva no ASP.NET Core 5.0 intitulado Azure: pacotes de integração do Azure prefixados com Microsoft removidos'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: b9f685b8c9fdcd73044f78840f2732809a0de710
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760518"
---
# <a name="azure-microsoft-prefixed-azure-integration-packages-removed"></a>Azure: pacotes de integração do Azure prefixados da Microsoft removidos

Os pacotes a seguir `Microsoft.*` que fornecem integração entre ASP.NET Core e SDKs do Azure não estão incluídos no ASP.NET Core 5,0:

* [Microsoft.Extensions.Configuração. AzureKeyVault](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.AzureKeyVault/), que integra [Azure Key Vault](/azure/key-vault/) ao sistema de [configuração](/aspnet/core/fundamentals/configuration/).
* [Microsoft. AspNetCore. dataprotection. AzureKeyVault](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureKeyVault/), que integra Azure Key Vault ao [sistema de proteção de dados ASP.NET Core](/aspnet/core/security/data-protection/introduction).
* [Microsoft. AspNetCore. dataprotection. AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/), que integra o [armazenamento de BLOBs do Azure](/azure/storage/blobs/) ao sistema de proteção de dados ASP.NET Core.

Para obter uma discussão sobre esse problema, consulte [dotnet/aspnetcore # 19570](https://github.com/dotnet/aspnetcore/issues/19570).

## <a name="version-introduced"></a>Versão introduzida

5,0 visualização 1

## <a name="old-behavior"></a>Comportamento antigo

Os `Microsoft.*` pacotes integraram os serviços do Azure com as APIs de proteção de dados e configuração.

## <a name="new-behavior"></a>Novo comportamento

Novos `Azure.*` pacotes integram os serviços do Azure com as APIs de configuração e proteção de dados.

## <a name="reason-for-change"></a>Motivo da alteração

A alteração foi feita porque os `Microsoft.*` pacotes foram:

* Usando versões desatualizadas do SDK do Azure. Atualizações simples não eram possíveis porque as novas versões do SDK do Azure incluíam alterações interruptivas.
* Vinculado à agenda de lançamento do .NET Core. A transferência da propriedade dos pacotes para a equipe do SDK do Azure habilita atualizações de pacote à medida que o SDK do Azure é atualizado.

## <a name="recommended-action"></a>Ação recomendada

Nos projetos ASP.NET Core 2,1 ou posteriores, substitua o antigo `Microsoft.*` pelos novos `Azure.*` pacotes.

| Antigo | Novo |
|--|--|
| `Microsoft.AspNetCore.DataProtection.AzureKeyVault` | [Azure. Extensions. AspNetCore. dataprotection. Keys](https://www.nuget.org/packages/Azure.Extensions.AspNetCore.DataProtection.Keys) |
| `Microsoft.AspNetCore.DataProtection.AzureStorage` | [Azure. Extensions. AspNetCore. dataprotection. BLOBs](https://www.nuget.org/packages/Azure.Extensions.AspNetCore.DataProtection.Blobs) |
| `Microsoft.Extensions.Configuration.AzureKeyVault` | [Azure.Extensions.AspNetCore.Configuração. Confidenciais](https://www.nuget.org/packages/Azure.Extensions.AspNetCore.Configuration.Secrets) |

Os novos pacotes usam uma nova versão do SDK do Azure que inclui alterações interruptivas. Os padrões de uso geral não são alterados. Algumas sobrecargas e opções podem diferir para se adaptar às alterações nas APIs do SDK do Azure subjacentes.

Os pacotes antigos vão:

* Ter suporte da equipe de ASP.NET Core pelo tempo de vida do .NET Core 2,1 e 3,1.
* Não ser incluído no .NET 5.

Ao atualizar seu projeto para o .NET 5, migre para os `Azure.*` pacotes para manter o suporte.

## <a name="affected-apis"></a>APIs afetadas

- <xref:Microsoft.Extensions.Configuration.AzureKeyVaultConfigurationExtensions.AddAzureKeyVault%2A?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.DataProtection.AzureDataProtectionBuilderExtensions.ProtectKeysWithAzureKeyVault%2A?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.DataProtection.AzureDataProtectionBuilderExtensions.PersistKeysToAzureBlobStorage%2A?displayProperty=nameWithType>

<!--

### Category

ASP.NET Core

### Affected APIs

- `Overload:Microsoft.Extensions.Configuration.AzureKeyVaultConfigurationExtensions.AddAzureKeyVault`
- `Overload:Microsoft.AspNetCore.DataProtection.AzureDataProtectionBuilderExtensions.ProtectKeysWithAzureKeyVault`
- `Overload:Microsoft.AspNetCore.DataProtection.AzureDataProtectionBuilderExtensions.PersistKeysToAzureBlobStorage`

-->
