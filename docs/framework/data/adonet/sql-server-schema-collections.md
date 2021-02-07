---
description: 'Saiba mais sobre: SQL Server coleções de esquema'
title: Coleções de esquema do SQL Server
ms.date: 03/30/2017
ms.assetid: c6403cc3-d78b-4f85-bab1-ada7a3446ec5
ms.openlocfilehash: 0299daada77b6968a0b1f875956da7bd2a221322
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99718662"
---
# <a name="sql-server-schema-collections"></a>Coleções de esquema do SQL Server

O Provedor de Dados do Microsoft .NET Framework para SQL Server dá suporte a coleções de esquema adicionais, além das coleções de esquema comuns. As coleções de esquemas variam ligeiramente de acordo com a versão utilizada do SQL Server. Para determinar a lista de coleções de esquemas compatíveis, chame o método **GetSchema** sem argumentos ou com o nome da coleção de esquemas "MetaDataCollections". Isso retornará uma <xref:System.Data.DataTable> com uma lista de coleções de esquemas compatíveis, o número de restrições ao qual cada uma dá suporte e o número de partes de identificador usado por elas.  
  
## <a name="databases"></a>Bancos de dados  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|database_name|String|Nome do banco de dados.|  
|dbid|Int16|ID do banco de dados.|  
|create_date|DateTime|Data de criação do banco de dados.|  
  
## <a name="foreign-keys"></a>Chaves estrangeiras  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|CONSTRAINT_CATALOG|String|Catálogo ao qual a restrição pertence.|  
|CONSTRAINT_SCHEMA|String|Esquema que contém a restrição.|  
|CONSTRAINT_NAME|String|Nome.|  
|TABLE_CATALOG|String|Nome de tabela da qual a restrição faz parte.|  
|TABLE_SCHEMA|String|Esquema que contém a tabela.|  
|TABLE_NAME|String|Nome da tabela|  
|CONSTRAINT_TYPE|String|Tipo de restrição. Somente "FOREIGN KEY" é permitido.|  
|IS_DEFERRABLE|String|Especifica se a restrição pode ser adiada. Retorna NO.|  
|INITIALLY_DEFERRED|String|Especifica se a restrição pode ser inicialmente adiada. Retorna NO.|  
  
## <a name="indexes"></a>Índices  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|constraint_catalog|String|Catálogo ao qual o índice pertence.|  
|constraint_schema|String|Esquema que contém o índice.|  
|constraint_name|String|Nome do índice.|  
|table_catalog|String|Nome da tabela à qual o índice está associado.|  
|table_schema|String|Esquema que contém a tabela à qual o índice está associado.|  
|table_name|String|Nome da tabela.|  
|index_name|String|Nome do índice.|  
  
### <a name="indexes-sql-server-2008"></a>Índices (SQL Server 2008)  

 A partir do .NET Framework versão 3,5 SP1 e SQL Server 2008, as colunas a seguir foram adicionadas à coleção de esquemas de índices para dar suporte a novos tipos espaciais, FileStream e colunas esparsas. Essas colunas não têm suporte em versões anteriores do .NET Framework e SQL Server.  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|type_desc|String|O tipo do índice será um dos seguintes:<br /><br /> – HEAP<br />– CLUSTERIZADO<br />– NÃO CLUSTERIZADO<br />– XML<br />– ESPACIAL|  
  
## <a name="indexcolumns"></a>IndexColumns  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|constraint_catalog|String|Catálogo ao qual o índice pertence.|  
|constraint_schema|String|Esquema que contém o índice.|  
|constraint_name|String|Nome do índice.|  
|table_catalog|String|Nome da tabela à qual o índice está associado.|  
|table_schema|String|Esquema que contém a tabela à qual o índice está associado.|  
|table_name|String|Nome da tabela.|  
|column_name|String|Nome da coluna à qual o índice está associado.|  
|ordinal_position|Int32|Posição ordinal na coluna.|  
|KeyType|Byte|O tipo de objeto.|  
|index_name|String|Nome do índice.|  
  
