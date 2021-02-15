---
title: Regras de uso (análise de código)
description: Saiba mais sobre as regras de uso da análise de código.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.usagerules
helpviewer_keywords:
- rules, usage
- managed code analysis rules, usage rules
- usage rules
author: gewarren
ms.author: gewarren
ms.openlocfilehash: c8b14d2f92502d5a82e41a322e599745bdcf8b85
ms.sourcegitcommit: a6bd4cad438fe479cbd112eae10f2cd449f06e40
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2020
ms.locfileid: "96585439"
---
# <a name="usage-rules"></a>Regras de uso

As regras de uso dão suporte ao uso adequado do .NET.

## <a name="in-this-section"></a>Nesta seção

|Regra|Descrição|
|----------|-----------------|
|[CA1801: Examinar parâmetros não utilizados](ca1801.md)|Uma assinatura de método inclui um parâmetro que não é usado no corpo do método.|
|[CA1816: Chamar GC.SuppressFinalize corretamente](ca1816.md)|Um método que é uma implementação de Dispose não chama `GC.SuppressFinalize` ; ou um método que não é uma implementação de `Dispose` chamadas `GC.SuppressFinalize` ; ou um método chama `GC.SuppressFinalize` e passa algo diferente de `this` ( `Me` em Visual Basic).|
|[CA2200: Relançar para preservar detalhes da pilha](ca2200.md)|Uma exceção é lançada novamente e a exceção é especificada explicitamente na instrução throw. Se uma exceção for lançada novamente pela especificação da exceção na instrução throw, a lista de chamadas de método entre o método original que lançou a exceção e o método atual será perdida.|
|[CA2201: Não acionar tipos de exceção reservados](ca2201.md)|Isso torna o erro original difícil de detectar e depurar.|
|[CA2207: Inicializar campos estáticos de tipo de valor em linha](ca2207.md)|Um tipo de valor declara um construtor estático explícito. Para corrigir uma violação dessa regra, inicialize todos os dados estáticos quando declarados e remova o construtor estático.|
|[CA2208: Criar instância de exceções de argumento corretamente](ca2208.md)|For feita uma chamada para o construtor padrão (sem parâmetros) de um tipo de exceção que seja ou derive de ArgumentException, ou um argumento de cadeia de caracteres incorreto é passado para um construtor com parâmetros de um tipo de exceção que seja ou derive de ArgumentException.|
|[CA2211: Campos não constantes não devem ser visíveis](ca2211.md)|Campos estáticos que não são constantes ou somente leitura não são thread-safe. O acesso a esse campo deve ser cuidadosamente controlado e requer técnicas de programação avançadas para sincronizar o acesso ao objeto de classe.|
|[CA2213: Campos descartáveis devem ser descartados](ca2213.md)|Um tipo que implementa <xref:System.IDisposable?displayProperty=fullName> declara campos que são de tipos que também implementam `IDisposable` . O `Dispose` método do campo não é chamado pelo `Dispose` método do tipo declarativo.|
|[CA2214: Não chamar métodos substituíveis em construtores](ca2214.md)|Quando um construtor chama um método virtual, é possível que o construtor da instância que invoca o método não tenha sido executado.|
|[CA2215: Métodos Dispose devem chamar o descarte da classe base](ca2215.md)|Se um tipo for herdado de um tipo descartável, ele deverá chamar o `Dispose` método do tipo base de seu próprio `Dispose` método.|
|[CA2216: Tipos descartáveis devem declarar o finalizador](ca2216.md)|Um tipo que implementa <xref:System.IDisposable?displayProperty=fullName> e tem campos que sugerem o uso de recursos não gerenciados, não implementa um finalizador conforme descrito pelo `Object.Finalize` .|
|[CA2217: Não marcar enumerações com FlagsAttribute](ca2217.md)|Uma enumeração visível externamente é marcada com `FlagsAttribute` , e tem um ou mais valores que não são potências de duas ou uma combinação de outros valores definidos na enumeração.|
|[CA2218: Substituir GetHashCode ao substituir Equals](ca2218.md)|Um tipo público substitui <xref:System.Object.Equals%2A?displayProperty=fullName> , mas não substitui <xref:System.Object.GetHashCode%2A?displayProperty=fullName> .|
|[CA2219: Não acionar exceções em cláusulas de exceção](ca2219.md)|Quando uma exceção é acionada em uma cláusula finally ou fault, a nova exceção oculta a exceção ativa. Quando uma exceção é acionada em uma cláusula de filtro, o tempo de execução captura silenciosamente a exceção. Isso torna o erro original difícil de detectar e depurar.|
|[CA2224: Substituir equals ao sobrecarregar operador equals](ca2224.md)|Um tipo público implementa o operador de igualdade, mas não substitui <xref:System.Object.Equals%2A?displayProperty=fullName> .|
|[CA2225: Sobrecargas de operador têm alternativas nomeadas](ca2225.md)|Uma sobrecarga de operador foi detectada, e o método alternativo nomeado esperado não foi encontrado. O membro alternativo nomeado fornece acesso à mesma funcionalidade que o operador e é fornecido para desenvolvedores que programam em idiomas que não dão suporte a operadores sobrecarregados.|
|[CA2226: Operadores devem ter sobrecargas simétricas](ca2226.md)|Um tipo implementa o operador de igualdade ou desigualdade e não implementa o operador oposto.|
|[CA2227: Propriedades de coleção devem ser somente leitura](ca2227.md)|Uma propriedade collection gravável permite que um usuário substitua a coleção por uma coleção diferente. Uma propriedade somente leitura evita que a coleção seja substituída, mas ainda permite que membros individuais sejam definidos.|
|[CA2229: Implementar construtores de serialização](ca2229.md)|Para corrigir uma violação dessa regra, implemente o construtor de serialização. Para uma classe lacrada, torne o construtor particular; do contrário, deixe-o protegido.|
|[CA2231: Sobrecarregar operador equals ao substituir ValueType.Equals](ca2231.md)|Um tipo de valor substitui `Object.Equals` mas não implementa o operador de igualdade.|
|[CA2234: Passar objetos System.Uri em vez de cadeias de caracteres](ca2234.md)|Foi feita uma chamada para um método com um parâmetro de cadeia de caracteres cujo nome contém "uri", "URI", "urn", "URN", "url" ou "URL".  O tipo declarativo do método contém uma sobrecarga de método correspondente que tem um <xref:System.Uri?displayProperty=fullName> parâmetro.|
|[CA2235: Marcar todos os campos não serializáveis](ca2235.md)|Um campo de instância de um tipo que não seja serializável é declarado em um tipo que é serializável.|
|[CA2237: Marcar tipos ISerializable com SerializableAttribute](ca2237.md)|Para ser reconhecido pelo Common Language Runtime como serializável, os tipos devem ser marcados com o atributo SerializableAttribute, mesmo que o tipo use uma rotina de serialização personalizada por meio da implementação da `ISerializable` interface.|
|[CA2241: Fornecer argumentos corretos para métodos de formatação](ca2241.md)|O argumento de formato passado para não <xref:System.String.Format%2A?displayProperty=nameWithType> contém um item de formato que corresponde a cada argumento de objeto ou vice-versa.|
|[CA2242: Testar para NaN corretamente](ca2242.md)|Essa expressão testa um valor em relação a `Single.Nan` ou `Double.Nan` . Use `Single.IsNan(Single)` ou `Double.IsNan(Double)` para testar o valor.|
|[CA2243: Literais de cadeias de caracteres de atributo devem ser analisados corretamente](ca2243.md)|O parâmetro literal da cadeia de caracteres de um atributo não é analisado corretamente para uma URL, um GUID ou uma versão.|
|[CA2244: Não duplicar inicializações de elementos indexados](ca2244.md)|Um inicializador de objeto tem mais de um inicializador de elemento indexado com o mesmo índice de constante. Todos, exceto o último inicializador, são redundantes.|
|[CA2245: Não atribuir uma propriedade a si mesma](ca2245.md)|Uma propriedade foi acidentalmente atribuída a ela mesma.|
|[CA2246: Não designar um símbolo e o membro dele na mesma instrução](ca2246.md)|Não é recomendável atribuir um símbolo e seu membro, ou seja, um campo ou uma propriedade, na mesma instrução. Não fica claro se o acesso de membro foi projetado para usar o valor antigo do símbolo antes da atribuição ou o novo valor da atribuição nesta instrução.|
|[CA2247: O argumento passado para o construtor TaskCompletionSource deve ser a enumeração TaskCreationOptions em vez da enumeração TaskContinuationOptions](ca2246.md)|TaskCompletionSource tem construtores que usam TaskCreationOptions que controlam a tarefa subjacente e construtores que assumem o estado do objeto armazenado na tarefa.  Passar acidentalmente um TaskContinuationOptions em vez de um TaskCreationOptions resultará na chamada que trata as opções como estado.|
|[CA2248: forneça o argumento ' Enum ' correto para ' Enum. HasFlag '](ca2248.md)|O tipo de enumeração passado como um argumento para a `HasFlag` chamada do método é diferente do tipo de enumeração de chamada.|
|[CA2249: Considerar o uso de String.Contains em vez de String.IndexOf](ca2249.md)|Chamadas para `string.IndexOf` onde o resultado é usado para verificar a presença ou a ausência de uma subcadeia de caracteres podem ser substituídas por `string.Contains` .|
