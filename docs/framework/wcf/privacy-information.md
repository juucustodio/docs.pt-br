---
description: 'Saiba mais sobre: Windows Communication Foundation informações de privacidade'
title: Informações de privacidade do Windows Communication Foundation
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation, privacy information
- WCF, privacy information
- privacy information [WCF]
ms.assetid: c9553724-f3e7-45cb-9ea5-450a22d309d9
ms.openlocfilehash: 4f942e84a072d15a12b6db7cc2c310d629a59f6b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99726683"
---
# <a name="windows-communication-foundation-privacy-information"></a>Informações de privacidade do Windows Communication Foundation

A Microsoft está comprometida em proteger a privacidade do usuário final. Quando você cria um aplicativo usando Windows Communication Foundation (WCF), versão 3,0, seu aplicativo pode afetar a privacidade dos usuários finais. Por exemplo, seu aplicativo pode coletar explicitamente as informações de contato do usuário ou pode solicitar ou enviar informações pela Internet para seu site. Se você inserir a tecnologia da Microsoft em seu aplicativo, essa tecnologia poderá ter seu próprio comportamento que pode afetar a privacidade. O WCF não envia nenhuma informação à Microsoft do seu aplicativo, a menos que você ou o usuário final opte por enviá-lo para nós.  
  
## <a name="wcf-in-brief"></a>WCF em resumo  

 O WCF é uma estrutura de mensagens distribuídas usando o Microsoft .NET Framework que permite aos desenvolvedores criar aplicativos distribuídos. As mensagens comunicadas entre dois aplicativos contêm informações de cabeçalho e corpo.  
  
 Os cabeçalhos podem conter roteamento de mensagens, informações de segurança, transações e muito mais, dependendo dos serviços usados pelo aplicativo. Normalmente, as mensagens são criptografadas por padrão. A única exceção é ao usar o `BasicHttpBinding` , que foi projetado para uso com serviços Web herdados e não protegidos. Como o designer de aplicativos, você é responsável pelo design final. As mensagens no corpo SOAP contêm dados específicos do aplicativo; no entanto, esses dados, como informações pessoais definidas pelo aplicativo, podem ser protegidos usando recursos de confidencialidade ou criptografia do WCF. As seções a seguir descrevem os recursos que potencialmente afetam a privacidade.  
  
## <a name="messaging"></a>Mensagens  

 Cada mensagem do WCF tem um cabeçalho de endereço que especifica o destino da mensagem e onde a resposta deve ir.  
  
 O componente de endereço de um endereço de ponto de extremidade é um Uniform Resource Identifier (URI) que identifica o ponto de extremidade. O endereço pode ser um endereço de rede ou um endereço lógico. O endereço pode incluir o nome do computador (hostname, nome de domínio totalmente qualificado) e um endereço IP. O endereço do ponto de extremidade também pode conter um GUID (identificador global exclusivo) ou uma coleção de GUIDs para endereçamento temporário usado para discernir cada endereço. Cada mensagem contém uma ID de mensagem que é um GUID. Este recurso segue o padrão de referência de WS-Addressing.  
  
 A camada de mensagens do WCF não grava nenhuma informação pessoal no computador local. No entanto, ele poderá propagar informações pessoais no nível da rede se um desenvolvedor de serviço tiver criado um serviço que expõe essas informações (por exemplo, usando o nome de uma pessoa em um nome de ponto de extremidade ou incluindo informações pessoais na linguagem de descrição dos serviços Web do ponto de extremidade, mas não exigindo que os clientes usem HTTPS para acessar o WSDL). Além disso, se um desenvolvedor executar a ferramenta [Svcutil.exe (ferramenta de utilitário de metadados ServiceModel)](servicemodel-metadata-utility-tool-svcutil-exe.md) em um ponto de extremidade que expõe informações pessoais, a saída da ferramenta poderá conter essas informações e o arquivo de saída será gravado no disco rígido local.  
  