## <a name="procedures"></a>Procedimentos  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|SPECIFIC_CATALOG|String|Nome específico do catálogo.|  
|SPECIFIC_SCHEMA|String|Nome específico do esquema.|  
|SPECIFIC_NAME|String|Nome específico do catálogo.|  
|ROUTINE_CATALOG|String|Catálogo ao qual o procedimento armazenado pertence.|  
|ROUTINE_SCHEMA|String|Esquema que contém o procedimento armazenado.|  
|ROUTINE_NAME|String|Nome do procedimento armazenado.|  
|ROUTINE_TYPE|String|Retorna PROCEDURE para procedimentos armazenados e FUNCTION para funções.|  
|CREATED|DateTime|Hora em que o procedimento foi criado.|  
|LAST_ALTERED|DateTime|A última vez em que o procedimento foi modificado.|  
  
## <a name="procedure-parameters"></a>Parâmetros de procedimento  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|SPECIFIC_CATALOG|String|Nome do catálogo do procedimento do qual esse é um parâmetro.|  
|SPECIFIC_SCHEMA|String|Esquema que contém o procedimento do qual esse parâmetro faz parte.|  
|SPECIFIC_NAME|String|Nome do procedimento do qual esse parâmetro faz parte.|  
|ORDINAL_POSITION|Int32|A posição ordinal do parâmetro começando em 1. Para o valor retornado de um procedimento, isso é 0.|  
|PARAMETER_MODE|String|Retorna IN no caso de um parâmetro de entrada, OUT no caso de um parâmetro de saída e INOUT no caso de um parâmetro de entrada/saída.|  
|IS_RESULT|String|Retorna YES se indica o resultado do procedimento que é uma função. Caso contrário, retorna NO.|  
|AS_LOCATOR|String|Retorna YES se declarado como localizador. Caso contrário, retorna NO.|  
|PARAMETER_NAME|String|Nome do parâmetro. NULL se isto corresponder ao valor de retorno de uma função.|  
|DATA_TYPE|String|Tipo de dados fornecido pelo sistema.|  
|CHARACTER_MAXIMUM_LENGTH|Int32|Comprimento máximo em caracteres para tipos de dados binários ou de caractere. Caso contrário, retorna NULL.|  
|CHARACTER_OCTET_LENGTH|Int32|Comprimento máximo em bytes para tipos de dados binários ou de caractere. Caso contrário, retorna NULL.|  
|COLLATION_CATALOG|String|Nome do catálogo da ordenação do parâmetro. Se não for um dos tipos de caractere, retorna NULL.|  
|COLLATION_SCHEMA|String|Sempre retorna NULL.|  
|COLLATION_NAME|String|Nome da ordenação do parâmetro. Se não for um dos tipos de caractere, retorna NULL.|  
|CHARACTER_SET_CATALOG|String|O nome de catálogo do conjunto de caracteres do parâmetro. Se não for um dos tipos de caractere, retorna NULL.|  
|CHARACTER_SET_SCHEMA|String|Sempre retorna NULL.|  
|CHARACTER_SET_NAME|String|O nome do conjunto de caracteres do parâmetro. Se não for um dos tipos de caractere, retorna NULL.|  
|NUMERIC_PRECISION|Byte|Precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, retorna NULL.|  
|NUMERIC_PRECISION_RADIX|Int16|Base de precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, retorna NULL.|  
|NUMERIC_SCALE|Int32|Escala de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, retorna NULL.|  
|DATETIME_PRECISION|Int16|Precisão em segundos fracionários se o tipo de parâmetro é datetime ou smalldatetime. Caso contrário, retorna NULL.|  
|INTERVAL_TYPE|String|NULL. Reservado para uso futuro pelo SQL Server.|  
|INTERVAL_PRECISION|Int16|NULL. Reservado para uso futuro pelo SQL Server.|  
  
## <a name="tables"></a>Tabelas  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|String|Catálogo da tabela.|  
|TABLE_SCHEMA|String|Esquema que contém a tabela.|  
|TABLE_NAME|String|Nome da tabela.|  
|TABLE_TYPE|String|Tipo de tabela. Pode ser VIEW ou BASE TABLE.|  
  
