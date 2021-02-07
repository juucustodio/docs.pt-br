---
description: 'Saiba mais sobre: problemas conhecidos no SqlClient para Entity Framework'
title: Problemas conhecidos em SqlClient para Entity Framework
ms.date: 03/30/2017
ms.assetid: 48fe4912-4d0f-46b6-be96-3a42c54780f6
ms.openlocfilehash: c1a82657f1b43cddb858692d055df3bf2dca47ec
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99697329"
---
# <a name="known-issues-in-sqlclient-for-entity-framework"></a>Problemas conhecidos em SqlClient para Entity Framework

Esta seção descreve os problemas conhecidos relacionados ao provedor de dados. NET Framework para SQL Server (SqlClient).  
  
## <a name="trailing-spaces-in-string-functions"></a>Espaço à direita em funções de cadeia de caracteres  

 SQL Server ignora espaços à direita em valores de cadeia de caracteres. Portanto, passe espaço à direita na cadeia de caracteres pode levar a resultados imprevisíveis, mesmo falhas.  
  
 Se você precisar ter espaços à direita na cadeia de caracteres, considere anexar um caractere de espaço em branco no final, para que SQL Server não corte a cadeia de caracteres. Se o espaço à direita não são necessários, devem ser quebrados antes de serem passados abaixo do pipeline de consulta.  
  
## <a name="right-function"></a>Função DIREITA  

 Se um valor de`null` não é passado como um argumento e primeiros 0 são passados como um segundo argumento para `RIGHT(nvarchar(max)`, 0`)` ou `RIGHT(varchar(max)`, 0`)`, um valor de `NULL` serão retornados em vez de uma cadeia de caracteres de `empty` .  
  
## <a name="cross-and-outer-apply-operators"></a>A CRUZ e EXTERIORES APLICAM operadores  

 Operadores de aplicação CRUZado e externo foram introduzidos no SQL Server 2005. Em alguns casos o pipeline de consulta pode gerar uma declaração de Transact-SQL que contém a CRUZ SE APLICASSE e/ou OUTER APPLY operadores. Como alguns provedores de back-end, incluindo versões do SQL Server anteriores ao SQL Server 2005, não dão suporte a esses operadores, essas consultas não podem ser executadas nesses provedores de back-end.  
  
 A seguir estão alguns cenários típicos que podem resultar na presença de CRUZ SE APLICAM e/ou OUTER APPLY operadores na consulta de saída:  
  
- Um subconsulta correlacionado com paginação.  
  
- `AnyElement` sobre subpropriedades uma consulta correlacionada, ou sobre uma coleção gerada por navegação.  
  
- LINQ consulta que uso que agrupa os métodos que aceitam um seletor do elemento.  
  
- Uma consulta em que uma CRUZ SE APLICA ou OUTER APPLY são especificados explicitamente  
  
- Uma consulta que tenha uma compilação de DEREF sobre uma compilação de referência.  
  
## <a name="skip-operator"></a>Operador SKIP  

 Se você estiver usando SQL Server 2000, usar ignorar por colunas não chave pode retornar resultados incorretos. Mais do que o número de linhas especificado podem ser ignoradas se a coluna de chave não tem dados duplicados nele. Isso ocorre devido a como o SKIP é convertido para SQL Server 2000. Por exemplo, na consulta a seguir, mais de cinco linhas podem ser ignoradas se `E.NonKeyColumn` houver valores duplicados:  
  
```sql  
SELECT [E] FROM Container.EntitySet AS [E] ORDER BY [E].[NonKeyColumn] DESC SKIP 5L  
```  
  
## <a name="targeting-the-correct-sql-server-version"></a>Direcionamento a versão correta do SQL Server  

 O Entity Framework se destina à consulta Transact-SQL com base na versão SQL Server especificada no `ProviderManifestToken` atributo do elemento Schema no arquivo de modelo de armazenamento (. SSDL). Esta versão pode diferir de versão do SQL Server que você real é conectada. Por exemplo, se você estiver usando SQL Server 2005, mas o `ProviderManifestToken` atributo for definido como 2008, a consulta Transact-SQL gerada poderá não ser executada no servidor. Por exemplo, uma consulta que usa os novos tipos de data/hora que foram introduzidos no SQL Server 2008 não será executada em versões anteriores do SQL Server. Se você estiver usando SQL Server 2005, mas o `ProviderManifestToken` atributo for definido como 2000, a consulta Transact-SQL gerada poderá ser menos otimizada ou você poderá receber uma exceção informando que não há suporte para a consulta. Para obter mais informações, consulte a CRUZ e OUTER APLICA a seção dos operadores, anteriormente neste tópico.  
  
 Determinados comportamentos de base de dados depende de nível de compatibilidade definido para base de dados. Se o `ProviderManifestToken` atributo for definido como 2005 e sua versão de SQL Server for 2005, mas o nível de compatibilidade de um banco de dados for definido como "80" (SQL Server 2000), o Transact-SQL gerado será direcionado SQL Server 2005, mas poderá não ser executado conforme o esperado devido à configuração de nível de compatibilidade. Por exemplo, você pode perder ordenação informações se um nome de coluna na cláusula ORDER a lista corresponde a um nome de coluna no seletor.  
  
## <a name="nested-queries-in-projection"></a>Consultas aninhadas na projeção  

 Consultas aninhadas em uma cláusula de projeção podem obter convertido em consultas de produto cartesiano no servidor. Em alguns servidores back-end, incluindo SQL Server, isso pode fazer com que a tabela TempDB fique muito grande. Isso pode diminuir o desempenho do servidor.  
  
 Veja a seguir um exemplo de uma consulta aninhada em uma cláusula de projeção:  
  
```sql  
SELECT c, (SELECT c, (SELECT c FROM AdventureWorksModel.Vendor AS c  ) As Inner2 FROM AdventureWorksModel.JobCandidate AS c  ) As Inner1 FROM AdventureWorksModel.EmployeeDepartmentHistory AS c  
```  
  
## <a name="server-generated-guid-identity-values"></a>Valores gerados a identidade do GUID de servidor  

 O Entity Framework dá suporte a valores de identidade de tipo GUID gerados pelo servidor, mas o provedor deve dar suporte ao retorno do valor de identidade gerado pelo servidor após a inserção de uma linha. A partir do SQL Server 2005, você pode retornar o tipo de GUID gerado pelo servidor em um banco de dados SQL Server por meio da [cláusula OUTPUT](/sql/t-sql/queries/output-clause-transact-sql).
  
## <a name="see-also"></a>Consulte também

- [SqlClient para Entity Framework](sqlclient-for-the-entity-framework.md)
- [Problemas conhecidos e considerações no LINQ to Entities](./language-reference/known-issues-and-considerations-in-linq-to-entities.md)
