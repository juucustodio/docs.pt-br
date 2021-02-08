---
description: 'Saiba mais sobre: <wsFederation>'
title: <wsFederation>
ms.date: 03/30/2017
ms.assetid: c537f770-68bd-4f82-96ad-6424ad91369f
author: BrucePerlerMS
ms.openlocfilehash: f28c140816dc6de6d618772d5213d6ab094b78c5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802119"
---
# \<wsFederation>

Fornece a configuração para o <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> (WSFAM).  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel.services>**](system-identitymodel-services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<federationConfiguration>**](federationconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<wsFederation>**  
  
## <a name="syntax"></a>Syntax  
  
```xml
<system.identityModel.services>  
  <federationConfiguration>  
    <wsFederation authenticationType=xs:string (URI)  
                  freshness=xs:decimal  
                  homerealm=xs:string (URI)  
                  issuer=xs:string (URI)  
                  persistentCookiesOnPassiveRedirects=xs:boolean  
                  passiveRedirectEnabled=xs:boolean  
                  policy=xs:string (URI)  
                  realm=xs:string (URI)  
                  reply=xs:string (URI)  
                  request=xs:string (URI)  
                  requestPtr=xs:string (URI)  
                  requireHttps=xs:boolean  
                  resource=xs:string (URI)  
                  signInQueryString=xs:string  
                  signOutQueryString=xs:string  
                  signOutReply=xs:string (URL)  
    </wsFederation>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|authenticationType|Um URI que especifica o tipo de autenticação. Define o parâmetro wauth de solicitação de entrada WS-Federation. Opcional. O padrão é uma cadeia de caracteres vazia, que especifica que o parâmetro wauth não está incluído na solicitação.|  
|atualização|A idade máxima desejada de solicitações de autenticação, em minutos. Define o parâmetro wfresh de solicitação de entrada WS-Federation. Opcional. O padrão é zero. Opcional. **AVISO:**  Na próxima versão do .NET Framework 4,5, o `freshness` atributo será do tipo `xs:string` e seu valor padrão será `null` .|  
|homeRealm|O realm inicial do IdP (provedor de identidade) a ser usado para autenticação. Define a WS-Federation parâmetro de solicitação de conexão de WHR. Opcional. O padrão é uma cadeia de caracteres vazia, que especifica que o parâmetro whr não está incluído na solicitação.|  
|emissor|O URI do emissor do token pretendido. Define a URL base de WS-Federation solicitações de entrada e solicitações de saída necessárias.|  
|persistentCookiesOnPassiveRedirects|Especifica se cookies persistentes são emitidos na autenticação. Opcional. O padrão é "false", os cookies não são emitidos.|  
|passiveRedirectEnabled|Especifica se o WSFAM está habilitado para redirecionar automaticamente solicitações não autorizadas para um STS. Opcional. O padrão é "true", as solicitações não autorizadas são redirecionadas automaticamente.|  
|policy|Uma URL que especifica o local da política relevante a ser usada nas solicitações de entrada. O padrão é uma cadeia de caracteres vazia. Define o parâmetro de wp de solicitação de entrada WS-Federation. Opcional. O padrão é uma cadeia de caracteres vazia, que especifica que o parâmetro WP não está incluído na solicitação.|  
|territórios|O URI do Realm solicitante. (Um URI que identifica a parte confiável (RP) para o serviço de token de segurança (STS).) Define a solicitação wtrealm WS-Federation parâmetro de solicitação de entrada. Obrigatório.|  
|resposta|Uma URL que identifica o endereço no qual o aplicativo RP (terceira parte confiável) gostaria de receber respostas do serviço de token de segurança (STS). Define o parâmetro Wreply de solicitação de entrada WS-Federation. Opcional. O padrão é uma cadeia de caracteres vazia, que especifica que o parâmetro Wreply não está incluído na solicitação.|  
|solicitação|A solicitação de emissão de token. Define o parâmetro wreq de solicitação de entrada WS-Federation. Opcional. O padrão é uma cadeia de caracteres vazia, que especifica que o parâmetro wreq não está incluído na solicitação. Não incluir o parâmetro wreq ou wreqptr na solicitação implica que o STS sabe que tipo de token emitir.|  
|requestPtr|Uma URL que especifica o local da solicitação de emissão de token. Define o parâmetro wreqptr da solicitação. Opcional. O padrão é uma cadeia de caracteres vazia, que especifica que o parâmetro wreqptr não está incluído na solicitação. Não incluir o parâmetro wreq ou wreqptr na solicitação implica que o STS sabe que tipo de token emitir.|  
|requireHttps|Especifica se a comunicação com o serviço de token de segurança (STS) deve usar o protocolo HTTPS. Opcional. O padrão é "true", o HTTPS deve ser usado.|  
|recurso|Um URI que identifica o recurso que está sendo acessado, a RP (terceira parte confiável), para o serviço de token de segurança (STS). Opcional. Define o parâmetro wres de solicitação de entrada WS-Federation. Opcional. O padrão é uma cadeia de caracteres vazia, que especifica que o parâmetro wres não está incluído na solicitação. **Observação:**  wres é um parâmetro herdado. `realm`Em vez disso, especifique o atributo para usar o parâmetro wtrealm.|  
|signInQueryString|Fornece um ponto de extensibilidade para especificar parâmetros de consulta definidos pelo aplicativo no WS-Federation URL de solicitação de entrada. Opcional. O padrão é uma cadeia de caracteres vazia, que especifica que nenhum parâmetro adicional deve ser incluído na solicitação. Os parâmetros são especificados como um fragmento de cadeia de caracteres de consulta usando a seguinte forma: `"param1=value1&param2=value2&param3=value3"` e assim por diante. **Observação:**  Em um arquivo de configuração, o caractere "&" na cadeia de caracteres de consulta deve ser especificado usando sua referência de entidade, `&` .|  
|signOutQueryString|Fornece um ponto de extensibilidade para especificar parâmetros de consulta definidos pelo aplicativo no WS-Federation URL de solicitação de entrada. Opcional. O padrão é uma cadeia de caracteres vazia, que especifica que nenhum parâmetro adicional deve ser incluído na solicitação. Os parâmetros são especificados como um fragmento de cadeia de caracteres de consulta usando a seguinte forma: `"param1=value1&param2=value2&param3=value3"` e assim por diante. **Observação:**  Em um arquivo de configuração, o caractere "&" na cadeia de caracteres de consulta deve ser especificado usando sua referência de entidade, `&` .|  
|signOutReply|Especifica a URL para a qual o cliente deve ser redirecionado pelo STS (serviço de token de segurança) durante a saída passiva por meio do protocolo WS-Federation. Define o parâmetro Wreply em uma solicitação de saída de WS-Federation. Opcional. O padrão é uma cadeia de caracteres vazia, que especifica que nenhum parâmetro adicional deve ser incluído na solicitação.|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<federationConfiguration>](federationconfiguration.md)|Contém as configurações que definem o <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> (WSFAM) e o <xref:System.IdentityModel.Services.SessionAuthenticationModule> (Sam).|  
  
## <a name="remarks"></a>Comentários  

 Você pode usar o `<wsFederation>` elemento para definir as configurações padrão de parâmetro de WS-Federation e o comportamento padrão para o WSFAM. WS-Federation configurações de parâmetro definidas no `<wsFederation>` elemento definir propriedades equivalentes expostas pela <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> classe. Essas propriedades permanecem as mesmas para cada solicitação emitida pelo WSFAM. Você pode alterar os parâmetros de WS-Federation dinamicamente durante o processamento da solicitação adicionando manipuladores de eventos para os eventos expostos por WSFAM; por exemplo, o <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectingToIdentityProvider> evento. Para obter mais informações, consulte a documentação da <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> classe.  
  
 O `<wsFederation>` elemento é representado pela <xref:System.IdentityModel.Services.Configuration.WSFederationElement> classe. O próprio objeto de configuração é representado pela <xref:System.IdentityModel.Services.Configuration.WsFederationConfiguration> classe. Uma única <xref:System.IdentityModel.Services.Configuration.WsFederationConfiguration> instância é definida no <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> objeto que é acessado por meio da <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=nameWithType> propriedade e fornece a configuração para o WSFAM.  
  
## <a name="example"></a>Exemplo  

 O XML a seguir mostra um `<wsFederation>` elemento que especifica as configurações para o WSFAM.  
  
> [!WARNING]
> Neste exemplo, o WSFAM não é necessário para usar HTTPS. Isso ocorre porque o `requireHttps` atributo no `<wsFederation>` elemento está definido `false` . Essa configuração não é recomendada para a maioria dos ambientes de produção, pois pode representar um risco de segurança.  
  
```xml
<wsFederation passiveRedirectEnabled="true"
              issuer="http://localhost:15839/wsFederationSTS/Issue"
              realm="http://localhost:50969/"
              reply="http://localhost:50969/"
              requireHttps="false"
              signOutReply="http://localhost:50969/SignedOutPage.html"
              signOutQueryString="Param1=value2&Param2=value2"
              persistentCookiesOnPassiveRedirects="true" />
```  
  
## <a name="see-also"></a>Confira também

- <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>
- <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=nameWithType>