## <a name="columns"></a>Colunas  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|String|Catálogo da tabela.|  
|TABLE_SCHEMA|String|Esquema que contém a tabela.|  
|TABLE_NAME|String|Nome da tabela.|  
|COLUMN_NAME|String|Nome da coluna.|  
|ORDINAL_POSITION|Int32|Número de identificação da coluna.|  
|COLUMN_DEFAULT|String|Valor padrão da coluna|  
|IS_NULLABLE|String|Possibilidade de nulidade da coluna. Se essa coluna permite NULL, ela retorna YES. Caso contrário, NO é retornado.|  
|DATA_TYPE|String|Tipo de dados fornecido pelo sistema.|  
|CHARACTER_MAXIMUM_LENGTH|Int32 – Sql8, Int16 – Sql7|Comprimento máximo, em caracteres, de dados binários, dados de caracteres e dados de texto e imagem. Caso contrário, será retornado NULL.|  
|CHARACTER_OCTET_LENGTH|Int32 – SQL8, Int16 – Sql7|Comprimento máximo, em bytes, de dados binários, dados de caracteres e dados de texto e imagem. Caso contrário, será retornado NULL.|  
|NUMERIC_PRECISION|Byte sem sinal|Precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|NUMERIC_PRECISION_RADIX|Int16|Base de precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|NUMERIC_SCALE|Int32|Escala de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|DATETIME_PRECISION|Int16|Código de subtipo para os tipos de dados datetime e interval do SQL-92. Para outros tipos de dados, é retornado NULL.|  
|CHARACTER_SET_CATALOG|String|Retorna o mestre, indicando o banco de dados no qual o conjunto de caracteres está localizado, se a coluna é do tipo de dados de caractere ou de texto. Caso contrário, será retornado NULL.|  
|CHARACTER_SET_SCHEMA|String|Sempre retorna NULL.|  
|CHARACTER_SET_NAME|String|Retorna o nome exclusivo do conjunto de caracteres se essa coluna é do tipo de dados de caractere ou de texto. Caso contrário, será retornado NULL.|  
|COLLATION_CATALOG|String|Retorna o mestre, indicando o banco de dados no qual a ordenação está definida, se a coluna é do tipo de dados de caractere ou de texto. Caso contrário, esta coluna será NULL.|  
  
### <a name="columns-sql-server-2008"></a>Colunas (SQL Server 2008)  

 A partir do .NET Framework versão 3,5 SP1 e SQL Server 2008, as colunas a seguir foram adicionadas à coleção de esquemas de colunas para dar suporte a novos tipos espaciais, FileStream e colunas esparsas. Essas colunas não têm suporte em versões anteriores do .NET Framework e SQL Server.  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|IS_FILESTREAM|String|YES se a coluna tem o atributo FILESTREAM.<br /><br /> NO se a coluna não tem o atributo FILESTREAM.|  
|IS_SPARSE|String|YES se a coluna é uma coluna esparsa.<br /><br /> NO se a coluna não é uma coluna esparsa.|  
|IS_COLUMN_SET|String|YES se a coluna é uma coluna do conjunto de colunas.<br /><br /> NO se a coluna não é uma coluna do conjunto de colunas.|  
  
### <a name="allcolumns-sql-server-2008"></a>Colunas (SQL Server 2008)  

 A partir do .NET Framework versão 3,5 SP1 e SQL Server 2008, a coleção de esquemas das colunas foi adicionada para dar suporte a colunas esparsas. Não há suporte para as colunas em versões anteriores do .NET Framework e SQL Server.  
  
 AllColumns têm as mesmas restrições e o esquema DataTable resultante como a coleção de esquemas Columns. A única diferença é que AllColumns inclui colunas do conjunto de colunas que não estão incluídas na coleção de esquemas Columns. A tabela a seguir descreve essas colunas.  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|String|Catálogo da tabela.|  
