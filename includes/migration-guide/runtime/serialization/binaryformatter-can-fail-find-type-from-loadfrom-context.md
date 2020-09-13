---
ms.openlocfilehash: ccba3cf98a1ca9e199d9a48f00e254bf34b93f72
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89496119"
---
### <a name="binaryformatter-can-fail-to-find-type-from-loadfrom-context"></a>BinaryFormatter pode não conseguir localizar o tipo do contexto LoadFrom

#### <a name="details"></a>Detalhes

A partir do .NET Framework 4.5, várias alterações de <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> podem causar diferenças na desserialização ao usar <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=fullName> para desserializar tipos que foram carregados no contexto LoadFrom. Essas alterações se devem a novas maneiras como <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> agora carrega um tipo, o que causa um comportamento diferente quando um <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=fullName> tenta desserializar esse tipo posteriormente. O associador de serialização padrão não pesquisa automaticamente o contexto LoadFrom, embora isso possa ter funcionado em algumas circunstâncias com base no comportamento antigo do XmlSerializer. Devido às alterações, quando um tipo está sendo carregado de um assembly carregado em um contexto diferente, um <xref:System.IO.FileNotFoundException?displayProperty=fullName> pode ser acionado.

#### <a name="suggestion"></a>Sugestão

Se essa exceção for observada, a propriedade <code>Binder</code> do <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=fullName> poderá ser definida como um associador personalizado que encontrará o tipo correto.<pre><code class="lang-csharp">var formatter = new BinaryFormatter { Binder = new TypeFinderBinder() }&#13;&#10;</code></pre>E, em seguida, o associador personalizado:<pre><code class="lang-csharp">public class TypeFinderBinder : SerializationBinder&#13;&#10;{&#13;&#10;private static readonly string s_assemblyName = Assembly.GetExecutingAssembly().FullName;&#13;&#10;&#13;&#10;public override Type BindToType(string assemblyName, string typeName)&#13;&#10;{&#13;&#10;return Type.GetType(String.Format(CultureInfo.InvariantCulture, &quot;{0}, {1}&quot;, typeName, s_assemblyName));&#13;&#10;}&#13;&#10;}&#13;&#10;</code></pre>

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Microsoft Edge|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize(System.IO.Stream,System.Runtime.Remoting.Messaging.HeaderHandler)?displayProperty=nameWithType>

<!--

#### Affected APIs

- `T:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter`
- `M:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize(System.IO.Stream)`
- `M:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize(System.IO.Stream,System.Runtime.Remoting.Messaging.HeaderHandler)`

-->
