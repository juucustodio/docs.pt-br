---
description: 'Saiba mais sobre: derivando de WebRequest'
title: Derivando de WebRequest
ms.date: 03/30/2017
helpviewer_keywords:
- WebRequest class, pluggable protocols
- protocol-specific request handler
- sending data, pluggable protocols
- pluggable protocols, class criteria
- Internet, pluggable protocols
- receiving data, pluggable protocols
- protocols, pluggable
ms.assetid: 9810c177-973e-43d7-823c-14960bd625ea
ms.openlocfilehash: ede2480767f11ef66bccc79ab4e3a4bc8aafc1fb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801898"
---
# <a name="deriving-from-webrequest"></a>Derivando de WebRequest

A classe <xref:System.Net.WebRequest> é uma classe base abstrata que fornece os métodos e as propriedades básicas para criar um manipulador de solicitação específico ao protocolo que se ajusta ao modelo de protocolo conectável do .NET Framework. Os aplicativos que usam a classe **WebRequest** podem solicitar dados usando qualquer protocolo com suporte sem a necessidade de especificar o protocolo usado.  
  
 Dois critérios devem ser atendidos para que uma classe específica ao protocolo seja usada como um protocolo conectável: a classe deve implementar a interface <xref:System.Net.IWebRequestCreate> e deve se registrar com o método <xref:System.Net.WebRequest.RegisterPrefix%2A?displayProperty=nameWithType>. A classe deve substituir todos os métodos abstratos e as propriedades de **WebRequest** para fornecer a interface conectável.  
  
 As instâncias de **WebRequest** são destinadas a um único uso; se desejar fazer outra solicitação, crie uma nova **WebRequest**. **WebRequest** dá suporte à interface <xref:System.Runtime.Serialization.ISerializable> para permitir aos desenvolvedores serializar uma **WebRequest** de modelo e, em seguida, reconstruir o modelo para solicitações adicionais.  
  
## <a name="iwebrequest-create-method"></a>Método IWebRequest Create  

 O método <xref:System.Net.IWebRequestCreate.Create%2A> é responsável por inicializar uma nova instância da classe específica ao protocolo. Quando uma nova **WebRequest** é criada, o método <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType> corresponde ao URI solicitado com os prefixos URI registrados com o método **RegisterPrefix**. O método **Create** do descendente específico ao protocolo correto deve retornar uma instância inicializada do descendente com a capacidade de executar uma transação de solicitação/resposta padrão para o protocolo sem a necessidade de modificar os campos específicos ao protocolo.  
  
## <a name="connectiongroupname-property"></a>Propriedade ConnectionGroupName  

 A propriedade <xref:System.Net.WebRequest.ConnectionGroupName%2A> é usada para nomear um grupo de conexões com um recurso, de modo que várias solicitações possam ser feitas em uma única conexão. Para implementar o compartilhamento de conexão, você deve usar um método específico ao protocolo de pooling e atribuição de conexões. Por exemplo, a classe <xref:System.Net.ServicePointManager> fornecida implementa o compartilhamento de conexão na classe <xref:System.Net.HttpWebRequest>. A classe **ServicePointManager** cria um <xref:System.Net.ServicePoint> que fornece uma conexão com um servidor específico para cada grupo de conexão.  
  
## <a name="contentlength-property"></a>Propriedade ContentLength  

 A propriedade <xref:System.Net.WebRequest.ContentLength%2A> especifica o número de bytes de dados que serão enviados para o servidor ao carregar dados.  
  
 Normalmente, a propriedade <xref:System.Net.WebRequest.Method%2A> deve ser definida para indicar que um upload está ocorrendo quando a propriedade **ContentLength** é definida com um valor maior que zero.  
  
## <a name="contenttype-property"></a>Propriedade ContentType  

 A propriedade <xref:System.Net.WebRequest.ContentType%2A> fornece informações especiais que o protocolo exige que sejam enviadas ao servidor para identificar o tipo de conteúdo que está sendo enviado. Normalmente, esse é o tipo de conteúdo MIME dos dados carregados.  
  
