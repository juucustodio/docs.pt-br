---
description: 'Saiba mais sobre: Noções básicas sobre o nível de proteção'
title: Noções básicas de nível de proteção
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, security
- ProtectionLevel property
ms.assetid: 0c034608-a1ac-4007-8287-b1382eaa8bf2
ms.openlocfilehash: 8c6e5bc97c02e9cec4841dac0d7cf8c8b59931e1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631704"
---
# <a name="understanding-protection-level"></a>Noções básicas de nível de proteção

A `ProtectionLevel` propriedade é encontrada em muitas classes diferentes, como as <xref:System.ServiceModel.ServiceContractAttribute> <xref:System.ServiceModel.OperationContractAttribute> classes e. A propriedade controla como uma parte (ou todo) de uma mensagem é protegida. Este tópico explica o recurso Windows Communication Foundation (WCF) e como ele funciona.

Para obter instruções sobre como definir o nível de proteção, consulte [como: definir a propriedade ProtectionLevel](how-to-set-the-protectionlevel-property.md).

> [!NOTE]
> Os níveis de proteção podem ser definidos somente no código, não na configuração.

## <a name="basics"></a>Informações básicas

Para entender o recurso de nível de proteção, as seguintes instruções básicas se aplicam:

- Existem três níveis básicos de proteção para qualquer parte de uma mensagem. A propriedade (onde quer que ela ocorra) é definida como um dos <xref:System.Net.Security.ProtectionLevel> valores de enumeração. Em ordem crescente de proteção, eles incluem:

  - `None`.

  - `Sign`. A parte protegida é assinada digitalmente. Isso garante a detecção de qualquer violação com a parte da mensagem protegida.

  - `EncryptAndSign`. A parte da mensagem é criptografada para garantir a confidencialidade antes de ser assinada.

- Você pode definir os requisitos de proteção somente para *dados de aplicativo* com esse recurso. Por exemplo, WS-Addressing cabeçalhos são dados de infraestrutura e, portanto, não são afetados pelo `ProtectionLevel` .

- Quando o modo de segurança é definido como `Transport` , toda a mensagem é protegida pelo mecanismo de transporte. Portanto, a definição de um nível de proteção separado para diferentes partes de uma mensagem não tem nenhum efeito.

- O `ProtectionLevel` é uma maneira para o desenvolvedor definir o *nível mínimo* com o qual uma associação deve ser compatível. Quando um serviço é implantado, a associação real especificada na configuração pode ou não dar suporte ao nível mínimo. Por exemplo, por padrão, a <xref:System.ServiceModel.BasicHttpBinding> classe não fornece segurança (embora possa ser habilitada). Portanto, usá-lo com um contrato que tenha uma configuração diferente de fará `None` com que uma exceção seja gerada.

- Se o serviço exigir que o mínimo `ProtectionLevel` de todas as mensagens seja `Sign` , um cliente (talvez criado por uma tecnologia não WCF) poderá criptografar e assinar todas as mensagens (que é mais do que o mínimo necessário). Nesse caso, o WCF não lançará uma exceção, pois o cliente fez mais do que o mínimo. No entanto, observe que os aplicativos WCF (serviços ou clientes) não protegerão uma parte de mensagem, se possível, mas estarão em conformidade com o nível mínimo. Observe também que, ao usar `Transport` como o modo de segurança, o transporte pode exceder a segurança do fluxo de mensagens, pois não é inerentemente possível proteger em um nível mais granular.

- Se você definir `ProtectionLevel` explicitamente como `Sign` ou `EncryptAndSign` , deverá usar uma associação com segurança habilitada ou uma exceção será gerada.

- Se você selecionar uma associação que habilite a segurança e não definir a `ProtectionLevel` propriedade em qualquer lugar do contrato, todos os dados do aplicativo serão criptografados e assinados.

- Se você selecionar uma associação que não tem segurança habilitada (por exemplo, a `BasicHttpBinding` classe tem segurança desabilitada por padrão) e o `ProtectionLevel` não estiver definido explicitamente, nenhum dos dados do aplicativo será protegido.

- Se você estiver usando uma associação que aplica segurança no nível de transporte, todos os dados do aplicativo serão protegidos de acordo com os recursos do transporte.

- Se você usar uma associação que aplica segurança no nível da mensagem, os dados do aplicativo serão protegidos de acordo com os níveis de proteção definidos no contrato. Se você não especificar um nível de proteção, todos os dados do aplicativo nas mensagens serão criptografados e assinados.

- O `ProtectionLevel` pode ser definido em níveis de escopo diferentes. Há uma hierarquia associada ao escopo, que é explicada na próxima seção.

## <a name="scoping"></a>Scoping

Definir o `ProtectionLevel` na API de nível superior define o nível para todos os níveis abaixo dele. Se o `ProtectionLevel` for definido como um valor diferente em um nível inferior, todas as APIs abaixo desse nível na hierarquia agora serão redefinidas para o novo nível (as APIs acima dela, no entanto, ainda serão afetadas pelo nível mais alto). A hierarquia é a seguinte: Os atributos no mesmo nível são os pares.

