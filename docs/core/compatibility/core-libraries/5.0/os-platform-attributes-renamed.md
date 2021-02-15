---
title: 'Alteração significativa: atributos OSPlatform renomeados ou removidos'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que os atributos da plataforma do sistema operacional que foram introduzidos em uma versão de visualização foram removidos ou renomeados.
ms.date: 11/01/2020
ms.openlocfilehash: be2ddd4909bef70f531ca48246f091923d6435ec
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739484"
---
# <a name="osplatform-attributes-renamed-or-removed"></a>Atributos OSPlatform renomeados ou removidos

Os seguintes atributos apresentados no .NET 5,0 Preview 8 foram removidos ou renomeados: `MinimumOSPlatformAttribute` , `RemovedInOSPlatformAttribute` e `ObsoletedInOSPlatformAttribute` .

## <a name="change-description"></a>Descrição das alterações

O .NET 5,0 Preview 8 introduziu os seguintes atributos no <xref:System.Runtime.Versioning> namespace:

- `MinimumOSPlatformAttribute`
- `RemovedInOSPlatformAttribute`
- `ObsoletedInOSPlatformAttribute`

No .NET 5,0 Preview 8, quando um projeto tem como alvo um tipo específico de sistema operacional do .NET 5 usando um [moniker de estrutura de destino](../../../../standard/frameworks.md) como `net5.0-windows` , o Build adiciona um atributo de nível de assembly `System.Runtime.Versioning.MinimumOSPlatformAttribute` .

No .NET 5,0 RC1, o `ObsoletedInOSPlatformAttribute` foi removido e `MinimumOSPlatformAttribute` e `RemovedInOSPlatformAttribute` foi renomeado da seguinte maneira:

| Nome da visualização 8 | RC1 e nome posterior |
| - | - |
| `MinimumOSPlatformAttribute` | <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> |
| `RemovedInOSPlatformAttribute` | <xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> |

No .NET 5,0 RC1 e posterior, quando um projeto tem como alvo um tipo específico de sistema operacional do .NET 5 usando um [moniker de estrutura de destino](../../../../standard/frameworks.md) como `net5.0-windows` , o Build adiciona um atributo de nível de assembly <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> .

## <a name="reason-for-change"></a>Motivo da alteração

O .NET 5,0 Preview 8 introduziu atributos no <xref:System.Runtime.Versioning> para especificar plataformas com suporte para APIs. Os atributos são consumidos pelo [analisador de compatibilidade de plataforma](../../code-analysis/5.0/ca1416-platform-compatibility-analyzer.md) para produzir avisos de compilação quando APIs específicas da plataforma são consumidas em plataformas que não dão suporte a essas APIs.

Para o .NET 5,0 RC1, um recurso adicional foi adicionado ao analisador de compatibilidade de plataforma para exclusão de plataforma. O recurso permite que as APIs sejam marcadas como totalmente sem suporte em plataformas de sistema operacional. Esse recurso solicitou alterações nos atributos, incluindo o uso de nomes mais adequados. O `ObsoletedInOSPlatformAttribute` foi removido porque não era mais necessário.

## <a name="version-introduced"></a>Versão introduzida

RC1 5,0

## <a name="recommended-action"></a>Ação recomendada

Ao redirecionar seu projeto do .NET 5,0 Preview 8 para o .NET 5,0 RC1, você poderá encontrar erros de compilação ou tempo de execução devido a essas alterações. Por exemplo, a renomeação do `MinimumOSPlatformAttribute` provavelmente produzirá erros, porque o atributo é aplicado a assemblies específicos da plataforma no momento da compilação, e os artefatos de Build antigos ainda referenciarão o antigo nome da API.

Exemplos de erros de tempo de compilação:

- **erro CS0246: não foi possível encontrar o nome do namespace ou tipo ' MinimumOSPlatformAttribute ' (está faltando uma diretiva using ou uma referência de assembly?)**
- **erro CS0246: não foi possível encontrar o nome do namespace ou tipo ' RemovedInOSPlatformAttribute ' (está faltando uma diretiva using ou uma referência de assembly?)**
- **erro CS0246: não foi possível encontrar o nome do namespace ou tipo ' ObsoletedInOSPlatformAttribute ' (está faltando uma diretiva using ou uma referência de assembly?)**

Erro de tempo de execução de exemplo:

**Exceção sem tratamento. System. TypeLoadException: não foi possível carregar o tipo ' System. Runtime. Versioning. MinimumOSPlatformAttribute ' do assembly ' System. Runtime, versão = 5.0.0.0, Culture = neutral, PublicKeyToken = b03f5f7f11d50a3a '.**

Para resolver esses erros:

- Atualize todas as referências de `MinimumOSPlatformAttribute` para <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> .
- Atualize todas as referências de `RemovedInOSPlatformAttribute` para <xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> .
- Remova todas as referências a `ObsoletedInOSPlatformAttribute` .
- Recompile o projeto (ou execute limpar + Build) para excluir os artefatos de Build antigos.

## <a name="affected-apis"></a>APIs afetadas

- `System.Runtime.Versioning.MinimumOSPlatformAttribute`
- `System.Runtime.Versioning.ObsoletedInOSPlatformAttribute`
- `System.Runtime.Versioning.RemovedInOSPlatformAttribute`

<!--

### Category

Core .NET libraries

### Affected APIs

- `T:System.Runtime.Versioning.MinimumOSPlatformAttribute`
- `T:System.Runtime.Versioning.ObsoletedInOSPlatformAttribute`
- `T:System.Runtime.Versioning.RemovedInOSPlatformAttribute`

-->
