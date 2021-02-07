---
description: 'Saiba mais sobre: como usar vários tokens de segurança do mesmo tipo'
title: 'Como: usar vários tokens de segurança do mesmo tipo'
ms.date: 03/30/2017
ms.assetid: cf179f48-4ed4-4caa-86a5-ef8eecc231cd
ms.openlocfilehash: 0cbf831c82fdc2aee5a09237c586286a5776d234
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99734250"
---
# <a name="how-to-use-multiple-security-tokens-of-the-same-type"></a>Como: usar vários tokens de segurança do mesmo tipo

- No .NET Framework 3,0, uma mensagem de cliente continha apenas um token de qualquer tipo determinado. Agora, as mensagens do cliente podem conter vários tokens de um tipo. Este tópico mostra como incluir vários tokens do mesmo tipo em uma mensagem do cliente.  
  
- Observe que você não pode configurar um serviço dessa forma: um serviço pode conter apenas um token de suporte.  
  
### <a name="to-use-multiple-security-tokens-of-the-same-type"></a>Para usar vários tokens de segurança do mesmo tipo  
  
1. Crie uma coleção de elementos de associação vazia a ser populada.  
  
     [!code-csharp[C_CustomBinding#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#9)]  
  
2. Crie um <xref:System.ServiceModel.Channels.SecurityBindingElement> chamando <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateMutualCertificateBindingElement%2A> .  
  
     [!code-csharp[C_CustomBinding#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#10)]  
  
3. Crie uma <xref:System.ServiceModel.Security.Tokens.SupportingTokenParameters> coleção.  
  
     [!code-csharp[C_CustomBinding#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#11)]  
  
4. Adicione tokens SAML à coleção.  
  
     [!code-csharp[C_CustomBinding#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#12)]  
  
5. Adicione a coleção ao <xref:System.ServiceModel.Channels.SecurityBindingElement> .  
  
     [!code-csharp[C_CustomBinding#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#13)]  
  
6. Adicione elementos de associação à coleção de elementos de associação.  
  
     [!code-csharp[C_CustomBinding#14](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#14)]  
  
7. Retorna uma nova associação personalizada criada a partir da coleção de elementos de associação.  
  
     [!code-csharp[C_CustomBinding#15](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#15)]  
  
## <a name="example"></a>Exemplo  

 A seguir está o método inteiro descrito pelo procedimento anterior.  
  
 [!code-csharp[C_CustomBinding#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#7)]  
