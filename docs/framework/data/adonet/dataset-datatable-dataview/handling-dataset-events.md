---
description: 'Saiba mais sobre: Manipulando eventos de conjunto de informações'
title: Manipular eventos do DataSet
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 54edefe0-bc38-419b-b486-3d8a0c356f13
ms.openlocfilehash: a0000396c7c1e2762a5a2937f7979d917257facc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652361"
---
# <a name="handling-dataset-events"></a>Manipular eventos do DataSet

O <xref:System.Data.DataSet> objeto fornece três eventos: <xref:System.ComponentModel.MarshalByValueComponent.Disposed> , <xref:System.Data.DataSet.Initialized> e <xref:System.Data.DataSet.MergeFailed> .  
  
## <a name="the-mergefailed-event"></a>O evento MergeFailed  

 O evento mais comumente usado do `DataSet` objeto é `MergeFailed` , que é gerado quando o esquema dos `DataSet` objetos que estão sendo mesclados está em conflito. Isso ocorre quando um destino e origem <xref:System.Data.DataRow> têm o mesmo valor de chave primária e a <xref:System.Data.DataSet.EnforceConstraints%2A> propriedade é definida como `true` . Por exemplo, se as colunas de chave primária de uma tabela que está sendo mesclada forem as mesmas entre as tabelas nos dois `DataSet` objetos, uma exceção será gerada e o `MergeFailed` evento será gerado. O <xref:System.Data.MergeFailedEventArgs> objeto passado para o `MergeFailed` evento tem uma <xref:System.Data.MergeFailedEventArgs.Conflict%2A> propriedade que identifica o conflito no esquema entre os dois `DataSet` objetos e uma <xref:System.Data.MergeFailedEventArgs.Table%2A> propriedade que identifica o nome da tabela em conflito.  
  
 O fragmento de código a seguir demonstra como adicionar um manipulador de eventos para o `MergeFailed` evento.  
  
```vb  
AddHandler workDS.MergeFailed, New MergeFailedEventHandler( _  
  AddressOf DataSetMergeFailed)  
  
Private Shared Sub DataSetMergeFailed(  _  
  sender As Object,args As MergeFailedEventArgs)  
  Console.WriteLine("Merge failed for table " & args.Table.TableName)  
  Console.WriteLine("Conflict = " & args.Conflict)  
End Sub  
```  
  
```csharp  
workDS.MergeFailed += new MergeFailedEventHandler(DataSetMergeFailed);  
  
private static void DataSetMergeFailed(  
  object sender, MergeFailedEventArgs args)  
{  
  Console.WriteLine("Merge failed for table " + args.Table.TableName);  
  Console.WriteLine("Conflict = " + args.Conflict);  
}  
```  
  
## <a name="the-initialized-event"></a>O evento initialized  

 O <xref:System.Data.DataSet.Initialized> evento ocorre depois que o `DataSet` Construtor Inicializa uma nova instância do `DataSet` .  
  
 A <xref:System.Data.DataSet.IsInitialized%2A> propriedade retornará `true` se o `DataSet` tiver concluído a inicialização; caso contrário, retornará `false` . O <xref:System.Data.DataSet.BeginInit%2A> método, que começa a inicialização de um `DataSet` , define <xref:System.Data.DataSet.IsInitialized%2A> como `false` . O <xref:System.Data.DataSet.EndInit%2A> método, que termina a inicialização do `DataSet` , o define como `true` . Esses métodos são usados pelo ambiente de design do Visual Studio para inicializar um `DataSet` que está sendo usado por outro componente. Normalmente, você não os usará em seu código.  
  
## <a name="the-disposed-event"></a>O evento Descartado  

 `DataSet` é derivado da <xref:System.ComponentModel.MarshalByValueComponent> classe, que expõe o <xref:System.ComponentModel.MarshalByValueComponent.Dispose%2A> método e o <xref:System.ComponentModel.MarshalByValueComponent.Disposed> evento. O <xref:System.ComponentModel.MarshalByValueComponent.Disposed> evento adiciona um manipulador de eventos para escutar o evento Descartado no componente. Você pode usar o <xref:System.ComponentModel.MarshalByValueComponent.Disposed> evento de um `DataSet` se quiser executar código quando o <xref:System.ComponentModel.MarshalByValueComponent.Dispose%2A> método for chamado. <xref:System.ComponentModel.MarshalByValueComponent.Dispose%2A> Libera os recursos usados pelo <xref:System.ComponentModel.MarshalByValueComponent> .  
  
> [!NOTE]
> Os `DataSet` `DataTable` objetos e herdam de <xref:System.ComponentModel.MarshalByValueComponent> e dão suporte à <xref:System.Runtime.Serialization.ISerializable> interface para comunicação remota. Esses são os únicos objetos ADO.NET que podem ser remotos. Para obter mais informações, consulte [comunicação remota do .net](/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100)).  
  
 Para obter informações sobre outros eventos disponíveis ao trabalhar com um `DataSet` , consulte [manipulando eventos de DataTable](handling-datatable-events.md) e [manipulando eventos de DataAdapter](../handling-dataadapter-events.md).  
  
## <a name="see-also"></a>Consulte também

- [DataSets, DataTables e DataViews](index.md)
- [Validando dados](/previous-versions/visualstudio/visual-studio-2013/t3b36awf(v=vs.120))
- [Recuperando e modificando dados no ADO.NET](../retrieving-and-modifying-data.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
