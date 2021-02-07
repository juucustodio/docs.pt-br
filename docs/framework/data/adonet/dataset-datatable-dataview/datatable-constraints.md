---
description: 'Saiba mais sobre: restrições de DataTable'
title: Restrições de DataTable
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 27c9f2fd-f64d-4b4e-bbf6-1d24f47067cb
ms.openlocfilehash: 0c712115fd87fefae3578b2f3fc0adfc416f412e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724902"
---
# <a name="datatable-constraints"></a>Restrições de DataTable

Você pode usar restrições para impor restrições nos dados em um <xref:System.Data.DataTable>, para manter a integridade dos dados. Uma restrição é uma regra automática, aplicada a uma coluna ou colunas relacionadas, que determina o curso de ação quando o valor de uma linha é modificado de alguma maneira. As restrições são impostas quando a `System.Data.DataSet.EnforceConstraints` propriedade de <xref:System.Data.DataSet> é **verdadeira**. Para um exemplo de código que mostra como definir a propriedade `EnforceConstraints`, consulte o tópico de referência <xref:System.Data.DataSet.EnforceConstraints%2A>.  
  
 Há dois tipos de restrições no ADO.NET: o <xref:System.Data.ForeignKeyConstraint> e o <xref:System.Data.UniqueConstraint>. Por padrão, ambas as restrições são criadas automaticamente quando você cria uma relação entre duas ou mais tabelas adicionando um <xref:System.Data.DataRelation> ao **conjunto** de informações. No entanto, você pode desabilitar esse comportamento especificando **createConstraints**  =  **false** ao criar a relação.  
  
## <a name="foreignkeyconstraint"></a>ForeignKeyConstraint  

 Um **ForeignKeyConstraint** impõe regras sobre como as atualizações e exclusões para tabelas relacionadas são propagadas. Por exemplo, se um valor em uma linha de uma tabela for atualizado ou excluído e esse mesmo valor também for usado em uma ou mais tabelas relacionadas, um **ForeignKeyConstraint** determinará o que acontece nas tabelas relacionadas.  
  
 As <xref:System.Data.ForeignKeyConstraint.DeleteRule%2A> <xref:System.Data.ForeignKeyConstraint.UpdateRule%2A> Propriedades e de **ForeignKeyConstraint** definem a ação a ser tomada quando o usuário tenta excluir ou atualizar uma linha em uma tabela relacionada. A tabela a seguir descreve as diferentes configurações disponíveis para as propriedades **DeleteRule** e **UpdateRule** do **ForeignKeyConstraint**.  
  
|Configuração de regra|Descrição|  
|------------------|-----------------|  
|**Cascade**|Excluir ou atualizar linhas relacionadas.|  
|**SetNull**|Defina valores em linhas relacionadas como **DBNull**.|  
|**SetDefault**|Definir valores em linhas relacionadas para o valor padrão.|  
|**Nenhum**|Nenhuma ação em linhas relacionadas. Este é o padrão.|  
  
 Um **ForeignKeyConstraint** pode restringir, bem como propagar, alterações em colunas relacionadas. Dependendo das propriedades definidas para o **ForeignKeyConstraint** de uma coluna, se a propriedade **EnforceConstraints** do **conjunto** de dado for **true**, executar determinadas operações na linha pai resultará em uma exceção. Por exemplo, se a propriedade **DeleteRule** de **ForeignKeyConstraint** for **None**, uma linha pai não poderá ser excluída se tiver qualquer linha filho.  
  
 Você pode criar uma restrição FOREIGN KEY entre colunas únicas ou entre uma matriz de colunas usando o construtor **ForeignKeyConstraint** . Passe o objeto **ForeignKeyConstraint** resultante para o método **Add** da propriedade **Constraints** da tabela, que é uma **ConstraintCollection**. Você também pode passar argumentos de construtor para várias sobrecargas do método **Add** de uma **ConstraintCollection** para criar um **ForeignKeyConstraint**.  
  
 Ao criar um **ForeignKeyConstraint**, você pode passar os valores de **DeleteRule** e **UpdateRule** para o construtor como argumentos, ou pode defini-los como propriedades, como no exemplo a seguir (em que o valor de **DeleteRule** é definido como **nenhum**).  
  
```vb  
Dim custOrderFK As ForeignKeyConstraint = New ForeignKeyConstraint("CustOrderFK", _  
  custDS.Tables("CustTable").Columns("CustomerID"), _  
  custDS.Tables("OrdersTable").Columns("CustomerID"))  
custOrderFK.DeleteRule = Rule.None
' Cannot delete a customer value that has associated existing orders.  
custDS.Tables("OrdersTable").Constraints.Add(custOrderFK)  
```  
  
