---
description: 'Saiba mais sobre: protegendo WCF Data Services'
title: Protegendo o WCF Data Services
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- securing application [WCF Data Services]
- WCF Data Services, security
ms.assetid: 99fc2baa-a040-4549-bc4d-f683d60298af
ms.openlocfilehash: c7f8cb989c33df3d124a1745046ea68cb27e8c2f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99773102"
---
# <a name="securing-wcf-data-services"></a>Protegendo o WCF Data Services

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Este artigo descreve as considerações de segurança específicas para desenvolver, implantar e executar WCF Data Services e aplicativos que acessam serviços que dão suporte ao Protocolo Open Data (OData). Você também deve seguir as recomendações para criar aplicativos de .NET Framework seguros.  
  
Ao planejar como proteger um serviço OData baseado em WCF Data Services, você deve abordar a autenticação, o processo de descoberta e verificação da identidade de uma entidade de segurança e autorização, o processo de determinar se uma entidade autenticada tem permissão para acessar os recursos solicitados. Considere também se deseja criptografar a mensagem usando SSL.  
  
## <a name="authenticating-client-requests"></a>Autenticando solicitações de clientes  

O WCF Data Services não implementa nenhum tipo de autenticação próprio, mas se baseia nas provisões de autenticação do host do serviço de dados. Isso significa que o serviço assume que qualquer solicitação recebida já foi autenticada pelo host de rede e que o host identificou corretamente o princípio para a solicitação de forma adequada por meio das interfaces fornecidas pelo WCF Data Services. Essas opções e abordagens de autenticação são detalhadas na [série de autenticação e OData](https://devblogs.microsoft.com/odata/?s=%22OData+and+authentication%22)de várias partes.  
  
### <a name="authentication-options-for-a-wcf-data-service"></a>Opções de autenticação para o Serviço de Dados WCF  

 A tabela a seguir lista alguns dos mecanismos de autenticação que estão disponíveis para ajudá-lo a autenticar solicitações a um Serviço de Dados WCF.  
  
|Opções de Autenticação|Descrição|  
|----------------------------|-----------------|  
|Autenticação anônima|Quando a autenticação anônima HTTP está habilitada, qualquer princípio pode se conectar ao serviço de dados. Não são necessárias credenciais para o acesso anônimo. Use esta opção somente quando quiser permitir que qualquer pessoa acesse o serviço de dados.|  
|Autenticações básica e digest|As credenciais que consistem em nome de usuário e senha são necessárias para autenticação. Oferecem suporte à autenticação de clientes não Windows. **Observação de segurança:**  As credenciais de autenticação básica (nome de usuário e senha) são enviadas em claro e podem ser interceptadas. A autenticação digest envia um hash baseado nas credenciais fornecidas, o que a torna mais segura do que a autenticação básica. Ambas são suscetíveis a ataques do tipo "man-in-the-middle". Ao usar esses métodos de autenticação, você deve considerar a criptografia da comunicação entre o cliente e o serviço de dados usando o protocolo SSL. <br /><br /> O Microsoft Serviços de Informações da Internet (IIS) fornece uma implementação de autenticação básica e Digest para solicitações HTTP em um aplicativo ASP.NET. Essa implementação do provedor de Autenticação do Windows permite que um aplicativo cliente do .NET Framework forneça credenciais do cabeçalho HTTP da solicitação ao serviço de dados para negociar perfeitamente a autenticação de um usuário do Windows. Para obter mais informações, consulte [referência técnica de autenticação Digest](/previous-versions/windows/it-pro/windows-server-2003/cc782794(v=ws.10)).<br /><br /> Quando desejar que seu serviço de dados use a autenticação básica com base em algum serviço de autenticação personalizado e não em credenciais do Windows, você deve implementar um módulo HTTP ADP.NET personalizado para autenticação.<br /><br /> Para obter um exemplo de como usar um esquema de autenticação básica personalizado com WCF Data Services, consulte a postagem do blog [OData e Authentication – parte 6 – autenticação básica personalizada](https://devblogs.microsoft.com/odata/odata-and-authentication-part-6-custom-basic-authentication/).|  
|Autenticação do Windows|As credenciais baseadas no Windows são trocadas por meio de NTLM ou Kerberos. Esse mecanismo é mais seguro do que a autenticação básica ou digest, mas requer que o cliente seja um aplicativo baseado no Windows. O IIS também fornece uma implementação de autenticação do Windows para solicitações HTTP em um aplicativo ASP.NET. Para obter mais informações, consulte [visão geral da autenticação do ASP.net Forms](/previous-versions/aspnet/7t6b43z4(v=vs.100)).<br /><br /> Para obter um exemplo de como usar a autenticação do Windows com WCF Data Services, consulte a postagem do blog [OData e Authentication – parte 2 – autenticação do Windows](https://devblogs.microsoft.com/odata/odata-and-authentication-part-2-windows-authentication/).|  
|Autenticação de formulários do ASP.NET|A autenticação de formulários permite que você autentique usuários usando seu próprio código e, em seguida, mantenha um token de autenticação em um cookie ou na URL da página. Você autentica o nome de usuário e a senha de seus usuários usando um formulário de logon que você cria. As solicitações não autenticadas são redirecionadas para uma página de logon, onde o usuário fornece credenciais e envia o formulário. Se o aplicativo autenticar a solicitação, o sistema emitirá um tíquete contendo uma chave para restabelecer a identidade para solicitações subsequentes. Para obter mais informações, consulte [provedor de autenticação de formulários](/previous-versions/aspnet/9wff0kyh(v=vs.100)). **Observação de segurança:**  Por padrão, o cookie que contém o tíquete de autenticação de formulários não é protegido quando você usa a autenticação de formulários em um aplicativo Web ASP.NET. Você deve considerar exigir que o SSL proteja o tíquete de autenticação e as credenciais do logon inicial. <br /><br /> Para obter um exemplo de como usar a autenticação de formulários com WCF Data Services, consulte a postagem de blog [OData e Authentication – parte 7 – autenticação de formulários](https://devblogs.microsoft.com/odata/odata-and-authentication-part-7-forms-authentication/).|  
|Autenticação baseada em declarações|Na autenticação baseada em declarações, o serviço de dados depende de um serviço de provedor de identidade confiável "de terceiros" para autenticar o usuário. O provedor de identidade positivamente autentica o usuário que está solicitando acesso a recursos do serviço de acesso e emite um token que concede acesso aos recursos solicitados. Esse token é então apresentado ao serviço de dados, que concede acesso ao usuário com base na relação de confiança com o serviço de identidade que emitiu o token de acesso.<br /><br /> A vantagem de usar um provedor de autenticação baseado em declarações é que ele pode ser usado para autenticar vários tipos de clientes em domínios de confiança. Empregando tal provedor de terceiros, um serviço de dados pode descarregar os requisitos de manutenção e autenticação de usuários. O OAuth 2,0 é um protocolo de autenticação baseado em declarações que é suportado pelo controle de acesso do Azure AppFabric para autorização federada como um serviço. Esse protocolo oferece suporte a serviços baseados em REST. Para obter um exemplo de como usar o OAuth 2,0 com WCF Data Services, consulte a postagem do blog [OData e Authentication – parte 8 – OAuth Wrap](https://devblogs.microsoft.com/odata/odata-and-authentication-part-8-oauth-wrap/).|  
  
<a name="clientAuthentication"></a>

### <a name="authentication-in-the-client-library"></a>Autenticação na biblioteca de cliente  

 Por padrão, a biblioteca de cliente WCF Data Services não fornece credenciais ao fazer uma solicitação para um serviço OData. Quando as credenciais de logon são exigidas pelo serviço de dados para autenticar um usuário, essas credenciais podem ser fornecidas em um <xref:System.Net.NetworkCredential> acessado da propriedade <xref:System.Data.Services.Client.DataServiceContext.Credentials%2A> do <xref:System.Data.Services.Client.DataServiceContext>, como no exemplo a seguir:  
  
```csharp  
// Set the client authentication credentials.  
context.Credentials =  
    new NetworkCredential(userName, password, domain);  
```  
  
```vb  
' Set the client authentication credentials.  
context.Credentials = _  
    New NetworkCredential(userName, password, domain)  
```  
  
 Para obter mais informações, consulte [como especificar credenciais de cliente para uma solicitação de serviço de dados](specify-client-creds-for-a-data-service-request-wcf.md).  
  
 Quando o serviço de dados exige credenciais de logon que não podem ser especificadas com um objeto <xref:System.Net.NetworkCredential>, como um cookie ou um token baseado em declarações, você deve definir manualmente os cabeçalhos na solicitação HTTP, geralmente os cabeçalhos `Authorization` e `Cookie`. Para obter mais informações sobre esse tipo de cenário de autenticação, consulte a postagem no blog [ OData e autenticação – parte 3 – ganchos latência](https://devblogs.microsoft.com/odata/odata-and-authentication-part-3-clientside-hooks/). Para obter um exemplo de como definir cabeçalhos HTTP em uma mensagem de solicitação, consulte [como: definir cabeçalhos na solicitação do cliente](how-to-set-headers-in-the-client-request-wcf-data-services.md).  
  
## <a name="impersonation"></a>Representação  

 Em geral, o serviço de dados acessa os recursos necessários, como arquivos no servidor ou em um banco de dados, usando as credenciais do processo de trabalho que está hospedando o serviço de dados. Ao usar a representação, os aplicativos ASP.NET podem ser executados com a identidade do Windows (conta de usuário) do usuário que faz a solicitação. A representação é normalmente usada em aplicativos que dependem do IIS para autenticar o usuário, e as credenciais desse princípio são usadas para acessar os recursos necessários. Para obter mais informações, consulte [representação ASP.net](/previous-versions/aspnet/xh507fc5(v=vs.100)).  
  
## <a name="configuring-data-service-authorization"></a>Configurando a autorização do serviço de dados  

 Autorização é a concessão de acesso a recursos do aplicativo a um princípio ou processo que é identificado com base em uma autenticação anteriormente bem-sucedida. Como uma prática geral, você só deve conceder direitos suficientes para os usuários do serviço de dados executarem as operações exigidas pelos aplicativos cliente.  
  
### <a name="restrict-access-to-data-service-resources"></a>Restringir o acesso a recursos do serviço de dados  

 Por padrão, o WCF Data Services permite que você conceda acesso de leitura e gravação comum a recursos do serviço de dados (conjunto de entidades e operações de serviço) a qualquer usuário que possa acessar o serviço de dados. As regras que definem o acesso de leitura e gravação podem ser definidas separadamente para cada conjunto de entidades exposto pelo serviço de dados, bem como quaisquer operações de serviço. Recomendamos a limitação do acesso de leitura e gravação somente aos recursos exigidos pelo aplicativo cliente. Para obter mais informações, consulte [requisitos mínimos de acesso a recursos](configuring-the-data-service-wcf-data-services.md#accessRequirements).  
  
### <a name="implement-role-based-interceptors"></a>Implementar interceptores baseados em função  

 Os interceptores permitem que você intercepte solicitações para recursos do serviço de dados antes que elas sejam manipuladas pelo serviço de dados. Para obter mais informações, consulte [Interceptors](interceptors-wcf-data-services.md). Os interceptores permitem que você tome decisões de autorização com base no usuário autenticado que está fazendo a solicitação. Para obter um exemplo de como restringir o acesso aos recursos do serviço de dados com base em uma identidade de usuário autenticado, consulte [como interceptar mensagens de serviço de dados](how-to-intercept-data-service-messages-wcf-data-services.md).  
  
### <a name="restrict-access-to-the-persisted-data-store-and-local-resources"></a>Restringir o acesso aos recursos locais e do repositório de dados persistente  

 As contas que são usadas para acessar o repositório persistente devem receber somente os direitos suficientes em um banco de dados ou no sistema de arquivos para dar suporte aos requisitos do serviço de dados. Quando a autenticação anônima é usada, essa é a conta usada para executar o aplicativo de hospedagem. Para obter mais informações, consulte [como: desenvolver um serviço de dados WCF em execução no IIS](how-to-develop-a-wcf-data-service-running-on-iis.md). Quando a representação é usada, os usuários autenticados devem receber acesso a esses recursos, normalmente como parte de um grupo do Windows.  
  
## <a name="other-security-considerations"></a>Outras considerações de segurança  
  
### <a name="secure-the-data-in-the-payload"></a>Proteger os dados na carga  

O OData é baseado no protocolo HTTP. Em uma mensagem HTTP, o cabeçalho pode conter credenciais de usuário valiosas, dependendo da autenticação implementada pelo serviço de dados. O corpo da mensagem também pode conter dados importantes do cliente que devem ser protegidos. Em ambos os casos, é recomendável que você use o protocolo SSL para proteger essas informações durante a transmissão.  
  
### <a name="ignored-message-headers-and-cookies"></a>Cabeçalhos e cookies de mensagens ignorados  

 Os cabeçalhos de solicitações HTTP, a não ser os que declaram tipos de conteúdo e locais de recursos, são ignorados e nunca são definidos pelo serviço de dados.  
  
 Os cookies podem ser usados como parte de um esquema de autenticação, como com a autenticação de formulários do ASP.NET. No entanto, todos os cookies HTTP definidos em uma solicitação de entrada são ignorados pelo WCF dataservices. O host de um serviço de dados pode processar o cookie, mas o tempo de execução de WCF Data Services nunca analisa ou retorna cookies. A biblioteca de cliente WCF Data Services também não processa cookies enviados na resposta.  
  
### <a name="custom-hosting-requirements"></a>Requisitos de hospedagem personalizada  

 Por padrão, WCF Data Services é criada como um aplicativo ASP.NET hospedado no IIS. Isso permite que o serviço de dados aproveite os comportamentos seguros da plataforma. Você pode definir WCF Data Services que são hospedados por um host personalizado. Para obter mais informações, consulte [hospedando o serviço de dados](hosting-the-data-service-wcf-data-services.md). Os componentes e a plataforma que hospedam um serviço de dados devem garantir os seguintes comportamentos de segurança para evitar ataques no serviço de dados:  
  
- Limitar o tamanho do URI aceito em uma solicitação do serviço de dados para todas as operações possíveis.  
  
- Limitar o tamanho de mensagens HTTP de entrada e saída.  
  
- Limitar o número total de solicitações pendentes em qualquer momento determinado.  
  
- Limite o tamanho dos cabeçalhos HTTP e seus valores e forneça WCF Data Services acesso aos dados de cabeçalho.  
  
- Detectar e deter ataques conhecidos, como ataques de mensagem de repetição e SYN TCP.  
  
### <a name="values-are-not-further-encoded"></a>Os valores não têm codificação adicional  

 Os valores de propriedade enviados ao serviço de dados não são codificados ainda mais pelo tempo de execução WCF Data Services. Por exemplo, quando uma propriedade de cadeia de caracteres de uma entidade tem conteúdo HTML formatado, as marcas não são codificadas em HTML pelo serviço de dados. O serviço de dados também não faz a codificação adicional de valores de propriedades na resposta. A biblioteca de cliente também não executa nenhuma codificação adicional.  
  
### <a name="considerations-for-client-applications"></a>Considerações para aplicativos cliente  

 As seguintes considerações de segurança se aplicam a aplicativos que usam o cliente WCF Data Services para acessar serviços OData:  
  
- A biblioteca de cliente presume que os protocolos usados para acessar o serviço de dados forneçam um nível de segurança adequado.  
  
- A biblioteca de cliente usa todos os valores padrão para tempos limite e opções de análise das pilhas de transporte subjacentes fornecidas pela plataforma.  
  
- A biblioteca de cliente não lê nenhuma configuração de arquivos de configuração de aplicativo.  
  
- A biblioteca de cliente não implementa nenhum mecanismo de acesso entre domínios. Em vez disso, ela depende dos mecanismos fornecidos pela pilha HTTP subjacente.  
  
- A biblioteca de cliente não tem nenhum elemento de interface do usuário, e nunca tenta exibir ou renderizar os dados que recebe ou envia.  
  
- Recomendamos que os aplicativos cliente sempre validem a entrada do usuário, bem como os dados aceitos de serviços não confiáveis.  
  
## <a name="see-also"></a>Consulte também

- [Configurando WCF Data Services](defining-wcf-data-services.md)
- [Biblioteca de cliente do WCF Data Services](wcf-data-services-client-library.md)
