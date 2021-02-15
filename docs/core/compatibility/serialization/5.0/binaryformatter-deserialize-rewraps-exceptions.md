---
title: 'Alteração significativa: BinaryFormatter. desserializar reencapsula algumas exceções'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que BinaryFormatter. desserializar reencapsula alguns objetos de exceção dentro de uma Serializaexception.
ms.date: 08/18/2020
ms.openlocfilehash: 90dc4cce6785fdb38644cca2a2e9aff65eb7a313
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760354"
---
# <a name="binaryformatterdeserialize-rewraps-some-exceptions-in-serializationexception"></a>BinaryFormatter. desserializate reencapsula algumas exceções na Serializaexception

O <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType> método agora reencapsula alguns objetos de exceção dentro de um <xref:System.Runtime.Serialization.SerializationException> antes de propagar a exceção de volta para o chamador.

## <a name="change-description"></a>Descrição das alterações

Anteriormente, o <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType> método permitia algumas exceções arbitrárias, como <xref:System.ArgumentNullException> , para propagar a pilha para seus chamadores.

No .NET 5,0 e posterior, o <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType> método captura de forma mais agressiva as exceções que ocorrem devido a operações de desserialização inválidas e as encapsula em um <xref:System.Runtime.Serialization.SerializationException> .

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Na maioria dos casos, você não precisa realizar nenhuma ação. No entanto, se seu site de chamada depende de uma determinada exceção sendo gerada, você pode desencapsular a exceção da externa <xref:System.Runtime.Serialization.SerializationException> , conforme mostrado no exemplo a seguir.

```csharp
Stream inputStream = GetInputStream();
var formatter = new BinaryFormatter();

try
{
    object deserialized = formatter.Deserialize(inputStream);
}
catch (MyException myEx)
{
    // Handle 'myEx' here in case it was thrown directly.
}
catch (SerializationException serEx) when (serEx.InnerException is MyException myEx)
{
    // Handle 'myEx' here in case it was wrapped in SerializationException.
}
```

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=fullName>

<!--

### Affected APIs

- `Overload:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize`

### Category

Serialization

-->
