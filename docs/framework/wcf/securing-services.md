---
description: 'Saiba mais sobre: protegendo serviços'
title: Serviços de segurança
ms.date: 03/30/2017
helpviewer_keywords:
- configuration [WCF], securing services
- WCF security
- WCF, security
ms.assetid: f0ecc6f7-f4b5-42a4-9cb1-b02e28e26620
ms.openlocfilehash: 6d72b814e0669cac90210bd02f36740673f3960e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99685303"
---
# <a name="securing-services"></a>Serviços de segurança

A segurança de um serviço de Windows Communication Foundation (WCF) consiste em dois requisitos principais: segurança e autorização de transferência. (Um terceiro requisito, auditoria de eventos de segurança, é descrito em [auditoria](./feature-details/auditing-security-events.md).) Resumindo, a segurança de transferência inclui autenticação (verificando a identidade do serviço e do cliente), confidencialidade (criptografia de mensagem) e integridade (assinatura digital para detectar violação). A autorização é o controle de acesso a recursos, por exemplo, permitindo que apenas usuários com privilégios leiam um arquivo. Usando os recursos do WCF, os dois requisitos principais são facilmente implementados.  
  
 Com exceção da <xref:System.ServiceModel.BasicHttpBinding> classe (ou do [\<basicHttpBinding>](../configure-apps/file-schema/wcf/basichttpbinding.md) elemento na configuração), a segurança de transferência é habilitada por padrão para todas as associações predefinidas. Os tópicos desta seção abrangem dois cenários básicos: implementando a segurança de transferência e a autorização em um serviço de intranet hospedado no Serviços de Informações da Internet (IIS) e implementando a segurança de transferência e a autorização em um serviço hospedado no IIS.  
  
> [!NOTE]
> O Windows XP Home não dá suporte à autenticação do Windows. Portanto, você não deve executar um serviço nesse sistema.  
  
## <a name="security-basics"></a>Noções básicas de segurança  

 A segurança depende de *credenciais*. Uma credencial comprova que uma entidade é quem afirma ser. (Uma *entidade* pode ser uma pessoa, um processo de software, uma empresa ou qualquer coisa que possa ser autorizada.) Por exemplo, um cliente de um serviço faz uma *declaração* de *identidade* e a credencial comprova que alega de alguma maneira. Em um cenário típico, ocorre uma troca de credenciais. Primeiro, um serviço faz uma reivindicação de sua identidade e a comprova para o cliente com uma credencial. Por outro lado, o cliente faz uma declaração de identidade e apresenta uma credencial para o serviço. Se ambas as partes confiam nas credenciais da outra, um *contexto seguro* pode ser estabelecido no qual todas as mensagens são trocadas em confidencialidade e todas as mensagens são assinadas para proteger sua integridade. Depois que o serviço estabelece a identidade do cliente, ele pode corresponder as declarações na credencial a uma *função* ou *Associação* em um grupo. Em ambos os casos, usando a função ou o grupo ao qual o cliente pertence, o serviço *autoriza* o cliente a executar um conjunto limitado de operações com base nos privilégios de função ou grupo.  
  
