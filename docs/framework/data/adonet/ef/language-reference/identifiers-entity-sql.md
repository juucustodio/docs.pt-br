---
description: 'Saiba mais sobre: identificadores (Entity SQL)'
title: Identificadores (Entity SQL)
ms.date: 03/30/2017
ms.assetid: d58a5edd-7b5c-48e1-b5d7-a326ff426aa4
ms.openlocfilehash: 932f45e8b65b6244eada330caeb9a04b6560d427
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99748655"
---
# <a name="identifiers-entity-sql"></a>Identificadores (Entity SQL)

Os identificadores são usados em [!INCLUDE[esql](../../../../../../includes/esql-md.md)] para representar alias de expressão de consulta, referências variáveis, propriedades de objetos, funções, e assim por diante. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornece dois tipos de identificadores: identificadores simples e identificadores entre aspas.  
  
## <a name="simple-identifiers"></a>Identificadores simples  

 Um identificador simples no [!INCLUDE[esql](../../../../../../includes/esql-md.md)] é uma sequência de caracteres alfanuméricos e de sublinhado. O primeiro caractere identificador deve ser um caractere alfabético (a-z ou A-Z).  
  
## <a name="quoted-identifiers"></a>Identificadores entre aspas  

 Um identificador citado é qualquer sequência de caracteres colocados entre colchetes ([]). Os identificadores citados permitem que você especifique identificadores com caracteres que não são válidos em identificadores. Todos os caracteres entre colchetes se tornam parte do identificador, incluindo todo o espaço em branco.  
  
 Um identificador citado não pode incluir os seguintes caracteres:  
  
- Nova linha.  
  
- Retornos de carro.  
  
- Guias.  
  
- Retrocesso.  
  
- Colchetes adicionais (isto é, colchetes dentro de colchetes que ícones o identificador).  
  
 Um identificador citar- pode incluir caracteres Unicode.  
  
 Os identificadores citados permite que você crie os caracteres de nome de propriedade que não são válidos em identificadores, conforme ilustrado no exemplo a seguir:  
  
 `SELECT c.ContactName AS [Contact Name] FROM customers AS c`  
  
 Você também pode usar identificadores citados para especificar um identificador que é uma palavra-chave reservado de [!INCLUDE[esql](../../../../../../includes/esql-md.md)]. Por exemplo, se o tipo `Email` tem uma propriedade chamada “de”, você pode desambiguar a palavra-chave de reservado de usar colchetes, como segue:  
  
 `SELECT e.[From] FROM emails AS e`  
  
 Você pode usar um identificador citado no lado direito de um operador ponto (.).  
  
 `SELECT t FROM ts as t WHERE t.[property] == 2`  
  
 Para usar o colchete quadrado em um identificador, adicione um sinal quadrado adicional. No exemplo a seguir “`abc]`” é o identificador:  
  
 `SELECT t from ts as t WHERE t.[abc]]] == 2`  
  
 Para a semântica de comparação de identificador entre aspas, consulte [conjunto de caracteres de entrada](input-character-set-entity-sql.md).  
  
## <a name="aliasing-rules"></a>Regras de serrilha  

 É recomendável especificar aliases em [!INCLUDE[esql](../../../../../../includes/esql-md.md)] consultas sempre que necessário, incluindo as seguintes [!INCLUDE[esql](../../../../../../includes/esql-md.md)] construções:  
  
- Campos de um construtor de linha.  
  
- Itens na cláusula de uma expressão de consulta.  
  
- Itens na cláusula SELECT de uma expressão de consulta.  
  
- Itens em cláusula GROUP BY de uma expressão de consulta.  
  
### <a name="valid-aliases"></a>Alias válidos  

 Os aliases válidos no [!INCLUDE[esql](../../../../../../includes/esql-md.md)] são um identificador simples ou um identificador entre aspas.  
  
### <a name="alias-generation"></a>Geração do alias  

 Se nenhum alias for especificado em uma [!INCLUDE[esql](../../../../../../includes/esql-md.md)] expressão de consulta, o [!INCLUDE[esql](../../../../../../includes/esql-md.md)] tentará gerar um alias com base nas seguintes regras simples:  
  
- Se a expressão de consulta (para um alias são não especificado) é um identificador simples ou citado, o identificador é usado como o alias. Por exemplo, `ROW(a, [b])` torna-se `ROW(a AS a, [b] AS [b])`.  
  
- Se a expressão de consulta é uma expressão mais complexa, mas o componente do último dessa expressão de consulta é um identificador simples, então o identificador é usado como o alias. Por exemplo, `ROW(a.a1, b.[b1])` torna-se `ROW(a.a1 AS a1, b.[b1] AS [b1])`.  
  
 Recomendamos que você não use a serrilha implícita se você desejar usar posteriormente o nome do alias. Quando o alias (implícitas ou explícitas) entrem em conflito ou são repetidas no mesmo escopo, haverá um erro de compilação. Um alias implícitas transmitirão a compilação mesmo se houver um alias explícitas ou implícitas de mesmo nome.  
  
 Alias implícitas são gerado automaticamente com base na entrada do usuário. Por exemplo, a seguinte linha de código gerará o NOME porque um alias para as duas colunas e portanto estarão em conflito.  
  
