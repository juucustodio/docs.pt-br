---
description: 'Saiba mais sobre: como configurar uma confirmação de assinatura'
title: 'Como: definir uma confirmação de assinatura'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- signature confirmation
- WCF, security
ms.assetid: 2424c137-c7c2-4aa9-8d5d-a066e12fefda
ms.openlocfilehash: 158ec2a5f74038f5c1ca1af847f57457a8881974
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99643183"
---
# <a name="how-to-set-up-a-signature-confirmation"></a>Como: definir uma confirmação de assinatura

A *confirmação de assinatura* é um mecanismo para um iniciador de mensagem garantir que uma resposta recebida tenha sido gerada em resposta à mensagem original do remetente. A confirmação de assinatura é definida na especificação WS-Security 1,1. Se um ponto de extremidade der suporte a WS-Security 1,0, você não poderá usar a confirmação de assinatura.

Os procedimentos a seguir especificam como habilitar a confirmação de assinatura usando um <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> . Você pode usar o mesmo procedimento com um <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> . O procedimento se baseia nas etapas básicas encontradas em [como: criar uma associação personalizada usando o SecurityBindingElement](how-to-create-a-custom-binding-using-the-securitybindingelement.md).

### <a name="to-enable-signature-confirmation-in-code"></a>Para habilitar a confirmação de assinatura no código

1. Criar uma instância da classe <xref:System.ServiceModel.Channels.BindingElementCollection>.

2. Crie uma instância da  <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> classe.

3. Defina o <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.RequireSignatureConfirmation%2A> para `true`.

4. Adicione o elemento Security à coleção Binding.

5. Crie uma associação personalizada, conforme especificado em [como: criar uma associação personalizada usando o SecurityBindingElement](how-to-create-a-custom-binding-using-the-securitybindingelement.md).

### <a name="to-enable-signature-confirmation-in-configuration"></a>Para habilitar a confirmação de assinatura na configuração

1. Adicione um `<customBinding>` elemento à `<bindings>` seção do arquivo de configuração.

2. Adicione um `<binding>` elemento e defina o atributo Name para um valor apropriado.

3. Adicione um elemento Encoding apropriado. O exemplo a seguir adiciona um `<TextMessageEncoding>` elemento.

4. Adicione um `<security>` elemento filho e defina o `requireSignatureConfirmation` atributo como `true` .

5. Opcional. Para habilitar a confirmação de assinatura durante a inicialização, adicione um [\<secureConversationBootstrap>](../../configure-apps/file-schema/wcf/secureconversationbootstrap.md) elemento filho e defina o `requireSignatureConfirmation` atributo como `true` .

6. Adicione um elemento de transporte apropriado. O exemplo a seguir adiciona um [\<httpTransport>](../../configure-apps/file-schema/wcf/httptransport.md) :

    ```xml
    <bindings>
      <customBinding>
        <binding name="SignatureConfirmationBinding">
          <security requireSignatureConfirmation="true">
            <secureConversationBootstrap requireSignatureConfirmation="true" />
              </security>
           <textMessageEncoding />
             <httpTransport />
        </binding>
      </customBinding>
    </bindings>
    ```

## <a name="example"></a>Exemplo

O código a seguir cria uma instância do <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> e define a <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.RequireSignatureConfirmation%2A> propriedade como `true` . Observe que este exemplo não usa o `<secureConversationBootstrap>` elemento mostrado no exemplo anterior. Este exemplo demonstra a confirmação de assinatura ao usar um token do Windows (protocolo Kerberos). Nesse caso, a assinatura do cliente é retornada em todas as respostas do serviço e é confirmada pelo cliente.

[!code-csharp[c_SignatureConfirmation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_signatureconfirmation/cs/source.cs#1)]
[!code-vb[c_SignatureConfirmation#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_signatureconfirmation/vb/source.vb#1)]

## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>
- <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>
- <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateMutualCertificateBindingElement%2A>
- [Como: criar uma associação personalizada utilizando o SecurityBindingElement](how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [Como: criar um SecurityBindingElement para um modo de autenticação especificado](how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)
