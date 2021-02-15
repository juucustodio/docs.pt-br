---
ms.openlocfilehash: 557d811e2eeaf926cb958471d214fc23c50a25f2
ms.sourcegitcommit: c04535ad05e374fb269fcfc6509217755fbc0d54
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "96584634"
---
- Em vez disso, use um serializador seguro e **não permita que um invasor especifique um tipo arbitrário para desserializar**. Para obter mais informações, consulte as [alternativas preferenciais](/dotnet/standard/serialization/binaryformatter-security-guide#preferred-alternatives).
- Torne a prova de adulteração dos dados serializados. Após a serialização, assine criptograficamente os dados serializados. Antes da desserialização, valide a assinatura criptográfica. Proteja a chave de criptografia de ser divulgada e design para rotações de chave.
- Essa opção torna o código vulnerável a ataques de negação de serviço e possíveis ataques de execução remota de código no futuro. Para obter mais informações, consulte o [Guia de segurança do BinaryFormatter](/dotnet/standard/serialization/binaryformatter-security-guide). Restringir tipos desserializados. Implemente um personalizado <xref:System.Runtime.Serialization.SerializationBinder?displayProperty=nameWithType> . Antes de desserializar, defina a `Binder` propriedade como uma instância de seu personalizado <xref:System.Runtime.Serialization.SerializationBinder> em todos os caminhos de código. No método substituído <xref:System.Runtime.Serialization.SerializationBinder.BindToType%2A> , se o tipo for inesperado, lance uma exceção para interromper a desserialização.
