---
title: Regras de confiabilidade (análise de código)
description: Saiba mais sobre as regras de confiabilidade da análise de código.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.reliabilityrules
helpviewer_keywords:
- rules, reliability
- reliability rules
- managed code analysis rules, reliability rules
author: gewarren
ms.author: gewarren
ms.openlocfilehash: a747dd4dcda351a1ddb0f3d069bb7bac895c32f8
ms.sourcegitcommit: 636af37170ae75a11c4f7d1ecd770820e7dfe7bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "96585090"
---
# <a name="reliability-rules"></a>Regras de confiabilidade

As regras de confiabilidade dão suporte à confiabilidade de aplicativo e biblioteca, como a memória correta e o uso de thread. As regras de confiabilidade incluem:

|Regra|Descrição|
|----------|-----------------|
|[CA2000: Descartar objetos antes de perder o escopo](ca2000.md)|Como pode ocorrer um evento excepcional que impedirá a execução do finalizador de um objeto, o objeto deve ser explicitamente descartado antes que todas as referências a ele estejam fora do escopo.|
|[CA2002: Não bloquear objetos com identidade fraca](ca2002.md)|Diz-se que um objeto tem uma identidade fraca quando puder ser acessado diretamente em todos os limites de domínio do aplicativo. Um thread que tente adquirir um bloqueio em um objeto com uma identidade fraca pode ser bloqueado por um segundo thread em um domínio de aplicativo diferente com um bloqueio no mesmo objeto.|
|[CA2007: não aguardar diretamente uma tarefa](ca2007.md)|Um método assíncrono [aguarda](../../../csharp/language-reference/operators/await.md) um <xref:System.Threading.Tasks.Task> diretamente.|
|[CA2008: Não criar tarefas sem passar um TaskScheduler](ca2008.md)|Uma operação de criação ou de continuação de tarefa usa uma sobrecarga de método que não especifica um <xref:System.Threading.Tasks.TaskScheduler> parâmetro.|
|[CA2009: Não chamar ToImmutableCollection em um valor ImmutableCollection](ca2009.md)|`ToImmutable` o método não era necessariamente chamado em uma coleção imutável do <xref:System.Collections.Immutable> namespace.|
|[CA2011: Não atribuir a propriedade em seu próprio setter](ca2011.md) | Uma propriedade recebeu acidentalmente um valor dentro de seu próprio [acessador set](../../../csharp/programming-guide/classes-and-structs/using-properties.md#the-set-accessor). |
|[CA2012: Usar ValueTasks corretamente](ca2012.md) | ValueTasks retornados de invocações de membro devem ser diretamente aguardados.  Tenta consumir um ValueTask várias vezes ou para acessar diretamente um resultado antes que seja conhecido a ser concluído pode resultar em uma exceção ou corrupção.  Ignorar essa ValueTask é provavelmente uma indicação de um bug funcional e pode prejudicar o desempenho. |
|[CA2013: Não usar ReferenceEquals com tipos de valor](ca2013.md) | Ao comparar valores usando <xref:System.Object.ReferenceEquals%2A?displayProperty=fullName> , se objA e objB forem tipos de valor, eles estarão em caixa antes de serem passados para o <xref:System.Object.ReferenceEquals%2A> método. Isso significa que, mesmo que objA e objB representem a mesma instância de um tipo de valor, o método, no <xref:System.Object.ReferenceEquals%2A> entanto, retorna false. |
|[CA2014: não use stackalloc em loops.](ca2014.md) | O espaço de pilha alocado por um stackalloc é liberado apenas no final da invocação do método atual.  Usá-lo em um loop pode resultar em aumento de pilha não associado e condições de estouro de pilha eventual. |
|[CA2015: não definir finalizadores para tipos derivados de MemoryManager &lt; T&gt;](ca2015.md) | Adicionar um finalizador a um tipo derivado de <xref:System.Buffers.MemoryManager%601> pode permitir que a memória seja liberada enquanto ainda estiver em uso por um <xref:System.Span%601> . |
|[CA2016: Encaminhe o parâmetro CancellationToken para os métodos que recebem um](ca2016.md) | Encaminhe o `CancellationToken` parâmetro para os métodos que usam um para garantir que as notificações de cancelamento da operação sejam propagadas corretamente ou repassem `CancellationToken.None` explicitamente para indicar, de forma intencional, não a propagação do token. |
