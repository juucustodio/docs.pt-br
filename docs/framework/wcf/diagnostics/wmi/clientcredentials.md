---
description: 'Saiba mais sobre: ClientCredentials'
title: ClientCredentials
ms.date: 03/30/2017
ms.assetid: 41dffd6b-8f14-4fed-aefb-2a1bb168efb3
ms.openlocfilehash: 7b0b5a05e5b61de717567de664079f2ed1e20f6b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99757654"
---
# <a name="clientcredentials"></a>ClientCredentials

ClientCredentials  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class ClientCredentials : Behavior  
{  
  string ClientCertificate;  
  string HttpDigest;  
  string IssuedToken;  
  string Peer;  
  string ServiceCertificate;  
  boolean SupportInteractive;  
  string UserName;  
  string Windows;  
};  
```  
  
## <a name="methods"></a>Métodos  

 A classe ClientCredentials não define nenhum método.  
  
## <a name="properties"></a>Propriedades  

 A classe ClientCredentials tem as seguintes propriedades:  
  
### <a name="clientcertificate"></a>ClientCertificate  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O certificado X. 509 que o cliente usa para se autenticar no serviço.  
  
### <a name="httpdigest"></a>HttpDigest  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 A credencial de Resumo de http atual.  
  
### <a name="issuedtoken"></a>IssuedToken  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O endereço do ponto de extremidade e a associação usados para contatar o serviço de token de segurança local.  
  
### <a name="peer"></a>Par  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 As credenciais que o nó par usa para se autenticar em outros nós na malha.  
  
### <a name="servicecertificate"></a>ServiceCertificate  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O certificado X. 509 do serviço.  
  
### <a name="supportinteractive"></a>SupportInteractive  

 Tipo de dados: booliano  
  
 Tipo de acesso: Somente leitura  
  
 Um valor booliano que especifica se a credencial dá suporte à negociação interativa.  
  
### <a name="username"></a>UserName  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 O nome de usuário e a senha que o cliente usa para se autenticar no serviço.  
  
### <a name="windows"></a>Windows  

 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: Somente leitura  
  
 As credenciais do Windows que o cliente usa para se autenticar no serviço.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em ServiceModel. mof.|  
|---------|-----------------------------------|  
|Namespace|Definido em root\ServiceModel|  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Description.ClientCredentials>
