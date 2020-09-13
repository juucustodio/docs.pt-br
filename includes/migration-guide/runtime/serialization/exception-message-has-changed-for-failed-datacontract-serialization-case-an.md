---
ms.openlocfilehash: 8d0404c728231f596500653d556e3be6fcc20c2c
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89496208"
---
### <a name="exception-message-has-changed-for-failed-datacontract-serialization-in-case-of-an-unknown-type"></a>A mensagem de exceção foi alterada para a falha na serialização DataContract no caso de um tipo desconhecido

#### <a name="details"></a>Detalhes

A partir do .NET Framework 4.6, a mensagem de exceção gerada se a serialização ou desserialização de <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> ou <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=fullName> falhar por causa de "tipos conhecidos" ausentes foi esclarecida.

#### <a name="suggestion"></a>Sugestão

Os aplicativos não devem depender de mensagens de exceção específicas. Se um aplicativo depender dessa mensagem, atualize-o para que ele espere a nova mensagem ou, preferencialmente, altere-o para depender somente do tipo de exceção.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Microsoft Edge|
|Versão|4.6|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor(System.Type)>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor(System.Type,System.Collections.Generic.IEnumerable{System.Type})>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor(System.Type,System.Runtime.Serialization.Json.DataContractJsonSerializerSettings)>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor(System.Type,System.String)>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor(System.Type,System.String,System.Collections.Generic.IEnumerable{System.Type})>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor(System.Type,System.Xml.XmlDictionaryString)>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor(System.Type,System.Xml.XmlDictionaryString,System.Collections.Generic.IEnumerable{System.Type})>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor(System.Type,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate,System.Boolean)>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor(System.Type,System.String,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate,System.Boolean)>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor(System.Type,System.Xml.XmlDictionaryString,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate,System.Boolean)>
- <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor(System.Type)>
- <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor(System.Type,System.Runtime.Serialization.DataContractSerializerSettings)>
- <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor(System.Type,System.Collections.Generic.IEnumerable{System.Type})>
- <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor(System.Type,System.String,System.String)>
- <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor(System.Type,System.String,System.String,System.Collections.Generic.IEnumerable{System.Type})>
- <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor(System.Type,System.Xml.XmlDictionaryString,System.Xml.XmlDictionaryString)>
- <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor(System.Type,System.Xml.XmlDictionaryString,System.Xml.XmlDictionaryString,System.Collections.Generic.IEnumerable{System.Type})>
- <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor(System.Type,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate)>
- <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor(System.Type,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate,System.Runtime.Serialization.DataContractResolver)>
- <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor(System.Type,System.String,System.String,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate)>
- <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor(System.Type,System.String,System.String,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate,System.Runtime.Serialization.DataContractResolver)>
- <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor(System.Type,System.Xml.XmlDictionaryString,System.Xml.XmlDictionaryString,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate)>
- <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor(System.Type,System.Xml.XmlDictionaryString,System.Xml.XmlDictionaryString,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate,System.Runtime.Serialization.DataContractResolver)>

<!--

#### Affected APIs

- `M:System.Runtime.Serialization.Json.DataContractJsonSerializer.#ctor(System.Type)`
- `M:System.Runtime.Serialization.Json.DataContractJsonSerializer.#ctor(System.Type,System.Collections.Generic.IEnumerable{System.Type})`
- `M:System.Runtime.Serialization.Json.DataContractJsonSerializer.#ctor(System.Type,System.Runtime.Serialization.Json.DataContractJsonSerializerSettings)`
- `M:System.Runtime.Serialization.Json.DataContractJsonSerializer.#ctor(System.Type,System.String)`
- `M:System.Runtime.Serialization.Json.DataContractJsonSerializer.#ctor(System.Type,System.String,System.Collections.Generic.IEnumerable{System.Type})`
- `M:System.Runtime.Serialization.Json.DataContractJsonSerializer.#ctor(System.Type,System.Xml.XmlDictionaryString)`
- `M:System.Runtime.Serialization.Json.DataContractJsonSerializer.#ctor(System.Type,System.Xml.XmlDictionaryString,System.Collections.Generic.IEnumerable{System.Type})`
- `M:System.Runtime.Serialization.Json.DataContractJsonSerializer.#ctor(System.Type,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate,System.Boolean)`
- `M:System.Runtime.Serialization.Json.DataContractJsonSerializer.#ctor(System.Type,System.String,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate,System.Boolean)`
- `M:System.Runtime.Serialization.Json.DataContractJsonSerializer.#ctor(System.Type,System.Xml.XmlDictionaryString,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate,System.Boolean)`
- `M:System.Runtime.Serialization.DataContractSerializer.#ctor(System.Type)`
- `M:System.Runtime.Serialization.DataContractSerializer.#ctor(System.Type,System.Runtime.Serialization.DataContractSerializerSettings)`
- `M:System.Runtime.Serialization.DataContractSerializer.#ctor(System.Type,System.Collections.Generic.IEnumerable{System.Type})`
- `M:System.Runtime.Serialization.DataContractSerializer.#ctor(System.Type,System.String,System.String)`
- `M:System.Runtime.Serialization.DataContractSerializer.#ctor(System.Type,System.String,System.String,System.Collections.Generic.IEnumerable{System.Type})`
- `M:System.Runtime.Serialization.DataContractSerializer.#ctor(System.Type,System.Xml.XmlDictionaryString,System.Xml.XmlDictionaryString)`
- `M:System.Runtime.Serialization.DataContractSerializer.#ctor(System.Type,System.Xml.XmlDictionaryString,System.Xml.XmlDictionaryString,System.Collections.Generic.IEnumerable{System.Type})`
- `M:System.Runtime.Serialization.DataContractSerializer.#ctor(System.Type,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate)`
- `M:System.Runtime.Serialization.DataContractSerializer.#ctor(System.Type,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate,System.Runtime.Serialization.DataContractResolver)`
- `M:System.Runtime.Serialization.DataContractSerializer.#ctor(System.Type,System.String,System.String,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate)`
- `M:System.Runtime.Serialization.DataContractSerializer.#ctor(System.Type,System.String,System.String,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate,System.Runtime.Serialization.DataContractResolver)`
- `M:System.Runtime.Serialization.DataContractSerializer.#ctor(System.Type,System.Xml.XmlDictionaryString,System.Xml.XmlDictionaryString,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate)`
- `M:System.Runtime.Serialization.DataContractSerializer.#ctor(System.Type,System.Xml.XmlDictionaryString,System.Xml.XmlDictionaryString,System.Collections.Generic.IEnumerable{System.Type},System.Int32,System.Boolean,System.Boolean,System.Runtime.Serialization.IDataContractSurrogate,System.Runtime.Serialization.DataContractResolver)`

-->