## <a name="hosting"></a>Hospedagem  

 O recurso de hospedagem no WCF permite que os aplicativos iniciem sob demanda ou habilitem o compartilhamento de porta entre vários aplicativos. Um aplicativo WCF pode ser hospedado em Serviços de Informações da Internet (IIS), semelhante ao ASP.NET.  
  
 A hospedagem não expõe nenhuma informação específica na rede e não mantém os dados no computador.  
  
## <a name="message-security"></a>Segurança de mensagem  

 A segurança do WCF fornece os recursos de segurança para aplicativos de mensagens. As funções de segurança fornecidas incluem autenticação e autorização.  
  
 A autenticação é realizada passando credenciais entre os clientes e os serviços. A autenticação pode ser por meio de segurança em nível de transporte ou por meio de segurança em nível de mensagem SOAP, da seguinte maneira:  
  
- Na segurança de mensagem SOAP, a autenticação é executada por meio de credenciais como nome de usuário/senhas, certificados X. 509, tíquetes Kerberos e tokens SAML, que podem conter informações pessoais, dependendo do emissor.  
  
- Usando a segurança de transporte, a autenticação é feita por meio de mecanismos de autenticação de transporte tradicionais, como esquemas de autenticação HTTP (básico, Digest, negociação, autorização integrada do Windows, NTLM, nenhum e anônimo) e autenticação de formulário.  
  
 A autenticação pode resultar em uma sessão segura estabelecida entre os pontos de extremidade de comunicação. A sessão é identificada por um GUID que dura o tempo de vida da sessão de segurança. A tabela a seguir mostra o que é mantido e onde.  
  
|Dados|Armazenamento|  
|----------|-------------|  
|As credenciais de apresentação, como nome de usuário, certificados X. 509, tokens Kerberos e referências a credenciais.|Mecanismos padrão de gerenciamento de credenciais do Windows, como o repositório de certificados do Windows.|  
|Informações de associação de usuários, como nomes de usuário e senhas.|Provedores de associação do ASP.NET.|  
|Informações de identidade sobre o serviço usado para autenticar o serviço para clientes.|Endereço do ponto de extremidade do serviço.|  
|Informações do chamador.|Logs de auditoria.|  
  
## <a name="auditing"></a>Auditoria  

 A auditoria registra o êxito e a falha de eventos de autenticação e autorização. Os registros de auditoria contêm os seguintes dados: URI de serviço, URI de ação e identificação do chamador.  
  
 A auditoria também registra quando o administrador modifica a configuração do log de mensagens (ativando ou desligando), pois o log de mensagens pode registrar dados específicos do aplicativo em cabeçalhos e corpos. Para o Windows XP, um registro é registrado no log de eventos do aplicativo. Para o Windows Vista e o Windows Server 2003, um registro é registrado no log de eventos de segurança.  
  
## <a name="transactions"></a>Transactions  

 O recurso de transações fornece serviços transacionais para um aplicativo WCF.  
  
 Os cabeçalhos de transação usados na propagação da transação podem conter IDs de transação ou IDs de inscrição, que são GUIDs.  
  
 O recurso de transações usa o Gerenciador de transações do Microsoft Coordenador de Transações Distribuídas (MSDTC) (um componente do Windows) para gerenciar o estado da transação. Por padrão, as comunicações entre os gerenciadores de transações são criptografadas. Os gerenciadores de transações podem registrar referências de ponto de extremidade, IDs de transação e IDs de inscrição como parte de seu estado durável. O tempo de vida desse Estado é determinado pelo tempo de vida do arquivo de log do Gerenciador de transações. O serviço MSDTC possui e mantém esse log.  
  
 O recurso de transações implementa os padrões de transação WS-Coordination e WS-Atomic.  
  
