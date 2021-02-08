---
description: 'Saiba mais sobre: usando ações para implementar o comportamento do lado do servidor'
title: Usando as ações implementar o comportamento do lado do servidor
ms.date: 03/30/2017
ms.assetid: 11a372db-7168-498b-80d2-9419ff557ba5
ms.openlocfilehash: 6decd6134184de860ae2865b6dcf34b3c0b81813
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791706"
---
# <a name="using-actions-to-implement-server-side-behavior"></a>Usando as ações implementar o comportamento do lado do servidor

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

As ações OData fornecem uma maneira de implementar um comportamento que age mediante um recurso recuperado de um serviço OData. Por exemplo, considere um filme como um recurso. Há muitas coisas que você pode fazer com um filme: check-out, avaliar/comentar ou check-in. Estes são exemplos de Ações que podem ser implementadas por um WCF Data Service que gerencia filmes. As ações são descritas em uma resposta OData que contém um recurso no qual a Ação pode ser invocada. Quando um usuário solicita um recurso que representa um filme, a resposta retornada do WCF Data Service contém informações sobre as Ações disponíveis para esse recurso. A disponibilidade de uma Ação pode depender do estado do serviço de dados ou recurso. Por exemplo, quando um filme fez o check-out, ele não pode ter o check-out feito por outro usuário. Os clientes podem invocar uma ação somente especificando uma URL. Por exemplo, `http://MyServer/MovieService.svc/Movies(6)` identificaria um filme digital específico e `http://MyServer/MovieService.svc/Movies(6)/Checkout` invocaria a ação no filme específico. As ações permitem que você exponha o modelo de serviço sem expor o modelo de dados. Continuando o exemplo do serviço de filmes, talvez você queira permitir que um usuário avalie um filme, mas não expor os dados de avaliação diretamente como um recurso. Você pode implementar uma Ação de Avaliação para permitir que o usuário avalie um filme, mas não acessar os dados de avaliação diretamente como um recurso.

## <a name="implementing-an-action"></a>Implementando uma ação

 Para implementar uma ação de serviço, você deve implementar as <xref:System.IServiceProvider> interfaces, [IDataServiceActionProvider](/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103))e [IDataServiceInvokable](/previous-versions/dotnet/wcf-data-services/hh859893(v=vs.103)) . <xref:System.IServiceProvider> permite que WCF Data Services Obtenha sua implementação de [IDataServiceActionProvider](/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103)). O [IDataServiceActionProvider](/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103)) permite que WCF Data Services crie, localize, descreva e invoque ações de serviço. O [IDataServiceInvokable](/previous-versions/dotnet/wcf-data-services/hh859893(v=vs.103)) permite invocar o código que implementa o comportamento das ações de serviço e obter os resultados, se houver. Lembre-se de que o WCF Data Services são Serviços do WCF por chamada, uma nova instância do serviço será criada cada vez que o serviço for chamado.  Verifique se nenhum trabalho desnecessário é feito quando o serviço é criado.

### <a name="iserviceprovider"></a>IServiceProvider

 O <xref:System.IServiceProvider> contém um método chamado <xref:System.IServiceProvider.GetService%2A>. Este método é chamado pelo WCF Data Services para recuperar um número de provedores de serviços, inclusive provedores de serviços de metadados e provedores de ação de serviço de dados. Quando solicitado por um provedor de ação de serviço de dados, retorne sua implementação [IDataServiceActionProvider](/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103)) .

### <a name="idataserviceactionprovider"></a>IDataServiceActionProvider

 [IDataServiceActionProvider](/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103)) contém métodos que permitem recuperar informações sobre as ações disponíveis. Ao implementar o [IDataServiceActionProvider](/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103)) , você está aumentando os metadados para o serviço, que é definido pela implementação do seu serviço do [IDataServiceActionProvider](/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103)) com ações e manipulando a expedição para essas ações, conforme apropriado.

#### <a name="advertiseserviceaction"></a>AdvertiseServiceAction

 O [método AdvertiseServiceAction](/previous-versions/dotnet/wcf-data-services/hh859971(v=vs.103)) é chamado para determinar quais ações estão disponíveis para o recurso especificado. Este método é chamado apenas para as ações que não estão sempre disponíveis. É usado para verificar se a ação deve ser incluída na resposta OData com base no estado do recurso que está sendo solicitado ou no estado do serviço. Como essa verificação é feita cabe completamente a você. Se é caro calcular a disponibilidade e o recurso atual estiver em um feed, é aceitável ignorar a verificação e divulgar a ação. O parâmetro `inFeed` estará definido como `true` se o recurso atual que está sendo retornado fizer parte de um feed.

#### <a name="createinvokable"></a>CreateInvokable

 [Createinvoqueble](/previous-versions/dotnet/wcf-data-services/hh859940(v=vs.103)) é chamado para criar um [IDataServiceInvokable](/previous-versions/dotnet/wcf-data-services/hh859893(v=vs.103)) que contém um delegado que encapsula o código que implementa o comportamento da ação. Isso cria a instância [IDataServiceInvokable](/previous-versions/dotnet/wcf-data-services/hh859893(v=vs.103)) , mas não invoca a ação. As ações do WCF Data Service têm efeitos colaterais e precisam trabalhar junto com o Provedor de Atualização para salvar essas alterações no disco. O método [IDataServiceInvokable. Invoke](/previous-versions/dotnet/wcf-data-services/hh859924(v=vs.103)) é chamado a partir do método SaveChanges () do provedor de atualização chamado.

