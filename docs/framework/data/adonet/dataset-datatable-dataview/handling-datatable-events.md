---
description: 'Saiba mais sobre: Manipulando eventos de DataTable'
title: Manipulação de eventos de DataTable
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 62f404a5-13ea-4b93-a29f-55b74a16c9d3
ms.openlocfilehash: 89519345ec0c9f2348153c480366396a66d37ae0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652348"
---
# <a name="handling-datatable-events"></a>Manipulação de eventos de DataTable

O <xref:System.Data.DataTable> objeto fornece uma série de eventos que podem ser processados por um aplicativo. A tabela a seguir descreve os `DataTable` eventos.  
  
|Evento|Descrição|  
|-----------|-----------------|  
|<xref:System.Data.DataTable.Initialized>|Ocorre depois que o <xref:System.Data.DataTable.EndInit%2A> método de um `DataTable` é chamado. Esse evento destina-se principalmente ao suporte a cenários de tempo de design.|  
|<xref:System.Data.DataTable.ColumnChanged>|Ocorre depois que um valor é alterado com êxito em um <xref:System.Data.DataColumn> .|  
|<xref:System.Data.DataTable.ColumnChanging>|Ocorre quando um valor é enviado para um `DataColumn` .|  
|<xref:System.Data.DataTable.RowChanged>|Ocorre depois `DataColumn` que um valor ou o <xref:System.Data.DataRow.RowState%2A> de um <xref:System.Data.DataRow> no `DataTable` foi alterado com êxito.|  
|<xref:System.Data.DataTable.RowChanging>|Ocorre quando uma alteração é enviada para um `DataColumn` valor ou o `RowState` de um `DataRow` no `DataTable` .|  
|<xref:System.Data.DataTable.RowDeleted>|Ocorre depois `DataRow` que um no `DataTable` é marcado como `Deleted` .|  
|<xref:System.Data.DataTable.RowDeleting>|Ocorre antes que um `DataRow` no `DataTable` seja marcado como `Deleted` .|  
|<xref:System.Data.DataTable.TableCleared>|Ocorre depois que uma chamada para o <xref:System.Data.DataTable.Clear%2A> método de `DataTable` foi limpa com êxito a cada `DataRow` .|  
|<xref:System.Data.DataTable.TableClearing>|Ocorre depois que o `Clear` método é chamado, mas antes do `Clear` início da operação.|  
|<xref:System.Data.DataTable.TableNewRow>|Ocorre depois que um novo `DataRow` é criado por uma chamada para o `NewRow` método do `DataTable` .|  
|<xref:System.ComponentModel.MarshalByValueComponent.Disposed>|Ocorre quando o `DataTable` é `Disposed` . Herdado de <xref:System.ComponentModel.MarshalByValueComponent>.|  
  
> [!NOTE]
> A maioria das operações que adicionam ou excluem linhas não geram os `ColumnChanged` `ColumnChanging` eventos e. No entanto, o `ReadXml` método gera `ColumnChanged` e `ColumnChanging` eventos, a menos que `XmlReadMode` seja definido como `DiffGram` ou seja definido como `Auto` quando o documento XML que está sendo lido for um `DiffGram` .  
  
> [!WARNING]
> Os dados corrompidos podem ocorrer se os dados são modificados em um `DataSet` do qual o `RowChanged` evento é gerado. Nenhuma exceção será gerada se ocorrer corrupção de dados.  
  