## <a name="windows-security-mechanisms"></a>Mecanismos de segurança do Windows  

 Se o cliente e o computador de serviço estiverem em um domínio do Windows que exija que ambos façam logon na rede, as credenciais serão fornecidas pela infraestrutura do Windows. Nesse caso, as credenciais são estabelecidas quando um usuário do computador faz logon na rede. Todos os usuários e todos os computadores na rede devem ser validados como pertencentes ao conjunto confiável de usuários e computadores. Em um sistema Windows, cada usuário e computador também é conhecido como uma *entidade de segurança*.  
  
 Em um domínio do Windows com suporte de um controlador *Kerberos* , o controlador Kerberos usa um esquema com base na concessão de tíquetes para cada entidade de segurança. Os tíquetes que o controlador concede são confiáveis para outros concedentes de tíquetes no sistema. Sempre que uma entidade tenta executar alguma operação ou acessar um *recurso* (como um arquivo ou diretório em um computador), o tíquete é examinado quanto à sua validade e, se for aprovado, o principal recebe outro tíquete para a operação. Esse método de concessão de tíquetes é mais eficiente do que a alternativa de tentar validar a entidade de segurança para cada operação.  
  
 Um mecanismo mais antigo e menos seguro usado em domínios do Windows é o NTLM (NT LAN Manager). Nos casos em que o Kerberos não pode ser usado (normalmente fora de um domínio do Windows, como em um grupo de trabalho), o NTLM pode ser usado como alternativa. O NTLM também está disponível como uma opção de segurança para o IIS.  
  
 Em um sistema Windows, a autorização funciona atribuindo cada computador e usuário a um conjunto de funções e grupos. Por exemplo, todos os computadores com Windows devem ser configurados e controlados por uma pessoa (ou grupo de pessoas) na função do *administrador*. Outra função é aquela do *usuário*, que tem um conjunto de permissões muito mais restrito. Além da função, os usuários são atribuídos a grupos. Um grupo permite que vários usuários executem na mesma função. Na prática, portanto, um computador Windows é administrado por meio da atribuição de usuários a grupos. Por exemplo, vários usuários podem ser atribuídos ao grupo de usuários de um computador e um conjunto de usuários muito mais restrito pode ser atribuído ao grupo de administradores. Em um computador local, um administrador também pode criar novos grupos e atribuir outros usuários (ou até mesmo outros grupos) ao grupo.  
  
 Em um computador que executa o Windows, todas as pastas em um diretório podem ser protegidas. Ou seja, você pode selecionar uma pasta e controlar quem pode acessar os arquivos, e se eles podem ou não copiar o arquivo ou (no caso mais privilegiado) alterar um arquivo, excluir um arquivo ou adicionar arquivos à pasta. Isso é conhecido como controle de acesso, e o mecanismo para ele é conhecido como ACL (lista de controle de acesso). Ao criar a ACL, você pode atribuir privilégios de acesso a qualquer grupo ou grupos, bem como a membros individuais de um domínio.  
  
 A infraestrutura do WCF foi projetada para usar esses mecanismos de segurança do Windows. Portanto, se você estiver criando um serviço que é implantado em uma intranet e cujos clientes estão restritos a membros do domínio do Windows, a segurança será facilmente implementada. Somente usuários válidos podem fazer logon no domínio. Após os usuários serem conectados, o controlador Kerberos permite que cada usuário estabeleça contextos seguros com qualquer outro computador ou aplicativo. Em um computador local, os grupos podem ser facilmente criados e, ao proteger pastas específicas, esses grupos podem ser usados para atribuir privilégios de acesso no computador.  
  
## <a name="implementing-windows-security-on-intranet-services"></a>Implementando a segurança do Windows nos serviços de intranet  

 Para proteger um aplicativo que é executado exclusivamente em um domínio do Windows, você pode usar as configurações de segurança padrão do <xref:System.ServiceModel.WSHttpBinding> ou da <xref:System.ServiceModel.NetTcpBinding> associação. Por padrão, qualquer pessoa no mesmo domínio do Windows pode acessar os serviços do WCF. Como esses usuários fizeram logon na rede, eles são confiáveis. As mensagens entre um serviço e um cliente são criptografadas para confidencialidade e assinadas quanto à integridade. Para obter mais informações sobre como criar um serviço que usa a segurança do Windows, consulte [como: proteger um serviço com credenciais do Windows](how-to-secure-a-service-with-windows-credentials.md).  
  
### <a name="authorization-using-the-principalpermissionattribute-class"></a>Autorização usando a classe PrincipalPermissionattribute  

 Se você precisar restringir o acesso de recursos em um computador, a maneira mais fácil é usar a <xref:System.Security.Permissions.PrincipalPermissionAttribute> classe. Esse atributo permite restringir a invocação de operações de serviço exigindo que o usuário esteja em um grupo ou função do Windows especificado ou que seja um usuário específico. Para obter mais informações, consulte [como: restringir o acesso com a classe PrincipalPermissionAttribute](how-to-restrict-access-with-the-principalpermissionattribute-class.md).  
  
