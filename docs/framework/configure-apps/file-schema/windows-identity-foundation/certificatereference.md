---
description: 'Saiba mais sobre: <certificateReference>'
title: <certificateReference>
ms.date: 03/30/2017
ms.assetid: 2ac8bc14-e9f1-48fb-b662-f5991558fbe4
author: BrucePerlerMS
ms.openlocfilehash: 3404d44457849fb78ae88617d049a2199f2b5509
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99681780"
---
# \<certificateReference>

Especifica as configurações que são usadas para localizar e validar um certificado X. 509 em um repositório de certificados.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel.services>**](system-identitymodel-services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<federationConfiguration>**](federationconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceCertificate>**](servicecertificate.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<certificateReference>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<system.identityModel.services>  
  <federationConfiguration>  
    <serviceCertificate>  
      <certificateReference
        storeName="AddressBook||AuthRoot||CertificateAuthority||Disallowed||My||Root||TrustedPeople||TrustedPublisher"  
        storeLocation="CurrentUser||LocalMachine"  
        x509FindType="FindByThumbprint||FindBySubjectName||FindBySubjectDistinguishedName||FindByIssuerName||FindByIssuerDistinguishedName||FindBySerialNumber||FindByTimeValid||FindByTimeNotYetValid||FindByTimeExpired||FindByTemplateName||FindByApplicationPolicy||FindByCertificatePolicy||FindByExtension||FindByKeyUsage||FindBySubjectKeyIdentifier"  
        findValue=xs:String  
        isChainIncluded=xs:Boolean >  
      </certificateReference>  
    </serviceCertificate>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|storeName|O nome do repositório de certificados X.509. O padrão é "My". Opcional.|  
|storeLocation|Um <xref:System.Security.Cryptography.X509Certificates.StoreLocation> valor que especifica o local do repositório de certificados X. 509. O valor padrão é "LocalMachine". Opcional.|  
|x509FindType|Um <xref:System.Security.Cryptography.X509Certificates.X509FindType> valor que especifica o tipo de pesquisa que deve ser executada. O padrão é "FindBySubjectDistinguishedName". Opcional.|  
|findValue|O valor a ser pesquisado no repositório de certificados X.509. Opcional.|  
|isChainIncluded|Especifica se a validação deve ser executada usando a cadeia de certificados. O padrão é "true"; a validação é executada usando a cadeia de certificados. Opcional.|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<serviceCertificate>](servicecertificate.md)|Configura o certificado que é usado para criptografar e descriptografar tokens.|  
  
## <a name="remarks"></a>Comentários  

 O `<certificateReference>` elemento especifica as configurações que são usadas para localizar e validar um certificado X. 509 em um repositório de certificados. Quando é especificado como o elemento filho do `<serviceCertificate>` elemento, ele especifica as configurações de localização e verificação do certificado X. 509 que é usado para criptografar e descriptografar tokens. O `<certificateReference>` elemento é representado pela <xref:System.ServiceModel.Configuration.CertificateReferenceElement> classe.
