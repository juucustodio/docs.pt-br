---
title: Introdução a Delegados
description: Saiba mais sobre os delegados neste artigo de visão geral que apresenta os conceitos básicos e discute as metas de design de linguagem para delegados.
ms.date: 02/02/2021
ms.technology: csharp-fundamentals
ms.assetid: 59b61d77-84e5-457b-8da5-fb5f24ca6ed6
ms.openlocfilehash: 72086301a6dd0552ab25baf732978802ad62669b
ms.sourcegitcommit: 4df8e005c074ceb1f978f007b222fe253be2baf3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/04/2021
ms.locfileid: "99548338"
---
# <a name="introduction-to-delegates"></a>Introdução a Delegados

Os delegados fornecem um mecanismo de *associação tardia* no .NET. Associação tardia significa que você cria um algoritmo em que o chamador também fornece pelo menos um método que implementa a parte do algoritmo.

Por exemplo, considere classificar uma lista de estrelas em um aplicativo de astronomia.
Você pode optar por classificar as estrelas por sua distância da terra ou a magnitude da estrela ou seu brilho percebido.

Em todos esses casos, o método Sort() faz essencialmente a mesma coisa: organiza os itens na lista com base em alguma comparação. O código que compara duas estrelas é diferente para cada uma das ordenações de classificação.

Esses tipos de soluções foram usados no software por meio século.
O conceito de delegado de linguagem C# fornece suporte de linguagem de primeira classe e segurança de tipos em torno do conceito.

Como você verá mais adiante nesta série, o código C# que você escreve para algoritmos como esse é tipo seguro e usa as regras de linguagem e o compilador para garantir que os tipos correspondam a argumentos e tipos de retorno.

[Ponteiros de função](~/_csharplang/proposals/csharp-9.0/function-pointers.md) foram adicionados ao C# 9 para cenários semelhantes, onde você precisa de mais controle sobre a Convenção de chamada. O código associado a um delegado é invocado usando um método virtual adicionado a um tipo delegate. Usando ponteiros de função, você pode especificar diferentes convenções.

## <a name="language-design-goals-for-delegates"></a>Metas de design da linguagem para delegados

Os designers de linguagem enumeraram várias metas para o recurso que eventualmente se tornaram delegados.

A equipe queria um constructo de linguagem comum que pudesse ser usada qualquer algoritmo de associação tardia. Os delegados permitem que os desenvolvedores aprendam um conceito e usem esse mesmo conceito em vários problemas de software diferentes.

Em segundo lugar, a equipe queria dar suporte a chamadas de método single ou multicast. (Delegados multicast são delegados que encadeiam várias chamadas de método.
Você verá exemplos [posteriormente nesta série](delegate-class.md).)

A equipe queria delegados para dar suporte à mesma segurança de tipos que os desenvolvedores esperam de todos os constructos de C#.

Por fim, a equipe reconheceu um padrão de evento que é um padrão específico em que delegados ou qualquer algoritmo de ligação tardia é muito útil. A equipe queria garantir que o código para delegados pudesse fornecer a base para o padrão de eventos .NET.

O resultado de todo esse trabalho era o suporte do delegado e do evento no C# e .NET. Os artigos restantes nesta seção abordarão os recursos de linguagem, o suporte à biblioteca e os idiomas comuns usados quando você trabalhar com delegados.

Você aprenderá sobre a palavra-chave `delegate` e qual código ela gera. Você aprenderá sobre os recursos na classe `System.Delegate` e como esses recursos são usados. Você aprenderá como criar delegados de segurança de tipos e como criar métodos que podem ser invocados por meio de delegados. Você também aprenderá a trabalhar com eventos e delegados usando expressões Lambda. Você verá onde delegados se tornam um dos blocos de construção para LINQ. Você aprenderá como os delegados são a base para o padrão de eventos .NET e como eles são diferentes.

Vamos começar.

[Próximo](delegate-class.md)
