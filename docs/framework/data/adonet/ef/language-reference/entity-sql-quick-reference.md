---
description: 'Saiba mais sobre: referência rápida do Entity SQL'
title: Referência rápida de Entity SQL
ms.date: 03/30/2017
ms.assetid: e53dad9e-5e83-426e-abb4-be3e78e3d6dc
ms.openlocfilehash: ddac48bece1f0e9df737db295d4d028529ea290f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724551"
---
# <a name="entity-sql-quick-reference"></a>Referência rápida de Entity SQL

Este tópico fornece uma referência rápida às consultas de [!INCLUDE[esql](../../../../../../includes/esql-md.md)]. As consultas deste tópico se baseiam no modelo de vendas AdventureWorks.  
  
## <a name="literals"></a>Literais  
  
### <a name="string"></a>String  

 Há literais de cadeia de caracteres Unicode e não Unicode. As cadeias de caracteres Unicode são precedidas por N. Por exemplo, `N'hello'` .  
  
 Este é um exemplo de um literal de cadeia de caracteres não Unicode:  
  
```sql  
'hello'  
--same as  
"hello"  
```  
  
 Saída:  
  
|Valor|  
|-----------|  
|hello|  
  
### <a name="datetime"></a>Datetime  

 Em literais DateTime, as partes de data e hora são obrigatórias. Não há valores padrão.  
  
 Exemplo:  
  
```sql  
DATETIME '2006-12-25 01:01:00.000'
--same as  
DATETIME '2006-12-25 01:01'  
```  
  
 Saída:  
  
|Valor|  
|-----------|  
|12/25/2006 1:01:00 AM|  
  
### <a name="integer"></a>Integer  

 Literais inteiros podem ser do tipo Int32 (123), UInt32 (123U), Int64 (123L) e UInt64 (123UL).  
  
 Exemplo:  
  
```sql  
--a collection of integers  
{1, 2, 3}  
```  
  
 Saída:  
  
|Valor|  
|-----------|  
|1|  
|2|  
|3|  
  
### <a name="other"></a>Outros  

 Outros literais com suporte do [!INCLUDE[esql](../../../../../../includes/esql-md.md)] são Guid, Binary, Float/Double, Decimal e `null`. Literais nulos em [!INCLUDE[esql](../../../../../../includes/esql-md.md)] são considerados compatíveis com cada outro tipo no modelo conceitual.  
  
## <a name="type-constructors"></a>Construtores de tipo  
  
### <a name="row"></a>ROW  

 A [linha](row-entity-sql.md) constrói um valor anônimo e estruturado de tipo (registro) como em:`ROW(1 AS myNumber, ‘Name’ AS myName).`  
  
 Exemplo:  
  
```sql  
SELECT VALUE row (product.ProductID AS ProductID, product.Name
    AS ProductName) FROM AdventureWorksEntities.Product AS product
```  
  
 Saída:  
  
|ProductID|Nome|  
|---------------|----------|  
|1|Adjustable Race|  
|879|Suporte de bicicleta multifuncional|  
|712|AWC Logo Cap|  
|...|...|  
  
### <a name="multiset"></a>MULTISET  

 As coleções de [vários](multiset-entity-sql.md) conjuntos de construções, como:  
  
 `MULTISET(1,2,2,3)` `--same as`-`{1,2,2,3}.`  
  
 Exemplo:  
  
```sql  
SELECT VALUE product FROM AdventureWorksEntities.Product AS product WHERE product.ListPrice IN MultiSet (125, 300)  
```  
  
 Saída:  
  
|ProductID|Nome|ProductNumber|…|  
|---------------|----------|-------------------|-------|  
|842|Touring-Panniers, Large|PA-T100|…|  
  
### <a name="object"></a>Objeto  

 Construções de [Construtor de tipo nomeado](named-type-constructor-entity-sql.md) (nomeados) objetos definidos pelo usuário, como `person("abc", 12)` .  
  
 Exemplo:  
  
```sql  
SELECT VALUE AdventureWorksModel.SalesOrderDetail (o.SalesOrderDetailID, o.CarrierTrackingNumber, o.OrderQty,
o.ProductID, o.SpecialOfferID, o.UnitPrice, o.UnitPriceDiscount,
o.rowguid, o.ModifiedDate) FROM AdventureWorksEntities.SalesOrderDetail
AS o  
```  
  
 Saída:  
  