|TABLE_SCHEMA|String|Esquema que contém a tabela.|  
|TABLE_NAME|String|Nome da tabela.|  
|COLUMN_NAME|String|Nome da coluna.|  
|ORDINAL_POSITION|Int32|Número de identificação da coluna.|  
|COLUMN_DEFAULT|String|Valor padrão da coluna|  
|IS_NULLABLE|String|Possibilidade de nulidade da coluna. Se essa coluna permite NULL, ela retorna YES. Caso contrário, será retornado NO.|  
|DATA_TYPE|String|Tipo de dados fornecido pelo sistema.|  
|CHARACTER_MAXIMUM_LENGTH|Int32|Comprimento máximo, em caracteres, de dados binários, dados de caracteres e dados de texto e imagem. Caso contrário, será retornado NULL.|  
|CHARACTER_OCTET_LENGTH|Int32|Comprimento máximo, em bytes, de dados binários, dados de caracteres e dados de texto e imagem. Caso contrário, será retornado NULL.|  
|NUMERIC_PRECISION|Byte sem sinal|Precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|NUMERIC_PRECISION_RADIX|Int16|Base de precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|NUMERIC_SCALE|Int32|Escala de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|DATETIME_PRECISION|Int16|Código de subtipo para os tipos de dados datetime e interval do SQL-92. Para outros tipos de dados, é retornado NULL.|  
|CHARACTER_SET_CATALOG|String|Retorna o mestre, indicando o banco de dados no qual o conjunto de caracteres está localizado, se a coluna é do tipo de dados de caractere ou de texto. Caso contrário, será retornado NULL.|  
|CHARACTER_SET_SCHEMA|String|Sempre retorna NULL.|  
|CHARACTER_SET_NAME|String|Retorna o nome exclusivo do conjunto de caracteres se essa coluna é do tipo de dados de caractere ou de texto. Caso contrário, será retornado NULL.|  
|COLLATION_CATALOG|String|Retorna o mestre, indicando o banco de dados no qual a ordenação está definida, se a coluna é do tipo de dados de caractere ou de texto. Caso contrário, esta coluna será NULL.|  
|IS_FILESTREAM|String|YES se a coluna tem o atributo FILESTREAM.<br /><br /> NO se a coluna não tem o atributo FILESTREAM.|  
|IS_SPARSE|String|YES se a coluna é uma coluna esparsa.<br /><br /> NO se a coluna não é uma coluna esparsa.|  
|IS_COLUMN_SET|String|YES se a coluna é uma coluna do conjunto de colunas.<br /><br /> NO se a coluna não é uma coluna do conjunto de colunas.|  
  
### <a name="columnsetcolumns-sql-server-2008"></a>ColumnSetColumns (SQL Server 2008)  

 A partir do .NET Framework versão 3,5 SP1 e SQL Server 2008, a coleção de esquemas ColumnSetColumns foi adicionada para dar suporte a colunas esparsas. Não há suporte para ColumnSetColumns em versões anteriores do .NET Framework e SQL Server. A coleção de esquemas ColumnSetColumns retorna o esquema para todas as colunas em um conjunto de colunas. A tabela a seguir descreve essas colunas.  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|String|Catálogo da tabela.|  
