---
description: 'Saiba mais sobre: ServiceCredentials'
title: ServiceCredentials
ms.date: 03/30/2017
ms.assetid: 9c780793-4785-46f7-add9-ac1ebeadb614
ms.openlocfilehash: bfd025a8f671a3c5aea537059cde0e751cfa9bb9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99715542"
---
# <a name="servicecredentials"></a>ServiceCredentials

ServiceCredentials  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ServiceCredentials : Behavior  
{  
  string ClientCertificate;  
  string IssuedTokenAuthentication;  
  string Peer;  
  string SecureConversationAuthentication;  
  string ServiceCertificate;  
  string UserNameAuthentication;  
  string WindowsAuthentication;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe ServiceCredentials não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe ServiceCredentials tem as seguintes propriedades:  
  
### <a name="clientcertificate"></a>ClientCertificate  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 As configurações de autenticação e provisionamento de certificado do cliente para este serviço.  
  
### <a name="issuedtokenauthentication"></a>IssuedTokenAuthentication  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 As configurações de autenticação de token emitidas atuais para este serviço.  
  
### <a name="peer"></a>Par  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 As configurações atuais de autenticação e provisionamento de credencial a serem usadas por pontos de extremidade de transporte pares.  
  
### <a name="secureconversationauthentication"></a>SecureConversationAuthentication  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 Especifica as configurações atuais de conversa segura.  
  
### <a name="servicecertificate"></a>ServiceCertificate  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O certificado associado a este serviço.  
  
### <a name="usernameauthentication"></a>UserNameAuthentication  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 As configurações de nome de usuário/senha para este serviço.  
  
### <a name="windowsauthentication"></a>WindowsAuthentication  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 As configurações de autenticação do Windows para este serviço.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Description.ServiceCredentials>
