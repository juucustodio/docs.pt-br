---
description: 'Saiba mais sobre: operações assíncronas (WCF Data Services)'
title: Operações assíncronas (WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, asynchronous operations
- asynchronous operations [WCF Data Services]
- WCF Data Services, client library
ms.assetid: 679644c7-e3fc-422c-b14a-b44b683900d0
ms.openlocfilehash: ede69fef4e284f2f7a06f4e1e842f07380d77cbf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766602"
---
# <a name="asynchronous-operations-wcf-data-services"></a>Operações assíncronas (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Os aplicativos Web devem acomodar uma latência maior entre cliente e servidor do que os aplicativos que são executados dentro das redes internas. Para otimizar o desempenho e a experiência do usuário do seu aplicativo, é recomendável usar os métodos assíncronos das <xref:System.Data.Services.Client.DataServiceContext> <xref:System.Data.Services.Client.DataServiceQuery%601> classes e ao acessar WCF Data Services servidores pela Web.  
  
 Embora os servidores de WCF Data Services processem solicitações HTTP de forma assíncrona, alguns métodos das bibliotecas de cliente do WCF Data Services são síncronos e aguardam até que toda a troca de solicitação-resposta seja concluída antes de continuar a execução. Os métodos assíncronos do WCF Data Services bibliotecas de cliente não esperam que essa troca seja concluída e pode permitir que seu aplicativo mantenha uma interface do usuário responsiva enquanto isso.  
  
 Você pode executar operações assíncronas usando um par de métodos nas <xref:System.Data.Services.Client.DataServiceContext> <xref:System.Data.Services.Client.DataServiceQuery%601> classes e que começam com *begin* e *end* , respectivamente. Os métodos *begin* registram um delegado que o serviço chama quando a operação é concluída. Os métodos *end* devem ser chamados no delegado que está registrado para manipular o retorno de chamada das operações concluídas. Ao chamar o método *end* para concluir uma operação assíncrona, você deve fazer isso na mesma <xref:System.Data.Services.Client.DataServiceQuery%601> instância ou <xref:System.Data.Services.Client.DataServiceContext> que você usou para iniciar a operação. Cada método *begin* usa um `state` parâmetro que pode passar um objeto de estado para o retorno de chamada. Esse objeto de estado é recuperado do <xref:System.IAsyncResult> que é fornecido com o retorno de chamada e é usado para chamar o método *end* correspondente para concluir a operação assíncrona. Por exemplo, quando você fornece a instância <xref:System.Data.Services.Client.DataServiceQuery%601> como o parâmetro `state` quando chama o método <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> na instância, a mesma instância <xref:System.Data.Services.Client.DataServiceQuery%601> é retornada pelo <xref:System.IAsyncResult>. Essa instância de <xref:System.Data.Services.Client.DataServiceQuery%601> é em seguida usada para chamar o método <xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A> para concluir a operação de consulta. Para obter mais informações, consulte [How to: execute assíncronas Data Service queries](how-to-execute-asynchronous-data-service-queries-wcf-data-services.md).  
  
> [!NOTE]
> Somente operações assíncronas têm suporte pelas bibliotecas de cliente que são fornecidas no .NET Framework para Silverlight. Para obter mais informações, consulte [WCF Data Services (Silverlight)](/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc838234(v=vs.95)).  
  
 As bibliotecas de cliente do .NET Framework dão suporte às seguintes operações assíncronas:  
  
|Operação|Métodos|  
|---------------|-------------|  
|Executando uma <xref:System.Data.Services.Client.DataServiceQuery%601>.|-   <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A><br />-   <xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A>|  
|Executando uma consulta do <xref:System.Data.Services.Client.DataServiceContext>.|-   <xref:System.Data.Services.Client.DataServiceContext.BeginExecute%2A><br />-   <xref:System.Data.Services.Client.DataServiceContext.EndExecute%2A>|  
|Executando uma consulta em lote do <xref:System.Data.Services.Client.DataServiceContext>.|-   <xref:System.Data.Services.Client.DataServiceContext.BeginExecuteBatch%2A><br />-   <xref:System.Data.Services.Client.DataServiceContext.EndExecuteBatch%2A>|  
|Carregando uma entidade relacionada no <xref:System.Data.Services.Client.DataServiceContext>.|-   <xref:System.Data.Services.Client.DataServiceContext.BeginLoadProperty%2A><br />-   <xref:System.Data.Services.Client.DataServiceContext.EndLoadProperty%2A>|  
|Salvando alterações nos objetos no <xref:System.Data.Services.Client.DataServiceContext>|-   <xref:System.Data.Services.Client.DataServiceContext.BeginSaveChanges%2A><br />-   <xref:System.Data.Services.Client.DataServiceContext.EndSaveChanges%2A>|  
  
## <a name="threading-considerations-for-asynchronous-operations"></a>Considerações de threads para operações assíncronas  

 Em um aplicativo multi-threaded, o delegado registrado como um retorno de chamada para a operação assíncrona não é necessariamente invocado no mesmo thread que foi usado para chamar o método *begin* , que cria a solicitação inicial. Em um aplicativo em que o retorno de chamada deve ser invocado em um thread específico, você deve realizar marshaling explicitamente da execução do método *end* , que manipula a resposta, para o thread desejado. Por exemplo, em aplicativos baseados no Windows Presentation Foundation (WPF) e aplicativos baseados no Silverlight, a resposta deverá ser lido de volta para o thread de interface de usuário usando o método <xref:System.Windows.Threading.Dispatcher.BeginInvoke%2A> no objeto <xref:System.Windows.Threading.Dispatcher>. Para obter mais informações, consulte [consultando o serviço de dados (WCF Data Services/Silverlight)](/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc903932(v=vs.95)).  
  
## <a name="see-also"></a>Consulte também

- [Biblioteca de cliente do WCF Data Services](wcf-data-services-client-library.md)
