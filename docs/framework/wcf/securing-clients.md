---
description: 'Saiba mais sobre: protegendo clientes'
title: Protegendo clientes
ms.date: 03/30/2017
helpviewer_keywords:
- clients [WCF], security considerations
ms.assetid: 44c8578c-9a5b-4acd-8168-1c30a027c4c5
ms.openlocfilehash: d78ad2fba00a0707dcf1c63681d9d76e68a31c00
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99676437"
---
# <a name="securing-clients"></a>Protegendo clientes

No Windows Communication Foundation (WCF), o serviço determina os requisitos de segurança para clientes. Ou seja, o serviço especifica o modo de segurança a ser usado e se o cliente deve ou não fornecer uma credencial. O processo de proteger um cliente, portanto, é simples: usar os metadados obtidos do serviço (se for publicado) e criar um cliente. Os metadados especificam como configurar o cliente. Se o serviço exigir que o cliente forneça uma credencial, você deverá obter uma credencial que atenda ao requisito. Este tópico discute o processo mais detalhadamente. Para obter mais informações sobre como criar um serviço seguro, consulte [protegendo serviços](securing-services.md).  
  
## <a name="the-service-specifies-security"></a>O serviço especifica a segurança  

 Por padrão, as associações do WCF têm recursos de segurança habilitados. (A exceção é o <xref:System.ServiceModel.BasicHttpBinding> .) Portanto, se o serviço foi criado usando o WCF, há uma chance maior de que ele implementará a segurança para garantir a autenticação, a confidencialidade e a integridade. Nesse caso, os metadados fornecidos pelo serviço indicarão o que é necessário para estabelecer um canal de comunicação seguro. Se os metadados de serviço não incluírem nenhum requisito de segurança, não será possível impor um esquema de segurança, como protocolo SSL (SSL) por HTTP, em um serviço. No entanto, se o serviço exigir que o cliente forneça uma credencial, o desenvolvedor, o implantador ou o administrador do cliente deverá fornecer a credencial real que o cliente usará para se autenticar no serviço.  
  