### <a name="impersonation"></a>Representação  

 A representação é outro mecanismo que você pode usar para controlar o acesso aos recursos. Por padrão, um serviço hospedado pelo IIS será executado sob a identidade da conta ASPNET. A conta ASPNET pode acessar somente os recursos para os quais tem permissão. No entanto, é possível definir a ACL de uma pasta para excluir a conta de serviço ASPNET, mas permitir que determinadas identidades acessem a pasta. Em seguida, a pergunta se torna como permitir que esses usuários acessem a pasta se a conta ASPNET não tiver permissão para fazer isso. A resposta é usar a representação, no qual o serviço tem permissão para usar as credenciais do cliente para acessar um recurso específico. Outro exemplo é ao acessar um banco de dados SQL Server ao qual somente determinados usuários têm permissão. Para obter mais informações sobre como usar a representação, consulte [como: representar um cliente em um serviço](how-to-impersonate-a-client-on-a-service.md) , [delegação e representação](./feature-details/delegation-and-impersonation-with-wcf.md).  
  
## <a name="security-on-the-internet"></a>Segurança na Internet  

 A segurança na Internet consiste nos mesmos requisitos de segurança em uma intranet. Um serviço precisa apresentar suas credenciais para provar sua autenticidade e os clientes precisam provar sua identidade para o serviço. Depois que a identidade de um cliente é comprovada, o serviço pode controlar a quantidade de acesso que o cliente tem aos recursos. No entanto, devido à natureza heterogênea da Internet, as credenciais apresentadas são diferentes daquelas usadas em um domínio do Windows. Enquanto um controlador Kerberos manipula a autenticação de usuários em um domínio com tíquetes para credenciais, na Internet, os serviços e os clientes dependem de qualquer uma das várias maneiras diferentes de apresentar as credenciais. O objetivo deste tópico, no entanto, é apresentar uma abordagem comum que permite criar um serviço WCF acessível na Internet.  
  
### <a name="using-iis-and-aspnet"></a>Usando IIS e ASP.NET  

 Os requisitos da segurança da Internet e os mecanismos para resolver esses problemas não são novos. O IIS é o servidor Web da Microsoft para a Internet e tem muitos recursos de segurança que resolvem esses problemas; Além disso, o ASP.NET inclui recursos de segurança que os serviços WCF podem usar. Para aproveitar esses recursos de segurança, hospede um serviço WCF no IIS.  
  
#### <a name="using-aspnet-membership-and-role-providers"></a>Usando Associação de ASP.NET e provedores de função  

 ASP.NET inclui uma associação e um provedor de função. O provedor é um banco de dados de pares de nome de usuário/senha para autenticar chamadores que também permite que você especifique os privilégios de acesso de cada chamador. Com o WCF, você pode usar facilmente uma associação e um provedor de função pré-existentes por meio da configuração. Para um aplicativo de exemplo que demonstra isso, consulte o exemplo de [provedor de associação e função](./samples/membership-and-role-provider.md) .  
  
### <a name="credentials-used-by-iis"></a>Credenciais usadas pelo IIS  

 Ao contrário de um domínio do Windows com suporte de um controlador Kerberos, a Internet é um ambiente sem um único controlador para gerenciar milhões de usuários fazendo logon a qualquer momento. Em vez disso, as credenciais na Internet geralmente estão na forma de certificados X. 509 (também conhecidos como protocolo SSL, ou SSL, certificados). Esses certificados são normalmente emitidos por uma *autoridade de certificação*, que pode ser uma empresa de terceiros que recebe a autenticidade do certificado e a pessoa para a qual ele foi emitido. Para expor seu serviço na Internet, você também deve fornecer um certificado confiável para autenticar seu serviço.  
  
 A questão surge neste ponto, como você obtém esse certificado? Uma abordagem é ir para uma autoridade de certificação de terceiros, como Authenticode ou VeriSign, quando você estiver pronto para implantar seu serviço e adquirir um certificado para seu serviço. No entanto, se você estiver na fase de desenvolvimento com o WCF e ainda não estiver pronto para confirmar a compra de um certificado, há ferramentas e técnicas para criar certificados X. 509 que você pode usar para simular uma implantação de produção. Para obter mais informações, consulte [trabalhando com certificados](./feature-details/working-with-certificates.md).  
  
## <a name="security-modes"></a>Modos de segurança  

 A programação da segurança do WCF envolve alguns pontos de decisão críticos. Uma das mais básicas é a escolha do *modo de segurança*. Os dois principais modos de segurança são o *modo de transporte* e o *modo de mensagem*.  
  
 Um terceiro modo, que combina a semântica de ambos os principais modos, é o *transporte com o modo de credenciais da mensagem*.  
  
 O modo de segurança determina como as mensagens são protegidas e cada opção tem vantagens e desvantagens, conforme explicado abaixo. Para obter mais informações sobre como definir o modo de segurança, consulte [como: definir o modo de segurança](how-to-set-the-security-mode.md).  
  