## <a name="credentials-property"></a>Propriedade Credentials  

 A propriedade <xref:System.Net.WebRequest.Credentials%2A> contém as informações necessárias para autenticar a solicitação no servidor. É necessário implementar os detalhes do processo de autenticação do protocolo. A classe <xref:System.Net.AuthenticationManager> é responsável por autenticar as solicitações e fornecer um token de autenticação. A classe que fornece as credenciais usadas pelo protocolo deve implementar a interface <xref:System.Net.ICredentials>.  
  
## <a name="headers-property"></a>Propriedade Headers  

 A propriedade <xref:System.Net.WebRequest.Headers%2A> contém uma coleção arbitrária de pares de nome/valor de metadados associados à solicitação. Todos os metadados necessários para o protocolo que podem ser expressos como um par nome/valor podem ser incluídos na propriedade **Headers**. Normalmente, essas informações devem ser definidas antes de chamar os métodos <xref:System.Net.WebRequest.GetRequestStream%2A> ou <xref:System.Net.WebRequest.GetResponse%2A>; depois que a solicitação for feita, os metadados serão considerados somente leitura.  
  
 Não é necessário usar a propriedade **Headers** para usar os metadados do cabeçalho. Os metadados específicos ao protocolo podem ser expostos como propriedades; por exemplo, a propriedade <xref:System.Net.HttpWebRequest.UserAgent%2A?displayProperty=nameWithType> expõe o cabeçalho HTTP **User-Agent**. Ao expor os metadados do cabeçalho como uma propriedade, você não deve permitir que a mesma propriedade seja definida usando a propriedade **Headers**.  
  
## <a name="method-property"></a>Propriedade Method  

 A propriedade <xref:System.Net.WebRequest.Method%2A> contém o verbo ou a ação que a solicitação está solicitando que o servidor execute. O padrão para a propriedade **Method** deve permitir uma ação de solicitação/resposta padrão sem a necessidade de definir propriedades específicas ao protocolo. Por exemplo, o método <xref:System.Net.HttpWebResponse.Method%2A> usa GET como padrão, que solicita um recurso de um servidor Web e retorna a resposta.  
  
 Normalmente, a propriedade **ContentLength** deve ser definida com um valor maior que zero quando a propriedade **Method** é definida com um verbo ou uma ação que indica que um upload está ocorrendo.  
  
## <a name="preauthenticate-property"></a>Propriedade PreAuthenticate  

 Os aplicativos definem a propriedade <xref:System.Net.WebRequest.PreAuthenticate%2A> para indicar que as informações de autenticação devem ser enviadas com a solicitação inicial, em vez de aguardar um desafio de autenticação. A propriedade **PreAuthenticate** só será significativa se o protocolo der suporte a credenciais de autenticação enviadas com a solicitação inicial.  
  
## <a name="proxy-property"></a>Propriedade Proxy  

 A propriedade <xref:System.Net.WebRequest.Proxy%2A> contém uma interface <xref:System.Net.IWebProxy> que é usada para acessar o recurso solicitado. A propriedade **Proxy** só será significativa se o protocolo der suporte a solicitações com proxy. É necessário definir o proxy padrão se for exigido um para o protocolo.  
  
 Em alguns ambientes, como quando protegido por um firewall corporativo, o protocolo pode precisar usar um proxy. Nesse caso, é necessário implementar a interface **IWebProxy** para criar uma classe proxy que funcionará para o protocolo.  
  
## <a name="requesturi-property"></a>Propriedade RequestUri  

 A propriedade <xref:System.Net.WebRequest.RequestUri%2A> contém o URI que foi passado para o método **WebRequest.Create**. Ela é somente leitura e não poderá ser alterada depois que **WebRequest** for criada. Se o protocolo der suporte ao redirecionamento, a resposta poderá ser recebida de um recurso identificado por outro URI. Se você precisar fornecer acesso ao URI que respondeu, deverá fornecer uma propriedade adicional que contém esse URI.  
  
