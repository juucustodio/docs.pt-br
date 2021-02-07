---
description: 'Saiba mais sobre: como criar um serviço que empregue um validador de certificado personalizado'
title: 'Como: criar um serviço que utiliza um validador de certificado personalizado'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, authentication
ms.assetid: bb0190ff-0738-4e54-8d22-c97d343708bf
ms.openlocfilehash: 8ed5d23143b7b69768cc556d9fd5663e46fd7da7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99668975"
---
# <a name="how-to-create-a-service-that-employs-a-custom-certificate-validator"></a>Como: criar um serviço que utiliza um validador de certificado personalizado

Este tópico mostra como implementar um validador de certificado personalizado e como configurar credenciais de cliente ou serviço para substituir a lógica de validação de certificado padrão pelo validador de certificado personalizado.  
  
 Se o certificado X. 509 for usado para autenticar um cliente ou serviço, o Windows Communication Foundation (WCF), por padrão, usará o repositório de certificados do Windows e a API de criptografia para validar o certificado e garantir que ele seja confiável. Às vezes, a funcionalidade de validação de certificado interna não é suficiente e deve ser alterada. O WCF fornece uma maneira fácil de alterar a lógica de validação, permitindo que os usuários adicionem um validador de certificado personalizado. Se um validador de certificado personalizado for especificado, o WCF não usará a lógica de validação de certificado interna, mas dependerá do validador personalizado.  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="to-create-a-custom-certificate-validator"></a>Para criar um validador de certificado personalizado  
  
1. Defina uma nova classe derivada de <xref:System.IdentityModel.Selectors.X509CertificateValidator> .  
  
2. Implemente o <xref:System.IdentityModel.Selectors.X509CertificateValidator.Validate%2A> método abstract. O certificado que deve ser validado é passado como um argumento para o método. Se o certificado passado não for válido de acordo com a lógica de validação, esse método lançará um <xref:System.IdentityModel.Tokens.SecurityTokenValidationException> . Se o certificado for válido, o método retornará ao chamador.  
  
    > [!NOTE]
    > Para retornar erros de autenticação de volta para o cliente, gere um <xref:System.ServiceModel.FaultException> no método <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A>.  
  
 [!code-csharp[c_CustomCertificateValidator#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcertificatevalidator/cs/source.cs#2)]
 [!code-vb[c_CustomCertificateValidator#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcertificatevalidator/vb/source.vb#2)]  
  
#### <a name="to-specify-a-custom-certificate-validator-in-service-configuration"></a>Para especificar um validador de certificado personalizado na configuração de serviço  
  
1. Adicione um [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md) elemento e um [\<serviceBehaviors>](../../configure-apps/file-schema/wcf/servicebehaviors.md) ao [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md) elemento.  
  
2. Adicione um [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) e defina o `name` atributo como um valor apropriado.  
  
3. Adicione um [\<serviceCredentials>](../../configure-apps/file-schema/wcf/servicecredentials.md) ao `<behavior>` elemento.  
  
4. Adicione um `<clientCertificate>` elemento ao `<serviceCredentials>` elemento.  
  
5. Adicione um [\<authentication>](../../configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md) ao `<clientCertificate>` elemento.  
  
6. Defina o `customCertificateValidatorType` atributo para o tipo de validador. O exemplo a seguir define o atributo para o namespace e o nome do tipo.  
  
7. Defina o `certificateValidationMode` atributo como `Custom` .  
  
    ```xml  
    <configuration>  
     <system.serviceModel>  
      <behaviors>  
       <serviceBehaviors>  
        <behavior name="ServiceBehavior">  
         <serviceCredentials>  
          <clientCertificate>  
          <authentication certificateValidationMode="Custom" customCertificateValidatorType="Samples.MyValidator, service" />  
          </clientCertificate>  
         </serviceCredentials>  
        </behavior>  
       </serviceBehaviors>  
      </behaviors>  
    </system.serviceModel>  
    </configuration>  
    ```  
  
#### <a name="to-specify-a-custom-certificate-validator-using-configuration-on-the-client"></a>Para especificar um validador de certificado personalizado usando a configuração no cliente  
  
1. Adicione um [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md) elemento e um [\<serviceBehaviors>](../../configure-apps/file-schema/wcf/servicebehaviors.md) ao [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md) elemento.  
  
2. Adicione um [\<endpointBehaviors>](../../configure-apps/file-schema/wcf/endpointbehaviors.md) elemento.  
  
3. Adicione um elemento `<behavior>` e defina o atributo `name` para um valor apropriado.  
  
4. Adicione um [\<clientCredentials>](../../configure-apps/file-schema/wcf/clientcredentials.md) elemento.  
  
5. Adicione um [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md) .  
  
6. Adicione um [\<authentication>](../../configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md) conforme mostrado no exemplo a seguir.  
  
7. Defina o `customCertificateValidatorType` atributo para o tipo de validador.  
  
8. Defina o `certificateValidationMode` atributo como `Custom` . O exemplo a seguir define o atributo para o namespace e o nome do tipo.  
  
    ```xml  
    <configuration>  
     <system.serviceModel>  
      <behaviors>  
       <endpointBehaviors>  
        <behavior name="clientBehavior">  
         <clientCredentials>  
          <serviceCertificate>  
           <authentication certificateValidationMode="Custom"
                  customCertificateValidatorType=  
             "Samples.CustomX509CertificateValidator, client"/>  
          </serviceCertificate>  
         </clientCredentials>  
        </behavior>  
       </endpointBehaviors>  
      </behaviors>  
     </system.serviceModel>  
    </configuration>  
    ```  
  
#### <a name="to-specify-a-custom-certificate-validator-using-code-on-the-service"></a>Para especificar um validador de certificado personalizado usando código no serviço  
  
1. Especifique o validador de certificado personalizado na <xref:System.ServiceModel.Description.ServiceCredentials.ClientCertificate%2A> propriedade. Você pode acessar as credenciais de serviço usando a <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> propriedade.  
  
2. Defina a propriedade <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.CertificateValidationMode%2A> como <xref:System.ServiceModel.Security.X509CertificateValidationMode.Custom>.  
  
 [!code-csharp[c_CustomCertificateValidator#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcertificatevalidator/cs/source.cs#1)]
 [!code-vb[c_CustomCertificateValidator#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcertificatevalidator/vb/source.vb#1)]  
  
#### <a name="to-specify-a-custom-certificate-validator-using-code-on-the-client"></a>Para especificar um validador de certificado personalizado usando código no cliente  
  
1. Especifique o validador de certificado personalizado usando a <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CustomCertificateValidator%2A> propriedade. Você pode acessar as credenciais do cliente usando a <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> propriedade. (A classe de cliente gerada pela [ferramenta de utilitário de metadados ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) sempre deriva da <xref:System.ServiceModel.ClientBase%601> classe.)  
  
2. Defina a propriedade <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A> como <xref:System.ServiceModel.Security.X509CertificateValidationMode.Custom>.  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  

 O exemplo a seguir mostra uma implementação de um validador de certificado personalizado e seu uso no serviço.  
  
### <a name="code"></a>Código  

 [!code-csharp[c_CustomCertificateValidator#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcertificatevalidator/cs/source.cs#3)]
 [!code-vb[c_CustomCertificateValidator#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcertificatevalidator/vb/source.vb#3)]  
  
## <a name="see-also"></a>Confira também

- <xref:System.IdentityModel.Selectors.X509CertificateValidator>