## <a name="reliable-sessions"></a>Sessões confiáveis  

 As sessões confiáveis no WCF fornecem a transferência de mensagens quando ocorrem falhas de transporte ou intermediárias. Eles fornecem uma transferência de mensagens exatamente uma vez, mesmo quando o transporte subjacente se desconecta (por exemplo, uma conexão TCP em uma rede sem fio) ou perde uma mensagem (um proxy HTTP descartando uma mensagem de saída ou de entrada). As sessões confiáveis também recuperam a reordenação de mensagens (como pode acontecer no caso de roteamento de vários caminhos), preservando a ordem na qual as mensagens foram enviadas.  
  
 As sessões confiáveis são implementadas usando o protocolo WS-ReliableMessaging (WS-RM). Eles adicionam cabeçalhos WS-RM que contêm informações de sessão, que são usadas para identificar todas as mensagens associadas a uma sessão confiável específica. Cada sessão WS-RM tem um identificador, que é um GUID.  
  
 Nenhuma informação pessoal é mantida na máquina do usuário final.  
  
## <a name="queued-channels"></a>Canais em fila  

 As filas armazenam mensagens de um aplicativo de envio em nome de um aplicativo de recebimento e encaminham essas mensagens posteriormente para o aplicativo de recebimento. Eles ajudam a garantir que a transferência de mensagens envie aplicativos para o recebimento de aplicativos quando, por exemplo, o aplicativo receptor é transitório. O WCF dá suporte para enfileiramento usando o MSMQ (enfileiramento de mensagens da Microsoft) como um transporte.  
  
 O recurso de canais em fila não adiciona cabeçalhos a uma mensagem. Em vez disso, ele cria uma mensagem de enfileiramento de mensagens com as propriedades de mensagem do enfileiramento de mensagens apropriadas definidas e invoca métodos de enfileiramento de mensagens para colocar a mensagem na fila do enfileiramento O enfileiramento de mensagens é um componente opcional fornecido com o Windows.  
  
 Nenhuma informação é retida na máquina do usuário final pelo recurso de canais em fila, pois usa o enfileiramento de mensagens como a infraestrutura de enfileiramento.  
  
## <a name="com-integration"></a>Integração de COM+  

 Esse recurso encapsula a funcionalidade COM e COM+ existente para criar serviços que são compatíveis com os serviços WCF. Esse recurso não usa cabeçalhos específicos e não retém dados no computador do usuário final.  
  
## <a name="com-service-moniker"></a>Moniker do serviço COM  

 Isso fornece um wrapper não gerenciado para um cliente padrão do WCF. Esse recurso não tem cabeçalhos específicos na conexão, nem mantém os dados no computador.  
  
## <a name="peer-channel"></a>Canal par  

 Um canal de mesmo nível permite o desenvolvimento de aplicativos com multipartes usando o WCF. As mensagens multipartes ocorrem no contexto de uma malha. As malhas são identificadas por um nome que os nós podem unir. Cada nó no canal de mesmo nível cria um ouvinte TCP em uma porta especificada pelo usuário e estabelece conexões com outros nós na malha para garantir a resiliência. Para se conectar a outros nós na malha, os nós também trocam alguns dados, incluindo o endereço do ouvinte e os endereços IP do computador, com outros nós na malha. As mensagens enviadas na malha podem conter informações de segurança relacionadas ao remetente para evitar falsificação e adulteração de mensagens.  
  
 Nenhuma informação pessoal é armazenada na máquina do usuário final.  
  
## <a name="it-professional-experience"></a>Experiência profissional de ti  
  
### <a name="tracing"></a>Rastreamento  

 O recurso de diagnóstico da infraestrutura do WCF registra as mensagens que passam pelas camadas de modelo de serviço e transporte, bem como as atividades e os eventos associados a essas mensagens. Este recurso está desativado por padrão. Ele é habilitado usando o arquivo de configuração do aplicativo e o comportamento de rastreamento pode ser modificado usando o provedor WMI WCF em tempo de execução. Quando habilitada, a infraestrutura de rastreamento emite um rastreamento de diagnóstico que contém mensagens, atividades e eventos de processamento para os ouvintes configurados. O formato e o local da saída são determinados pelas opções de configuração de ouvinte do administrador, mas normalmente é um arquivo formatado XML. O administrador é responsável por definir a ACL (lista de controle de acesso) nos arquivos de rastreamento. Em particular, quando hospedado pelo WAS (sistema de ativação do Windows), o administrador deve verificar se os arquivos não são atendidos do diretório raiz virtual público, se isso não for desejado.  
  
 Há dois tipos de rastreamento: log de mensagens e rastreamento de diagnóstico do modelo de serviço, descritos na seção a seguir. Cada tipo é configurado por meio de sua própria origem de rastreamento: <xref:System.ServiceModel.Configuration.DiagnosticSection.MessageLogging%2A> e <xref:System.ServiceModel> . Ambas as fontes de rastreamento de log capturam dados que são locais para o aplicativo.  
  
