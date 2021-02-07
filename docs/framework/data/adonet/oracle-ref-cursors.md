---
description: 'Saiba mais sobre: CURSOres de referência do Oracle'
title: REF CURSORs do Oracle
ms.date: 03/30/2017
ms.assetid: c6b25b8b-0bdd-41b2-9c7c-661f070c2247
ms.openlocfilehash: 0a9c5e95a9f0d2da74fd6a3db19f15699a3e2787
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99672446"
---
# <a name="oracle-ref-cursors"></a>REF CURSORs do Oracle

O .NET Framework Provedor de Dados para Oracle dá suporte ao tipo de dados **cursor de referência** do Oracle. Ao usar o provedor de dados para trabalhar com REF CURSORs do Oracle, você deve considerar os seguintes comportamentos.  
  
> [!NOTE]
> Alguns comportamentos diferem dos do Provedor OLE DB para Oracle (MSDAORA).  
  
- Por motivos de desempenho, o Provedor de Dados para Oracle não associa automaticamente tipos de dados de **cursor de referência** , como MSDAORA, a menos que você os especifique explicitamente.  
  
- O provedor de dados não oferece suporte a nenhuma sequência de escape de ODBC, incluindo o escape {resultset} usado para especificar parâmetros de REF CURSOR.  
  
- Para executar um procedimento armazenado que retorna CURSOres de referência, você deve definir os parâmetros no <xref:System.Data.OracleClient.OracleParameterCollection> com um <xref:System.Data.OracleClient.OracleType> de **cursor** e uma <xref:System.Data.OracleClient.OracleParameter.Direction%2A> de **saída**. O provedor de dados oferece suporte a REF CURSORs de associação como parâmetros de saída somente. O provedor não oferece suporte a REF CURSORs como parâmetros de entrada.  
  
- A obtenção de <xref:System.Data.OracleClient.OracleDataReader> do valor do parâmetro não é suportada. Os valores são do tipo <xref:System.DBNull> após a execução do comando.  
  
- O único valor de enumeração **CommandBehavior** que funciona com cursores de referência (por exemplo, ao chamar <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A> ) é **CloseConnection**; todos os outros são ignorados.  
  
- A ordem dos CURSOres de referência no **OracleDataReader** depende da ordem dos parâmetros no **OracleParameterCollection**. A propriedade <xref:System.Data.OracleClient.OracleParameter.ParameterName%2A> é ignorada.  
  
- Não há suporte para o tipo de dados de **tabela** PL/SQL. No entanto, REF CURSORs são mais eficientes. Se você precisar usar um tipo de dados de **tabela** , use o OLE DB .NET provedor de dados com MSDAORA.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Exemplos de REF CURSOR](ref-cursor-examples.md)  
 Contém três exemplos que demonstram como usar REF CURSORs.  
  
 [Parâmetros de REF CURSOR em um OracleDataReader](ref-cursor-parameters-in-an-oracledatareader.md)  
 Demonstra como executar um procedimento armazenado PL/SQL que retorna um parâmetro de CURSOR REF e lê o valor como um **OracleDataReader**.  
  
 [Recuperar dados de vários REF CURSORs usando um OracleDataReader](retrieving-data-from-multiple-ref-cursors.md)  
 Demonstra como executar um procedimento armazenado PL/SQL que retorna dois parâmetros de CURSOR de referência e lê os valores usando um **OracleDataReader**.  
  
 [Preenchendo um DataSet usando um ou mais REF CURSORs](filling-a-dataset-using-one-or-more-ref-cursors.md)  
 Demonstra como executar um procedimento armazenado PL/SQL, que retorna dois parâmetros de REF CURSOR e preenche um <xref:System.Data.DataSet> com as linhas retornadas.  
  
## <a name="see-also"></a>Consulte também

- [Oracle e ADO.NET](oracle-and-adonet.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
