---
description: 'Saiba mais sobre: coleções de esquemas ODBC'
title: Coleções de esquema ODBC
ms.date: 03/30/2017
ms.assetid: 1bb126a5-ceec-4649-a4bc-8aa19e801046
ms.openlocfilehash: ceac67e49914db7010e315a2dfcdb630bea1e29f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786193"
---
# <a name="odbc-schema-collections"></a>Coleções de esquema ODBC

Esta seção discute o suporte da coleção de esquemas para os drivers ODBC para Microsoft SQL Server, Oracle e Microsoft Jet.

## <a name="microsoft-sql-server-odbc-driver"></a>Microsoft SQL Server driver ODBC

O driver ODBC Microsoft SQL Server dá suporte às seguintes coleções de esquema específicas, além das coleções de esquema comuns:

- Tabelas

- Índices

- Colunas

- Procedimentos

- ProcedureColumns

- ProcedureParameters

- Exibições

### <a name="tables-and-views"></a>Tabelas e Exibições

|ColumnName|Tipo de dados|
|----------------|--------------|
|TABLE_CAT|String|
|TABLE_SCHEM|String|
|TABLE_NAME|String|
|TABLE_TYPE|String|
|COMENTÁRIOS|String|

### <a name="indexes"></a>Índices

|ColumnName|Tipo de dados|
|----------------|--------------|
|TABLE_CAT|String|
|TABLE_SCHEM|String|
|TABLE_NAME|String|
|NON_UNIQUE|Int16|
|INDEX_QUALIFIER|String|
|INDEX_NAME|String|
|TYPE|Int16|
|ORDINAL_POSITION|Int16|
|COLUMN_NAME|String|
|ASC_OR_DESC|String|
|CARDINALITY|Int32|
|PAGES|Int32|
|FILTER_CONDITION|String|
|SS_TYPE_SCHEMA|String|
|SS_DATA_TYPE|Byte|

### <a name="columns"></a>Colunas

|ColumnName|Tipo de dados|
|----------------|--------------|
|TABLE_CAT|String|
|TABLE_SCHEM|String|
|TABLE_NAME|String|
|COLUMN_NAME|String|
|DATA_TYPE|Int16|
|TYPE_NAME|String|
|COLUMN_SIZE|Int32|
|BUFFER_LENGTH|Int32|
|DECIMAL_DIGITS|Int16|
|NUM_PREC_RADIX|Int16|
|NULLABLE|Int16|
|COMENTÁRIOS|String|
|COLUMN_DEF|String|
|SQL_DATA_TYPE|Int16|
|SQL_DATETIME_SUB|Int16|
|CHAR_OCTET_LENGTH|Int32|
|ORDINAL_POSITION|Int32|
|IS_NULLABLE|String|
|SS_TYPE_CATALOG|String|
|SS_TYPE_SCHEMA|String|
|SS_DATA_TYPE|Byte|

### <a name="procedures"></a>Procedimentos

|ColumnName|Tipo de dados|
|----------------|--------------|
|PROCEDURE_CAT|String|
|PROCEDURE_SCHEM|String|
|PROCEDURE_NAME|String|
|NUM_INPUT_PARAMS|Int32|
|NUM_OUTPUT_PARAMS|Int32|
|NUM_RESULT_SETS|Int32|
|COMENTÁRIOS|String|
|PROCEDURE_TYPE|Int16|

### <a name="procedurecolumns"></a>ProcedureColumns

|ColumnName|Tipo de dados|
|----------------|--------------|
|PROCEDURE_CAT|String|
|PROCEDURE_SCHEM|String|
|PROCEDURE_NAME|String|
|COLUMN_NAME|String|
|COLUMN_TYPE|Int16|
|DATA_TYPE|Int16|
|TYPE_NAME|String|
|COLUMN_SIZE|Int32|
|BUFFER_LENGTH|Int32|
|DECIMAL_DIGITS|Int16|
|NUM_PREC_RADIX|Int16|
|NULLABLE|Int16|
|COMENTÁRIOS|String|
|COLUMN_DEF|String|
|SQL_DATA_TYPE|Int16|
|SQL_DATETIME_SUB|Int16|
|CHAR_OCTET_LENGTH|Int32|
|ORDINAL_POSITION|Int32|
|IS_NULLABLE|String|
|SS_TYPE_CATALOG|String|
|SS_TYPE_SCHEMA|String|
|SS_DATA_TYPE|Byte|

### <a name="procedureparameters"></a>ProcedureParameters

|ColumnName|Tipo de dados|
|----------------|--------------|
|PROCEDURE_CAT|String|
|PROCEDURE_SCHEM|String|
|PROCEDURE_NAME|String|
|COLUMN_NAME|String|
|COLUMN_TYPE|Int16|
|DATA_TYPE|Int16|
|TYPE_NAME|String|
|COLUMN_SIZE|Int32|
|BUFFER_LENGTH|Int32|
|DECIMAL_DIGITS|Int16|
|NUM_PREC_RADIX|Int16|
|NULLABLE|Int16|
|COMENTÁRIOS|String|
|COLUMN_DEF|String|
|SQL_DATA_TYPE|Int16|
|SQL_DATETIME_SUB|Int16|
|CHAR_OCTET_LENGTH|Int32|
|ORDINAL_POSITION|Int32|
|IS_NULLABLE|String|
|SS_TYPE_CATALOG|String|
|SS_TYPE_SCHEMA|String|
|SS_DATA_TYPE|Byte|

## <a name="microsoft-oracle-odbc-driver"></a>Driver ODBC da Microsoft Oracle

O driver ODBC do Microsoft SQL Server da Oracle dá suporte às seguintes coleções de esquema específicas, além das coleções de esquema comuns:

- Tabelas

- Colunas

- Procedimentos

- ProcedureColumns

- ProcedureParameters

- Exibições

- Índices

### <a name="tables-and-views"></a>Tabelas e Exibições

|ColumnName|Tipo de dados|
|----------------|--------------|
|TABLE_QUALIFIER|String|
|TABLE_OWNER|String|
|TABLE_NAME|String|
|TABLE_TYPE|String|
|COMENTÁRIOS|String|

### <a name="columns"></a>Colunas

|ColumnName|Tipo de dados|
|----------------|--------------|
|TABLE_QUALIFIER|String|
|TABLE_OWNER|String|
|TABLE_NAME|String|
|COLUMN_NAME|String|
|DATA_TYPE|Int16|
|TYPE_NAME|String|
|PRECISION|Int32|
|LENGTH|Int32|
|SCALE|Int16|
|RADIX|Int16|
|NULLABLE|Int16|
|COMENTÁRIOS|String|
|ORDINAL_POSITION|Int32|

### <a name="procedures"></a>Procedimentos

|ColumnName|Tipo de dados|
|----------------|--------------|
|PROCEDURE_QUALIFIER|String|
|PROCEDURE_OWNER|String|
|PROCEDURE_NAME|String|
|NUM_INPUT_PARAMS|Int16|
|NUM_OUTPUT_PARAMS|Int16|
|NUM_RESULT_SETS|Int16|
|COMENTÁRIOS|String|
|PROCEDURE_TYPE|Int16|

### <a name="procedurecolumns"></a>ProcedureColumns

|ColumnName|Tipo de dados|
|----------------|--------------|
|PROCEDURE_QUALIFIER|String|
|PROCEDURE_OWNER|String|
|PROCEDURE_NAME|String|
|COLUMN_NAME|String|
|COLUMN_TYPE|Int16|
|DATA_TYPE|Int16|
|TYPE_NAME|String|
|PRECISION|Int32|
|LENGTH|Int32|
|SCALE|Int16|
|RADIX|Int16|
|NULLABLE|Int16|
|COMENTÁRIOS|String|
|SOBRECARGA|Int32|
|ORDINAL_POSITION|Int32|

## <a name="microsoft-jet-odbc-driver"></a>Driver ODBC do Microsoft Jet

O driver ODBC do Microsoft Jet dá suporte às seguintes coleções de esquema específicas, além das coleções de esquema comuns:

- Tabelas

- Índices

- Colunas

- Procedimentos

- ProcedureColumns

- ProcedureParameters

- Exibições

### <a name="tables-and-views"></a>Tabelas e Exibições

|ColumnName|Tipo de dados|
|----------------|--------------|
|TABLE_QUALIFIER|String|
|TABLE_OWNER|String|
|TABLE_NAME|String|
|TABLE_TYPE|String|
|COMENTÁRIOS|String|

### <a name="columns"></a>Colunas

|ColumnName|Tipo de dados|
|----------------|--------------|
|TABLE_QUALIFIER|String|
|TABLE_OWNER|String|
|TABLE_NAME|String|
|COLUMN_NAME|String|
|DATA_TYPE|Int16|
|TYPE_NAME|String|
|PRECISION|Int32|
|LENGTH|Int32|
|SCALE|Int16|
|RADIX|Int16|
|NULLABLE|Int16|
|COMENTÁRIOS|String|
|ORDINAL_POSITION|Int32|

### <a name="procedures"></a>Procedimentos

|ColumnName|Tipo de dados|
|----------------|--------------|
|PROCEDURE_QUALIFIER|String|
|PROCEDURE_OWNER|String|
|PROCEDURE_NAME|String|
|NUM_INPUT_PARAMS|Int16|
|NUM_OUTPUT_PARAMS|Int16|
|NUM_RESULT_SETS|Int16|
|COMENTÁRIOS|String|
|PROCEDURE_TYPE|Int16|

### <a name="procedurecolumns"></a>ProcedureColumns

|ColumnName|Tipo de dados|
|----------------|--------------|
|PROCEDURE_QUALIFIER|String|
|PROCEDURE_OWNER|String|
|PROCEDURE_NAME|String|
|COLUMN_NAME|String|
|COLUMN_TYPE|Int16|
|DATA_TYPE|Int16|
|TYPE_NAME|String|
|PRECISION|Int32|
|LENGTH|Int32|
|SCALE|Int16|
|RADIX|Int16|
|NULLABLE|Int16|
|COMENTÁRIOS|String|
|SOBRECARGA|Int32|
|ORDINAL_POSITION|Int32|

### <a name="procedureparameters"></a>ProcedureParameters

|ColumnName|Tipo de dados|
|----------------|--------------|
|PROCEDURE_CAT|String|
|PROCEDURE_SCHEM|String|
|PROCEDURE_NAME|String|
|COLUMN_NAME|String|
|COLUMN_TYPE|Int16|
|DATA_TYPE|Int16|
|TYPE_NAME|String|
|COLUMN_SIZE|Int32|
|BUFFER_LENGTH|Int32|
|DECIMAL_DIGITS|Int16|
|NUM_PREC_RADIX|Int16|
|NULLABLE|Int16|
|COMENTÁRIOS|String|
|COLUMN_DEF|String|
|SQL_DATA_TYPE|Int16|
|SQL_DATETIME_SUB|Int16|
|CHAR_OCTET_LENGTH|Int32|
|ORDINAL_POSITION|Int32|
|IS_NULLABLE|String|

## <a name="see-also"></a>Consulte também

- [Visão geral do ADO.NET](ado-net-overview.md)
