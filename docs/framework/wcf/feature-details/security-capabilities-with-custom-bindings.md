---
description: 'Saiba mais sobre: recursos de segurança com associações personalizadas'
title: Recursos de segurança com associações personalizadas
ms.date: 03/30/2017
ms.assetid: a2425679-484a-4e6c-9c98-7da7304f1516
ms.openlocfilehash: 0d4298bcb0b22d607c4abb15d879e3b093394bad
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99779836"
---
# <a name="security-capabilities-with-custom-bindings"></a>Recursos de segurança com associações personalizadas

Você pode executar as tarefas de segurança mais comuns usando uma das associações fornecidas pelo sistema. No entanto, se você precisar de mais controle, poderá criar uma associação personalizada com uma <xref:System.ServiceModel.Channels.SecurityBindingElement> , conforme explicado nestes tópicos. Para obter mais informações sobre associações personalizadas, consulte [associações personalizadas](../extending/custom-bindings.md).  
  
## <a name="in-this-section"></a>Nesta seção  

 [SecurityBindingElement Authentication Modes](securitybindingelement-authentication-modes.md)  
 Descreve os modos de autenticação que são possíveis com uma associação personalizada.  
  
 [Como: criar uma associação personalizada utilizando o SecurityBindingElement](how-to-create-a-custom-binding-using-the-securitybindingelement.md)  
 Descreve as etapas básicas para criar uma associação personalizada com um elemento de segurança.  
  
 [Como: criar um SecurityBindingElement para um modo de autenticação especificado](how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)  
 Descreve como criar um elemento de segurança para um modo de autenticação especificado.  
  
 [Como: desabilitar sessões seguras em uma WSFederationHttpBinding](how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)  
 Descreve como desabilitar sessões seguras ao criar um serviço de Federação.  
  
 [Como: habilitar a detecção de reprodução de mensagem](how-to-enable-message-replay-detection.md)  
 Descreve como determinar quando ocorre um ataque de reprodução.  
  
 [Como: criar uma credencial de suporte](how-to-create-a-supporting-credential.md)  
 Descreve como fornecer uma credencial de suporte a um serviço, se o serviço exigir.  
  
 [Como: definir uma confirmação de assinatura](how-to-set-up-a-signature-confirmation.md)  
 Descreve as etapas para confirmar as assinaturas ao assinar digitalmente as mensagens.  
  
 [Como: definir a distorção máxima do relógio](how-to-set-a-max-clock-skew.md)  
 Descreve como definir a diferença de tempo máxima permitida entre um serviço e um cliente.  
  
 [Como: desabilitar criptografia de assinaturas digitais](how-to-disable-encryption-of-digital-signatures.md)  
 Descreve como desabilitar a criptografia de assinaturas digitais pode ter um benefício de desempenho.  
  
## <a name="reference"></a>Referência  

 <xref:System.ServiceModel.Channels.SecurityBindingElement>  
  
 [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md)  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Noções básicas de nível de proteção](../understanding-protection-level.md)  
  
 [Protegendo serviços e clientes](securing-services-and-clients.md)  
  
## <a name="see-also"></a>Consulte também

- [Associações e segurança](bindings-and-security.md)
- [Visão geral de segurança](security-overview.md)
- [Associações fornecidas pelo sistema](../system-provided-bindings.md)
