---
description: 'Saiba mais sobre: como personalizar os comportamentos de vinculação de dados (WCF Data Services)'
title: 'Como: Personalizar comportamentos de vinculação de dados (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, customizing
- WCF Data Services, data binding
ms.assetid: 40476b89-8941-4771-8d21-2fe430c85a9d
ms.openlocfilehash: 60c8808f90f8e0a824a8b2b641508c0fe33f14cc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765679"
---
# <a name="how-to-customize-data-binding-behaviors-wcf-data-services"></a>Como: Personalizar comportamentos de vinculação de dados (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Com WCF Data Services, você pode fornecer uma lógica personalizada que é chamada pelo <xref:System.Data.Services.Client.DataServiceCollection%601> quando um objeto é adicionado ou removido da coleção de associação ou quando uma alteração de propriedade é detectada. Essa lógica personalizada é fornecida como métodos, referenciados como <xref:System.Func%602> delegados, que retornam um valor de `false` quando o comportamento padrão ainda deve ser executado quando o método personalizado é concluído e `true` quando o processamento subsequente do evento deve ser interrompido.  
  
 Os exemplos neste tópico fornecem métodos personalizados para os `entityChanged` `entityCollectionChanged` parâmetros e de <xref:System.Data.Services.Client.DataServiceCollection%601> . Os exemplos neste tópico usam o serviço de dados de exemplo Northwind e as classes de serviço de dados do cliente geradas automaticamente. Esse serviço e as classes de dados do cliente são criados quando você conclui o guia de [início rápido do WCF Data Services](quickstart-wcf-data-services.md).  
  
## <a name="example"></a>Exemplo  

 A seguinte página code-behind do arquivo XAML cria um <xref:System.Data.Services.Client.DataServiceCollection%601> com métodos personalizados que são chamados quando ocorrem alterações nos dados associados à coleção de associação. Quando o <xref:System.Collections.ObjectModel.ObservableCollection%601.CollectionChanged> evento ocorre, o método fornecido impede que um item que foi removido da coleção de associação seja excluído do serviço de dados. Quando o <xref:System.Collections.ObjectModel.ObservableCollection%601.PropertyChanged> evento ocorre, o `ShipDate` valor é validado para garantir que as alterações não sejam feitas em pedidos que já foram enviados.  
  
 [!code-csharp[Astoria Northwind Client#WpfDataBindingCustom](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerorderscustom.xaml.cs#wpfdatabindingcustom)]
 [!code-vb[Astoria Northwind Client#WpfDataBindingCustom](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom.xaml.vb#wpfdatabindingcustom)]
 [!code-vb[Astoria Northwind Client#WpfDataBindingCustom](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom2.xaml.vb#wpfdatabindingcustom)]  
  
## <a name="example"></a>Exemplo  

 O XAML a seguir define a janela para o exemplo anterior.  
  
 [!code-xaml[Astoria Northwind Client#WpfDataBindingCustomXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerorderscustom.xaml#wpfdatabindingcustomxaml)]  
  
## <a name="see-also"></a>Consulte também

- [Biblioteca de cliente do WCF Data Services](wcf-data-services-client-library.md)
