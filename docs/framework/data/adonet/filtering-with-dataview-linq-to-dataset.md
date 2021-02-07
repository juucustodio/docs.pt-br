---
description: 'Saiba mais sobre: filtragem com DataView (LINQ to DataSet)'
title: Filtrando com DataView (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5632d74a-ff53-4ea7-9fe7-4a148eeb1c68
ms.openlocfilehash: 152b2e1d82cd5cf0eac24fd952de26d83fbffe58
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724135"
---
# <a name="filtering-with-dataview-linq-to-dataset"></a>Filtrando com DataView (LINQ to DataSet)

A capacidade de filtrar dados usando critérios específicos e apresentá-los para um cliente através de um controle da interface do usuário é um aspecto importante da vinculação de dados. O <xref:System.Data.DataView> fornece várias maneiras para filtrar dados e retornar subconjuntos de linhas de dados que atendem a critérios específicos de filtro. Além dos recursos de filtragem baseada em cadeia de caracteres, <xref:System.Data.DataView> o também fornece a capacidade de usar expressões LINQ para os critérios de filtragem. As expressões LINQ permitem operações de filtragem muito mais complexas e poderosas do que a filtragem baseada em cadeia de caracteres.  
  
 Há duas maneiras para filtrar dados usando um <xref:System.Data.DataView>:  
  
- Crie um <xref:System.Data.DataView> de uma consulta de LINQ to DataSet com uma cláusula WHERE.  
  
- Use os recursos de filtragem baseados em cadeia de caracteres existentes de <xref:System.Data.DataView>.  
  
## <a name="creating-dataview-from-a-query-with-filtering-information"></a>Criando um DataView a partir de uma consulta com informações de filtragem  

 Um <xref:System.Data.DataView> objeto pode ser criado a partir de uma consulta LINQ to DataSet. Se a consulta contiver uma cláusula `Where`, o <xref:System.Data.DataView> será criado com as informações de filtragem da consulta. A expressão na cláusula `Where` é usada para determinar quais linhas de dados serão incluídas no <xref:System.Data.DataView> e é a base para o filtro.  
  
 Os filtros baseados em expressão oferecem uma filtragem mais avançada e complexa do que os filtros mais simples baseados em cadeia de caracteres. Os filtros baseados em cadeia de caracteres e baseados em expressão são mutuamente excludentes. Quando a <xref:System.Data.DataView.RowFilter%2A> baseada em cadeia de caracteres for definida após <xref:System.Data.DataView> ser criado a partir de uma consulta, o filtro baseado em expressão inferido da consulta será limpo.  
  
> [!NOTE]
> Na maioria dos casos, as expressões usadas para filtragem não devem ter efeitos colaterais e devem ser determinísticas. Além disso, as expressões não devem conter lógica que dependa de um número definido de execuções, pois as operações de filtragem podem ser executadas qualquer número de vezes.  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir consulta a tabela SalesOrderDetail para pedidos com uma quantidade maior que 2 e menor que 6; cria <xref:System.Data.DataView> a partir da consulta e associa o objeto <xref:System.Data.DataView> a uma <xref:System.Windows.Forms.BindingSource>:  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhere](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhere)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhere](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhere)]  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir cria um <xref:System.Data.DataView> de uma consulta para os pedidos feitos após 6 de junho de 2001:  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhere3](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhere3)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhere3](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhere3)]  
  