### <a name="message-logging"></a>Registro em log de mensagens  

 A origem do rastreamento de log de mensagens ( <xref:System.ServiceModel.Configuration.DiagnosticSection.MessageLogging%2A> ) permite que um administrador Registre as mensagens que fluem pelo sistema. Por meio da configuração, o usuário pode decidir registrar somente mensagens inteiras ou cabeçalhos de mensagem, se deseja registrar nas camadas de modelo de transporte e/ou serviço e se deseja incluir mensagens malformadas. Além disso, o usuário pode configurar a filtragem para restringir quais mensagens são registradas.  
  
 Por padrão, o log de mensagens está desabilitado. O administrador do computador local pode impedir que o administrador de nível de aplicativo ative o log de mensagens.  
  
#### <a name="encrypted-and-decrypted-message-logging"></a>Registro em log de mensagens criptografadas e descriptografadas  

 As mensagens são registradas, criptografadas ou descriptografadas, conforme descrito nos termos a seguir.  
  
 Registro em log de transporte  
 Registra as mensagens recebidas e enviadas no nível de transporte. Essas mensagens contêm todos os cabeçalhos e podem ser criptografadas antes de serem enviadas na conexão e quando forem recebidas.  
  
 Se as mensagens forem criptografadas antes de serem enviadas na conexão e quando forem recebidas, elas também serão criptografadas em log. Uma exceção é quando um protocolo de segurança é usado (https): em seguida, eles são descriptografados em log antes de serem enviados e depois de serem recebidos, mesmo que sejam criptografados na conexão.  
  
 Registro em log do serviço  
 Registra as mensagens recebidas ou enviadas no nível do modelo de serviço, após a ocorrência do processamento do cabeçalho do canal, logo antes e depois da inserção do código do usuário.  
  
 As mensagens registradas nesse nível são descriptografadas mesmo que elas tenham sido protegidas e criptografadas na conexão.  
  
 Log de mensagens malformados  
 Registra mensagens que a infraestrutura do WCF não pode entender ou processar.  
  
 As mensagens são registradas como estão, ou seja, criptografadas ou não  
  
 Quando as mensagens são registradas em formato descriptografado ou não criptografado, por padrão, o WCF remove as chaves de segurança e as informações potencialmente pessoais das mensagens antes de fazer logon. As seções a seguir descrevem quais informações são removidas e quando. O administrador do computador e o implantador de aplicativos devem executar certas ações de configuração para alterar o comportamento padrão para chaves de log e informações potencialmente pessoais.  
  