|SalesOrderDetailID|CarrierTrackingNumber|OrderQty|ProductID|...|  
|------------------------|---------------------------|--------------|---------------|---------|  
|1|4911-403C-98|1|776|...|  
|2|4911-403C-98|3|777|...|  
|...|...|...|...|...|  
  
## <a name="references"></a>Referências  
  
### <a name="ref"></a>REF  

 [Ref](ref-entity-sql.md) cria uma referência a uma instância de tipo de entidade. Por exemplo, a seguinte consulta retorna referências para cada entidade Order no conjunto de entidades Orders:  
  
```sql  
SELECT REF(o) AS OrderID FROM Orders AS o  
```  
  
 Saída:  
  
|Valor|  
|-----------|  
|1|  
|2|  
|3|  
|...|  
  
 O exemplo a seguir usa o operador de extração de propriedade (.) para acessar uma propriedade de uma entidade. Quando o operador de extração de propriedade é usado, a referência é cancelada automaticamente.  
  
 Exemplo:  
  
```sql  
SELECT VALUE REF(p).Name FROM
    AdventureWorksEntities.Product AS p
```  
  
 Saída:  
  
|Valor|  
|-----------|  
|Adjustable Race|  
|Suporte de bicicleta multifuncional|  
|AWC Logo Cap|  
|...|  
  
### <a name="deref"></a>DEREF  

 [DEREF](deref-entity-sql.md) faz a referência de um valor de referência e produz o resultado dessa desreferência. Por exemplo, a seguinte consulta gera as entidades Order para cada Order no conjunto de entidades Orders: `SELECT DEREF(o2.r) FROM (SELECT REF(o) AS r FROM LOB.Orders AS o) AS o2`.  
  
 Exemplo:  
  
```sql  
SELECT VALUE DEREF(REF(p)).Name FROM
    AdventureWorksEntities.Product AS p
```  
  
 Saída:  
  
|Valor|  
|-----------|  
|Adjustable Race|  
|Suporte de bicicleta multifuncional|  
|AWC Logo Cap|  
|...|  
  
### <a name="createref-and-key"></a>CREATEREF AND KEY  

 [CREATEREF](createref-entity-sql.md) cria uma referência passando uma chave. A [chave](key-entity-sql.md) extrai a parte de chave de uma expressão com referência de tipo.  
  
 Exemplo:  
  
```sql  
SELECT VALUE Key(CreateRef(AdventureWorksEntities.Product, row(p.ProductID)))
    FROM AdventureWorksEntities.Product AS p
```  
  
 Saída:  
  
|ProductID|  
|---------------|  
|980|  
|365|  
|771|  
|...|  
  
## <a name="functions"></a>Funções  
  
### <a name="canonical"></a>Canônico  

 O namespace para [funções canônicas](canonical-functions.md) é EDM, como em `Edm.Length("string")` . Você não precisa especificar o namespace, a menos que outro namespace seja importado e contenha uma função com o mesmo nome de uma função canônica. Se dois namespaces têm a mesma função, o usuário deve especificar o nome completo.  
  
 Exemplo:  
  
```sql  
SELECT Length(c. FirstName) AS NameLen FROM
    AdventureWorksEntities.Contact AS c
    WHERE c.ContactID BETWEEN 10 AND 12  
```  
  
 Saída:  
  
|NameLen|  
|-------------|  
|6|  
|6|  
|5|  
  
### <a name="microsoft-provider-specific"></a>Específico do provedor da Microsoft  

 As [funções específicas do provedor da Microsoft](../sqlclient-for-ef-functions.md) estão no `SqlServer` namespace.  
  
 Exemplo:  
  
```sql  
SELECT SqlServer.LEN(c.EmailAddress) AS EmailLen FROM
    AdventureWorksEntities.Contact AS c WHERE
    c.ContactID BETWEEN 10 AND 12  
```  
  
 Saída:  
  
|EmailLen|  
|--------------|  
|27|  
|27|  
|26|  
  
## <a name="namespaces"></a>Namespaces  

 O [uso](using-entity-sql.md) de especifica namespaces usados em uma expressão de consulta.  
  
 Exemplo:  
  