- <xref:System.ServiceModel.ServiceContractAttribute>

- <xref:System.ServiceModel.OperationContractAttribute>

- <xref:System.ServiceModel.FaultContractAttribute>

- <xref:System.ServiceModel.MessageContractAttribute>

- <xref:System.ServiceModel.MessageHeaderAttribute>

- <xref:System.ServiceModel.MessageBodyMemberAttribute>

## <a name="programming-protectionlevel"></a>Programando ProtectionLevel

Para programar o a `ProtectionLevel` qualquer momento na hierarquia, basta definir a propriedade como um valor apropriado ao aplicar o atributo. Para obter exemplos, consulte [como: definir a propriedade ProtectionLevel](how-to-set-the-protectionlevel-property.md).

> [!NOTE]
> Definir a propriedade em falhas e contratos de mensagem requer a compreensão de como esses recursos funcionam. Para obter mais informações, consulte [como: definir a propriedade ProtectionLevel](how-to-set-the-protectionlevel-property.md) e [usar contratos de mensagem](./feature-details/using-message-contracts.md).

## <a name="ws-addressing-dependency"></a>Dependência de WS-Addressing

Na maioria dos casos, usar a [ferramenta de utilitário de metadados ServiceModel (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md) para gerar um cliente garante que os contratos de cliente e serviço sejam idênticos. No entanto, os contratos aparentemente idênticos podem fazer com que o cliente gere uma exceção. Isso ocorre sempre que uma associação não dá suporte à especificação de WS-Addressing e vários níveis de proteção são especificados no contrato. Por exemplo, a <xref:System.ServiceModel.BasicHttpBinding> classe não oferece suporte à especificação ou se você criar uma associação personalizada que não ofereça suporte a WS-Addressing. O `ProtectionLevel` recurso depende da especificação de WS-Addressing para permitir diferentes níveis de proteção em um único contrato. Se a associação não oferecer suporte à especificação de WS-Addressing, todos os níveis serão definidos para o mesmo nível de proteção. O nível de proteção efetivo para todos os escopos no contrato será definido como o nível de proteção mais forte usado no contrato.

Isso pode causar um problema difícil de depurar à primeira vista. É possível criar um contrato de cliente (uma interface) que inclua métodos para mais de um serviço. Ou seja, a mesma interface é usada para criar um cliente que se comunica com vários serviços e a interface única contém métodos para todos os serviços. O desenvolvedor deve cuidar desse cenário raro para invocar apenas os métodos que são aplicáveis a cada serviço específico. Se a associação for a <xref:System.ServiceModel.BasicHttpBinding> classe, não haverá suporte para vários níveis de proteção. No entanto, um serviço que responde ao cliente pode responder a um cliente com um nível de proteção mais baixo do que o necessário. Nesse caso, o cliente gerará uma exceção porque espera um nível de proteção mais alto.

Um exemplo do código ilustra esse problema. O exemplo a seguir mostra um serviço e um contrato de cliente. Suponha que a associação seja o [\<basicHttpBinding>](../configure-apps/file-schema/wcf/basichttpbinding.md) elemento. Portanto, todas as operações em um contrato têm o mesmo nível de proteção. Esse nível de proteção uniforme é determinado como o nível máximo de proteção em todas as operações.

O contrato de serviço é:

[!code-csharp[c_ProtectionLevel#7](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#7)]
[!code-vb[c_ProtectionLevel#7](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#7)]

O código a seguir mostra a interface de contrato do cliente. Observe que ele inclui um `Tax` método que deve ser usado com um serviço diferente:

[!code-csharp[c_ProtectionLevel#8](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#8)]
[!code-vb[c_ProtectionLevel#8](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#8)]

Quando o cliente chama o `Price` método, ele gera uma exceção quando recebe uma resposta do serviço. Isso ocorre porque o cliente não especifica um `ProtectionLevel` no e, `ServiceContractAttribute` portanto, o cliente usa o padrão ( <xref:System.Net.Security.ProtectionLevel.EncryptAndSign> ) para todos os métodos, incluindo o `Price` método. No entanto, o serviço retorna o valor usando o <xref:System.Net.Security.ProtectionLevel.Sign> nível porque o contrato de serviço define um único método que tem seu nível de proteção definido como <xref:System.Net.Security.ProtectionLevel.Sign> . Nesse caso, o cliente gerará um erro ao validar a resposta do serviço.

## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- <xref:System.ServiceModel.FaultContractAttribute>
- <xref:System.ServiceModel.MessageContractAttribute>
- <xref:System.ServiceModel.MessageHeaderAttribute>
- <xref:System.ServiceModel.MessageBodyMemberAttribute>
- <xref:System.Net.Security.ProtectionLevel>
- [Serviços de segurança](securing-services.md)
- [Como: definir a propriedade ProtectionLevel](how-to-set-the-protectionlevel-property.md)
- [Especificando e lidando com falhas em contratos e serviços](specifying-and-handling-faults-in-contracts-and-services.md)
- [Utilizando contratos de mensagem](./feature-details/using-message-contracts.md)
