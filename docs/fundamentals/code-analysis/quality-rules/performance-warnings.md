---
title: Regras de desempenho (análise de código)
description: Saiba mais sobre as regras de desempenho da análise de código.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.performancerules
helpviewer_keywords:
- rules, performance
- performance rules
- performance, rules
- managed code analysis rules, performance rules
author: gewarren
ms.author: gewarren
ms.openlocfilehash: 4409cc46eb73f13f8e59d7a51899da27035bb6af
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "96584724"
---
# <a name="performance-rules"></a>Regras de desempenho

As regras de desempenho dão suporte a bibliotecas e aplicativos de alto desempenho.

## <a name="in-this-section"></a>Nesta seção

| Regra | Descrição |
| - | - |
| [CA1802: Usar literais quando apropriado](ca1802.md) | Um campo é declarado estático e somente leitura (compartilhado e ReadOnly em Visual Basic) e é inicializado com um valor que é computáveis no momento da compilação. Como o valor atribuído ao campo de destino é computáveis em tempo de compilação, altere a declaração para um campo const (const no Visual Basic) para que o valor seja calculado em tempo de compilação em vez de em tempo de execução. |
| [CA1805: Não inicializar desnecessariamente](ca1805.md) | O tempo de execução do .NET inicializa todos os campos de tipos de referência para seus valores padrão antes de executar o construtor. Na maioria dos casos, a inicialização explícita de um campo para seu valor padrão é redundante, o que aumenta os custos de manutenção e pode prejudicar o desempenho (como com o maior tamanho do assembly). |
| [CA1806: Não ignorar resultados do método](ca1806.md) | Um novo objeto é criado, mas nunca usado, ou um método que cria e retorna uma nova cadeia de caracteres é chamado e a nova cadeia de caracteres nunca é usada ou um método Component Object Model (COM) ou P/Invoke Retorna um HRESULT ou um código de erro que nunca é usado. |
| [CA1810: Inicializar campos estáticos de tipo de referência em linha](ca1810.md) | Quando um tipo declara um construtor estático explícito, o compilador JIT (just-in-time) adiciona uma verificação a cada método estático e construtor de instância do tipo para garantir que o construtor estático tenha sido chamado anteriormente. As verificações de construtor estático podem diminuir o desempenho. |
| [CA1812: Evitar classes internas sem instâncias](ca1812.md) | Uma instância de um tipo no nível de assembly não é criada pelo código no assembly. |
| [CA1813: Evitar atributos não selados](ca1813.md) | O .NET fornece métodos para recuperar atributos personalizados. Por padrão, esses métodos pesquisam a hierarquia de herança do atributo. A validação do atributo elimina a pesquisa na hierarquia de herança e pode melhorar o desempenho. |
| [CA1814: Preferir matrizes denteadas a matrizes multidimensionais](ca1814.md) | Uma matriz denteada é uma matriz cujos elementos são matrizes. As matrizes que compõem os elementos podem ser de tamanhos diferentes, o que pode resultar em menos espaço desperdiçado para alguns conjuntos de dados. |
| [CA1815: Substituir equals e o operador equals em tipos de valor](ca1815.md) | Para tipos de valor, a implementação herdada de Equals usa a biblioteca Reflection e compara o conteúdo de todos os campos. Reflection é computacionalmente cara, e pode ser desnecessário comparar a igualdade de cada campo. Se você espera que os usuários comparem ou classifiquem instâncias, ou usem instâncias como chaves de tabela de hash, o tipo de valor deverá implementar Equals. |
| [CA1819: Propriedades não devem retornar matrizes](ca1819.md) | As matrizes retornadas por propriedades não são protegidas por gravação, mesmo que a propriedade seja somente leitura. Para manter a matriz à prova de adulteração, a propriedade deve retornar uma cópia da matriz. Normalmente, os usuários não compreenderão as implicações adversas no desempenho de chamar uma propriedade assim. |
| [CA1820: Testar para verificar se há cadeias de caracteres vazias usando o tamanho da cadeia de caracteres](ca1820.md) | A comparação de cadeias de caracteres usando-se a propriedade String.Length ou o método String.IsNullOrEmpty é significativamente mais rápida do que o uso de Equals. |
| [CA1821: Remover finalizadores vazios](ca1821.md) | Sempre que possível, evite finalizadores por conta da sobrecarga adicional no desempenho envolvida no acompanhamento do tempo de vida do objeto. Um finalizador vazio incorre em sobrecarga adicional sem nenhum benefício. |
| [CA1822: Marcar membros como estáticos](ca1822.md) | Membros que não acessam dados de instância ou métodos de instância de chamada podem ser marcados como estáticos (compartilhados em Visual Basic). Depois que você marcar os métodos como estáticos, o compilador emitirá sites de chamada não virtuais para esses membros. Isso pode proporcionar um ganho de desempenho mensurável para o código sensível ao desempenho. |
| [CA1823: Evitar campos particulares não utilizados](ca1823.md) | Foram detectados campos particulares que aparentemente não são acessados no assembly. |
| [CA1824: Marque assemblies com NeutralResourcesLanguageAttribute](ca1824.md) | O atributo NeutralResourcesLanguage informa o Gerenciador de recursos da linguagem que foi usada para exibir os recursos de uma cultura neutra para um assembly. Isso melhora o desempenho da pesquisa para o primeiro recurso carregado e pode reduzir o conjunto de trabalho. |
| [CA1825: Evitar alocações de matriz de comprimento zero](ca1825.md) | A inicialização de uma matriz de comprimento zero leva à alocação de memória desnecessária. Em vez disso, use a instância de matriz vazia estaticamente alocada chamando <xref:System.Array.Empty%2A?displayProperty=nameWithType> . A alocação de memória é compartilhada entre todas as invocações desse método. |
| [CA1826: Usar a propriedade em vez do método Linq Enumerable](ca1826.md) | <xref:System.Linq.Enumerable> O método LINQ foi usado em um tipo que dá suporte a uma propriedade equivalente e mais eficiente. |
| [CA1827: Não usar Count/LongCount quando Any puder ser usado](ca1827.md) | <xref:System.Linq.Enumerable.Count%2A> o <xref:System.Linq.Enumerable.LongCount%2A> método or foi usado onde o <xref:System.Linq.Enumerable.Any%2A> método seria mais eficiente. |
| [CA1828: Não usar CountAsync/LongCountAsync quando AnyAsync puder ser usado](ca1828.md) | <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.CountAsync%2A> o <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.LongCountAsync%2A> método or foi usado onde o <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.AnyAsync%2A> método seria mais eficiente. |
| [CA1829: Usar a propriedade Length/Count em vez do método Enumerable.Count](ca1829.md) | <xref:System.Linq.Enumerable.Count%2A> O método LINQ foi usado em um tipo que dá suporte a uma propriedade equivalente, mais eficiente `Length` ou `Count` . |
| [CA1830: Preferir os métodos Acrescentar e Inserir fortemente tipados provoca uma sobrecarga no StringBuilder](ca1830.md) | <xref:System.Text.StringBuilder.Append%2A> e <xref:System.Text.StringBuilder.Insert%2A> fornecem sobrecargas para vários tipos além de System. String.  Quando possível, prefira as sobrecargas fortemente tipadas usando ToString () e a sobrecarga baseada em cadeia de caracteres. |
| [CA1831: Usar AsSpan em vez de indexadores baseados em intervalo na cadeia de caracteres quando apropriado](ca1831.md) | Ao usar um indexador de intervalo em uma cadeia de caracteres e atribuir implicitamente o valor a um &lt; tipo de caractere ReadOnlySpan &gt; , o método <xref:System.String.Substring%2A?#System_String_Substring_System_Int32_System_Int32_> será usado em vez de <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> , que produz uma cópia da parte solicitada da cadeia de caracteres. |
| [CA1832: Usar AsSpan ou AsMemory em vez de indexadores baseados em intervalo para obter a parte ReadOnlySpan ou ReadOnlyMemory de uma matriz](ca1832.md) | Ao usar um indexador de intervalo em uma matriz e atribuir implicitamente o valor a um <xref:System.ReadOnlySpan%601> <xref:System.ReadOnlyMemory%601> tipo ou, o método <xref:System.Runtime.CompilerServices.RuntimeHelpers.GetSubArray%2A> será usado em vez de, o <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> que produzirá uma cópia da parte solicitada da matriz. |
| [CA1833: Usar AsSpan ou AsMemory em vez de indexadores baseados em intervalo para obter a parte Span ou Memory de uma matriz](ca1833.md) | Ao usar um indexador de intervalo em uma matriz e atribuir implicitamente o valor a um <xref:System.Span%601> <xref:System.Memory%601> tipo ou, o método <xref:System.Runtime.CompilerServices.RuntimeHelpers.GetSubArray%2A> será usado em vez de, o <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> que produzirá uma cópia da parte solicitada da matriz. |
| [CA1834: usar StringBuilder.Append (char) para cadeias de caracteres únicas](ca1834.md) | <xref:System.Text.StringBuilder> tem uma `Append` sobrecarga que usa `char` como argumento. Prefira chamar a `char` sobrecarga para melhorar o desempenho. |
| [CA1835: prefira as sobrecargas baseadas em Memory' para ' ReadAsync ' e ' WriteAsync '](ca1835.md) | ' Stream ' tem uma sobrecarga ' ReadAsync ' que usa um ' byte de memória &lt; &gt; ' como o primeiro argumento e uma sobrecarga ' WriteAsync ' que usa um ' ReadOnlyMemory &lt; byte &gt; ' como o primeiro argumento. Prefira chamar as sobrecargas com base na memória, que são mais eficientes. |
| [CA1836: preferir `IsEmpty` `Count` quando disponível](ca1836.md) | Prefira `IsEmpty` a propriedade que seja mais eficiente do que `Count` , `Length` <xref:System.Linq.Enumerable.Count%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29> ou <xref:System.Linq.Enumerable.LongCount%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29> para determinar se o objeto contém ou não itens. |
| [CA1837: usar `Environment.ProcessId` em vez de `Process.GetCurrentProcess().Id`](ca1837.md) | `Environment.ProcessId` é mais simples e mais rápido do que `Process.GetCurrentProcess().Id` . |
| [CA1838: Evite `StringBuilder` parâmetros para P/Invokes](ca1838.md) | O marshaling de `StringBuilder` sempre cria uma cópia de buffer nativo, resultando em várias alocações para uma operação de marshaling. |
