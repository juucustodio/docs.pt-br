---
description: 'Saiba mais sobre: mapeamento de tipo SQL-CLR'
title: Mapeamento de tipo SQL-CLR
ms.date: 07/23/2018
ms.assetid: 4ed76327-54a7-414b-82a9-7579bfcec04b
ms.openlocfilehash: 59d3594287ceb20f5c3887c58a0f5527df35218a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803731"
---
# <a name="sql-clr-type-mapping"></a>Mapeamento de tipo SQL-CLR

No LINQ to SQL, o modelo de dados de um banco de dados relacional mapeia para um modelo de objeto que é expresso na linguagem de programação de sua escolha. Quando o aplicativo é executado, o LINQ to SQL converte consultas integradas à linguagem no modelo de objeto em SQL e as envia para o banco de dados para execução. Quando o banco de dados retorna os resultados, o LINQ to SQL converte os resultados de volta para os objetos com os quais você pode trabalhar em sua própria linguagem de programação.  
  
 Para converter dados entre o modelo de objeto e o banco de dado, um *mapeamento de tipo* deve ser definido. O LINQ to SQL usa um mapeamento de tipo para corresponder a cada tipo CLR (Common Language Runtime) com um tipo específico de SQL Server. Você pode definir mapeamentos de tipo e outras informações de mapeamento, como estrutura de banco de dados e relações de tabela, dentro do modelo de objeto com mapeamento baseado em atributos. Como alternativa, você pode especificar as informações de mapeamento fora do modelo de objeto com um arquivo de mapeamento externo. Para obter mais informações, consulte [mapeamento baseado em atributo](attribute-based-mapping.md) e [mapeamento externo](external-mapping.md).  
  
 Este tópico aborda os seguintes pontos:  
  
