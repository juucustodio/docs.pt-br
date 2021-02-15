---
title: Configuração no .NET
description: Saiba como usar a API de configuração para configurar aplicativos .NET.
author: IEvangelist
ms.author: dapine
ms.date: 09/16/2020
ms.topic: overview
ms.openlocfilehash: 5955e46c2f5acb6776ada4e3fd6a65507d3faa1f
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740120"
---
# <a name="configuration-in-net"></a>Configuração no .NET

A configuração no .NET é executada usando um ou mais [provedores de configuração](#configuration-providers). Os provedores de configuração lêem dados de configuração de pares chave-valor usando uma variedade de fontes de configuração:

- Arquivos de configurações, como *appsettings.jsem*
- Variáveis de ambiente
- [Cofre da Chave do Azure](/azure/key-vault/general/overview)
- [Configuração de Aplicativos do Azure](/azure/azure-app-configuration/overview)
- Argumentos de linha de comando
- Provedores personalizados, instalados ou criados
- Arquivos de diretório
- Objetos do .NET na memória

## <a name="configure-console-apps"></a>Configurar aplicativos de console

Os novos aplicativos de console .NET criados usando [dotnet novo](../tools/dotnet-new.md) ou Visual Studio, por padrão, *não* expõem recursos de configuração. Para adicionar a configuração em um novo aplicativo de console .NET, [adicione uma referência de pacote](../tools/dotnet-add-package.md) a `Microsoft.Extensions.Hosting` . Modifique o arquivo *Program.cs* para corresponder ao seguinte código:

:::code language="csharp" source="snippets/configuration/console/Program.cs" highlight="18":::

O <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])?displayProperty=nameWithType> método fornece a configuração padrão para o aplicativo na seguinte ordem:

1. [ChainedConfigurationProvider](xref:Microsoft.Extensions.Configuration.ChainedConfigurationSource) : Adiciona um existente `IConfiguration` como uma origem.
1. *appsettings.js* usando o [provedor de configuração JSON](configuration-providers.md#file-configuration-provider).
1. *appSettings.* `Environment` *. JSON* usando o [provedor de configuração JSON](configuration-providers.md#file-configuration-provider). Por exemplo, *appSettings*. ***Produção * * _._json* e *appSettings*. * * * desenvolvimento** _._json *.
1. Segredos do aplicativo quando o aplicativo é executado no `Development` ambiente.
1. Variáveis de ambiente usando o [provedor de configuração de variáveis de ambiente](configuration-providers.md#environment-variable-configuration-provider).
1. Argumentos de linha de comando usando o [provedor de configuração de linha de comando](configuration-providers.md#command-line-configuration-provider).

Os provedores de configuração adicionados posteriormente substituem as configurações de chave anteriores. Por exemplo, se `SomeKey` for definido tanto no *appsettings.jsquanto no* ambiente, o valor do ambiente será usado. Usando os provedores de configuração padrão, o [provedor de configuração de linha de comando](configuration-providers.md#command-line-configuration-provider) substitui todos os outros provedores.

### <a name="binding"></a>Associação

Uma das principais vantagens da configuração no .NET é a capacidade de associar valores de configuração a instâncias de objetos .NET. Por exemplo, o provedor de configuração JSON pode ser usado para mapear *appsettings.jsem* arquivos para objetos .net e é usado com injeção de dependência. Isso habilita o padrão de opções, o padrão de opções usa classes para fornecer acesso com rigidez de tipos a grupos de configurações relacionadas.

## <a name="configuration-providers"></a>Provedores de configuração

A tabela a seguir mostra os provedores de configuração disponíveis para aplicativos .NET Core.

| Provedor                                                                                                               | Fornece a configuração de         |
|------------------------------------------------------------------------------------------------------------------------|------------------------------------|
| [Provedor de configuração de Azure App](/azure/azure-app-configuration/quickstart-aspnet-core-app)                          | Configuração de Aplicativo do Azure            |
| [Provedor de configuração de Azure Key Vault](/azure/key-vault/general/tutorial-net-virtual-machine)                        | Cofre de Chave do Azure                    |
| [Provedor de configuração de linha de comando](configuration-providers.md#command-line-configuration-provider)                  | Parâmetros de linha de comando            |
| [Provedor de Configuração personalizado](custom-configuration-provider.md)                                                      | Fonte personalizada                      |
| [Provedor de configuração de variáveis de ambiente](configuration-providers.md#environment-variable-configuration-provider) | Variáveis de ambiente              |
| [Provedor de configuração de arquivo](configuration-providers.md#file-configuration-provider)                                  | Arquivos JSON, XML e INI           |
| [Provedor de configuração de chave por arquivo](configuration-providers.md#key-per-file-configuration-provider)                  | Arquivos de diretório                    |
| [Provedor de configuração de memória](configuration-providers.md#memory-configuration-provider)                              | Coleções na memória              |
| [Segredos do aplicativo (Gerenciador de segredo)](/aspnet/core/security/app-secrets)                                                      | Arquivo no diretório de perfil do usuário |

Para obter mais informações sobre vários provedores de configuração, consulte [provedores de configuração no .net](configuration-providers.md).

## <a name="see-also"></a>Confira também

- [Provedores de configuração no .NET](configuration-providers.md)
- [Implementar um provedor de configuração personalizado](custom-configuration-provider.md)
- Os bugs de configuração devem ser criados no repositório [github.com/dotnet/Extensions](https://github.com/dotnet/extensions/issues)
