---
title: Como inspecionar o conteúdo do assembly usando MetadataLoadContext
description: Saiba como usar o MetadataLoadContext, que é uma API que permite carregar assemblies .NET para fins de inspeção.
author: MSDN-WhiteKnight
ms.date: 03/10/2020
ms.openlocfilehash: 7205230986aa852813a651d2fcb7c5ef88ab18fe
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94831345"
---
# <a name="how-to-inspect-assembly-contents-using-metadataloadcontext"></a>Como inspecionar o conteúdo do assembly usando MetadataLoadContext

Por padrão, a API de reflexão no .NET permite que os desenvolvedores inspecionem o conteúdo dos assemblies carregados no contexto de execução principal. No entanto, às vezes não é possível carregar um assembly no contexto de execução, por exemplo, porque ele foi compilado para outra plataforma ou arquitetura de processador, ou é um [assembly de referência](reference-assemblies.md). A <xref:System.Reflection.MetadataLoadContext?displayProperty=fullName> API permite que você carregue e inspecione esses assemblies. Os assemblies carregados no <xref:System.Reflection.MetadataLoadContext> são tratados somente como metadados, ou seja, você pode examinar os tipos no assembly, mas não pode executar qualquer código contido nele. Ao contrário do contexto de execução principal, o <xref:System.Reflection.MetadataLoadContext> não carrega automaticamente as dependências do diretório atual; em vez disso, ele usa a lógica de associação personalizada fornecida pelo <xref:System.Reflection.MetadataAssemblyResolver> passado para ela.

## <a name="prerequisites"></a>Pré-requisitos

Para usar <xref:System.Reflection.MetadataLoadContext> o, instale o pacote NuGet [System. Reflection. MetadataLoadContext](https://www.nuget.org/packages/System.Reflection.MetadataLoadContext) . Ele tem suporte em qualquer estrutura de destino compatível com .NET Standard 2,0, por exemplo, .NET Core 2,0 ou .NET Framework 4.6.1.

## <a name="create-metadataassemblyresolver-for-metadataloadcontext"></a>Criar MetadataAssemblyResolver para MetadataLoadContext

A criação do <xref:System.Reflection.MetadataLoadContext> requer o fornecimento da instância do <xref:System.Reflection.MetadataAssemblyResolver> . A maneira mais simples de fornecer um é usar o <xref:System.Reflection.PathAssemblyResolver> , que resolve assemblies da coleção determinada de cadeias de caracteres de caminho do assembly. Essa coleção, além dos assemblies que você deseja inspecionar diretamente, também deve incluir todas as dependências necessárias. Por exemplo, para ler o atributo personalizado localizado em um assembly externo, você deve incluir esse assembly ou uma exceção será gerada. Na maioria dos casos, você deve incluir pelo menos o *assembly principal*, ou seja, o assembly que contém os tipos de sistema internos, como <xref:System.Object?displayProperty=nameWithType> . O código a seguir mostra como criar o <xref:System.Reflection.PathAssemblyResolver> usando a coleção que consiste no assembly inspecionado e no assembly principal do tempo de execução atual:

[!code-csharp[](snippets/inspect-contents-using-metadataloadcontext/MetadataLoadContextSnippets.cs#CoreAssembly)]

Se você precisar de acesso a todos os tipos de BCL, poderá incluir todos os assemblies de tempo de execução na coleção. O código a seguir mostra como criar o <xref:System.Reflection.PathAssemblyResolver> usando a coleção que consiste no assembly inspecionado e todos os assemblies do tempo de execução atual:

[!code-csharp[](snippets/inspect-contents-using-metadataloadcontext/MetadataLoadContextSnippets.cs#RuntimeAssemblies)]

## <a name="create-metadataloadcontext"></a>Criar MetadataLoadContext

Para criar o <xref:System.Reflection.MetadataLoadContext> , invoque seu construtor <xref:System.Reflection.MetadataLoadContext.%23ctor%28System.Reflection.MetadataAssemblyResolver%2CSystem.String%29> , passando o anteriormente criado <xref:System.Reflection.MetadataAssemblyResolver> como o primeiro parâmetro e o nome do assembly principal como o segundo parâmetro. Você pode omitir o nome do assembly de núcleo, caso em que o construtor tentará usar nomes padrão: "mscorlib", "System. Runtime" ou "netstandard".

Depois de criar o contexto, você pode carregar os assemblies nele usando métodos como <xref:System.Reflection.MetadataLoadContext.LoadFromAssemblyPath%2A> . Você pode usar todas as APIs de reflexão em assemblies carregados, exceto aqueles que envolvem a execução de código. O <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A> método envolve a execução de construtores, portanto, use o <xref:System.Reflection.MemberInfo.GetCustomAttributesData%2A> método quando você precisar examinar atributos personalizados no <xref:System.Reflection.MetadataLoadContext> .

O exemplo de código a seguir cria <xref:System.Reflection.MetadataLoadContext> , carrega o assembly nele e gera atributos de assembly no console:

[!code-csharp[](snippets/inspect-contents-using-metadataloadcontext/MetadataLoadContextSnippets.cs#CreateContext)]

## <a name="example"></a>Exemplo

Para obter um exemplo de código completo, consulte o [exemplo inspecionar conteúdo do assembly usando MetadataLoadContext](/samples/dotnet/samples/inspect-assembly-contents-using-metadataloadcontext/).