|TABLE_SCHEMA|String|Esquema que contém a tabela.|  
|TABLE_NAME|String|Nome da tabela.|  
|COLUMN_NAME|String|Nome da coluna.|  
|ORDINAL_POSITION|Int32|Número de identificação da coluna.|  
|COLUMN_DEFAULT|String|Valor padrão da coluna|  
|IS_NULLABLE|String|Possibilidade de nulidade da coluna. Se essa coluna permite NULL, ela retorna YES. Caso contrário, será retornado NO.|  
|DATA_TYPE|String|Tipo de dados fornecido pelo sistema.|  
|CHARACTER_MAXIMUM_LENGTH|Int32|Comprimento máximo, em caracteres, de dados binários, dados de caracteres e dados de texto e imagem. Caso contrário, será retornado NULL.|  
|CHARACTER_OCTET_LENGTH|Int32|Comprimento máximo, em bytes, de dados binários, dados de caracteres e dados de texto e imagem. Caso contrário, será retornado NULL.|  
|NUMERIC_PRECISION|Byte sem sinal|Precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|NUMERIC_PRECISION_RADIX|Int16|Base de precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|NUMERIC_SCALE|Int32|Escala de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|DATETIME_PRECISION|Int16|Código de subtipo para os tipos de dados datetime e interval do SQL-92. Para outros tipos de dados, é retornado NULL.|  
|CHARACTER_SET_CATALOG|String|Retorna o mestre, indicando o banco de dados no qual o conjunto de caracteres está localizado, se a coluna é do tipo de dados de caractere ou de texto. Caso contrário, será retornado NULL.|  
|CHARACTER_SET_SCHEMA|String|Sempre retorna NULL.|  
|CHARACTER_SET_NAME|String|Retorna o nome exclusivo do conjunto de caracteres se essa coluna é do tipo de dados de caractere ou de texto. Caso contrário, será retornado NULL.|  
|COLLATION_CATALOG|String|Retorna o mestre, indicando o banco de dados no qual a ordenação está definida, se a coluna é do tipo de dados de caractere ou de texto. Caso contrário, esta coluna será NULL.|  
|IS_FILESTREAM|String|YES se a coluna tem o atributo FILESTREAM.<br /><br /> NO se a coluna não tem o atributo FILESTREAM.|  
|IS_SPARSE|String|YES se a coluna é uma coluna esparsa.<br /><br /> NO se a coluna não é uma coluna esparsa.|  
|IS_COLUMN_SET|String|YES se a coluna é uma coluna do conjunto de colunas.<br /><br /> NO se a coluna não é uma coluna do conjunto de colunas.|  
  
## <a name="users"></a>Usuários  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|uid|Int16|ID do usuário ID, exclusivo neste banco de dados. 1 é o proprietário do banco de dados.|  
|user_name|String|Nome de usuário ou nome do grupo, exclusivo neste banco de dados.|  
|createdate|DateTime|Data em que a conta foi adicionada.|  
|updatedate|DateTime|A data em que a conta foi alterada pela última vez.|  
  
## <a name="views"></a>Exibições  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|String|Catálogo da exibição.|  
|TABLE_SCHEMA|String|Esquema que contém a exibição.|  
|TABLE_NAME|String|Nome da exibição.|  
|CHECK_OPTION|String|Tipo de WITH CHECK OPTION. É CASCADE se a exibição original foi criada usando WITH CHECK OPTION. Caso contrário, será retornado NONE.|  
|IS_UPDATABLE|String|Especifica se a exibição é atualizável. Sempre retorna NO.|  
  
## <a name="viewcolumns"></a>ViewColumns  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|VIEW_CATALOG|String|Catálogo da exibição.|  
|VIEW_SCHEMA|String|Esquema que contém a exibição.|  
|VIEW_NAME|String|Nome da exibição.|  
|TABLE_CATALOG|String|Catálogo da tabela que está associado a esta exibição.|  
|TABLE_SCHEMA|String|Esquema que contém a tabela associada a esta exibição.|  
|TABLE_NAME|String|Nome da tabela associada à exibição. Tabela base.|  
|COLUMN_NAME|String|Nome da coluna.|  
  
## <a name="userdefinedtypes"></a>UserDefinedTypes  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|assembly_name|String|O nome do arquivo para o assembly.|  
|udt_name|String|O nome de classe para o assembly.|  
|version_major|Objeto|Número de versão principal.|  
|version_minor|Objeto|Número de versão secundária.|  
|version_build|Objeto|Número de build.|  
|version_revision|Objeto|Número de revisão.|  
|culture_info|Objeto|As informações de cultura associadas a esse UDT.|  
|public_key|Objeto|A chave pública usada por este assembly.|  
|is_fixed_length|Boolean|Especifica se o tamanho do tipo é sempre o mesmo que max_length.|  
|max_length|Int16|Tamanho máximo do tipo em bytes.|  
|Create_Date|DateTime|A data em que o assembly foi criado/registrado.|  
|Permission_set_desc|String|O nome amigável do conjunto de permissões/nível de segurança do assembly.|  
  
## <a name="see-also"></a>Confira também

- [Como recuperar informações de esquema de banco de dados](retrieving-database-schema-information.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