#### <a name="information-removed-from-message-headers-when-logging-decryptedunencrypted-messages"></a>Informações removidas dos cabeçalhos de mensagem ao registrar em log as mensagens descriptografadas/não criptografadas  

 Quando as mensagens são registradas em formato descriptografado/não criptografado, as chaves de segurança e as informações potencialmente pessoais são removidas por padrão dos cabeçalhos e corpos das mensagens antes de serem registradas. A lista a seguir mostra o que o WCF considera as chaves e as informações potencialmente pessoais.  
  
 Chaves que são removidas:  
  
 \- Para xmlns: WST = " http://schemas.xmlsoap.org/ws/2004/04/trust " e xmlns: WST = " http://schemas.xmlsoap.org/ws/2005/02/trust "  
  
 WST: BinarySecret  
  
 WST: entropia  
  
 \- Para xmlns: wsse = " http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.1.xsd " e xmlns: wsse = " http://docs.oasis-open.org/wss/2005/xx/oasis-2005xx-wss-wssecurity-secext-1.1.xsd "  
  
 wsse: senha  
  
 wsse: nonce  
  
 Informações potencialmente pessoais que são removidas:  
  
 \- Para xmlns: wsse = " http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.1.xsd " e xmlns: wsse = " http://docs.oasis-open.org/wss/2005/xx/oasis-2005xx-wss-wssecurity-secext-1.1.xsd "  
  
 wsse: nome de usuário  
  
 wsse: BinarySecurityToken  
  
 \- Para xmlns: SAML = "urn: Oasis: names: TC: SAML: 1.0: Assertion", os itens em negrito (abaixo) são removidos:  
  
 \<Declaração  
  
 MajorVersion = "1"  
  
 MinorVersion = "1"  
  
 AssertionId = "[ID]"  
  
 Emissor = "[cadeia de caracteres]"  
  
 IssueInstant = "[dateTime]"  
  
 >  
  
 \<Conditions NotBefore="[dateTime]" NotOnOrAfter="[dateTime]">  
  
 \<AudienceRestrictionCondition>  
  
 \<Audience>URI\</Audience>+  
  
 \</AudienceRestrictionCondition>*  
  
 \<DoNotCacheCondition />*  
  
 <\!--tipo de base abstrato  
  
 \<Condition />*  
  
 -->  
  
 \</Conditions>?  
  
 \<Advice>  
  
 \<AssertionIDReference>SESSÃO\</AssertionIDReference>*  
  
 \<Assertion>declaração\</Assertion>*  
  
 [qualquer] *  
  
 \</Advice>?  
  
 <\!--Tipos base abstratos  
  
 \<Statement />*  
  
 \<SubjectStatement>  
  
 \<Subject>  
  
 `<NameIdentifier`  
  
 `NameQualifier="[string]"?`  
  
 `Format="[uri]"?`  
  
 `>`  
  
 `[string]`  
  
 `</NameIdentifier>?`  
  
 \<SubjectConfirmation>  
  
 \<ConfirmationMethod>AnyUri\</ConfirmationMethod>+  
  
 \<SubjectConfirmationData>[qualquer] \</SubjectConfirmationData> ?  
  
 \<ds:KeyInfo>...\</ds:KeyInfo>?  
  
 \</SubjectConfirmation>?  
  
 \</Subject>  
  
 \</SubjectStatement>*  
  
 -->  
  
 \<AuthenticationStatement  
  
 AuthenticationMethod = "[URI]"  
  
 AuthenticationInstant = "[dateTime]"  
  
 >  
  
 Subjetiva  
  
 `<SubjectLocality`  
  
 `IPAddress="[string]"?`  
  
 `DNSAddress="[string]"?`  
  
 `/>?`  
  
 <Authoritybinding  
  
 AuthorityKind = "[QName]"  
  
 Location = "[URI]"  
  
 Binding = "[URI]"  
  
 />*  
  
 \</AuthenticationStatement>*  
  
 \<AttributeStatement>  
  
 Subjetiva  
  
 \<Atributo  
  
 AttributeName = "[cadeia de caracteres]"  
  
 AttributeNamespace = "[URI]"  
  
 >  
  
 `<AttributeValue>[any]</AttributeValue>+`  
  
 \</Attribute>+  
  
 \</AttributeStatement>*  
  
 \<AuthorizationDecisionStatement  
  
 Recurso = "[URI]"  
  
 Decisão = "[permitir&#124;negar&#124;indeterminado]"  
  
 >  
  
 Subjetiva  
  
 \<Action Namespace="[uri]">Strings\</Action>+  
  
 \<Evidence>  
  
 \<AssertionIDReference>SESSÃO\</AssertionIDReference>+  
  
 \<Assertion>declaração\</Assertion>+  
  
 \</Evidence>?  
  
 \</AuthorizationDecisionStatement>*  
  
 \</Assertion>  
  