## <a name="timeout-property"></a>Propriedade Timeout  

 A propriedade <xref:System.Net.WebRequest.Timeout%2A> contém o tempo, em milissegundos, de espera antes que a solicitação atinja o tempo limite e gere uma exceção. **Timeout** se aplica somente a solicitações síncronas feitas com o método <xref:System.Net.WebRequest.GetResponse%2A>; as solicitações assíncronas devem usar o método <xref:System.Net.WebRequest.Abort%2A> para cancelar uma solicitação pendente.  
  
 A configuração da propriedade **Timeout** só será significativa se a classe específica ao protocolo implementar um processo de tempo limite.  
  
## <a name="abort-method"></a>Método Abort  

 O método <xref:System.Net.WebRequest.Abort%2A> cancela uma solicitação assíncrona pendente para um servidor. Depois que a solicitação for cancelada, uma chamada a **GetResponse**, **BeginGetResponse**, **EndGetResponse**, **GetRequestStream**, **BeginGetRequestStream** ou **EndGetRequestStream** gerará uma <xref:System.Net.WebException> com a propriedade <xref:System.Net.WebException.Status%2A> definida como <xref:System.Net.WebExceptionStatus>.  
  
## <a name="begingetrequeststream-and-endgetrequeststream-methods"></a>Métodos BeginGetRequestStream e EndGetRequestStream  

 O método <xref:System.Net.WebRequest.BeginGetRequestStream%2A> inicia uma solicitação assíncrona para o fluxo que é usado para carregar dados no servidor. O método <xref:System.Net.WebRequest.EndGetRequestStream%2A> conclui a solicitação assíncrona e retorna o fluxo solicitado. Esses métodos implementam o método **GetRequestStream** usando o padrão assíncrono do .NET Framework.  
  
## <a name="begingetresponse-and-endgetresponse-methods"></a>Métodos BeginGetResponse e EndGetResponse  

 O método <xref:System.Net.WebRequest.BeginGetResponse%2A> inicia uma solicitação assíncrona para um servidor. O método <xref:System.Net.WebRequest.EndGetResponse%2A> conclui a solicitação assíncrona e retorna a resposta solicitada. Esses métodos implementam o método **GetResponse** usando o padrão assíncrono do .NET Framework.  
  
## <a name="getrequeststream-method"></a>Método GetRequestStream  

 O método <xref:System.Net.WebRequest.GetRequestStream%2A> retorna um fluxo que é usado para gravar dados no servidor solicitado. O fluxo retornado deve ser um fluxo somente gravação que não faz buscas; ele se destina como um fluxo de dados unidirecional que é gravado no servidor. O fluxo retorna falso para as propriedades <xref:System.IO.Stream.CanRead%2A> e <xref:System.IO.Stream.CanSeek%2A> e verdadeiro para a propriedade <xref:System.IO.Stream.CanWrite%2A>.  
  
 O método **GetRequestStream** normalmente abre uma conexão com o servidor e, antes de retornar o fluxo, envia informações de cabeçalho que indicam que os dados estão sendo enviados para o servidor. Como **GetRequestStream** inicia a solicitação, a configuração de propriedades **Header** ou da propriedade **ContentLength** normalmente não é permitida após a chamada a **GetRequestStream**.  
  
## <a name="getresponse-method"></a>Método GetResponse  

 O método <xref:System.Net.WebRequest.GetResponse%2A> retorna um descendente específico ao protocolo da classe <xref:System.Net.WebResponse> que representa a resposta do servidor. A menos que a solicitação já tenha sido iniciada pelo método **GetRequestStream**, o método **GetResponse** cria uma conexão com o recurso identificado pelo **RequestUri**, envia informações de cabeçalho que indicam o tipo de solicitação que está sendo feita e, em seguida, recebe a resposta do recurso.  
  
 Depois que o método **GetResponse** for chamado, todas as propriedades deverão ser consideradas somente leitura. As instâncias de **WebRequest** são destinadas a um único uso; se desejar fazer outra solicitação, crie uma nova **WebRequest**.  
  
 O método **GetResponse** é responsável por criar um descendente apropriado de **WebResponse** para conter a resposta de entrada.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Net.WebRequest>
- <xref:System.Net.HttpWebRequest>
- <xref:System.Net.FileWebRequest>
- [Programando protocolos conectáveis](programming-pluggable-protocols.md)
- [Derivando de WebResponse](deriving-from-webresponse.md)
