---
description: 'Saiba mais sobre: coleções de esquema Oracle'
title: Coleções de esquema do Oracle
ms.date: 03/30/2017
ms.assetid: 89a75de8-dee8-45e2-a97f-254d7e62e7e1
ms.openlocfilehash: c3093887c9359cbb170846c0ae425e0f77fc2580
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99672407"
---
# <a name="oracle-schema-collections"></a>Coleções de esquema do Oracle

O Microsoft .NET Framework Provedor de Dados para Oracle dá suporte às seguintes coleções de esquema específicas, além das coleções de esquema comuns:

- Colunas

- Índices

- IndexColumns

- Procedimentos

- Sequências

- Sinônimos

- Tabelas

- Usuários

- Exibições

- Funções

- Pacotes

- PackageBodies

- Argumentos

- UniqueKeys

- PrimaryKeys

- ForeignKeys

- ForeignKeyColumns

- ProcedureParameters

## <a name="columns"></a>Colunas

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Proprietário da tabela, exibição ou cluster.|
|TABLE_NAME|String|Tabela, exibição ou nome do cluster.|
|COLUMN_NAME|String|Nome da coluna.|
|ID|Decimal|Número de sequência da coluna como criado.|
|TIPO de dados|String|Tipo de dados da coluna.|
|LENGTH|Decimal|Comprimento da coluna em bytes.|
|PRECISION|Decimal|Precisão decimal para tipo de dados de número; precisão binária para tipo de dados FLOAT, NULL para todos os outros tipos de dado.|
|SCALE|Decimal|Dígitos à direita do ponto decimal em um número.|
|NULLABLE|String|Especifica se uma coluna permite nulos. O valor será N se houver uma restrição NOT NULL na coluna ou se a coluna fizer parte de uma chave primária.|