```csharp  
ForeignKeyConstraint custOrderFK = new ForeignKeyConstraint("CustOrderFK",  
  custDS.Tables["CustTable"].Columns["CustomerID"],
  custDS.Tables["OrdersTable"].Columns["CustomerID"]);  
custOrderFK.DeleteRule = Rule.None;
// Cannot delete a customer value that has associated existing orders.  
custDS.Tables["OrdersTable"].Constraints.Add(custOrderFK);  
```  
  
### <a name="acceptrejectrule"></a>AcceptRejectRule  

 As alterações nas linhas podem ser aceitas usando o método **AcceptChanges** ou canceladas usando o método **RejectChanges** do **DataSet**, **DataTable** ou **DataRow**. Quando um **conjunto** de um DataSet contém **ForeignKeyConstraint**, invocar os métodos **AcceptChanges** ou **RejectChanges** impõe o **AcceptRejectRule**. A propriedade **AcceptRejectRule** de **ForeignKeyConstraint** determina qual ação será executada nas linhas filhas quando **AcceptChanges** ou **RejectChanges** for chamado na linha pai.  
  
 A tabela a seguir lista as configurações disponíveis para o **AcceptRejectRule**.  
  
|Configuração de regra|Descrição|  
|------------------|-----------------|  
|**Cascade**|Aceitar ou rejeitar alterações em linhas filho.|  
|**Nenhum**|Nenhuma ação em linhas filho. Este é o padrão.|  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir cria um <xref:System.Data.ForeignKeyConstraint>, define várias das suas propriedades, incluindo <xref:System.Data.ForeignKeyConstraint.AcceptRejectRule%2A> e adiciona-os ao <xref:System.Data.ConstraintCollection> de um objeto <xref:System.Data.DataTable>.  
  
 [!code-csharp[DataWorks Data.AcceptRejectRule#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.AcceptRejectRule/CS/source.cs#1)]
 [!code-vb[DataWorks Data.AcceptRejectRule#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.AcceptRejectRule/VB/source.vb#1)]  
  
## <a name="uniqueconstraint"></a>UniqueConstraint  

 O objeto **UniqueConstraint** , que pode ser atribuído a uma única coluna ou a uma matriz de colunas em uma **DataTable**, garante que todos os dados na coluna ou colunas especificadas sejam exclusivos por linha. Você pode criar uma restrição exclusiva para uma coluna ou matriz de colunas usando o construtor **UniqueConstraint** . Passe o objeto **UniqueConstraint** resultante para o método **Add** da propriedade **Constraints** da tabela, que é uma **ConstraintCollection**. Você também pode passar argumentos de construtor para várias sobrecargas do método **Add** de uma **ConstraintCollection** para criar um **UniqueConstraint**. Ao criar um **UniqueConstraint** para uma coluna ou colunas, você pode opcionalmente especificar se a coluna ou as colunas são uma chave primária.  
  
 Você também pode criar uma restrição exclusiva para uma coluna definindo a propriedade **Unique** da coluna como **true**. Como alternativa, definir a propriedade **Unique** de uma única coluna como **false** remove qualquer restrição exclusiva que possa existir. Definir uma coluna ou colunas como uma chave primária para uma tabela criará automaticamente uma restrição exclusiva para a coluna ou colunas especificadas. Se você remover uma coluna da propriedade **PrimaryKey** de uma **DataTable**, o **UniqueConstraint** será removido.  
  
 O exemplo a seguir cria um **UniqueConstraint** para duas colunas de uma **DataTable**.  
  
```vb  
Dim custTable As DataTable = custDS.Tables("Customers")  
Dim custUnique As UniqueConstraint = _  
    New UniqueConstraint(New DataColumn()   {custTable.Columns("CustomerID"), _  
    custTable.Columns("CompanyName")})  
custDS.Tables("Customers").Constraints.Add(custUnique)  
```  
  
```csharp  
DataTable custTable = custDS.Tables["Customers"];  
UniqueConstraint custUnique = new UniqueConstraint(new DataColumn[]
    {custTable.Columns["CustomerID"],
    custTable.Columns["CompanyName"]});  
custDS.Tables["Customers"].Constraints.Add(custUnique);  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataRelation>
- <xref:System.Data.DataTable>
- <xref:System.Data.ForeignKeyConstraint>
- <xref:System.Data.UniqueConstraint>
- [Definição do esquema de DataTable](datatable-schema-definition.md)
- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