#### <a name="getserviceactions"></a>GetServiceActions

 Esse método retorna uma coleção de instâncias [ServiceAction](/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103)) que representam todas as ações que um serviço de dados WCF expõe. [ServiceAction](/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103)) é a representação de metadados de uma ação e inclui informações como o nome da ação, seus parâmetros e seu tipo de retorno.

#### <a name="getserviceactionsbybindingparametertype"></a>GetServiceActionsByBindingParameterType

 Esse método retorna uma coleção de todas as instâncias de [ServiceAction](/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103)) que podem ser associadas ao tipo de parâmetro de associação especificado. Em outras palavras, todos os [ServiceAction](/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103))s que podem agir no tipo de recurso especificado (também chamado de tipo de parâmetro de associação). Isso é usado quando o serviço retorna um recurso para incluir informações sobre as ações que podem ser invocadas em relação a esse recurso. Esse método deve retornar apenas as ações que podem ser associadas ao tipo de parâmetro de associação exato (sem tipo derivado). Este método é chamado uma vez por solicitação por tipo encontrado e o resultado é armazenado em cache pelo WCF Data Services.

#### <a name="tryresolveserviceaction"></a>TryResolveServiceAction

 Esse método procura um [ServiceAction](/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103)) especificado e retorna `true` se [ServiceAction](/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103)) é encontrado. Se for encontrado, o [ServiceAction](/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103)) será retornado no `serviceAction` `out` parâmetro.

### <a name="idataserviceinvokable"></a>IDataServiceInvokable

 Essa interface oferece um modo de executar uma ação do WCF Data Service. Ao implementar IDataServiceInvokable, você é responsável por 3 coisas:

1. Capturar e potencialmente fazer o marshaling dos parâmetros

2. Distribuir os parâmetros para o código que realmente implementa a Ação quando Invoke() é chamado

3. Armazenar os resultados de Invoke() para que eles possam ser recuperados usando GetResult()

 Os parâmetros podem ser passados como tokens. Isso ocorre porque é possível escrever um provedor de serviços de dados que funcione com os tokens que representam recursos. Se for esse o caso, você precisará converter (realizar marshaling) esses tokens em recursos reais antes de distribuir para a ação real. Depois que o parâmetro tiver sido empacotado, ele deverá estar em um estado editável para que as alterações no recurso que ocorrem quando a ação for chamada sejam salvas e gravadas no disco.

 Essa interface requer dois métodos: Invoke e GetResult. Invoke chama o representante que implementa o comportamento da ação e GetResult retorna o resultado da ação.

## <a name="invoking-a-wcf-data-service-action"></a>Chamar uma ação do WCF Data Service

 As ações são chamadas usando uma solicitação HTTP POST. O URL especifica o recurso seguido pelo nome da ação. Os parâmetros são passados no corpo da solicitação. Por exemplo, se houve um serviço chamado MovieService que expôs uma ação chamada Avaliar. Você pode usar a seguinte URL para chamar a ação Avaliar em um filme específico:

 `http://MovieServer/MovieService.svc/Movies(1)/Rate`

 Movies(1) especifica o filme que você deseja avaliar e Avaliar especifica a ação. O valor real da avaliação estará no corpo da solicitação de HTTP conforme mostrado no seguinte exemplo:

```http
POST http://MovieServer/MoviesService.svc/Movies(1)/Rate HTTP/1.1
Content-Type: application/json
Content-Length: 20
Host: localhost:15238
{
   "rating": 4
}
```

> [!WARNING]
> O código de exemplo acima somente funcionará com o WCF Data Services 5.2 e posterior que tem o suporte para JSON light. Se estiver usando uma versão anterior do WCF Data Services, você deverá especificar o tipo de conteúdo detalhado de json da seguinte maneira: `application/json;odata=verbose`.

 Como alternativa, você pode chamar uma ação usando o cliente do WCF Data Services conforme mostrado no seguinte snippet de código.

```csharp
MoviesModel context = new MoviesModel (new Uri("http://MyServer/MoviesService.svc/"));
//...
context.Execute(new Uri("http://MyServer/MoviesService.svc/Movies(1)/Rate"), "POST", new BodyOperationParameter("rating",4) );
```

 No snippet de código acima, a classe `MoviesModel` foi gerada com o Visual Studio para Adicionar a Referência de Serviço a um WCF Data Service.

## <a name="see-also"></a>Consulte também

- [WCF Data Services 4.5](index.md)
- [Configurando WCF Data Services](defining-wcf-data-services.md)
- [Desenvolvendo e implantando WCF Data Services](developing-and-deploying-wcf-data-services.md)
- [Provedores de serviços de dados personalizados](custom-data-service-providers-wcf-data-services.md)
