---
description: 'Saiba mais sobre: como criar um aplicativo assíncrono do Windows Presentation Framework (WCF Data Services)'
title: 'Como: criar um aplicativo assíncrono do Windows Presentation Framework (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, asynchronous operations
ms.assetid: 834614df-1427-4839-b0be-90f68e5afffd
ms.openlocfilehash: 8bc8045854ed0b73c06276e2c81e7e03a0ecc8d6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766161"
---
# <a name="how-to-create-an-asynchronous-windows-presentation-framework-application-wcf-data-services"></a>Como: criar um aplicativo assíncrono do Windows Presentation Framework (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Com o WCF Data Services, você pode associar dados obtidos de um serviço de dados ao elemento de interface do usuário de um aplicativo do Windows Presentation Framework (WPF). Para obter mais informações, consulte [associando dados a controles](binding-data-to-controls-wcf-data-services.md). Você também pode executar operações no serviço de dados de maneira assíncrona, o que permite que o aplicativo continue respondendo enquanto aguarda uma resposta a uma solicitação de serviço de dados. Os aplicativos para o Silverlight são necessários para acessar o serviço de dados de forma assíncrona. Para obter mais informações, consulte [operações assíncronas](asynchronous-operations-wcf-data-services.md).  
  
 Este tópico mostra como acessar um serviço de dados de forma assíncrona e associar os resultados a elementos de um aplicativo do WPF. Os exemplos neste tópico usam o serviço de dados de exemplo Northwind e as classes de serviço de dados do cliente geradas automaticamente. Esse serviço e as classes de dados do cliente são criados quando você conclui o guia de [início rápido do WCF Data Services](quickstart-wcf-data-services.md).  
  
## <a name="example"></a>Exemplo  

 O XAML a seguir define a janela do aplicativo WPF.  
  
 [!code-xaml[Astoria Northwind Client#WpfDataBindingAsyncXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerordersasync.xaml#wpfdatabindingasyncxaml)]  
  
## <a name="example"></a>Exemplo  

 A seguinte página code-behind do arquivo XAML executa uma consulta assíncrona usando o serviço de dados e associa os resultados aos elementos na janela do WPF.  
  
 [!code-csharp[Astoria Northwind Client#WpfDataBindingAsync](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customerordersasync.xaml.cs#wpfdatabindingasync)]
 [!code-vb[Astoria Northwind Client#WpfDataBindingAsync](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customerordersasync.xaml.vb#wpfdatabindingasync)]  
  
## <a name="see-also"></a>Consulte também

- [Biblioteca de cliente do WCF Data Services](wcf-data-services-client-library.md)
