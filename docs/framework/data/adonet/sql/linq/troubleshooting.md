---
description: 'Saiba mais sobre: solução de problemas'
title: Solução de problemas
ms.date: 03/30/2017
ms.assetid: 8cd4401c-b12c-4116-a421-f3dcffa65670
ms.openlocfilehash: f62d6dbcd8a248cd684bed224ee62b3a205d7174
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99681013"
---
# <a name="troubleshooting"></a>Solução de problemas

As seguintes informações expostas alguns problemas que você pode encontrar em seus aplicativos de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] , e oferece sugestões para evitar ou reduzir de outra maneira o efeito desses problemas.  
  
 Problemas adicionais são abordados em [perguntas](frequently-asked-questions.md)frequentes.  
  
## <a name="unsupported-standard-query-operators"></a>Operadores padrões sem suporte de consulta  

 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não suporta todos os métodos padrão de operador de consulta (por exemplo, <xref:System.Linq.Enumerable.ElementAt%2A>). Como resultado, os projetos que compilam ainda podem gerar erros em tempo de execução. Para obter mais informações, consulte [conversão do operador de consulta padrão](standard-query-operator-translation.md).  
  
## <a name="memory-issues"></a>Problemas de memória  

 Se uma consulta envolve uma coleção na memória e [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Table%601> , a consulta pode ser executada na memória, dependendo da ordem na qual as duas coleções são especificadas. Se a consulta deve ser executada na memória, os dados da tabela de base de dados deverão ser recuperados.  
  
 Essa abordagem é ineficiente e pode resultar em uso significativa de memória e do processador. Tente evitar esses consultas do domínio.  
  
## <a name="file-names-and-sqlmetal"></a>Nomes de arquivo e SQLMetal  

 Para especificar um nome do arquivo de entrada, adicione o nome do arquivo à linha de comando como o arquivo de entrada. Não há suporte para a inclusão do nome de arquivo na cadeia de conexão (usando a opção **/conn**). Para obter mais informações, consulte [SqlMetal.exe (ferramenta de geração de código)](../../../../tools/sqlmetal-exe-code-generation-tool.md).  
  
## <a name="class-library-projects"></a>Projetos de biblioteca de classe  

 O Object Relational Designer cria uma cadeia de conexão no `app.config` arquivo do projeto. Em projetos de biblioteca de classes, o arquivo de `app.config` não é usado. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] usa a cadeia de conexão fornecida em arquivos em tempo de design. Altere o valor em `app.config` não altera a base de dados que conecta seu aplicativo.  
  
## <a name="cascade-delete"></a>Excluir em cascata  

 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] Não dá suporte ou reconhece operações de exclusão em cascata. Se você deseja excluir uma linha em uma tabela que possui restrições nele, você deve fazer:  
  
- Defina a regra `ON DELETE CASCADE` na restrição de chave estrangeira no banco de dados.  
  
- Use seu próprio código para excluir primeiro os objetos filho que impedem que o objeto pai seja excluído.  
  
 Se não, uma exceção é lançada de <xref:System.Data.SqlClient.SqlException> .  
  
 Para obter mais informações, consulte [como: excluir linhas do banco de dados](how-to-delete-rows-from-the-database.md).  
  
## <a name="expression-not-queryable"></a>Expressão não Queryable  

 Se você receber a "expressão [Expression] não é passível de consulta; está faltando uma referência de assembly? " erro, certifique-se do seguinte:  
  
- Seu aplicativo está direcionando .NET Compact Framework 3,5.  
  
- Você tem uma referência a `System.Core.dll` e a `System.Data.Linq.dll`.  
  
- Você tem uma `Imports` diretiva (Visual Basic) ou `using` (C#) para o <xref:System.Linq> e o <xref:System.Data.Linq> .  
  
## <a name="duplicatekeyexception"></a>DuplicateKeyException  

 No decorrer da depuração de um [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] projeto, você pode atravessar as relações de uma entidade. Isso leva esses itens para o cache e [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fica ciente de sua presença. Se você tentar então executar <xref:System.Data.Linq.Table%601.Attach%2A> ou <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> ou método semelhante que gerencia as várias linhas que têm a mesma chave, <xref:System.Data.Linq.DuplicateKeyException> é lançada.  
  
## <a name="string-concatenation-exceptions"></a>Exceções de concatenação de cadeia de caracteres  

 Concatenação em operandos mapeou a `[n]text` e o outro `[n][var]char` não é suportado. Uma exceção é lançada para concatenação de cadeias de caracteres mapeadas para dois conjuntos de diferentes tipos. Para obter mais informações, consulte [métodos System. String](system-string-methods.md).  
  
## <a name="skip-and-take-exceptions-in-sql-server-2000"></a>Ignore e tome exceções no SQL Server 2000  

 Você deve usar membros de identidade (<xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A>) quando você usa <xref:System.Linq.Queryable.Take%2A> ou <xref:System.Linq.Queryable.Skip%2A> em um base de dados SQL Server 2000. A consulta deve estar com uma única tabela (isto é, não uma união), ou seja <xref:System.Linq.Queryable.Distinct%2A>, <xref:System.Linq.Queryable.Except%2A>, <xref:System.Linq.Queryable.Intersect%2A>, ou operação de <xref:System.Linq.Queryable.Union%2A> , e não deve incluir uma operação de <xref:System.Linq.Queryable.Concat%2A> . Para obter mais informações, consulte a seção "suporte do SQL Server 2000" na [tradução do operador de consulta padrão](standard-query-operator-translation.md).  
  
 Esse requisito não se aplica a SQL Server 2005.  
  
## <a name="groupby-invalidoperationexception"></a>GroupBy InvalidOperationException  

 Essa exceção é lançada quando um valor de coluna é zero em uma consulta de <xref:System.Linq.Enumerable.GroupBy%2A> que se agrupe por uma expressão de `boolean` , como `group x by (Phone==@phone)`. Como a expressão é a `boolean` , a chave é inferida para ser `boolean` , não `nullable` `boolean` . Quando a comparação de conversão produz um valor nulo, é feita uma tentativa de atribuir um `nullable` `boolean` a um `boolean` , e a exceção é lançada.  
  
 Para evitar essa situação (pressupõe que o desejar tratar nulos como false), use uma abordagem como o seguinte:  
  
 `GroupBy="(Phone != null) && (Phone=@Phone)"`  
  
## <a name="oncreated-partial-method"></a>Método parcial deOnCreated()  

 O método gerado `OnCreated()` é chamado em cada vez que o construtor do objeto é chamado, incluindo a situação em que [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] chama o construtor para fazer uma cópia para valores originais. Leve em conta esse comportamento se você implementar o método de `OnCreated()` em sua própria classe parcial.  
  
## <a name="see-also"></a>Consulte também

- [Depuração de suporte](debugging-support.md)
- [Perguntas frequentes](frequently-asked-questions.md)