#### <a name="transport-mode"></a>Modo de transporte  

 Há várias camadas entre a rede e o aplicativo. Uma delas é a camada  de transporte *,* que gerencia a transferência de mensagens entre pontos de extremidade. Para a finalidade atual, só é necessário que você entenda que o WCF usa vários protocolos de transporte, cada um dos quais pode proteger a transferência de mensagens. (Para obter mais informações sobre transportes, consulte [transportes](./feature-details/transports.md).)  
  
 Um protocolo comumente usado é HTTP; outro é o TCP. Cada um desses protocolos pode proteger a transferência de mensagens por um mecanismo (ou mecanismos) específico para o protocolo. Por exemplo, o protocolo HTTP é protegido usando SSL sobre HTTP, geralmente abreviado como "HTTPS". Portanto, ao selecionar o modo de transporte para segurança, você está optando por usar o mecanismo conforme determinado pelo protocolo. Por exemplo, se você selecionar a <xref:System.ServiceModel.WSHttpBinding> classe e definir seu modo de segurança como transporte, você está selecionando SSL sobre http (https) como o mecanismo de segurança. A vantagem do modo de transporte é que ele é mais eficiente do que o modo de mensagem, pois a segurança é integrada em um nível comparativamente baixo. Ao usar o modo de transporte, o mecanismo de segurança deve ser implementado de acordo com a especificação para o transporte e, portanto, as mensagens podem fluir com segurança apenas do ponto a ponto no transporte.  
  
#### <a name="message-mode"></a>Modo de mensagem  

 Por outro lado, o modo de mensagem fornece segurança, incluindo os dados de segurança como parte de cada mensagem. Usando cabeçalhos de segurança XML e SOAP, as credenciais e outros dados necessários para garantir a integridade e a confidencialidade da mensagem são incluídos em cada mensagem. Cada mensagem inclui dados de segurança, de modo que resulta em uma tarifa no desempenho porque cada mensagem deve ser processada individualmente. (No modo de transporte, quando a camada de transporte está protegida, todas as mensagens fluem livremente.) No entanto, a segurança da mensagem tem uma vantagem sobre a segurança do transporte: é mais flexível. Ou seja, os requisitos de segurança não são determinados pelo transporte. Você pode usar qualquer tipo de credencial de cliente para proteger a mensagem. (No modo de transporte, o protocolo de transporte determina o tipo de credencial do cliente que você pode usar.)  
  
#### <a name="transport-with-message-credentials"></a>Transporte com credenciais de mensagem  

 O terceiro modo combina o melhor de segurança de transporte e de mensagem. Nesse modo, a segurança de transporte é usada para garantir com eficiência a confidencialidade e a integridade de cada mensagem. Ao mesmo tempo, cada mensagem inclui seus dados de credencial, o que permite que a mensagem seja autenticada. Com a autenticação, a autorização também pode ser implementada. Ao autenticar um remetente, o acesso aos recursos pode ser concedido (ou negado) de acordo com a identidade do remetente.  
  
## <a name="specifying-the-client-credential-type-and-credential-value"></a>Especificando o tipo de credencial do cliente e o valor da credencial  

 Depois de selecionar um modo de segurança, talvez você também queira especificar um tipo de credencial de cliente. O tipo de credencial do cliente especifica o tipo que um cliente deve usar para se autenticar no servidor.  
  
 No entanto, nem todos os cenários exigem um tipo de credencial de cliente. Usando SSL sobre HTTP (HTTPS), um serviço se autentica para o cliente. Como parte dessa autenticação, o certificado do serviço é enviado ao cliente em um processo chamado *negociação*. O transporte protegido por SSL garante que todas as mensagens sejam confidenciais.  
  
 Se você estiver criando um serviço que exige que o cliente seja autenticado, sua escolha de um tipo de credencial de cliente dependerá do transporte e do modo selecionado. Por exemplo, o uso do transporte HTTP e a escolha do modo de transporte oferece várias opções, como básico, resumo e outros. (Para obter mais informações sobre esses tipos de credenciais, consulte [Understanding http Authentication](./feature-details/understanding-http-authentication.md).)  
  
 Se você estiver criando um serviço em um domínio do Windows que estará disponível somente para outros usuários da rede, o tipo de credencial do cliente do Windows será mais fácil de usar. No entanto, talvez você também precise fornecer um serviço com um certificado. Isso é mostrado em [como especificar valores de credenciais de cliente](how-to-specify-client-credential-values.md).  
  
