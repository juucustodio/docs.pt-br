---
description: 'Saiba mais sobre: Associação de dados'
title: Associação de dados
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: cbec8b02-a1e8-4ae8-a83b-bb5190413ac5
ms.openlocfilehash: d5566fae505f5c5cd54b2a2990cf04169211003c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99729556"
---
# <a name="data-binding"></a>Associação de dados

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] dá suporte à associação a controles comuns, como controles de grade. Especificamente, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o define os padrões básicos para a associação a uma grade de dados e o processamento de associação mestre-Detail, tanto com relação à exibição quanto à atualização.

## <a name="underlying-principle"></a>Princípio subjacente

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] traduz consultas LINQ para SQL para execução em um banco de dados. Os resultados são `IEnumerable` fortemente tipados. Como esses objetos são objetos CLR (Common Language Runtime) comuns, a vinculação de dados de objetos comuns pode ser usada para exibir os resultados. Por outro lado, as operações de alteração (inserções, atualizações e exclusões) exigem etapas adicionais.

## <a name="operation"></a>Operação

Implicitamente, a associação aos controles do Windows Forms é realizada por meio da implementação de <xref:System.ComponentModel.IListSource>. Fontes de dados genéricas <xref:System.Data.Linq.Table%601> ( `Table<T>` em C# ou `Table(Of T)` Visual Basic) e genéricas foram `DataQuery` atualizadas para implementar <xref:System.ComponentModel.IListSource> . Os mecanismos de associação de dados (Windows Forms e Windows Presentation Foundation) da interface do usuário testam se sua fonte de dados implementa <xref:System.ComponentModel.IListSource> . Portanto, escrever um efeito direto de uma consulta para uma fonte de dados de um controle chama implicitamente [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] a geração de coleção, como no exemplo a seguir:

[!code-csharp[DLinqDataBinding#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqDataBinding/cs/Program.cs#1)]
[!code-vb[DLinqDataBinding#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqDataBinding/vb/Module1.vb#1)]

O mesmo ocorre com o Windows Presentation Foundation:

[!code-csharp[DLinqDataBinding#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqDataBinding/cs/Program.cs#2)]
[!code-vb[DLinqDataBinding#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqDataBinding/vb/Module1.vb#2)]

As gerações de coleção são implementadas por <xref:System.Data.Linq.Table%601> genérico e por `DataQuery` genérico em <xref:System.ComponentModel.IListSource.GetList%2A>.

## <a name="ilistsource-implementation"></a>Implementação de IListSource

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] implementa <xref:System.ComponentModel.IListSource> em dois locais:

- A fonte de dados é <xref:System.Data.Linq.Table%601> : [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] procura a tabela para preencher uma `DataBindingList` coleção que mantém uma referência na tabela.

- A fonte de dados é um <xref:System.Linq.IQueryable%601>. Há dois cenários:

  - Se o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] encontrar o subjacente <xref:System.Data.Linq.Table%601> do <xref:System.Linq.IQueryable%601> , a origem permitirá a edição e a situação será a mesma do primeiro ponto de marcador.

  - Se [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não for possível localizar o subjacente <xref:System.Data.Linq.Table%601> , a origem não permitirá a edição (por exemplo, `groupby` ). [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] procura a consulta para preencher um genérico `SortableBindingList` , que é um simples <xref:System.ComponentModel.BindingList%601> que implementa o recurso de classificação para entidades T para uma determinada propriedade.

## <a name="specialized-collections"></a>Coleções especializadas

Para muitos recursos descritos anteriormente neste documento, <xref:System.ComponentModel.BindingList%601> foi especializado para algumas classes diferentes. Essas classes são `SortableBindingList` genérica e `DataBindingList`genérica. As duas são declaradas como internas.

### <a name="generic-sortablebindinglist"></a>SortableBindingList genérica

Essa classe herda de <xref:System.ComponentModel.BindingList%601> e é uma versão classificável de <xref:System.ComponentModel.BindingList%601>. A classificação é uma solução na memória e nunca entra em contato com o próprio banco de dados. <xref:System.ComponentModel.BindingList%601> implementa <xref:System.ComponentModel.IBindingList>, mas, por padrão, não dá suporte à classificação. No entanto, <xref:System.ComponentModel.BindingList%601> implementa <xref:System.ComponentModel.IBindingList> com métodos de *núcleo* virtual. Você pode substituir esses métodos facilmente. `SortableBindingList` genérica substitui <xref:System.ComponentModel.BindingList%601.SupportsSortingCore%2A>, <xref:System.ComponentModel.BindingList%601.SortPropertyCore%2A>, <xref:System.ComponentModel.BindingList%601.SortDirectionCore%2A> e <xref:System.ComponentModel.BindingList%601.ApplySortCore%2A>. `ApplySortCore` é chamada por <xref:System.ComponentModel.IBindingList.ApplySort%2A> e classifica a lista de itens de T para uma determinada propriedade.

Uma exceção será gerada se a propriedade não pertencer a T.

Para obter a classificação, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o cria uma `SortableBindingList.PropertyComparer` classe genérica que herda de genérico e implementa um comparador <xref:System.Collections.Generic.Comparer%601.System%23Collections%23IComparer%23Compare%2A> padrão para um determinado tipo T, a `PropertyDescriptor` e uma direção. Essa classe cria dinamicamente um `Comparer` de T onde T é `PropertyType` de `PropertyDescriptor`. Em seguida, o comparador padrão é recuperado do `Comparer` estático genérico. Uma instância padrão é obtida usando reflexão.

A `SortableBindingList` genérica também é a classe base para `DataBindingList`. A `SortableBindingList` genérica oferece dois métodos virtuais para suspender ou retomar o controle de itens adicionar/remover. Esses dois métodos podem ser usados para recursos base como classificação, mas serão realmente implementados por classes superiores, como `DataBindingList`genérica.

### <a name="generic-databindinglist"></a>DataBindingList genérica

Esta classe herda de `SortableBindingLIst`genérica. A `DataBindingList` genérica mantém uma referência na `Table` genérica subjacente da `IQueryable` genérica usada para o preenchimento inicial da coleção. A `DatabindingList` genérica adiciona o controle para adicionar/remover itens à coleção substituindo `InsertItem`() e `RemoveItem`(). Também implementa o recurso abstrato suspender/retomar para tornar o controle condicional. Esse recurso faz a `DataBindingList` genérica tirar proveito de todo o uso polimorfo do recurso de rastreamento das classes pai.

## <a name="binding-to-entitysets"></a>Associando a EntitySets

A associação a `EntitySet` é um caso especial porque `EntitySet` já é uma coleção que implementa <xref:System.ComponentModel.IBindingList>. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] Adiciona classificação e cancelamento ( <xref:System.ComponentModel.ICancelAddNew> ) suporte. Uma classe `EntitySet` usa uma lista interna para armazenar entidades. Essa lista é uma coleção de baixo nível baseada em uma matriz genérica, a classe genérica `ItemList`.

### <a name="adding-a-sorting-feature"></a>Adicionando um recurso de classificação

As matrizes oferecem um método `Array.Sort()` de classificação () que você pode usar com um `Comparer` de T. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o usa a `SortableBindingList.PropertyComparer` classe genérica descrita anteriormente neste tópico para obter isso `Comparer` para a propriedade e a direção a ser classificada. Um método `ApplySort` é adicionado ao `ItemList` genérico para chamar esse recurso.

No lado de `EntitySet`, você agora precisa declarar suporte à classificação:

- <xref:System.ComponentModel.IBindingList.SupportsSorting%2A> retorna `true`.

- <xref:System.ComponentModel.IBindingList.ApplySort%2A> chama `entities.ApplySort()` e, em seguida, `OnListChanged()`.

- As propriedades <xref:System.ComponentModel.IBindingList.SortDirection%2A> e <xref:System.ComponentModel.IBindingList.SortProperty%2A> expõem a definição de classificação atual, que é armazenada em membros locais.

Quando você usa um System. Windows. Forms. BindingSource e associa um EntitySet \<TEntity> a System. Windows. Forms. BindingSource. DataSource, você deve chamar EntitySet \<TEntity> . GetNewBindingList atualizar BindingSource. List.

Se você usar um System. Windows. Forms. BindingSource e definir a Propriedade BindingSource. DataMember e definir BindingSource. DataSource como uma classe que tem uma propriedade chamada em BindingSource. DataMember que expõe o EntitySet \<TEntity> , não será necessário chamar EntitySet \<TEntity> . GetNewBindingList atualizar a BindingSource. List, mas você perde a capacidade de classificação.

## <a name="caching"></a>Cache

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] as consultas implementam <xref:System.ComponentModel.IListSource.GetList%2A> . Quando a classe BindingSource do Windows Forms encontra essa interface, ela chama GetList() três vezes para uma única conexão. Para contornar essa situação, o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] implementa um cache por instância para armazenar e sempre retornar a mesma coleção gerada.

## <a name="cancellation"></a>Cancelamento

O <xref:System.ComponentModel.IBindingList> define um método <xref:System.ComponentModel.IBindingList.AddNew%2A> que é usado pelos controles para criar um novo item de uma coleção associada. O controle `DataGridView` mostra esse recurso muito bem quando a última linha visível contém uma estrela em seu cabeçalho. A estrela mostra que você pode adicionar um novo item.

Além desse recurso, uma coleção também pode implementar <xref:System.ComponentModel.ICancelAddNew>. Esse recurso permite que os controles cancelem ou validem se o novo item editado foi validado ou não.

<xref:System.ComponentModel.ICancelAddNew> é implementado em todas as [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] coleções de ligação de ligações (genéricas `SortableBindingList` e genéricas `EntitySet` ). Em ambas as implementações, o código é executado da seguinte maneira:

- Permite que itens sejam inseridos e removidos da coleção.

- Não controla as alterações desde que a interface do usuário não confirme a edição.

- Não controla as alterações desde que a edição seja cancelada (<xref:System.ComponentModel.ICancelAddNew.CancelNew%2A>).

- Permite controlar quando a edição é confirmada (<xref:System.ComponentModel.ICancelAddNew.EndNew%2A>).

- Permite que a coleção se comporte normalmente se o novo item não for proveniente de <xref:System.ComponentModel.IBindingList.AddNew%2A>.

## <a name="troubleshooting"></a>Solução de problemas

Esta seção chama vários itens que podem ajudar a resolver problemas de seus aplicativos de vinculação de dados do [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].

- Você deve usar propriedades; usar somente campos não é suficiente. O Windows Forms requer esse uso.

- Por padrão, `image` , `varbinary` e os `timestamp` tipos de banco de dados são mapeados para a matriz de bytes. Como `ToString()` não é suportado nesse cenário, esses objetos não podem ser exibidos.

- Um membro de classe mapeado para uma chave primária tem um setter, mas [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não dá suporte à alteração de identidade de objeto. Portanto, a chave primária/exclusiva que é usada no mapeamento não pode ser atualizada no banco de dados. Uma alteração na grade causa uma exceção quando você chama <xref:System.Data.Linq.DataContext.SubmitChanges%2A> .

- Se uma entidade estiver associada em duas grades separadas (por exemplo, uma mestra e outra de detalhes), `Delete` na grade mestra não será propagado para a grade de detalhes.

## <a name="see-also"></a>Consulte também

- [Informações gerais](background-information.md)