```sql  
SELECT product.NAME, person.NAME  
```  
  
 A seguinte linha de código, que usa alias explícitas, também falhará. No entanto, a falha será mais aparente ler o código.  
  
```sql  
SELECT 1 AS X, 2 AS X …  
```  
  
## <a name="scoping-rules"></a>Regras de escopo  

 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] define regras de escopo que determinam quando variáveis específicas são visíveis na linguagem de consulta. Algumas expressões ou instruções apresenta novos nomes. As regras de escopo determinar onde os nomes podem ser usados, e quando ou onde uma nova declaração com o mesmo nome que outro pode ocultar o antecessor.  
  
 Quando os nomes são definidos em uma [!INCLUDE[esql](../../../../../../includes/esql-md.md)] consulta, eles são considerados definidos dentro de um escopo. Um escopo aborda uma região inteira de consulta. Todas as expressões ou referências de nome em um determinado escopo podem ver os nomes que são definidos dentro do escopo. Antes que um escopo iniciar e depois termina, os nomes que são definidos no escopo não podem ser referenciados.  
  
 Os escopos podem ser aninhados. Partes de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] introduzem novos escopos que abrangem regiões inteiras, e essas regiões podem conter outras [!INCLUDE[esql](../../../../../../includes/esql-md.md)] expressões que também introduzem escopos. Quando os escopos estão aninhados, referências podem ser feitas para nomes que são definidos no escopo interno, que contém a referência. As referências podem também ser feitas a todos os nomes que são definidos em quaisquer escopos externos. Todos os dois escopos definidos no mesmo escopo são considerados escopos irmãos. Referências não podem ser feitas para nomes que são definidos em escopos irmãos.  
  
 Se um nome declarado em um escopo interno corresponde a um nome declarado em um escopo externo, referências dentro do escopo interno ou em escopos declarados dentro do escopo se referem somente o nome recentemente declarado. O nome no escopo externo está oculto.  
  
 Mesmo dentro do mesmo escopo, os nomes não pode ser referenciado antes que eles sejam definidos.  
  
 Os nomes globais podem existir como parte do ambiente de execução. Isso pode incluir nomes de coleções ou de variáveis de ambiente persistentes. Para que um nome é global, deve ser declarado no escopo mais externo.  
  
 Os parâmetros não estão em um escopo. Porque as referências aos parâmetros incluem a sintaxe especial, os nomes dos parâmetros nunca colidirão com outros nomes na consulta.  
  
### <a name="query-expressions"></a>Expressões de consulta  

 Uma [!INCLUDE[esql](../../../../../../includes/esql-md.md)] expressão de consulta introduz um novo escopo. Nomes que são definidos na cláusula são apresentados no escopo por ordem de aparência, da esquerda para a direita. Na lista de adição, expressões podem referenciar os nomes que foram anteriormente definido na lista. As propriedades públicas (campos e assim por diante) dos elementos identificadas na cláusula não são adicionadas ao - escopo. Sempre devem ser referenciados pelo nome alias- qualificado. Normalmente, todas as partes da expressão SELECT são considerados - dentro do escopo.  
  
 O cláusula GROUP BY também apresenta um novo escopo irmãos. Cada grupo pode ter um nome de grupo que faz referência à coleção de elementos no grupo. Cada expressão de agrupamento também introduzir um novo nome no grupo- escopo. Além disso, a agregação de in a aninhada (ou o grupo nomeado) também são adicionados ao escopo. As expressões elas mesmas de agrupamento estão dentro do escopo -. No entanto, quando um cláusula GROUP BY é usado, a seleto- lista (projeção), TENDO a cláusula, e a cláusula GROUP BY são considerados estar dentro do escopo grupo-, e não a - escopo. Agregados recebem o tratamento especial, como descrito na lista com marcadores.  
  
 Os seguintes são notas adicionais sobre escopos:  
  
- A lista seleto- pode gerar nomes novos no escopo, em ordem. As expressões de projeção à direita podem se referir aos nomes projetados para a esquerda.  
  
- A cláusula GROUP BY pode consultar os nomes (alias) especificados na lista select.  
  
- A ordem de classificação das cláusulas dentro da expressão SELECT determina a ordem que os nomes são introduzidos no escopo. A cláusula é avaliado primeiro, seguido por uma cláusula WHERE, cláusula GROUP BY TENDO, a cláusula, a cláusula SELECT, e finalmente a cláusula GROUP BY.  
  
### <a name="aggregate-handling"></a>Tratamento aggregate  

 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] dá suporte a duas formas de agregações: agregações baseadas em coleção e agregações baseadas em grupo. Agregados coleção com base são a compilação preferencial em [!INCLUDE[esql](../../../../../../includes/esql-md.md)], e grupo- com agregados são suportadas para compatibilidade SQL.  
  
 Ao resolver uma agregação, o [!INCLUDE[esql](../../../../../../includes/esql-md.md)] primeiro tenta tratá-la como uma agregação baseada em coleção. Se isso falhar, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] o transformará a entrada de agregação em uma referência à agregação Nest e tentará resolver essa nova expressão, conforme ilustrado no exemplo a seguir.  
  
 `AVG(t.c) becomes AVG(group..(t.c))`  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
- [Visão geral da Entity SQL](entity-sql-overview.md)
- [Conjunto de caracteres de entrada](input-character-set-entity-sql.md)
