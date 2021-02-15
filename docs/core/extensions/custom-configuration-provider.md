---
title: Implementar um provedor de configuração personalizado no .NET
description: Saiba como implementar um provedor de configuração personalizada em aplicativos .NET.
author: IEvangelist
ms.author: dapine
ms.date: 12/04/2020
ms.topic: how-to
ms.openlocfilehash: 22e46b7df8b02421633d6be251d990879baa8b2b
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740113"
---
# <a name="implement-a-custom-configuration-provider-in-net"></a>Implementar um provedor de configuração personalizado no .NET

Há muitos [provedores de configuração](configuration-providers.md) disponíveis para fontes de configuração comuns, como arquivos JSON, XML e ini. Talvez seja necessário implementar um provedor de configuração personalizado quando um dos provedores disponíveis não atender às suas necessidades de aplicativo. Neste artigo, você aprenderá a implementar um provedor de configuração personalizado que se baseia em um banco de dados como sua fonte de configuração.

## <a name="custom-configuration-provider"></a>Provedor de Configuração personalizado

O aplicativo de exemplo demonstra como criar um provedor de configuração básica que lê pares chave-valor de configuração de um banco de dados usando [Entity Framework (EF) Core](/ef/core).

O provedor tem as seguintes características:

- O banco de dados EF na memória é usado para fins de demonstração. Para usar um banco de dados que exija uma cadeia de conexão, implemente um `ConfigurationBuilder` secundário para fornecer a cadeia de conexão de outro provedor de configuração.
- O provedor lê uma tabela de banco de dados na configuração na inicialização. O provedor não consulta o banco de dados em uma base por chave.
- O recarregamento na alteração não está implementado, portanto, a atualização do banco de dados após a inicialização do aplicativo não tem efeito sobre a configuração do aplicativo.

Defina uma `Settings` entidade de tipo de registro para armazenar valores de configuração no banco de dados. Por exemplo, você pode adicionar um arquivo *Settings.cs* em sua pasta *modelos* :

:::code language="csharp" source="snippets/configuration/custom-provider/Models/Settings.cs":::

Para obter informações sobre tipos de registro, consulte [tipos de registro em C# 9](../../csharp/whats-new/csharp-9.md#record-types).

Adicione um `EntityConfigurationContext` para armazenar e acessar os valores configurados.

*Providers/EntityConfigurationContext. cs*:

:::code language="csharp" source="snippets/configuration/custom-provider/Providers/EntityConfigurationContext.cs":::

Crie uma classe que implementa <xref:Microsoft.Extensions.Configuration.IConfigurationSource>.

*Providers/EntityConfigurationSource. cs*:

:::code language="csharp" source="snippets/configuration/custom-provider/Providers/EntityConfigurationSource.cs":::

Crie o provedor de configuração personalizado através da herança de <xref:Microsoft.Extensions.Configuration.ConfigurationProvider>. O provedor de configuração inicializa o banco de dados quando ele está vazio. Como as chaves de configuração não diferenciam maiúsculas de minúsculas, o dicionário usado para inicializar o banco de dados é criado com o comparador que não diferencia maiúsculas de minúsculas ([StringComparer. OrdinalIgnoreCase](xref:System.StringComparer.OrdinalIgnoreCase)).

*Providers/EntityConfigurationProvider. cs*:

:::code language="csharp" source="snippets/configuration/custom-provider/Providers/EntityConfigurationProvider.cs":::

Um `AddEntityConfiguration` método de extensão permite adicionar a origem de configuração a uma <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> instância do.

*Extensões/ConfigurationBuilderExtensions. cs*:

:::code language="csharp" source="snippets/configuration/custom-provider/Extensions/ConfigurationBuilderExtensions.cs":::

O código a seguir mostra como usar o `EntityConfigurationProvider` personalizado em *Program.cs*:

:::code language="csharp" source="snippets/configuration/custom-provider/Program.cs" highlight="27-28":::

## <a name="see-also"></a>Confira também

- [Configuração no .NET](configuration.md)
- [Provedores de configuração no .NET](configuration-providers.md)