## <a name="indexes"></a>Índices

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Proprietário do índice|
|INDEX_NAME|String|Nome do índice.|
|INDEX_TYPE|String|Tipo de índice (NORMAL, BITMAP, NORMAL baseado em função, BITMAP baseado em função ou domínio).|
|TABLE_OWNER|String|Proprietário do objeto indexado.|
|TABLE_NAME|String|Nome do objeto indexado.|
|TABLE_TYPE|String|Tipo do objeto indexado (por exemplo, tabela, CLUSTER).|
|EXCLUSIVIDADE|String|Se o índice é exclusivo ou não exclusivo.|
|COMPRESSION|String|Se o índice está habilitado ou DESABILITAdo.|
|PREFIX_LENGTH|Decimal|Número de colunas no prefixo da chave de compactação.|
|TABLESPACE_NAME|String|Nome do espaço de tabela que contém o índice.|
|INI_TRANS|Decimal|Número inicial de transações.|
|MAX_TRANS|Decimal|Número máximo de transações.|
|INITIAL_EXTENT|Decimal|Tamanho da extensão inicial.|
|NEXT_EXTENT|Decimal|Tamanho das extensões secundárias.|
|MIN_EXTENTS|Decimal|Número mínimo de extensões permitidas no segmento.|
|MAX_EXTENTS|Decimal|Número máximo de extensões permitidas no segmento.|
|PCT_INCREASE|Decimal|Percentual de aumento no tamanho da extensão.|
|PCT_THRESHOLD|Decimal|Porcentagem de limite de espaço de bloco permitida por entrada de índice.|
|INCLUDE_COLUMN|Decimal|A ID da coluna da última coluna a ser incluída no índice de chave primária da tabela organizada de índice (sem estouro). Esta coluna é mapeada para a coluna COLUMN_ID das exibições do dicionário de dados * _TAB_COLUMNS.|
|LISTAS livres|Decimal|Número de listas livres de processo alocadas para este segmento.|
|FREELIST_GROUPS|Decimal|Número de grupos de listas livres alocados para este segmento.|
|PCT_FREE|Decimal|Porcentagem mínima de espaço livre em um bloco.|
|LOGOUT|String|Registrando informações.|
|BLEVEL|Decimal|B *-nível de árvore: profundidade do índice de seu bloco raiz para seus blocos folha. Uma profundidade de 0 indica que o bloco raiz e o bloco folha são os mesmos.|
|LEAF_BLOCKS|Decimal|Número de blocos folha no índice|
|DISTINCT_KEYS|Decimal|Número de valores indexados distintos. Para índices que impõem restrições UNIQUE e PRIMARY KEY, esse valor é o mesmo que o número de linhas na tabela (USER_TABLES. NUM_ROWS).|
|AVG_LEAF_BLOCKS_PER_KEY|Decimal|Número médio de blocos folha nos quais cada valor distinto no índice aparece arredondado para o número inteiro mais próximo. Para índices que impõem restrições UNIQUE e PRIMARY KEY, esse valor é sempre 1.|
|AVG_DATA_BLOCKS_PER_KEY|Decimal|Número médio de blocos de dados na tabela que são apontados por um valor distinto no índice arredondado para o número inteiro mais próximo. Essa estatística é o número médio de blocos de dados que contêm linhas que contêm um determinado valor para as colunas indexadas.|
|CLUSTERING_FACTOR|Decimal|Indica a quantidade de ordem das linhas na tabela com base nos valores do índice.|
|STATUS|String|Se um índice não particionado é válido ou não pode ser usado.|
|NUM_ROWS|Decimal|O número de linhas no índice.|
|SAMPLE_SIZE|Decimal|Tamanho do exemplo usado para analisar o índice.|
|LAST_ANALYZED|Datetime|Data em que esse índice foi analisado mais recentemente.|
|DETERMINADO|String|Número de threads por instância para verificação do índice.|
|OCASIÕES|String|Número de instâncias em que os índices serão examinados.|
|PARTICIONADA|String|Se esse índice está particionado (Sim &#124; não).|
|TEMPORARY|String|Se o índice está em uma tabela temporária.|
|CRIADO|String|Se o nome do índice é gerado pelo sistema (Y&#124;N).|
|SECONDARY|String|Se o índice é um objeto secundário criado pelo método ODCIIndexCreate do cartucho de dados Oracle9i (Y&#124;N).|
|BUFFER_POOL|String|Nome do pool de buffers padrão a ser usado para os blocos de índice.|
|USER_STATS|String|Se as estatísticas foram inseridas diretamente pelo usuário.|
|DURAÇÃO|String|Indica a duração de uma tabela temporária: 1) SYS $ SESSION: as linhas são preservadas durante a sessão, 2) SYS $ TRANSACTION: as linhas são excluídas após COMMIT, 3) NULL para a tabela permanente.|
|PCT_DIRECT_ACCESS|Decimal|Para um índice secundário em uma tabela organizada por índice, a porcentagem de linhas com uma estimativa válida|
|ITYP_OWNER|String|Para um índice de domínio, o proprietário do indextype.|
|ITYP_NAME|String|Para um índice de domínio, o nome do indextype.|
|PARAMETERS|String|Para um índice de domínio, a cadeia de caracteres do parâmetro.|
|GLOBAL_STATS|String|Para índices particionados, indica se as estatísticas foram coletadas analisando o índice como um todo (Sim) ou se foram estimadas de estatísticas em partições e subpartições de índice subjacentes (não).|
|DOMIDX_STATUS|String|Reflete o status do índice de domínio. NULL: o índice especificado não é um índice de domínio. VÁLIDO: o índice é um índice de domínio válido. IDXTYP_INVLD: o tipo de índice deste índice de domínio é inválido.|
|DOMIDX_OPSTATUS|String|Reflete o status de uma operação que foi executada em um índice de domínio: NULL: o índice especificado não é um índice de domínio. VÁLIDO: a operação executada sem erros. FALHA: a operação falhou com um erro.|
|FUNCIDX_STATUS|String|Indica o status de um índice baseado em função: NULL: este não é um índice baseado em função, habilitado: o índice baseado em função está habilitado, DESABILITAdo: o índice baseado em função está desabilitado.|
|JOIN_INDEX|String|Indica se este é um índice de junção ou não.|

## <a name="indexcolumns"></a>IndexColumns

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|INDEX_OWNER|String|Proprietário do índice.|
|INDEX_NAME|String|Nome do índice.|
|TABLE_OWNER|String|Proprietário da tabela ou cluster.|
|TABLE_NAME|String|Nome da tabela ou cluster.|
|COLUMN_NAME|String|Nome da coluna ou atributo da coluna de tipo de objeto.|
|COLUMN_POSITION|Decimal|Posição da coluna ou atributo dentro do índice.|
|COLUMN_LENGTH|Decimal|Comprimento indexado da coluna.|
|CHAR_LENGTH|Decimal|Comprimento máximo de ponto da coluna.|
|ASCENDE|String|Se a coluna está classificada em ordem decrescente.|