- [Mapeamento de tipo padrão](#DefaultTypeMapping)  
  
- [Matriz de comportamento em tempo de execução de mapeamento de tipo](#BehaviorMatrix)  
  
- [Diferenças de comportamento entre CLR e a execução de SQL](#BehaviorDiffs)  
  
- [Mapeamento enum](#EnumMapping)  
  
- [Mapeamento numérico](#NumericMapping)  
  
- [Mapeamento de texto e XML](#TextMapping)  
  
- [Mapeamento de data e hora](#DateMapping)  
  
- [Mapeamento binário](#BinaryMapping)  
  
- [Mapeamento variado](#MiscMapping)  
  
<a name="DefaultTypeMapping"></a>

## <a name="default-type-mapping"></a>Mapeamento de tipo padrão  

 Você pode criar o modelo de objeto ou arquivo de mapeamento externo automaticamente com o Object Relational Designer (Designer Relacional de Objetos) ou a ferramenta de linha de comando SQLMetal. Os mapeamentos de tipo padrão para essas ferramentas definem quais tipos CLR são escolhidos para mapear colunas dentro do banco de dados do SQL Server. Para obter mais informações sobre como usar essas ferramentas, consulte [criando o modelo de objeto](creating-the-object-model.md).  
  
 Você também pode usar o método <xref:System.Data.Linq.DataContext.CreateDatabase%2A> para criar um banco de dados do SQL Server com base nas informações de mapeamento no modelo de objeto ou no arquivo de mapeamento externo. Os mapeamentos de tipo padrão para o método <xref:System.Data.Linq.DataContext.CreateDatabase%2A> definem quais tipos de colunas do SQL Server são criados para mapear para os tipos CLR no modelo de objeto. Para obter mais informações, consulte [como criar dinamicamente um banco de dados](how-to-dynamically-create-a-database.md).  
  
<a name="BehaviorMatrix"></a>

## <a name="type-mapping-run-time-behavior-matrix"></a>Matriz de comportamento em tempo de execução de mapeamento de tipo  

 O diagrama a seguir mostra o comportamento em tempo de execução esperado de mapeamentos de tipo específico quando os dados são recuperados de ou salvos no banco de dados. Com exceção da serialização, o LINQ to SQL não oferece suporte a mapeamento entre qualquer tipo de dados CLR ou SQL Server que não for especificado nesta matriz. Para obter mais informações sobre o suporte de serialização, consulte [serialização binária](#BinarySerialization).  

![SQL Server à tabela de mapeamento de tipo de dados SQL CLR](./media/sql-clr-type-mapping.png)

> [!NOTE]
> Alguns mapeamentos de tipo podem resultar em estouro ou exceções de perda de dados ao converter para ou do banco de dados.  
  
### <a name="custom-type-mapping"></a>Mapeamento de tipo personalizado  

 Com o LINQ to SQL, você não está limitado aos mapeamentos de tipo padrão usados pelo Designer Relacional de Objetos, pelo SQLMetal e pelo método <xref:System.Data.Linq.DataContext.CreateDatabase%2A>. Você pode criar mapeamentos de tipo personalizados explicitamente especificando-os em um arquivo DBML. Em seguida, você pode usar esse arquivo DBML para criar o código do modelo de objeto e o arquivo de mapeamento. Para obter mais informações, consulte [mapeamentos de tipo personalizado do SQL-CLR](sql-clr-custom-type-mappings.md).  
  
<a name="BehaviorDiffs"></a>

## <a name="behavior-differences-between-clr-and-sql-execution"></a>Diferenças de comportamento entre CLR e a execução de SQL  

 Devido às diferenças na precisão e na execução entre CLR e SQL Server, você poderá receber resultados diferentes ou observar um comportamento diferente dependendo de onde você executa os cálculos. Os cálculos realizados em consultas LINQ to SQL são realmente convertidos para Transact-SQL e, em seguida, executados no banco de dados do SQL Server. Os cálculos realizados fora das consultas LINQ to SQL são executados dentro do contexto do CLR.  
  
 Por exemplo, a seguir estão algumas diferenças de comportamento entre o CLR e o SQL Server:  
  
- O SQL Server pede alguns tipos de dados de maneira diferente dos dados de tipo equivalente no CLR. Por exemplo, os dados do SQL Server do tipo `UNIQUEIDENTIFIER` são pedidos de maneira diferente dos dados CLR de tipo <xref:System.Guid?displayProperty=nameWithType>.  
  
- O SQL Server manipula algumas operações de comparação de cadeia de caracteres de maneira diferente do que no CLR. No SQL Server, o comportamento de comparação de cadeia de caracteres depende das configurações de ordenação no servidor. Para obter mais informações, consulte [trabalhando com agrupamentos](/previous-versions/sql/sql-server-2008-r2/ms187582(v=sql.105)) no manuais online do Microsoft SQL Server.  
  
- O SQL Server pode retornar valores diferentes para algumas funções mapeadas do CLR. Por exemplo, as funções de igualdade serão diferentes porque o SQL Server considera que duas cadeias de caracteres serão iguais se diferirem apenas no espaço em branco à direita, enquanto o CLR não as considera iguais.  
  
<a name="EnumMapping"></a>

## <a name="enum-mapping"></a>Mapeamento enum  

 O LINQ to SQL dá suporte a mapeamento do tipo <xref:System.Enum?displayProperty=nameWithType> CLR para tipos do SQL Server de duas maneiras:  
  
- Mapeamento para tipos numéricos do SQL (`TINYINT`, `SMALLINT`, `INT`, `BIGINT`)  
  
     Quando você mapeia um tipo <xref:System.Enum?displayProperty=nameWithType> CLR para um tipo numérico do SQL, mapeia o valor inteiro subjacente do <xref:System.Enum?displayProperty=nameWithType> CLR para o valor da coluna de banco de dados do SQL Server. Por exemplo, se um <xref:System.Enum?displayProperty=nameWithType> chamado `DaysOfWeek` contém um membro chamado `Tue` com um valor inteiro subjacente de 3, esse membro mapeia para um valor de banco de dados de 3.  
  
- Mapeamento para tipos de texto do SQL (`CHAR`, `NCHAR`, `VARCHAR`, `NVARCHAR`)  
  
     Quando você mapeia um tipo <xref:System.Enum?displayProperty=nameWithType> CLR para um tipo de texto do SQL, o valor do banco de dados SQL é mapeado para os nomes dos membros do <xref:System.Enum?displayProperty=nameWithType> CLR. Por exemplo, se um <xref:System.Enum?displayProperty=nameWithType> chamado `DaysOfWeek` contém um membro chamado `Tue` com um valor inteiro subjacente de 3, esse membro mapeia para um valor de banco de dados de `Tue`.  
  
> [!NOTE]
> Ao mapear tipos de texto do SQL para um <xref:System.Enum?displayProperty=nameWithType> CLR, inclua somente os nomes dos membros do <xref:System.Enum> na coluna SQL mapeada. Outros valores não têm suporte na coluna SQL mapeada para <xref:System.Enum>.  
  
 A ferramenta de linha de comando do Designer Relacional de Objetos e do SQLMetal não pode mapear automaticamente um tipo SQL para uma classe <xref:System.Enum> CLR. Você deve configurar explicitamente esse mapeamento personalizando um arquivo DBML para ser usado pelo Designer Relacional de Objetos e pelo SQLMetal. Para obter mais informações sobre mapeamento de tipo personalizado, consulte [mapeamentos de tipo personalizado do SQL-CLR](sql-clr-custom-type-mappings.md).  
  
 Porque uma coluna SQL destinada a enumeração será do mesmo tipo que outras colunas numéricas e de texto; essas ferramentas não reconhecerão sua intenção e usarão como padrão o mapeamento conforme descrito nas seções [mapeamento numérico](#NumericMapping) e [texto e mapeamento XML](#TextMapping) a seguir. Para obter mais informações sobre como gerar código com o arquivo DBML, consulte [geração de código em LINQ to SQL](code-generation-in-linq-to-sql.md).  
  
 O método <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> cria uma coluna SQL do tipo numérico para mapear um tipo <xref:System.Enum?displayProperty=nameWithType> CLR.  
  
<a name="NumericMapping"></a>

## <a name="numeric-mapping"></a>Mapeamento numérico  

 O LINQ to SQL permite mapear vários tipos numéricos CLR e SQL Server. A tabela a seguir mostra os tipos de CLR que o Designer Relacional de Objetos e o SQLMetal selecionam ao criar um modelo de objeto ou um arquivo de mapeamento externo com base no seu banco de dados.  
  
|Tipo do SQL Server|Mapeamento do tipo CLR padrão usado pelo Designer Relacional de Objetos e pelo SQLMetal|  
|---------------------|-----------------------------------------------------------------|  
|`BIT`|<xref:System.Boolean?displayProperty=nameWithType>|  
|`TINYINT`|<xref:System.Int16?displayProperty=nameWithType>|  
|`INT`|<xref:System.Int32?displayProperty=nameWithType>|  
|`BIGINT`|<xref:System.Int64?displayProperty=nameWithType>|  
|`SMALLMONEY`|<xref:System.Decimal?displayProperty=nameWithType>|  
|`MONEY`|<xref:System.Decimal?displayProperty=nameWithType>|  
|`DECIMAL`|<xref:System.Decimal?displayProperty=nameWithType>|  
|`NUMERIC`|<xref:System.Decimal?displayProperty=nameWithType>|  
|`REAL/FLOAT(24)`|<xref:System.Single?displayProperty=nameWithType>|  
|`FLOAT/FLOAT(53)`|<xref:System.Double?displayProperty=nameWithType>|  
  
 A tabela a seguir mostra os mapeamentos de tipo padrão usados pelo método <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> para definir o tipo de colunas SQL são criadas para mapear para tipos CLR definidos no seu modelo de objeto ou arquivos de mapeamento externo.  
  
|Tipo CLR|Tipo padrão do SQL Server usado pelo <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType>|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Boolean?displayProperty=nameWithType>|`BIT`|  
|<xref:System.Byte?displayProperty=nameWithType>|`TINYINT`|  
|<xref:System.Int16?displayProperty=nameWithType>|`SMALLINT`|  
|<xref:System.Int32?displayProperty=nameWithType>|`INT`|  
|<xref:System.Int64?displayProperty=nameWithType>|`BIGINT`|  
|<xref:System.SByte?displayProperty=nameWithType>|`SMALLINT`|  
|<xref:System.UInt16?displayProperty=nameWithType>|`INT`|  
|<xref:System.UInt32?displayProperty=nameWithType>|`BIGINT`|  
|<xref:System.UInt64?displayProperty=nameWithType>|`DECIMAL(20)`|  
|<xref:System.Decimal?displayProperty=nameWithType>|`DECIMAL(29,4)`|  
|<xref:System.Single?displayProperty=nameWithType>|`REAL`|  
|<xref:System.Double?displayProperty=nameWithType>|`FLOAT`|  
  
 Há muitos outros mapeamentos numéricos que você pode escolher, mas alguns podem resultar em estouro ou exceções de perda de dados ao converter para ou do banco de dados. Para obter mais informações, consulte a [matriz de comportamento de tempo de execução de mapeamento de tipo](#BehaviorMatrix).  
  
### <a name="decimal-and-money-types"></a>Tipos de decimal e dinheiro  

 A precisão padrão do tipo de SQL Server `DECIMAL` (18 dígitos decimais à esquerda e à direita do ponto decimal) é muito menor do que a precisão do <xref:System.Decimal?displayProperty=nameWithType> tipo CLR com o qual ele é emparelhado por padrão. Isso pode levar na perda de precisão quando você salva dados no banco de dados. No entanto, apenas o oposto pode acontecer se o tipo `DECIMAL` do SQL Server é configurado com mais de 29 dígitos de precisão. Quando um tipo `DECIMAL` do SQL Server tiver sido configurado com uma precisão maior do que o <xref:System.Decimal?displayProperty=nameWithType> CLR, a perda de precisão poderá ocorrer ao recuperar dados do banco de dados.  
  
 Os tipos `MONEY` e `SMALLMONEY` do SQL Server, que também são emparelhados com o tipo <xref:System.Decimal?displayProperty=nameWithType> CLR por padrão, têm uma precisão muito menor, que pode resultar em estouro ou exceções de perda de dados ao salvar dados no banco de dados.  
  
<a name="TextMapping"></a>

## <a name="text-and-xml-mapping"></a>Mapeamento de texto e XML  

 Também há muitos tipos XML e baseados em texto que você pode mapear com o LINQ to SQL. A tabela a seguir mostra os tipos de CLR que o Designer Relacional de Objetos e o SQLMetal selecionam ao criar um modelo de objeto ou um arquivo de mapeamento externo com base no seu banco de dados.  
  
|Tipo do SQL Server|Mapeamento do tipo CLR padrão usado pelo Designer Relacional de Objetos e pelo SQLMetal|  
|---------------------|-----------------------------------------------------------------|  
|`CHAR`|<xref:System.String?displayProperty=nameWithType>|  
|`NCHAR`|<xref:System.String?displayProperty=nameWithType>|  
|`VARCHAR`|<xref:System.String?displayProperty=nameWithType>|  
|`NVARCHAR`|<xref:System.String?displayProperty=nameWithType>|  
|`TEXT`|<xref:System.String?displayProperty=nameWithType>|  
|`NTEXT`|<xref:System.String?displayProperty=nameWithType>|  
|`XML`|<xref:System.Xml.Linq.XElement?displayProperty=nameWithType>|  
  
 A tabela a seguir mostra os mapeamentos de tipo padrão usados pelo método <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> para definir o tipo de colunas SQL são criadas para mapear para tipos CLR definidos no seu modelo de objeto ou arquivos de mapeamento externo.  
  
|Tipo CLR|Tipo padrão do SQL Server usado pelo <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType>|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Char?displayProperty=nameWithType>|`NCHAR(1)`|  
|<xref:System.String?displayProperty=nameWithType>|`NVARCHAR(4000)`|  
|<xref:System.Char?displayProperty=nameWithType>[]|`NVARCHAR(4000)`|  
|Tipo personalizado implementando `Parse()` e `ToString()`|`NVARCHAR(MAX)`|  
  
 Há muitos outros mapeamentos XML e baseados em texto que você pode escolher, mas alguns podem resultar em estouro ou exceções de perda de dados ao converter para ou do banco de dados. Para obter mais informações, consulte a [matriz de comportamento de tempo de execução de mapeamento de tipo](#BehaviorMatrix).  
  
### <a name="xml-types"></a>Tipos XML  

 O tipo de dados `XML` do SQL Server está disponível a partir do Microsoft SQL Server 2005. Você pode mapear o tipo de dados `XML` do SQL Server para <xref:System.Xml.Linq.XElement>, <xref:System.Xml.Linq.XDocument> ou <xref:System.String>. Se a coluna armazena os fragmentos XML que não podem ser lidos no <xref:System.Xml.Linq.XElement>, a coluna deverá ser mapeada para <xref:System.String> para evitar erros em tempo de execução. Os fragmentos XML que devem ser mapeados para <xref:System.String> incluem o seguinte:  
  
- Uma sequência dos elementos XML  
  
- Atributos  
  
- Identificadores públicos (PI)  
  
- Comentários  
  
 Embora você possa mapear <xref:System.Xml.Linq.XElement> e <xref:System.Xml.Linq.XDocument> para SQL Server conforme mostrado na [matriz de comportamento de tempo de execução de mapeamento de tipo](#BehaviorMatrix), o <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> método não tem mapeamento de tipo de SQL Server padrão para esses tipos.  
  
### <a name="custom-types"></a>Tipos personalizados  

 Se uma classe implementa `Parse()` e `ToString()` , você pode mapear o objeto para qualquer tipo de texto SQL (,,,,, `CHAR` `NCHAR` `VARCHAR` `NVARCHAR` `TEXT` `NTEXT` , `XML` ). O objeto é armazenado no banco de dados enviando o valor retornado por `ToString()` para a coluna mapeada do banco de dados. O objeto é reconstruído chamando `Parse()` na cadeia de caracteres retornada pelo banco de dados.  
  
> [!NOTE]
> O LINQ to SQL não dá suporte à serialização usando <xref:System.Xml.Serialization.IXmlSerializable?displayProperty=nameWithType>.  
  
<a name="DateMapping"></a>

## <a name="date-and-time-mapping"></a>Mapeamento de data e hora  

 Com o LINQ to SQL, você pode mapear muito tipos de data e hora do SQL Server. A tabela a seguir mostra os tipos de CLR que o Designer Relacional de Objetos e o SQLMetal selecionam ao criar um modelo de objeto ou um arquivo de mapeamento externo com base no seu banco de dados.  
  
|Tipo do SQL Server|Mapeamento do tipo CLR padrão usado pelo Designer Relacional de Objetos e pelo SQLMetal|  
|---------------------|-----------------------------------------------------------------|  
|`SMALLDATETIME`|<xref:System.DateTime?displayProperty=nameWithType>|  
|`DATETIME`|<xref:System.DateTime?displayProperty=nameWithType>|  
|`DATETIME2`|<xref:System.DateTime?displayProperty=nameWithType>|  
|`DATETIMEOFFSET`|<xref:System.DateTimeOffset?displayProperty=nameWithType>|  
|`DATE`|<xref:System.DateTime?displayProperty=nameWithType>|  
|`TIME`|<xref:System.TimeSpan?displayProperty=nameWithType>|  
  
 A tabela a seguir mostra os mapeamentos de tipo padrão usados pelo método <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> para definir o tipo de colunas SQL são criadas para mapear para tipos CLR definidos no seu modelo de objeto ou arquivos de mapeamento externo.  
  
|Tipo CLR|Tipo padrão do SQL Server usado pelo <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType>|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.DateTime?displayProperty=nameWithType>|`DATETIME`|  
|<xref:System.DateTimeOffset?displayProperty=nameWithType>|`DATETIMEOFFSET`|  
|<xref:System.TimeSpan?displayProperty=nameWithType>|`TIME`|  
  
 Há muitos outros mapeamentos de data e hora que você pode escolher, mas alguns podem resultar em estouro ou exceções de perda de dados ao converter para ou do banco de dados. Para obter mais informações, consulte a [matriz de comportamento de tempo de execução de mapeamento de tipo](#BehaviorMatrix).  
  
> [!NOTE]
> Os tipos de dados `DATETIME2`, `DATETIMEOFFSET`, `DATE` e `TIME` do SQL Server estão disponíveis a partir do Microsoft SQL Server 2008. O LINQ to SQL oferece suporte ao mapeamento para esses novos tipos a partir do .NET Framework versão 3.5 SP1.  
  
### <a name="systemdatetime"></a>System.Datetime  

 O intervalo e a precisão do tipo <xref:System.DateTime?displayProperty=nameWithType> CLR são maiores do que o intervalo e a precisão do tipo `DATETIME` do SQL Server, que é o mapeamento de tipo padrão para o método <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType>. Para ajudar a evitar exceções relacionadas a datas fora do intervalo de `DATETIME`, use `DATETIME2`, que está disponível a partir do Microsoft SQL Server 2008. `DATETIME2` pode corresponder ao intervalo e à precisão do CLR <xref:System.DateTime?displayProperty=nameWithType> .  
  
 As datas do SQL Server não têm nenhum conceito de <xref:System.TimeZone>, um recurso que tem suporte de modo avançado no CLR. Os valores <xref:System.TimeZone> são salvos como estão no banco de dados sem conversão de <xref:System.TimeZone>, independentemente das informações de <xref:System.DateTimeKind> originais. Quando os valores <xref:System.DateTime> são recuperados do banco de dados, eles são carregados como estão em um <xref:System.DateTime> com um <xref:System.DateTimeKind> de <xref:System.DateTimeKind.Unspecified>. Para obter mais informações sobre os métodos com suporte <xref:System.DateTime?displayProperty=nameWithType> , consulte [métodos System. DateTime](system-datetime-methods.md).  
  
### <a name="systemtimespan"></a>System.TimeSpan  

 O Microsoft SQL Server 2008 e o .NET Framework 3.5 SP1 permitem mapear o tipo <xref:System.TimeSpan?displayProperty=nameWithType> CLR para o tipo `TIME` do SQL Server. No entanto, há uma grande diferença entre o intervalo ao qual o <xref:System.TimeSpan?displayProperty=nameWithType> CLR dá suporte e a que o tipo `TIME` do SQL Server dá suporte. Os valores de mapeamento menores que 0 ou maiores que 23:59:59,9999999 horas para `TIME` do SQL resultará em exceções de estouro. Para obter mais informações, consulte [System. TimeSpan Methods](system-timespan-methods.md).  
  
 No Microsoft SQL Server 2000 e no SQL Server 2005, você não pode mapear campos de banco de dados para <xref:System.TimeSpan>. No entanto, as operações no <xref:System.TimeSpan> têm suporte porque os valores <xref:System.TimeSpan> podem ser retornados da subtração de <xref:System.DateTime> ou introduzidos em uma expressão como um literal ou uma variável associada.  
  
<a name="BinaryMapping"></a>

## <a name="binary-mapping"></a>Mapeamento binário  

 Há muitos tipos do SQL Server que podem mapear para o tipo <xref:System.Data.Linq.Binary?displayProperty=nameWithType> CLR. A tabela a seguir mostra os tipos de SQL Server que fazem o Designer Relacional de Objetos e o SQLMetal definir um tipo <xref:System.Data.Linq.Binary?displayProperty=nameWithType> CLR ao criar um modelo de objeto ou um arquivo de mapeamento externo com base no seu banco de dados.  
  
|Tipo do SQL Server|Mapeamento do tipo CLR padrão usado pelo Designer Relacional de Objetos e pelo SQLMetal|  
|---------------------|-----------------------------------------------------------------|  
|`BINARY(50)`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`VARBINARY(50)`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`VARBINARY(MAX)`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`VARBINARY(MAX)` com o `FILESTREAM` atributo|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`IMAGE`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`TIMESTAMP`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
  
 A tabela a seguir mostra os mapeamentos de tipo padrão usados pelo método <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> para definir o tipo de colunas SQL são criadas para mapear para tipos CLR definidos no seu modelo de objeto ou arquivos de mapeamento externo.  
  
|Tipo CLR|Tipo padrão do SQL Server usado pelo <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType>|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|`VARBINARY(MAX)`|  
|<xref:System.Byte?displayProperty=nameWithType>|`VARBINARY(MAX)`|  
|<xref:System.Runtime.Serialization.ISerializable?displayProperty=nameWithType>|`VARBINARY(MAX)`|  
  
 Há muitos outros mapeamentos binários que você pode escolher, mas alguns podem resultar em estouro ou exceções de perda de dados ao converter para ou do banco de dados. Para obter mais informações, consulte a [matriz de comportamento de tempo de execução de mapeamento de tipo](#BehaviorMatrix).  
  
### <a name="sql-server-filestream"></a>SQL Server FILESTREAM  

 O atributo `FILESTREAM` para colunas `VARBINARY(MAX)` está disponível a partir do Microsoft SQL Server 2008; você pode mapeá-lo com o LINQ to SQL a partir do .NET Framework versão 3.5 SP1.  
  
 Embora você possa mapear colunas `VARBINARY(MAX)` com o atributo `FILESTREAM` para objetos <xref:System.Data.Linq.Binary>, o método <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> não é capaz de criar automaticamente colunas com o atributo `FILESTREAM`. Para obter mais informações sobre o `FILESTREAM` , consulte [visão geral de FileStream](/previous-versions/sql/sql-server-2008-r2/bb933993(v=sql.105)).  
  
<a name="BinarySerialization"></a>

### <a name="binary-serialization"></a>Serialização binária  

 Se uma classe implementa a interface <xref:System.Runtime.Serialization.ISerializable>, você poderá serializar um objeto para qualquer campo binário do SQL (`BINARY`, `VARBINARY`, `IMAGE`). O objeto é serializado e desserializado de acordo com a maneira como a interface <xref:System.Runtime.Serialization.ISerializable> é implementada. Para obter mais informações, consulte [serialização binária](../../../../../standard/serialization/binary-serialization.md).
  
<a name="MiscMapping"></a>

## <a name="miscellaneous-mapping"></a>Mapeamento variado  

 A tabela a seguir mostra os mapeamentos de tipo padrão para alguns tipos variados que ainda não foram mencionados. A tabela a seguir mostra os tipos de CLR que o Designer Relacional de Objetos e o SQLMetal selecionam ao criar um modelo de objeto ou um arquivo de mapeamento externo com base no seu banco de dados.  
  
|Tipo do SQL Server|Mapeamento do tipo CLR padrão usado pelo Designer Relacional de Objetos e pelo SQLMetal|  
|---------------------|-----------------------------------------------------------------|  
|`UNIQUEIDENTIFIER`|<xref:System.Guid?displayProperty=nameWithType>|  
|`SQL_VARIANT`|<xref:System.Object?displayProperty=nameWithType>|  
  
 A tabela a seguir mostra os mapeamentos de tipo padrão usados pelo método <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> para definir o tipo de colunas SQL são criadas para mapear para tipos CLR definidos no seu modelo de objeto ou arquivos de mapeamento externo.  
  
|Tipo CLR|Tipo padrão do SQL Server usado pelo <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType>|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Guid?displayProperty=nameWithType>|`UNIQUEIDENTIFIER`|  
|<xref:System.Object?displayProperty=nameWithType>|`SQL_VARIANT`|  
  
 O LINQ to SQL não dá suporte a nenhum outro mapeamentos de tipo para esses tipos variados.  Para obter mais informações, consulte a [matriz de comportamento de tempo de execução de mapeamento de tipo](#BehaviorMatrix).  
  
## <a name="see-also"></a>Consulte também

- [Mapeamento baseado em atributos](attribute-based-mapping.md)
- [Mapeamento externo](external-mapping.md)
- [Tipos de dados e funções](data-types-and-functions.md)
- [Incompatibilidade de SQL-CLR](sql-clr-type-mismatches.md)
