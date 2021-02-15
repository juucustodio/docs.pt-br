---
description: 'Saiba mais sobre: Manipulando eventos de DataView'
title: Manipulação de eventos de DataView
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e5675663-fc91-4e0d-87a9-481b25b64c0f
ms.openlocfilehash: d3e72adefa6b320d48b90d481a20644b62009cdd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652309"
---
# <a name="handling-dataview-events"></a>Manipulação de eventos de DataView

Você pode usar o <xref:System.Data.DataView.ListChanged> evento do <xref:System.Data.DataView> para determinar se um modo de exibição foi atualizado. As atualizações que geram o evento incluem adicionar, excluir ou modificar uma linha na tabela subjacente; adicionando ou excluindo uma coluna para o esquema da tabela subjacente; e uma alteração em uma relação pai ou filho. O evento **ListChanged** também notifica se a lista de linhas que você está exibindo mudou significativamente devido ao aplicativo de uma nova ordem de classificação ou de um filtro.  
  
 O evento **ListChanged** implementa o delegado **ListChangedEventHandler** do <xref:System.ComponentModel> namespace e usa como entrada um <xref:System.ComponentModel.ListChangedEventArgs> objeto. Você pode determinar que tipo de alteração ocorreu usando o <xref:System.ComponentModel.ListChangedType> valor de enumeração na propriedade **ListChangedType** do objeto **ListChangedEventArgs** . Para alterações que envolvem adicionar, excluir ou mover linhas, o novo índice da linha adicionada ou movida e o índice anterior da linha excluída podem ser acessados usando a propriedade **NewIndex** do objeto **ListChangedEventArgs** . No caso de uma linha movida, o índice anterior da linha movida pode ser acessado usando a propriedade **OldIndex** do objeto **ListChangedEventArgs** .  
  
 O **DataViewManager** também expõe um evento **ListChanged** para notificá-lo se uma tabela tiver sido adicionada ou removida, ou se uma alteração tiver sido feita na coleção **Relations** do **DataSet** subjacente.  
  
 O exemplo de código a seguir mostra como adicionar um manipulador de eventos **ListChanged** .  
  
```vb  
AddHandler custView.ListChanged, _  
  New System.ComponentModel.ListChangedEventHandler( _  
  AddressOf OnListChanged)  
  
Private Shared Sub OnListChanged( _  
  sender As Object, args As System.ComponentModel.ListChangedEventArgs)  
  Console.WriteLine("ListChanged:")  
  Console.WriteLine(vbTab & "    Type = " & _  
    System.Enum.GetName(args.ListChangedType.GetType(), _  
    args.ListChangedType))  
  Console.WriteLine(vbTab & "OldIndex = " & args.OldIndex)  
  Console.WriteLine(vbTab & "NewIndex = " & args.NewIndex)  
End Sub  
```  
  
```csharp  
custView.ListChanged  += new
  System.ComponentModel.ListChangedEventHandler(OnListChanged);  
  
protected static void OnListChanged(object sender,
  System.ComponentModel.ListChangedEventArgs args)  
{  
  Console.WriteLine("ListChanged:");  
  Console.WriteLine("\t    Type = " + args.ListChangedType);  
  Console.WriteLine("\tOldIndex = " + args.OldIndex);  
  Console.WriteLine("\tNewIndex = " + args.NewIndex);  
}  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataView>
- <xref:System.ComponentModel.ListChangedEventHandler>
- [DataViews](dataviews.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