```sql  
using SqlServer; LOWER('AA');  
```  
  
 Saída:  
  
|Valor|  
|-----------|  
|aa|  
  
## <a name="paging"></a>Paginamento  

 A paginação pode ser expressa declarando-se uma subcláusula [Skip](skip-entity-sql.md) e [Limit](limit-entity-sql.md) com a cláusula [order by](order-by-entity-sql.md) .  
  
 Exemplo:  
  
```sql  
SELECT c.ContactID as ID, c.LastName AS Name FROM
    AdventureWorks.Contact AS c ORDER BY c.ContactID SKIP 9 LIMIT 3;  
```  
  
 Saída:  
  
|ID|Nome|  
|--------|----------|  
|10|Adina|  
|11|Agcaoili|  
|12|Aguilar|  
  
## <a name="grouping"></a>Agrupamento  

 O [agrupamento](group-by-entity-sql.md) especifica os grupos nos quais os objetos retornados por uma expressão de consulta ([Select](select-entity-sql.md)) devem ser colocados.  
  
 Exemplo:  
  
```sql  
SELECT VALUE name FROM AdventureWorksEntities.Product AS P
    GROUP BY P.Name HAVING MAX(P.ListPrice) > 5  
```  
  
 Saída:  
  
|name|  
|----------|  
|LL Mountain Seat Assembly|  
|ML Mountain Seat Assembly|  
|HL Mountain Seat Assembly|  
|...|  
  
## <a name="navigation"></a>Navegação  

 O operador de navegação de relação permite que você navegue na relação de uma entidade (from end) para outra (to end). A [navegação](navigate-entity-sql.md) usa o tipo de relação qualificado como \<namespace> . \<relationship type name> . Navigate retornará Ref \<T> se a cardinalidade da extremidade to for 1. Se a cardinalidade do to end for n, a coleção<Ref \<T>> será retornada.  
  
 Exemplo:  
  
```sql  
SELECT a.AddressID, (SELECT VALUE DEREF(v) FROM
    NAVIGATE(a, AdventureWorksModel.FK_SalesOrderHeader_Address_BillToAddressID) AS v)
    FROM AdventureWorksEntities.Address AS a  
```  
  
 Saída:  
  
|AddressID|  
|---------------|  
|1|  
|2|  
|3|  
|...|  
  
## <a name="select-value-and-select"></a>SELECT VALUE AND SELECT  
  
### <a name="select-value"></a>SELECT VALUE  

 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornece a cláusula SELECT VALUE para ignorar a construção de linha implícita. Somente um item pode ser especificado em uma cláusula SELECT VALUE. Quando tal cláusula é usada, nenhum wrapper de linha é construído em volta dos itens na cláusula SELECT e uma coleção da forma desejada pode ser produzida, por exemplo: `SELECT VALUE a` .  
  
 Exemplo:  
  
```sql  
SELECT VALUE p.Name FROM AdventureWorksEntities.Product AS p
```  
  
 Saída:  
  
|Nome|  
|----------|  
|Adjustable Race|  
|Suporte de bicicleta multifuncional|  
|AWC Logo Cap|  
|...|  
  
### <a name="select"></a>SELECT  

 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] também fornece o construtor de linha para construir linhas arbitrárias. SELECT utiliza um ou mais elementos na projeção e resulta em um registro de dados com campos; por exemplo: `SELECT a, b, c`.  
  
 Exemplo:  
  
 SELECT p.Name, p.ProductID FROM AdventureWorksEntities.Product as p Output:  
  
|Nome|ProductID|  
|----------|---------------|  
|Adjustable Race|1|  
|Suporte de bicicleta multifuncional|879|  
|AWC Logo Cap|712|  
|...|...|  
  
## <a name="case-expression"></a>CASE EXPRESSION  

 A [expressão CASE](case-entity-sql.md) avalia um conjunto de expressões boolianas para determinar o resultado.  
  
 Exemplo:  
  
```sql  
CASE WHEN AVG({25,12,11}) < 100 THEN TRUE ELSE FALSE END  
```  
  
 Saída:  
  
|Valor|  
|-----------|  
|TRUE|  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
- [Visão geral da Entity SQL](entity-sql-overview.md)