#### <a name="credential-values"></a>Valores de credencial  

 Um *valor de credencial* é a credencial real que o serviço usa. Depois de especificar um tipo de credencial, talvez você também precise configurar seu serviço com as credenciais reais. Se você selecionou Windows (e o serviço será executado em um domínio do Windows), não especifique um valor de credencial real.  
  
## <a name="identity"></a>Identidade  

 No WCF, a *identidade* do termo tem significados diferentes para o servidor e o cliente. Em resumo, ao executar um serviço, uma identidade é atribuída ao contexto de segurança após a autenticação. Para exibir a identidade real, verifique as <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> Propriedades e da <xref:System.ServiceModel.ServiceSecurityContext> classe. Para obter mais informações, consulte [como examinar o contexto de segurança](how-to-examine-the-security-context.md).  
  
 Por outro lado, no cliente, a identidade é usada para validar o serviço. Em tempo de design, um desenvolvedor cliente pode definir o [\<identity>](../configure-apps/file-schema/wcf/identity.md) elemento como um valor obtido do serviço. Em tempo de execução, o cliente verifica o valor do elemento em relação à identidade real do serviço. Se a verificação falhar, o cliente encerrará a comunicação. O valor pode ser um UPN (nome principal do usuário) se o serviço for executado sob a identidade de um usuário específico ou um SPN (nome da entidade de serviço) se o serviço for executado em uma conta de computador. Para obter mais informações, consulte [identidade de serviço e autenticação](./feature-details/service-identity-and-authentication.md). A credencial também pode ser um certificado ou um campo encontrado em um certificado que identifica o certificado.  
  
## <a name="protection-levels"></a>Níveis de proteção  

 A `ProtectionLevel` Propriedade ocorre em várias classes de atributos (como as <xref:System.ServiceModel.ServiceContractAttribute> classes e <xref:System.ServiceModel.OperationContractAttribute> ). O nível de proteção é um valor que especifica se as mensagens (ou partes da mensagem) que dão suporte a um serviço são assinadas, assinadas e criptografadas ou enviadas sem assinaturas ou criptografia. Para obter mais informações sobre a propriedade, consulte [noções básicas](understanding-protection-level.md)sobre o nível de proteção e para obter exemplos de programação, consulte [como definir a propriedade ProtectionLevel](how-to-set-the-protectionlevel-property.md). Para obter mais informações sobre como criar um contrato de serviço com o `ProtectionLevel` no contexto, consulte [Criando contratos de serviço](designing-service-contracts.md).  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel>
- <xref:System.ServiceModel.Description.ServiceCredentials>
- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- [Identidade e autenticação de serviço](./feature-details/service-identity-and-authentication.md)
- [Noções básicas de nível de proteção](understanding-protection-level.md)
- [Delegação e representação](./feature-details/delegation-and-impersonation-with-wcf.md)
- [Criando contratos de serviço](designing-service-contracts.md)
- [Segurança](./feature-details/security.md)
- [Visão geral de segurança](./feature-details/security-overview.md)
- [Como: definir a propriedade ProtectionLevel](how-to-set-the-protectionlevel-property.md)
- [Como: proteger um serviço com credenciais do Windows](how-to-secure-a-service-with-windows-credentials.md)
- [Como: definir o modo de segurança](how-to-set-the-security-mode.md)
- [Como: especificar o tipo de credencial de cliente](how-to-specify-the-client-credential-type.md)
- [Como: restringir o acesso com a classe PrincipalPermissionAttribute](how-to-restrict-access-with-the-principalpermissionattribute-class.md)
- [Como: representar um cliente em um serviço](how-to-impersonate-a-client-on-a-service.md)
- [Como: examinar o contexto de segurança](how-to-examine-the-security-context.md)