## <a name="additional-related-events"></a>Eventos relacionados adicionais  

 A <xref:System.Data.DataTable.Constraints%2A> propriedade contém uma <xref:System.Data.ConstraintCollection> instância. A <xref:System.Data.ConstraintCollection> classe expõe um <xref:System.Data.ConstraintCollection.CollectionChanged> evento. Esse evento é acionado quando uma restrição é adicionada, modificada ou removida do `ConstraintCollection` .  
  
 A <xref:System.Data.DataTable.Columns%2A> propriedade contém uma <xref:System.Data.DataColumnCollection> instância. A `DataColumnCollection` classe expõe um <xref:System.Data.DataColumnCollection.CollectionChanged> evento. Esse evento é acionado quando um `DataColumn` é adicionado, modificado ou removido do `DataColumnCollection` . As modificações que fazem com que o evento seja acionado incluem alterações no nome, tipo, expressão ou posição ordinal de uma coluna.  
  
 A <xref:System.Data.DataSet.Tables%2A> propriedade de um <xref:System.Data.DataSet> mantém uma <xref:System.Data.DataTableCollection> instância. A `DataTableCollection` classe expõe tanto um `CollectionChanged` quanto um `CollectionChanging` evento. Esses eventos são acionados quando um `DataTable` é adicionado ou removido do `DataSet` .  
  
 As alterações em `DataRows` também podem disparar eventos para um associado <xref:System.Data.DataView> . A `DataView` classe expõe um <xref:System.Data.DataView.ListChanged> evento que é acionado quando um `DataColumn` valor é alterado ou quando a ordem de composição ou de classificação da exibição é alterada. A <xref:System.Data.DataRowView> classe expõe um <xref:System.Data.DataRowView.PropertyChanged> evento que é acionado quando um valor associado é `DataColumn` alterado.  
  
## <a name="sequence-of-operations"></a>sequência de operações  

 Aqui está a sequência de operações que ocorrem quando uma `DataRow` é adicionada, modificada ou excluída:  
  
1. Crie o registro proposto e aplique as alterações.  
  
2. Verifique as restrições de colunas que não são de expressão.  
  
3. Gere os `RowChanging` `RowDeleting` eventos ou conforme aplicável.  
  
4. Defina o registro proposto como o registro atual.  
  
5. Atualize todos os índices associados.  
  
6. Gerar `ListChanged` eventos para `DataView` objetos associados e `PropertyChanged` eventos para `DataRowView` objetos associados.  
  
7. Avalie todas as colunas de expressão, mas adie a verificação de qualquer restrição nessas colunas.  
  
8. Gerar `ListChanged` eventos para `DataView` objetos associados e `PropertyChanged` eventos para `DataRowView` objetos associados afetados pelas avaliações de coluna de expressão.  
  
9. Gerar `RowChanged` ou `RowDeleted` eventos conforme aplicável.  
  
10. Verifique as restrições nas colunas de expressão.  
  
> [!NOTE]
> As alterações nas colunas de expressão nunca geram `DataTable` eventos. As alterações nas colunas de expressão geram `DataView` e apenas `DataRowView` eventos. As colunas de expressão podem ter dependências em várias outras colunas e podem ser avaliadas várias vezes durante uma única `DataRow` operação. Cada avaliação de expressão gera eventos e uma única `DataRow` operação pode gerar vários `ListChanged` `PropertyChanged` eventos e quando as colunas de expressão são afetadas, possivelmente incluindo vários eventos para a mesma coluna de expressão.  
  
> [!WARNING]
> Não lance um <xref:System.NullReferenceException> dentro do `RowChanged` manipulador de eventos. Se um <xref:System.NullReferenceException> for lançado no `RowChanged` evento de a `DataTable` , o `DataTable` será corrompido.  
  
### <a name="example"></a>Exemplo  

 O exemplo a seguir demonstra como criar manipuladores de eventos para os eventos,,,,,, `RowChanged` `RowChanging` `RowDeleted` `RowDeleting` `ColumnChanged` `ColumnChanging` `TableNewRow` , `TableCleared` e `TableClearing` . Cada manipulador de eventos exibe a saída na janela do console quando ela é acionada.  
  
 [!code-csharp[DataWorks DataTable.Events#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataTable.Events/CS/source.cs#1)]
 [!code-vb[DataWorks DataTable.Events#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataTable.Events/VB/source.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- [Manipulando dados em uma DataTable](manipulating-data-in-a-datatable.md)
- [Manipulação de eventos DataAdapter](../handling-dataadapter-events.md)
- [Manipular eventos do DataSet](handling-dataset-events.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
