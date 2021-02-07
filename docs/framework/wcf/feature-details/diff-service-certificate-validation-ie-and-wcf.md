---
description: 'Saiba mais sobre: diferenças entre a validação do certificado de serviço feita pelo Internet Explorer e pelo WCF'
title: Diferenças entre validação de certificado de serviço pelo Internet Explorer e o WCF
ms.date: 03/30/2017
helpviewer_keywords:
- service certificate validation [WCF]
- certificates [WCF], service certificate validation
ms.assetid: 9dffcab2-70a9-40f0-99fd-d3a0b296028f
ms.openlocfilehash: 2d635aec0949ec4e65cd965089206bbf6d6815a6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99756351"
---
# <a name="differences-between-service-certificate-validation-done-by-internet-explorer-and-wcf"></a>Diferenças entre validação de certificado de serviço pelo Internet Explorer e o WCF

Devido à diferença entre o modo como o Internet Explorer e o Windows Communication Foundation (WCF) validam certificados de serviço quando o HTTPS é usado, é possível que o Internet Explorer não possa acessar a página de ajuda ou WSDL (Web Services Description Language) de um serviço, mesmo que um cliente WCF seja capaz de enviar mensagens para os pontos de extremidade de serviço com êxito. Isso ocorre porque o Internet Explorer verifica se o certificado de serviço tem os `ServerAuthentication` identificadores de objeto (OID) nos sinalizadores de uso avançado, enquanto o WCF não impõe essa restrição. Se o Internet Explorer não puder acessar a página de ajuda do serviço ou o WSDL para o serviço, use a [ferramenta de utilitário de metadados ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) para acessar os metadados do serviço.  
  
## <a name="see-also"></a>Consulte também

- [Diferentes validações de certificado entre segurança de SOAP, HTTPS, SSL através de TCP](cert-val-diff-https-ssl-over-tcp-and-soap.md)
- [Como: recuperar metadados e implementar um serviço em conformidade](how-to-retrieve-metadata-and-implement-a-compliant-service.md)