#### <a name="information-removed-from-message-bodies-when-logging-decryptedunencrypted-messages"></a>Informações removidas de corpos de mensagens ao registrar em log mensagens descriptografadas/sem criptografia  

 Conforme descrito anteriormente, o WCF remove as chaves e as informações potencialmente pessoais conhecidas dos cabeçalhos de mensagem para mensagens descriptografadas/descriptografadas registradas. Além disso, o WCF remove as chaves e as informações potencialmente pessoais conhecidas dos corpos de mensagens para os elementos e ações do corpo na lista a seguir, que descrevem as mensagens de segurança envolvidas na troca de chaves.  
  
 Para os seguintes namespaces:  
  
 xmlns: WST = " http://schemas.xmlsoap.org/ws/2004/04/trust " e xmlns: WST = " http://schemas.xmlsoap.org/ws/2005/02/trust " (por exemplo, se nenhuma ação estiver disponível)  
  
 As informações são removidas para esses elementos do corpo, que envolvem a troca de chaves:  
  
 WST: RequestSecurityToken  
  
 WST: RequestSecurityTokenResponse  
  
 WST: RequestSecurityTokenResponseCollection  
  
 As informações também são removidas para cada uma das seguintes ações:  
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/Issue`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/Issue`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/Renew`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/Renew`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/Cancel`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/Cancel`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/Validate`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/Validate`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/SCT`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/SCT`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/SCT/Amend`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/SCT/Amend`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/SCT/Renew`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/SCT/Renew`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RST/SCT/Cancel`
  
- `http://schemas.xmlsoap.org/ws/2005/02/trust/RSTR/SCT/Cancel`
  
- `http://schemas.xmlsoap.org/ws/2004/04/security/trust/RST/SCT`
  
- `http://schemas.xmlsoap.org/ws/2004/04/security/trust/RSTR/SCT`
  
- `http://schemas.xmlsoap.org/ws/2004/04/security/trust/RST/SCT-Amend`
  
- `http://schemas.xmlsoap.org/ws/2004/04/security/trust/RSTR/SCT-Amend`
  
#### <a name="no-information-is-removed-from-application-specific-headers-and-body-data"></a>Nenhuma informação é removida dos cabeçalhos e dos dados de corpo específicos do aplicativo  

 O WCF não rastreia informações pessoais em cabeçalhos específicos do aplicativo (por exemplo, cadeias de caracteres de consulta) ou dados de corpo (por exemplo, número de cartão de crédito).  
  
 Quando o log de mensagens está ativado, informações pessoais em cabeçalhos específicos do aplicativo e informações de corpo podem estar visíveis nos logs. Novamente, o implantador de aplicativos é responsável por definir as ACLs nos arquivos de configuração e de log. Eles também poderão desativar o registro em log se não quiserem que essas informações fiquem visíveis ou filtrar essas informações dos arquivos de log depois de serem registradas.  
  
### <a name="service-model-tracing"></a>Rastreamento do modelo de serviço  

 A fonte de rastreamento do modelo de serviço ( <xref:System.ServiceModel> ) permite o rastreamento de atividades e eventos relacionados ao processamento de mensagens. Esse recurso usa a funcionalidade de diagnóstico .NET Framework do <xref:System.Diagnostics> . Assim como acontece com a <xref:System.ServiceModel.Configuration.DiagnosticSection.MessageLogging%2A> propriedade, o local e sua ACL são configuráveis pelo usuário usando .NET Framework arquivos de configuração de aplicativo. Assim como ocorre com o log de mensagens, o local do arquivo é sempre configurado quando o administrador habilita o rastreamento; Portanto, o administrador controla a ACL.  
  
 Os rastreamentos contêm cabeçalhos de mensagem quando uma mensagem está no escopo. As mesmas regras para ocultar informações potencialmente pessoais em cabeçalhos de mensagens na seção anterior se aplicam: as informações pessoais identificadas anteriormente são removidas por padrão dos cabeçalhos em rastreamentos. Tanto o administrador do computador quanto o implantador de aplicativos devem modificar a configuração para registrar informações potencialmente pessoais. No entanto, as informações pessoais contidas em cabeçalhos específicos do aplicativo são registradas em rastreamentos. O implantador de aplicativos é responsável por definir as ACLs nos arquivos de configuração e de rastreamento. Eles também podem desativar o rastreamento para ocultar essas informações ou filtrar essas informações dos arquivos de rastreamento depois de serem registrados.  
  
 Como parte do rastreamento de ServiceModel, as IDs exclusivas (chamadas de IDs de atividade e, normalmente, um GUID) vinculam diferentes atividades em conjunto como uma mensagem fluindo por diferentes partes da infraestrutura.  
  