### <a name="example"></a>Exemplo  

 A filtragem também pode ser combinada com a classificação. O exemplo a seguir cria um <xref:System.Data.DataView> de uma consulta para os contatos cujo sobrenome comece com "S" e classificados por sobrenome e depois nome:  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhereOrderByThenBy](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhereorderbythenby)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhereOrderByThenBy](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhereorderbythenby)]  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir usa o algoritmo SoundEx para localizar os contatos cujo sobrenome é semelhante a "Zhu". O algoritmo SoundEx é implementado no método SoundEx.  
  
 [!code-csharp[DP DataView Samples#LDVSoundExFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvsoundexfilter)]
 [!code-vb[DP DataView Samples#LDVSoundExFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvsoundexfilter)]  
  
 SoundEx é um algoritmo fonético usado para indexação de nomes por som, pois eles são pronunciados em inglês, originalmente desenvolvidos pelo censo Bureau dos EUA. O método SoundEx retorna um código de quatro caracteres para um nome que consiste em uma letra em inglês seguida por três números. A letra é a primeira letra do nome e os números codificam as consoantes restantes no nome. Os nomes de som semelhantes compartilham o mesmo código SoundEx. A implementação de SoundEx usada no método SoundEx do exemplo anterior é mostrada aqui:  
  
 [!code-csharp[DP DataView Samples#SoundEx](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#soundex)]
 [!code-vb[DP DataView Samples#SoundEx](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#soundex)]  
  
## <a name="using-the-rowfilter-property"></a>Usando a propriedade RowFilter  

 A funcionalidade de filtragem baseada em cadeia de caracteres existente do <xref:System.Data.DataView> ainda funciona no contexto LINQ to DataSet. Para obter mais informações sobre filtragem baseada em cadeia de caracteres <xref:System.Data.DataView.RowFilter%2A> , consulte [classificando e Filtrando dados](./dataset-datatable-dataview/sorting-and-filtering-data.md).  
  
 O exemplo a seguir cria um <xref:System.Data.DataView> da tabela de contatos e define a propriedade <xref:System.Data.DataView.RowFilter%2A> para retornar as linhas onde o sobrenome do contatos é "Zhu":  
  
 [!code-csharp[DP DataView Samples#LDVRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvrowfilter)]
 [!code-vb[DP DataView Samples#LDVRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvrowfilter)]  
  
 Depois <xref:System.Data.DataView> que um tiver sido criado a partir de uma <xref:System.Data.DataTable> consulta ou LINQ to DataSet, você poderá usar a <xref:System.Data.DataView.RowFilter%2A> propriedade para especificar subconjuntos de linhas com base em seus valores de coluna. Os filtros baseados em cadeia de caracteres e baseados em expressão são mutuamente excludentes. A definição da <xref:System.Data.DataView.RowFilter%2A> propriedade limpará a expressão de filtro inferida da consulta LINQ to DataSet e a expressão de filtro não poderá ser redefinida.  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhereSetRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywheresetrowfilter)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhereSetRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywheresetrowfilter)]  
  
 Se você quiser retornar os resultados de uma consulta específica nos dados, ao contrário de fornecer uma exibição dinâmica de um subconjunto dos dados, você poderá usar os métodos <xref:System.Data.DataView.Find%2A> ou <xref:System.Data.DataView.FindRows%2A> de <xref:System.Data.DataView>, em vez de definir a propriedade <xref:System.Data.DataView.RowFilter%2A>. A propriedade <xref:System.Data.DataView.RowFilter%2A> é melhor usada em um aplicativo associado a dados onde um controle de associação exibe resultados filtrados. Definir a propriedade <xref:System.Data.DataView.RowFilter%2A> reconstrói o índice para os dados, adicionando a sobrecarga ao seu aplicativo e diminuindo o desempenho. Os métodos <xref:System.Data.DataView.Find%2A> e <xref:System.Data.DataView.FindRows%2A> usam o índice atual sem exigir que o índice seja reconstruído. Se você chamar <xref:System.Data.DataView.Find%2A> ou <xref:System.Data.DataView.FindRows%2A> apenas uma vez, deverá usar o <xref:System.Data.DataView> existente. Se você chamar <xref:System.Data.DataView.Find%2A> ou <xref:System.Data.DataView.FindRows%2A> várias vezes, deverá criar um novo <xref:System.Data.DataView> para recriar o índice na coluna em que você deseja pesquisar e, em seguida, chamar os métodos <xref:System.Data.DataView.Find%2A> ou <xref:System.Data.DataView.FindRows%2A>. Para obter mais informações sobre <xref:System.Data.DataView.Find%2A> os <xref:System.Data.DataView.FindRows%2A> métodos e, consulte [Localizando linhas](./dataset-datatable-dataview/finding-rows.md) e o [desempenho de DataView](dataview-performance.md).  
  
## <a name="clearing-the-filter"></a>Limpando o filtro  

 O filtro em um objeto <xref:System.Data.DataView> podem ser limpas depois da filtragem ter sido definida usando a propriedade <xref:System.Data.DataView.RowFilter%2A>. O filtro em um <xref:System.Data.DataView> pode ser desmarcado de duas maneiras diferentes:  
  
- Defina a propriedade <xref:System.Data.DataView.RowFilter%2A> como `null`.  
  
- Defina a propriedade <xref:System.Data.DataView.RowFilter%2A> como uma cadeia de caracteres vazia.  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir cria um objeto <xref:System.Data.DataView> a partir de uma consulta e limpa o filtro definindo a propriedade <xref:System.Data.DataView.RowFilter%2A> como `null`:  
  
 [!code-csharp[DP DataView Samples#LDVClearRowFilter2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearrowfilter2)]
 [!code-vb[DP DataView Samples#LDVClearRowFilter2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearrowfilter2)]  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir cria um <xref:System.Data.DataView> a partir de uma tabela define a propriedade <xref:System.Data.DataView.RowFilter%2A> e, em seguida, limpa o filtro configurando a propriedade <xref:System.Data.DataView.RowFilter%2A> como uma cadeia de caracteres vazia:  
  
 [!code-csharp[DP DataView Samples#LDVClearRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearrowfilter)]
 [!code-vb[DP DataView Samples#LDVClearRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearrowfilter)]  
  
## <a name="see-also"></a>Consulte também

- [Associação e LINQ to DataSet de dados](data-binding-and-linq-to-dataset.md)
- [Classificar com DataView](sorting-with-dataview-linq-to-dataset.md)