## <a name="obtaining-metadata"></a>Obtendo metadados  

 Ao criar um cliente, a primeira etapa é obter os metadados para o serviço com o qual o cliente irá se comunicar. Isso pode ser feito de duas maneiras. Primeiro, se o serviço publicar um ponto de extremidade de intercâmbio de metadados (MEX) ou disponibilizar seus metadados via HTTP ou HTTPS, você poderá baixar os metadados usando a [ferramenta de utilitário de metadados ServiceModel (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md), que gera ambos os arquivos de código para um cliente, bem como um arquivo de configuração. (Para obter mais informações sobre como usar a ferramenta, consulte [acessando serviços usando um cliente WCF](accessing-services-using-a-wcf-client.md).) Se o serviço não publicar um ponto de extremidade MEX e também não disponibilizar seus metadados via HTTP ou HTTPS, você deverá entrar em contato com o criador de serviços para obter a documentação que descreve os requisitos de segurança e os metadados.  
  
> [!IMPORTANT]
> É recomendável que os metadados venham de uma fonte confiável e que não sejam adulterados. Os metadados recuperados usando o protocolo HTTP são enviados em texto não criptografado e podem ser adulterados. Se o serviço usar as <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A> Propriedades e, use a URL fornecida pelo criador de serviço para baixar os dados usando o protocolo HTTPS.  
  
## <a name="validating-security"></a>Validando a segurança  

 As fontes de metadados podem ser divididas em duas categorias amplas: fontes de confiança e fontes não confiáveis. Se você confiar em uma fonte e tiver baixado o código do cliente e outros metadados do ponto de extremidade do MEX seguro da origem, poderá criar o cliente, fornecê-lo com as credenciais corretas e executá-lo sem nenhuma outra preocupação.  
  
 No entanto, se você optar por baixar um cliente e metadados de uma fonte da qual você sabe pouco, certifique-se de validar as medidas de segurança que o código usa. Por exemplo, você não deve simplesmente criar um cliente que envie suas informações pessoais ou financeiras para um serviço, a menos que o serviço exija confidencialidade e integridade (pelo menos). Você deve confiar no proprietário do serviço na medida em que está disposto a divulgar essas informações, pois essas informações ficarão visíveis para elas.  
  
 Como regra, portanto, ao usar o código e os metadados de uma fonte não confiável, verifique o código e os metadados para garantir que ele atenda ao nível de segurança que você precisa.  
  
## <a name="setting-a-client-credential"></a>Configurando uma credencial do cliente  

 Definir uma credencial de cliente em um cliente consiste em duas etapas:  
  
1. Determine o *tipo de credencial do cliente* que o serviço requer. Isso é feito por um dos dois métodos. Primeiro, se você tiver a documentação do criador de serviços, ele deverá especificar o tipo de credencial do cliente (se houver) que o serviço requer. Em segundo lugar, se você tiver apenas um arquivo de configuração gerado pela ferramenta de Svcutil.exe, poderá examinar as associações individuais para determinar qual tipo de credencial é necessário.  
  
2. Especifique uma credencial de cliente real. A credencial de cliente real é chamada de *valor de credencial de cliente* para distingui-la do tipo. Por exemplo, se o tipo de credencial do cliente especificar um certificado, você deverá fornecer um certificado X. 509 emitido por uma autoridade de certificação em que o serviço confia.  
  
### <a name="determining-the-client-credential-type"></a>Determinando o tipo de credencial do cliente  

 Se você tiver o arquivo de configuração que a ferramenta de Svcutil.exe gerou, examine a [\<bindings>](../configure-apps/file-schema/wcf/bindings.md) seção para determinar qual tipo de credencial de cliente é necessário. Dentro da seção estão elementos de associação que especificam os requisitos de segurança. Especificamente, examine o \<security> elemento de cada associação. Esse elemento inclui o `mode` atributo, que pode ser definido como um dos três valores possíveis ( `Message` , `Transport` ou `TransportWithMessageCredential` ). O valor do atributo determina o modo e o modo determina quais elementos filho são significativos.  
  
 O `<security>` elemento pode conter um `<transport>` elemento ou ou `<message>` ambos. O elemento significativo é aquele que corresponde ao modo de segurança. Por exemplo, o código a seguir especifica que o modo de segurança é `"Message"` , e o tipo de credencial do cliente para o `<message>` elemento é `"Certificate"` . Nesse caso, o `<transport>` elemento pode ser ignorado. No entanto, o `<message>` elemento Especifica que um certificado X. 509 deve ser fornecido.  

```xml  
<wsHttpBinding>  
    <binding name="WSHttpBinding_ICalculator">  
       <security mode="Message">  
           <transport clientCredentialType="Windows"
                      realm="" />  
           <message clientCredentialType="Certificate"
                    negotiateServiceCredential="true"  
                    algorithmSuite="Default"
                    establishSecurityContext="true" />  
       </security>  
    </binding>  
</wsHttpBinding>  
```  

 Observe que, se o `clientCredentialType` atributo for definido como `"Windows"` , conforme mostrado no exemplo a seguir, você não precisará fornecer um valor de credencial real. Isso ocorre porque a segurança integrada do Windows fornece a credencial real (um token Kerberos) da pessoa que está executando o cliente.  
  
```xml  
<security mode="Message">  
    <transport clientCredentialType="Windows "
        realm="" />  
</security>  
```  
  
### <a name="setting-the-client-credential-value"></a>Definindo o valor da credencial do cliente  

 Se for determinado que o cliente deve fornecer uma credencial, use o método apropriado para configurar o cliente. Por exemplo, para definir um certificado de cliente, use o <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> método.  
  
 Uma forma comum de credencial é o certificado X. 509. Você pode fornecer a credencial de duas maneiras:  
  
- Programando-o no seu código de cliente (usando o `SetCertificate` método).  
  
 Adicionando uma [\<behaviors>](../configure-apps/file-schema/wcf/behaviors.md) seção do arquivo de configuração para o cliente e usando o `clientCredentials` elemento (mostrado abaixo).  
  
#### <a name="setting-a-clientcredentials-value-in-code"></a>Definindo um \<clientCredentials> valor no código  

 Para definir um [\<clientCredentials>](../configure-apps/file-schema/wcf/clientcredentials.md) valor no código, você deve acessar a <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> propriedade da <xref:System.ServiceModel.ClientBase%601> classe. A propriedade retorna um <xref:System.ServiceModel.Description.ClientCredentials> objeto que permite o acesso a vários tipos de credenciais, conforme mostrado na tabela a seguir.  
  
|Propriedade ClientCredential|Descrição|Observações|  
|-------------------------------|-----------------|-----------|  
|<xref:System.ServiceModel.Description.ClientCredentials.ClientCertificate%2A>|Retorna um <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>|Representa um certificado X. 509 fornecido pelo cliente para se autenticar no serviço.|  
|<xref:System.ServiceModel.Description.ClientCredentials.HttpDigest%2A>|Retorna um <xref:System.ServiceModel.Security.HttpDigestClientCredential>|Representa uma credencial HTTP Digest. A credencial é um hash do nome de usuário e da senha.|  
|<xref:System.ServiceModel.Description.ClientCredentials.IssuedToken%2A>|Retorna um <xref:System.ServiceModel.Security.IssuedTokenClientCredential>|Representa um token de segurança personalizado emitido por um serviço de token de segurança, normalmente usado em cenários de Federação.|  
|<xref:System.ServiceModel.Description.ClientCredentials.Peer%2A>|Retorna um <xref:System.ServiceModel.Security.PeerCredential>|Representa uma credencial par para participação em uma malha de mesmo nível em um domínio do Windows.|  
|<xref:System.ServiceModel.Description.ClientCredentials.ServiceCertificate%2A>|Retorna um <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>|Representa um certificado X. 509 fornecido pelo serviço em uma negociação fora de banda.|  
|<xref:System.ServiceModel.Description.ClientCredentials.UserName%2A>|Retorna um <xref:System.ServiceModel.Security.UserNamePasswordClientCredential>|Representa um par de nome de usuário e senha.|  
|<xref:System.ServiceModel.Description.ClientCredentials.Windows%2A>|Retorna um <xref:System.ServiceModel.Security.WindowsClientCredential>|Representa uma credencial de cliente do Windows (uma credencial Kerberos). As propriedades da classe são somente leitura.|  
  
#### <a name="setting-a-clientcredentials-value-in-configuration"></a>Definindo um \<clientCredentials> valor na configuração  

 Os valores de credenciais são especificados usando um comportamento de ponto de extremidade como elementos filho do [\<clientCredentials>](../configure-apps/file-schema/wcf/clientcredentials.md) elemento. O elemento usado depende do tipo de credencial do cliente. Por exemplo, o exemplo a seguir mostra a configuração para definir um certificado X. 509 usando o <[\<clientCertificate>](../configure-apps/file-schema/wcf/clientcertificate-of-clientcredentials-element.md) .  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>
        <behavior name="myEndpointBehavior">  
          <clientCredentials>  
            <clientCertificate findvalue="myMachineName"
            storeLocation="Current" X509FindType="FindBySubjectName" />  
          </clientCredentials>  
        </behavior>
      </endpointBehaviors>
    </behaviors>
  </system.serviceModel>  
</configuration>  
```  
  
 Para definir a credencial do cliente na configuração, adicione um [\<endpointBehaviors>](../configure-apps/file-schema/wcf/endpointbehaviors.md) elemento ao arquivo de configuração. Além disso, o elemento de comportamento adicionado deve ser vinculado ao ponto de extremidade do serviço usando o `behaviorConfiguration` atributo do elemento [ \<endpoint> \<client> de](../configure-apps/file-schema/wcf/endpoint-of-client.md) , conforme mostrado no exemplo a seguir. O valor do `behaviorConfiguration` atributo deve corresponder ao valor do atributo de comportamento `name` .  

```xml
<configuration>
  <system.serviceModel>
    <client>
      <endpoint address="http://localhost/servicemodelsamples/service.svc"
                binding="wsHttpBinding"
                bindingConfiguration="Binding1"
                behaviorConfiguration="myEndpointBehavior"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </client>
  </system.serviceModel>
</configuration>
```
  
> [!NOTE]
> Alguns dos valores de credencial do cliente não podem ser definidos usando arquivos de configuração do aplicativo, por exemplo, nome de usuário e senha, ou valores de usuário e senha do Windows. Esses valores de credenciais podem ser especificados somente no código.  
  
 Para obter mais informações sobre como definir a credencial do cliente, consulte [como especificar valores de credencial do cliente](how-to-specify-client-credential-values.md).  
  
> [!NOTE]
> `ClientCredentialType` é ignorado quando `SecurityMode` é definido `"TransportWithMessageCredential",` como, conforme mostrado na configuração de exemplo a seguir.  
  
```xml  
<wsHttpBinding>  
    <binding name="PingBinding">  
        <security mode="TransportWithMessageCredential"  >  
           <message  clientCredentialType="UserName"
               establishSecurityContext="false"
               negotiateServiceCredential="false" />  
           <transport clientCredentialType="Certificate"  />  
         </security>  
    </binding>  
</wsHttpBinding>  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A>
- <xref:System.ServiceModel.ClientBase%601>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A>
- <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A>
- [\<bindings>](../configure-apps/file-schema/wcf/bindings.md)
- [Ferramenta Configuration Editor (SvcConfigEditor.exe)](configuration-editor-tool-svcconfigeditor-exe.md)
- [Serviços de segurança](securing-services.md)
- [Usando um cliente WCF para acessar um serviço](accessing-services-using-a-wcf-client.md)
- [Como: especificar valores de credenciais de cliente](how-to-specify-client-credential-values.md)
- [Ferramenta Utilitário de Metadados ServiceModel (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md)
- [Como: especificar o tipo de credencial de cliente](how-to-specify-the-client-credential-type.md)