#### <a name="custom-trace-listeners"></a>Ouvintes de rastreamento personalizados  

 Para o log de mensagens e o rastreamento, um ouvinte de rastreamento personalizado pode ser configurado, o que pode enviar rastreamentos e mensagens na transmissão (por exemplo, para um banco de dados remoto). O implantador de aplicativos é responsável por configurar ouvintes personalizados ou permitir que os usuários façam isso. Eles também são responsáveis por qualquer informação pessoal exposta no local remoto e para aplicar as ACLs adequadamente a esse local.  
  
### <a name="other-features-for-it-professionals"></a>Outros recursos para profissionais de ti  

 O WCF tem um provedor WMI que expõe as informações de configuração de infraestrutura do WCF por meio do WMI (fornecido com o Windows). Por padrão, a interface WMI está disponível para administradores.  
  
 A configuração do WCF usa o mecanismo de configuração do .NET Framework. Os arquivos de configuração são armazenados no computador. O desenvolvedor de aplicativos e o administrador criam os arquivos de configuração e a ACL para cada um dos requisitos do aplicativo. Um arquivo de configuração pode conter endereços de ponto de extremidade e links para certificados no repositório de certificados. Os certificados podem ser usados para fornecer dados de aplicativo para configurar várias propriedades dos recursos usados pelo aplicativo.  
  
 O WCF também usa a funcionalidade de despejo de .NET Framework processo chamando o <xref:System.Environment.FailFast%2A> método.  
  
### <a name="it-pro-tools"></a>Ferramentas de profissionais de ti  

 O WCF também fornece as seguintes ferramentas profissionais de ti, que são fornecidas na SDK do Windows.  
  
#### <a name="svctraceviewerexe"></a>SvcTraceViewer.exe  

 O visualizador exibe os arquivos de rastreamento do WCF. O visualizador mostra qualquer informação contida nos rastreamentos.  
  
#### <a name="svcconfigeditorexe"></a>SvcConfigEditor.exe  

 O editor permite que o usuário crie e edite arquivos de configuração do WCF. O editor mostra qualquer informação contida nos arquivos de configuração. A mesma tarefa pode ser realizada com um editor de texto.  
  
#### <a name="servicemodel_reg"></a>ServiceModel_Reg  

 Essa ferramenta permite que o usuário gerencie instalações de ServiceModel em um computador. A ferramenta exibe mensagens de status em uma janela de console quando ela é executada e, no processo, pode exibir informações sobre a configuração da instalação do WCF.  
  
#### <a name="wsatconfigexe-and-wsatuidll"></a>WSATConfig.exe e WSATUI.dll  

 Essas ferramentas permitem que os profissionais de ti configurem o suporte de rede interoperável WS-AtomicTransaction no WCF. As ferramentas exibem e permitem que o usuário altere os valores das configurações de WS-AtomicTransaction usadas com mais frequência armazenadas no registro.  
  
## <a name="cross-cutting-features"></a>Recursos de corte cruzado  

 Os recursos a seguir são de corte cruzado. Ou seja, eles podem ser compostos com qualquer um dos recursos anteriores.  
  
### <a name="service-framework"></a>Estrutura de serviço  

 Os cabeçalhos podem conter uma ID de instância, que é um GUID que associa uma mensagem a uma instância de uma classe CLR.  
  
 O WSDL (Web Services Description Language) contém uma definição da porta. Cada porta tem um endereço de ponto de extremidade e uma associação que representa os serviços usados pelo aplicativo. Expor o WSDL pode ser desativado usando a configuração. Nenhuma informação é mantida no computador.  
  
## <a name="see-also"></a>Consulte também

- [Windows Communication Foundation](index.md)
- [Segurança](./feature-details/security.md)
