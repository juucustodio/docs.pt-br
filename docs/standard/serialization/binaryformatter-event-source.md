---
title: Origem do evento BinaryFormatter
description: Saiba como usar a origem do evento BinaryFormatter para registrar quando a serialização ou desserialização estiver ocorrendo.
ms.date: 12/03/2020
ms.author: levib
author: GrabYourPitchforks
ms.openlocfilehash: 9ae2af77b6cfc270207fb0f2969ada8c2eca1153
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740413"
---
# <a name="binaryformatter-event-source"></a>Origem do evento BinaryFormatter

A partir do .NET 5,0, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> o inclui um interno <xref:System.Diagnostics.Tracing.EventSource> que fornece visibilidade sobre quando uma serialização ou desserialização de objeto está ocorrendo. Os aplicativos podem usar <xref:System.Diagnostics.Tracing.EventListener> tipos derivados para escutar essas notificações e fazê-las em log.

Essa funcionalidade não é um substituto para um <xref:System.Runtime.Serialization.SerializationBinder> ou um <xref:System.Runtime.Serialization.ISerializationSurrogate> e não pode ser usada para modificar os dados que estão sendo serializados ou desserializados. Em vez disso, esse sistema de eventos destina-se a fornecer informações sobre os tipos que estão sendo serializados ou desserializados. Ele também pode ser usado para detectar chamadas indesejadas na `BinaryFormatter` infraestrutura, como chamadas provenientes de código de biblioteca de terceiros.

## <a name="description-of-events"></a>Descrição de eventos

A `BinaryFormatter` origem do evento tem o nome conhecido `System.Runtime.Serialization.Formatters.Binary.BinaryFormatterEventSource` . Os ouvintes podem assinar 6 eventos.

### <a name="serializationstart-event-id--10"></a>Evento SerializationStart (ID = `10` )

Gerado quando foi <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType> chamado e iniciou o processo de serialização. Esse evento é emparelhado com o `SerializationEnd` evento. O `SerializationStart` evento pode ser chamado recursivamente se um objeto chamar `BinaryFormatter.Serialize` em sua própria rotina de serialização.

Esse evento não contém uma carga.

### <a name="serializationend-event-id--11"></a>Evento SerializationEnd (ID = `11` )

Gerado quando `BinaryFormatter.Serialize` concluiu seu trabalho. Cada ocorrência de `SerializationEnd` denota a conclusão do último evento não emparelhado `SerializationStart` .

Esse evento não contém uma carga.

### <a name="serializingobject-event-id--12"></a>Evento serializaobject (ID = `12` )

Gerado quando `BinaryFormatter.Serialize` está no processo de serialização de um tipo não primitivo. A `BinaryFormatter` infraestrutura faz casos especiais determinados tipos (como `string` e `int` ) e não gera esse evento quando esses tipos são encontrados. Esse evento é gerado para tipos definidos pelo usuário e outros tipos que `BinaryFormatter` não compreendem nativamente.

Esse evento pode ser gerado zero ou mais vezes entre `SerializationStart` `SerializationEnd` eventos e.

Esse evento contém uma carga com um argumento:

* `typeName` ( `string` ): O nome qualificado do assembly (consulte <xref:System.Type.AssemblyQualifiedName?displayProperty=nameWithType> ) do tipo que está sendo serializado.

### <a name="deserializationstart-event-id--20"></a>Evento DeserializationStart (ID = `20` )

Gerado quando foi <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType> chamado e iniciou o processo de desserialização. Esse evento é emparelhado com o `DeserializationEnd` evento. O `DeserializationStart` evento pode ser chamado recursivamente se um objeto chamar `BinaryFormatter.Deserialize` em sua própria rotina de desserialização.

Esse evento não contém uma carga.

### <a name="deserializationend-event-id--21"></a>Evento DeserializationEnd (ID = `21` )

Gerado quando `BinaryFormatter.Deserialize` concluiu seu trabalho. Cada ocorrência de `DeserializationEnd` denota a conclusão do último evento não emparelhado `DeserializationStart` .

Esse evento não contém uma carga.

### <a name="deserializingobject-event-id--22"></a>Evento deserializaobject (ID = `22` )

Gerado quando `BinaryFormatter.Deserialize` está no processo de desserializar um tipo não primitivo. A `BinaryFormatter` infraestrutura faz casos especiais determinados tipos (como `string` e `int` ) e não gera esse evento quando esses tipos são encontrados. Esse evento é gerado para tipos definidos pelo usuário e outros tipos que `BinaryFormatter` não compreendem nativamente.

Esse evento pode ser gerado zero ou mais vezes entre `DeserializationStart` `DeserializationEnd` eventos e.

Esse evento contém uma carga com um argumento.

* `typeName` ( `string` ): O nome qualificado do assembly (consulte <xref:System.Type.AssemblyQualifiedName?displayProperty=nameWithType> ) do tipo que está sendo desserializado.

### <a name="advanced-subscribing-to-a-subset-of-notifications"></a>\[Assinatura avançada de \] um subconjunto de notificações

Os ouvintes que desejam assinar apenas um subconjunto de notificações podem escolher quais palavras-chave habilitar.

* `Serialization` = `(EventKeywords)1`: Gera os `SerializationStart` `SerializationEnd` eventos, e `SerializingObject` .
* `Deserialization` = `(EventKeywords)2`: Gera os `DeserializationStart` `DeserializationEnd` eventos, e `DeserializingObject` .

Se nenhum filtro de palavra-chave for fornecido durante o `EventListener` registro, todos os eventos serão gerados.

Para obter mais informações, consulte <xref:System.Diagnostics.Tracing.EventKeywords?displayProperty=nameWithType>.

## <a name="sample-code"></a>Código de exemplo

O seguinte código:

- Cria um `EventListener` tipo derivado que grava em `System.Console` ,
- assina esse ouvinte para `BinaryFormatter` notificações produzidas,
- Serializa e desserializa um grafo de objeto simples usando `BinaryFormatter` , e
- analisa os eventos que foram gerados.

:::code language="csharp" source="snippets/binaryformatter-event-source/csharp/Program.cs":::

O código anterior produz uma saída semelhante ao exemplo a seguir:

```output
Event SerializationStart (id=10) received.
Event SerializingObject (id=12) received.
typeName = BinaryFormatterEventSample.Person, BinaryFormatterEventSample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null
Event SerializingObject (id=12) received.
typeName = BinaryFormatterEventSample.Book, BinaryFormatterEventSample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null
Event SerializationStop (id=11) received.
Event DeserializationStart (id=20) received.
Event DeserializingObject (id=22) received.
typeName = BinaryFormatterEventSample.Person, BinaryFormatterEventSample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null
Event DeserializingObject (id=22) received.
typeName = BinaryFormatterEventSample.Book, BinaryFormatterEventSample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null
Event DeserializationStop (id=21) received.
Rehydrated person Logan Edwards
Favorite book: A Tale of Two Cities by Charles Dickens, list price 10.25
```

Neste exemplo, os logs baseados em console `EventListener` que a serialização inicia, instâncias de `Person` e `Book` são serializados e, em seguida, a serialização é concluída. Da mesma forma, quando a desserialização é iniciada, as instâncias de `Person` e `Book` são desserializadas e a desserialização é concluída.

Em seguida, o aplicativo imprime os valores contidos em desserializados `Person` para demonstrar que o objeto fazia serialização e desserialização apropriada.

## <a name="see-also"></a>Confira também

Para obter mais informações sobre `EventListener` como usar para `EventSource` notificações baseadas em recebimento, consulte [a `EventListener` classe](xref:System.Diagnostics.Tracing.EventListener).
