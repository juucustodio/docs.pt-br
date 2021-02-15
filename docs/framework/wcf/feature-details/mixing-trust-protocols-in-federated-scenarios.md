---
description: 'Saiba mais sobre: misturar protocolos de confiança em cenários federados'
title: Misturando protocolos confiáveis em cenários federados
ms.date: 03/30/2017
ms.assetid: d7b5fee9-2246-4b09-b8d7-9e63cb817279
ms.openlocfilehash: f882b3728ed791f611a9f71f32840e68d8e17a1d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99733717"
---
# <a name="mixing-trust-protocols-in-federated-scenarios"></a>Misturando protocolos confiáveis em cenários federados

Pode haver cenários em que os clientes federados se comunicam com um serviço e um serviço de token de segurança (STS) que não têm a mesma versão de confiança. O serviço WSDL pode conter uma `RequestSecurityTokenTemplate` asserção com WS-Trust elementos que são de versões diferentes do STS. Nesses casos, um cliente Windows Communication Foundation (WCF) converte os elementos de WS-Trust recebidos do `RequestSecurityTokenTemplate` para corresponder à versão de confiança do STS. O WCF lida com versões de confiança incompatíveis apenas para associações padrão. Todos os parâmetros de algoritmo padrão que são reconhecidos pelo WCF fazem parte da associação padrão. Este tópico descreve o comportamento do WCF com várias configurações de confiança entre o serviço e o STS.  
  
## <a name="rp-feb-2005-and-sts-feb-2005"></a>RP fev 2005 e STS fevereiro de 2005  

 O WSDL para a parte confiável (RP) contém os seguintes elementos na `RequestSecurityTokenTemplate` seção:  
  
- `CanonicalizationAlgorithm`  
  
- `EncryptionAlgorithm`  
  
- `EncryptWith`  
  
- `SignWith`  
  
- `KeySize`  
  
- `KeyType`  
  
 O arquivo de configuração do cliente contém uma lista de parâmetros.  
  
 O WCF não pode diferenciar os parâmetros de cliente e de serviço; Ele adiciona todos os parâmetros e os envia no `RequestSecurityTokenTemplate` (RST).  
  
## <a name="rp-trust-13-and-sts-trust-13"></a>RP Trust 1,3 e o STS Trust 1,3  

 O WSDL para RP contém os seguintes elementos na `RequestSecurityTokenTemplate` seção:  
  
- `CanonicalizationAlgorithm`  
  
- `EncryptionAlgorithm`  
  
- `EncryptWith`  
  
- `SignWith`  
  
- `KeySize`  
  
- `KeyType`  
  
- `KeyWrapAlgorithm`  
  
 O arquivo de configuração do cliente contém um `secondaryParameters` elemento que encapsula os parâmetros especificados pela RP.  
  
 O WCF remove `EncryptionAlgorithm` os `CanonicalizationAlgorithm` `KeyWrapAlgorithm` elementos e do elemento de nível superior sob o RST, se eles estiverem presentes dentro do `SecondaryParameters` elemento. O WCF anexa o `SecondaryParameters` elemento ao RST de saída sem modificações.  
  
## <a name="rp-trust-feb-2005-and-sts-trust-13"></a>RP confiável fev 2005 e confiança STS 1,3  

 O WSDL para RP contém os seguintes elementos na `RequestSecurityTokenTemplate` seção:  
  
- `CanonicalizationAlgorithm`  
  
- `EncryptionAlgorithm`  
  
- `EncryptWith`  
  
- `SignWith`  
  
- `KeySize`  
  
- `KeyType`  
  
 O arquivo de configuração do cliente contém uma lista de parâmetros.  
  
 No arquivo de configuração do cliente, o WCF não pode diferenciar os parâmetros do serviço e do cliente. Portanto, o WCF converte todos os parâmetros em um namespace da versão de confiança 1,3.  
  
 O WCF manipula `KeyType` os `KeySize` elementos, e da `TokenType` seguinte maneira:  
  
- Baixe o WSDL, crie a associação e atribua `KeyType` , `KeySize` e `TokenType` dos parâmetros de RP. O arquivo de configuração do cliente é gerado.  
  
- O cliente agora pode alterar qualquer parâmetro no arquivo de configuração.  
  
- Durante o tempo de execução, o WCF copia todos os parâmetros especificados na `AdditionalTokenParameters` seção do arquivo de configuração do cliente `KeyType` , exceto, `KeySize` e `TokenType` , porque esses parâmetros são contabilizados durante a geração do arquivo de configuração.  
  
## <a name="rp-trust-13-and-sts-trust-feb-2005"></a>RP Trust 1,3 e a confiança STS de fevereiro de 2005  

 O WSDL para RP contém os seguintes elementos na `RequestSecurityTokenTemplate` seção:  
  
- `CanonicalizationAlgorithm`  
  
- `EncryptionAlgorithm`  
  
- `EncryptWith`  
  
- `SignWith`  
  
- `KeySize`  
  
- `KeyType`  
  
- `KeyWrapAlgorithm`  
  
 O arquivo de configuração do cliente contém um `secondaryParamters` elemento que encapsula os parâmetros especificados pela RP.  
  
 O WCF copia todos os parâmetros especificados na `SecondaryParameters` seção para o elemento RST de nível superior, mas não os converte para o namespace 2005 WS-Trust.
