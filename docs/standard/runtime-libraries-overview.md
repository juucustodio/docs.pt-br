---
title: Visão geral das bibliotecas de tempo de execução
description: Saiba o que está incluído na seção bibliotecas de tempo de execução do Sumário.
author: tdykstra
ms.date: 11/12/2020
ms.openlocfilehash: 5a8f888e1778553e2968277738cfef5134f11589
ms.sourcegitcommit: 34968a61e9bac0f6be23ed6ffb837f52d2390c85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94687890"
---
# <a name="runtime-libraries-overview"></a>Visão geral das bibliotecas de tempo de execução

O [tempo de execução do .net](../core/introduction.md#sdk-and-runtimes), que é instalado em um computador para uso por [aplicativos dependentes da estrutura](../core/introduction.md#deployment-models), tem um conjunto padrão de bibliotecas de classes, conhecido como bibliotecas de tempo de [execução](glossary.md#runtime), [bibliotecas de estruturas](glossary.md#framework-libraries)ou a [BCL (biblioteca de classes base)](glossary.md#bcl). Além disso, há extensões para as bibliotecas de tempo de execução, fornecidas em pacotes NuGet.

Essas bibliotecas fornecem implementações para muitos tipos, algoritmos e funcionalidades de utilitário específicos de aplicativos e gerais.

## <a name="runtime-libraries"></a>Bibliotecas de runtime

Essas bibliotecas fornecem os tipos básicos e a funcionalidade do utilitário e são a base de todas as outras bibliotecas de classes do .NET. Um exemplo é a <xref:System.String?displayProperty=nameWithType> classe, que fornece APIs para trabalhar com cadeias de caracteres. Outro exemplo são as [bibliotecas de serialização](serialization/index.md).

## <a name="extensions-to-the-runtime-libraries"></a>Extensões para as bibliotecas de tempo de execução

Algumas bibliotecas são fornecidas em pacotes NuGet em vez de incluídos na [estrutura compartilhada](glossary.md#shared-framework)do tempo de execução. Por exemplo:

* [Logging](../core/extensions/logging.md)
* [Injeção de dependência](../core/extensions/dependency-injection.md)
* [Configuration](../core/extensions/configuration.md)

## <a name="see-also"></a>Consulte também

* [Introdução ao .NET](../core/introduction.md)
* [Instalar o SDK ou tempo de execução do .NET](../core/install/index.yml)
* [Selecione o SDK .NET ou a versão de tempo de execução instalada para usar](../core/versions/selection.md)
* [Publicar aplicativos dependentes da estrutura](../core/deploying/index.md#publish-framework-dependent)