## <a name="procedures"></a>Procedimentos

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Proprietário do objeto.|
|OBJECT_NAME|String|Nome do objeto.|
|SUBOBJECT_NAME|String|Nome do subobjeto (por exemplo, partição).|
|OBJECT_ID|Decimal|O número do objeto Dictionary do objeto.|
|DATA_OBJECT_ID|Decimal|O número do objeto Dictionary do segmento que contém o objeto.|
|LAST_DDL_TIME|Datetime|Carimbo de data/hora para a última modificação do objeto resultante de um comando DDL (incluindo concessões e revogações).|
|timestamp|String|Carimbo de data/hora para a especificação do objeto (dados de caractere).|
|STATUS|String|Status do objeto (válido, inválido ou N/A).|
|TEMPORARY|String|Se o objeto é temporário (a sessão atual pode ver apenas os dados colocados nesse objeto).|
|CRIADO|String|O nome deste sistema de objetos foi gerado? (Y &#124; N).|
|SECONDARY|String|Se este é um objeto secundário criado pelo método ODCIIndexCreate do cartucho de dados Oracle9i (Y &#124; N).|
|CREATED|DateTime|A data em que o objeto foi criado.|

## <a name="sequences"></a>Sequências

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|SEQUENCE_OWNER|String|Nome do proprietário da sequência.|
|SEQUENCE_NAME|String|Nome da sequência.|
|MIN_VALUE|Decimal|Valor mínimo da sequência.|
|MAX_VALUE|Decimal|Valor máximo da sequência.|
|INCREMENT_BY|Decimal|Valor pelo qual a sequência é incrementada.|
|CYCLE_FLAG|String|A sequência é encapsulada ao longo do limite de alcance.|
|ORDER_FLAG|String|São números de sequência gerados na ordem.|
|CACHE_SIZE|Decimal|Número de números de sequência para armazenar em cache.|
|LAST_NUMBER|Decimal|Último número de sequência gravado no disco. Se uma sequência usar o Caching, o número gravado em disco será o último número colocado no cache de sequência. Esse número provavelmente será maior que o último número de sequência usado.|

## <a name="synonyms"></a>Sinônimos

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Proprietário do sinônimo.|
|SYNONYM_NAME|String|Nome do sinônimo.|
|TABLE_OWNER|String|Proprietário do objeto referenciado pelo sinônimo.|
|TABLE_NAME|String|Nome do objeto referenciado pelo sinônimo.|
|DB_LINK|String|Nome do link de banco de dados referenciado, se houver.|

## <a name="tables"></a>Tabelas

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Proprietário da tabela.|
|TABLE_NAME|String|Nome da tabela.|
|TYPE|String|Tipo de tabela.|

## <a name="users"></a>Usuários

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|NAME|String|Nome do usuário.|
|ID|Decimal|Número de identificação do usuário.|
|CREATEDATE|Datetime|Data de criação do usuário.|

## <a name="views"></a>Exibições

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Proprietário da exibição.|
|VIEW_NAME|String|Nome da exibição.|
|TEXT_LENGTH|Decimal|Comprimento do texto da exibição.|
|TEXT|String|Exibir texto.|
|TYPE_TEXT_LENGTH|Decimal|Comprimento da cláusula de tipo da exibição tipada.|
|TYPE_TEXT|String|Cláusula Type da exibição tipada.|
|OID_TEXT_LENGTH|Decimal|Comprimento da cláusula WITH OID da exibição tipada.|
|OID_TEXT|String|COM a cláusula OID da exibição tipada.|
|VIEW_TYPE_OWNER|String|Proprietário do tipo de exibição se a exibição for uma exibição tipada.|
|VIEW_TYPE|String|Tipo de exibição se a exibição for uma exibição tipada.|
|SUPERVIEW_NAME|String|Nome da superexibição.|

## <a name="functions"></a>Funções

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Proprietário do objeto.|
|OBJECT_NAME|String|Nome do objeto.|
|SUBOBJECT_NAME|String|Nome do subobjeto (por exemplo, partição).|
|OBJECT_ID|Decimal|O número do objeto Dictionary do objeto.|
|DATA_OBJECT_ID|Decimal|O número do objeto Dictionary do segmento que contém o objeto.|
|Object_Type|String|Tipo do objeto.|
|CREATED|DateTime|A data em que o objeto foi criado.|
|LAST_DDL_TIME|Datetime|Carimbo de data/hora para a última modificação do objeto resultante de um comando DDL (incluindo concessões e revogações).|
|timestamp|String|Carimbo de data/hora para a especificação do objeto (dados de caractere)|
|STATUS|String|Status do objeto (válido, inválido ou N/A).|
|TEMPORARY|String|Se o objeto é temporário (a sessão atual pode ver apenas os dados colocados nesse objeto).|
|CRIADO|String|O nome deste sistema de objetos foi gerado? (Y &#124; N).|
|SECONDARY|String|Se este é um objeto secundário criado pelo método ODCIIndexCreate do cartucho de dados Oracle9i (Y &#124; N).|

## <a name="packages"></a>Pacotes

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Proprietário do objeto.|
|OBJECT_NAME|String|Nome do objeto.|
|SUBOBJECT_NAME|String|Nome do subobjeto (por exemplo, partição).|
|OBJECT_ID|Decimal|O número do objeto Dictionary do objeto.|
|DATA_OBJECT_ID|Decimal|O número do objeto Dictionary do segmento que contém o objeto.|
|LAST_DDL_TIME|Datetime|Carimbo de data/hora para a última modificação do objeto resultante de um comando DDL (incluindo concessões e revogações).|
|timestamp|String|Carimbo de data/hora para a especificação do objeto (dados de caractere).|
|STATUS|String|Status do objeto (válido, inválido ou N/A).|
|TEMPORARY|String|Se o objeto é temporário (a sessão atual pode ver apenas os dados colocados nesse objeto).|
|CRIADO|String|O nome deste sistema de objetos foi gerado? (Y &#124; N).|
|SECONDARY|String|Se este é um objeto secundário criado pelo método ODCIIndexCreate do cartucho de dados Oracle9i (Y &#124; N).|
|CREATED|DateTime|A data em que o objeto foi criado.|

## <a name="packagebodies"></a>PackageBodies

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Proprietário do objeto.|
|OBJECT_NAME|String|Nome do objeto.|
|SUBOBJECT_NAME|String|Nome do subobjeto (por exemplo, partição).|
|OBJECT_ID|Decimal|O número do objeto Dictionary do objeto.|
|DATA_OBJECT_ID|Decimal|O número do objeto Dictionary do segmento que contém o objeto.|
|LAST_DDL_TIME|Datetime|Carimbo de data/hora para a última modificação do objeto resultante de um comando DDL (incluindo concessões e revogações).|
|timestamp|String|Carimbo de data/hora para a especificação do objeto (dados de caractere).|
|STATUS|String|Status do objeto (válido, inválido ou N/A).|
|TEMPORARY|String|Se o objeto é temporário (a sessão atual pode ver apenas os dados colocados nesse objeto).|
|CRIADO|String|O nome deste sistema de objetos foi gerado? (Y &#124; N).|
|SECONDARY|String|Se este é um objeto secundário criado pelo método ODCIIndexCreate do cartucho de dados Oracle9i (Y &#124; N).|
|CREATED|DateTime|A data em que o objeto foi criado.|

## <a name="arguments"></a>Argumentos

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Nome do proprietário do objeto.|
|PACKAGE_NAME|String|Nome do pacote.|
|OBJECT_NAME|String|Nome do procedimento ou da função.|
|ARGUMENT_NAME|String|Nome do argumento.|
|PROPOSTAS|Decimal|Posição na lista de argumentos ou NULL para o valor de retorno da função.|
|SEQUENCE|Decimal|Sequência de argumentos, incluindo todos os níveis de aninhamento.|
|DEFAULT_VALUE|String|Valor padrão para o argumento.|
|DEFAULT_LENGTH|Decimal|Comprimento do valor padrão para o argumento.|
|IN_OUT|String|Direção do argumento (IN, OUT ou IN/OUT).|
|DATA_LENGTH|Decimal|Comprimento da coluna em bytes.|
|DATA_PRECISION|Decimal|Comprimento em dígitos decimais (número) ou dígitos binários (FLOAT).|
|DATA_SCALE|Decimal|Dígitos à direita do ponto decimal em um número.|
|DATA_TYPE|String|Tipo de dados do argumento.|

## <a name="uniquekeys"></a>UniqueKeys

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Proprietário da definição de restrição.|
|CONSTRAINT_NAME|String|Nome da definição de restrição.|
|TABLE_NAME|String|Nome associado à tabela (ou exibição) com definição de restrição.|
|SEARCH_CONDITION|String|Texto da condição de pesquisa para uma restrição de verificação.|
|R_OWNER|String|Proprietário da tabela referenciada em uma restrição referencial.|
|R_CONSTRAINT_NAME|String|Nome da definição de restrição exclusiva para a tabela referenciada.|
|DELETE_RULE|String|Excluir regra para uma restrição referencial (em cascata ou nenhuma ação).|
|STATUS|String|Status de imposição da restrição (habilitado ou DESABILITAdo).|
|DEFERRABLE|String|Se a restrição é adiada.|
|Valid|String|Se todos os dados obedecem à restrição (VALIDAdo ou não VALIDAdo).|
|CRIADO|String|Se o nome da restrição é gerado pelo usuário ou pelo sistema.|
|SATISFATÓRIO|String|Um valor Sim indica que essa restrição especifica um século de maneira ambígua. Para evitar erros resultantes dessa ambiguidade, reescreva a restrição usando a função TO_DATE com um ano de quatro dígitos.|
|Utilize|String|Se uma restrição habilitada é imposta ou não imposta.|
|LAST_CHANGE|Datetime|Quando a restrição foi habilitada ou desabilitada pela última vez|
|INDEX_OWNER|String|Nome do usuário que possui o índice|
|INDEX_NAME|String|Nome do índice|

## <a name="primarykeys"></a>PrimaryKeys

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Proprietário da definição de restrição.|
|CONSTRAINT_NAME|String|Nome da definição de restrição.|
|TABLE_NAME|String|Nome associado à tabela (ou exibição) com definição de restrição.|
|SEARCH_CONDITION|String|Texto da condição de pesquisa para uma restrição de verificação.|
|R_OWNER|String|Proprietário da tabela referenciada em uma restrição referencial.|
|R_CONSTRAINT_NAME|String|Nome da definição de restrição exclusiva para a tabela referenciada.|
|DELETE_RULE|String|Excluir regra para uma restrição referencial (em cascata ou nenhuma ação).|
|STATUS|String|Status de imposição da restrição (habilitado ou DESABILITAdo).|
|DEFERRABLE|String|Se a restrição é adiada.|
|Valid|String|Se todos os dados obedecem à restrição (VALIDAdo ou não VALIDAdo).|
|CRIADO|String|Se o nome da restrição é gerado pelo usuário ou pelo sistema.|
|SATISFATÓRIO|String|Um valor Sim indica que essa restrição especifica um século de maneira ambígua. Para evitar erros resultantes dessa ambiguidade, reescreva a restrição usando a função TO_DATE com um ano de quatro dígitos.|
|Utilize|String|Se uma restrição habilitada é imposta ou não imposta.|
|LAST_CHANGE|Datetime|Quando a restrição foi habilitada ou desabilitada pela última vez.|
|INDEX_OWNER|String|Nome do usuário que possui o índice.|
|INDEX_NAME|String|Nome do índice.|

## <a name="foreignkeys"></a>ForeignKeys

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|PRIMARY_KEY_CONSTRAINT_NAME|String|Nome da definição de restrição.|
|PRIMARY_KEY_OWNER|String|Proprietário da definição de restrição.|
|PRIMARY_KEY_TABLE_NAME|String|Nome associado à tabela (ou exibição) com definição de restrição|
|FOREIGN_KEY_OWNER|String|Proprietário da definição de restrição.|
|FOREIGN_KEY_CONSTRAINT_NAME|String|Nome da definição de restrição.|
|FOREIGN_KEY_TABLE_NAME|String|Nome associado à tabela (ou exibição) com definição de restrição.|
|SEARCH_CONDITION|String|Texto da condição de pesquisa para uma restrição de verificação|
|R_OWNER|String|Proprietário da tabela referenciada em uma restrição referencial.|
|R_CONSTRAINT_NAME|String|Nome da definição de restrição exclusiva para a tabela referenciada.|
|DELETE_RULE|String|Excluir regra para uma restrição referencial (em cascata ou nenhuma ação).|
|STATUS|String|Status de imposição da restrição (habilitado ou DESABILITAdo).|
|Valid|String|Se todos os dados obedecem à restrição (VALIDAdo ou não VALIDAdo).|
|CRIADO|String|Se o nome da restrição é gerado pelo usuário ou pelo sistema.|
|Utilize|String|Se uma restrição habilitada é imposta ou não imposta.|
|LAST_CHANGE|Datetime|Quando a restrição foi habilitada ou desabilitada pela última vez.|
|INDEX_OWNER|String|Nome do usuário que possui o índice.|
|INDEX_NAME|String|Nome do índice.|

## <a name="foreignkeycolumns"></a>ForeignKeyColumns

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Proprietário da definição de restrição.|
|CONSTRAINT_NAME|String|Nome da definição de restrição.|
|TABLE_NAME|String|Nome da tabela com definição de restrição.|
|COLUMN_NAME|String|Nome da coluna ou atributo da coluna de tipo de objeto especificada na definição de restrição.|
|PROPOSTAS|Decimal|Posição original da coluna ou do atributo na definição do objeto.|

## <a name="procedureparameters"></a>ProcedureParameters

|ColumnName|Tipo de dados|Descrição|
|----------------|--------------|-----------------|
|OWNER|String|Proprietário do objeto.|
|OBJECT_NAME|String|Nome do procedimento ou da função.|
|PACKAGE_NAME|String|Nome do procedimento ou da função.|
|OBJECT_ID|Decimal|Número de objeto do objeto.|
|SOBRECARGA|String|Identificador exclusivo de sobrecarga.|
|ARGUMENT_NAME|String|Nome do argumento.|
|PROPOSTAS|Decimal|Posição na lista de argumentos ou NULL para um valor de retorno de função.|
|SEQUENCE|Decimal|Sequência de argumentos, incluindo todos os níveis de aninhamento.|
|DATA_LEVEL|Decimal|Profundidade de aninhamento do argumento para tipos compostos.|
|DATA_TYPE|String|Tipo de dados do argumento.|
|DEFAULT_VALUE|String|Valor padrão para o argumento.|
|DEFAULT_LENGTH|Decimal|Comprimento do valor padrão para o argumento.|
|IN_OUT|String|Direção do argumento (IN, OUT ou IN/OUT).|
|DATA_LENGTH|Decimal|Comprimento da coluna (em bytes).|
|DATA_PRECISION|Decimal|Comprimento em dígitos decimais (número) ou dígitos binários (FLOAT).|
|DATA_SCALE|Decimal|Dígitos à direita do ponto decimal em um número.|
|RADIX|Decimal|Base do argumento de um número.|
|CHARACTER_SET_NAME|String|Nome do conjunto de caracteres do argumento.|
|TYPE_OWNER|String|Proprietário do tipo do argumento.|
|TYPE_NAME|String|Nome do tipo do argumento. Se o tipo for um tipo local de pacote (ou seja, for declarado em uma especificação de pacote), essa coluna exibirá o nome do pacote.|
|TYPE_SUBNAME|String|Relevante apenas para tipos locais de pacote. Exibe o nome do tipo declarado no pacote identificado na coluna TYPE_NAME.|
|TYPE_LINK|String|Relevante apenas para tipos locais de pacote quando o pacote identificado na coluna TYPE_NAME é um pacote remoto. Esta coluna exibe o link de banco de dados usado para fazer referência ao pacote remoto.|
|PLS_TYPE|String|Para argumentos numéricos, o nome do tipo PL/SQL do argumento. Do contrário, nulo.|
|CHAR_LENGTH|Decimal|Limite de caracteres para tipos de dados de cadeia de caracteres.|
|CHAR_USED|String|Indica se o limite de bytes (B) ou o limite de caracteres (C) é oficial para a cadeia de caracteres.|

## <a name="see-also"></a>Consulte também

- [Visão geral do ADO.NET](ado-net-overview.md)
