---
description: 'Saiba mais sobre: HttpTransportBindingElement'
title: HttpTransportBindingElement
ms.date: 03/30/2017
ms.assetid: 088a7bce-6bb2-4839-ad74-f68d4b1aa0f9
ms.openlocfilehash: 6c516dd7124d52828145787d55421d12031c2d36
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99757365"
---
# <a name="httptransportbindingelement"></a>HttpTransportBindingElement

HttpTransportBindingElement  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class HttpTransportBindingElement : TransportBindingElement  
{  
  boolean AllowCookies;  
  string AuthenticationScheme;  
  boolean BypassProxyOnLocal;  
  string HostNameComparisonMode;  
  boolean KeepAliveEnabled;  
  sint32 MaxBufferSize;  
  string ProxyAddress;  
  string ProxyAuthenticationScheme;  
  string Realm;  
  string TransferMode;  
  boolean UnsafeConnectionNtlmAuthentication;  
  boolean UseDefaultWebProxy;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe HttpTransportBindingElement não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe HttpTransportBindingElement tem as seguintes propriedades:  
  
### <a name="allowcookies"></a>AllowCookies  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor que indica se o cliente aceita cookies e os propaga em solicitações futuras.  
  
### <a name="authenticationscheme"></a>AuthenticationScheme  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O esquema de autenticação usado para autenticar solicitações de cliente sendo processadas por um ouvinte HTTP.  
  
### <a name="bypassproxyonlocal"></a>BypassProxyOnLocal  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor que indica se os proxies são ignorados para endereços locais.  
  
### <a name="hostnamecomparisonmode"></a>HostNameComparisonMode  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Um valor que indica se o nome do host é usado para acessar o serviço ao fazer a correspondência no URI.  
  
### <a name="keepaliveenabled"></a>KeepAliveEnabled  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Quando habilitadas, as conexões HTTP são mantidas ativas, independentemente do nível de atividade.  
  
### <a name="maxbuffersize"></a>MaxBufferSize  

 Tipo de dados: sint32  
  
 Tipo de acesso: Somente leitura  
  
 O tamanho máximo do pool de buffers.  
  
### <a name="proxyaddress"></a>ProxyAddress  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Um URI que contém o endereço do proxy a ser usado para solicitações HTTP.  
  
### <a name="proxyauthenticationscheme"></a>ProxyAuthenticationScheme  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O esquema de autenticação usado para autenticar solicitações de cliente sendo processadas por um proxy HTTP.  
  
### <a name="realm"></a>Realm  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O realm de autenticação.  
  
### <a name="transfermode"></a>TransferMode  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Um valor que especifica se as mensagens são armazenadas em buffer ou transmitidas ou uma solicitação ou resposta.  
  
### <a name="unsafeconnectionntlmauthentication"></a>UnsafeConnectionNtlmAuthentication  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor que indica se o compartilhamento de conexão não segura está habilitado no servidor.  
  
### <a name="usedefaultwebproxy"></a>UseDefaultWebProxy  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor que indica se as configurações de proxy de todo o computador são usadas em vez das configurações específicas do usuário.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>
