---
description: 'Saiba mais sobre: mapeamento entre JSON e XML'
title: Mapeamento entre JSON e XML
ms.date: 03/30/2017
ms.assetid: 22ee1f52-c708-4024-bbf0-572e0dae64af
ms.openlocfilehash: 1d9652d1683446da9946987a31a92906d5e38e55
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99793669"
---
# <a name="mapping-between-json-and-xml"></a>Mapeamento entre JSON e XML

Os leitores e gravadores produzidos pelo <xref:System.Runtime.Serialization.Json.JsonReaderWriterFactory> fornecem um conteúdo de API XML sobre JavaScript Object Notation (JSON). O JSON codifica dados usando um subconjunto dos literais de objeto do JavaScript. Os leitores e gravadores produzidos por essa fábrica também são usados quando o conteúdo JSON está sendo enviado ou recebido por aplicativos Windows Communication Foundation (WCF) usando o <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement> ou o <xref:System.ServiceModel.WebHttpBinding> .

Quando inicializado com conteúdo JSON, o leitor JSON se comporta da mesma maneira que um leitor XML textual faz sobre uma instância do XML. O gravador JSON, quando dada uma sequência de chamadas que em um leitor XML textual, produz uma determinada instância XML, grava o conteúdo JSON. O mapeamento entre essa instância do XML e o conteúdo JSON é descrito neste tópico para uso em cenários avançados.

Internamente, o JSON é representado como um XML infoset quando processado pelo WCF. Normalmente, você não precisa se preocupar com essa representação interna, pois o mapeamento é apenas um lógico: JSON normalmente não é fisicamente convertido em XML na memória ou convertido em JSON de XML. O mapeamento significa que as APIs XML são usadas para acessar o conteúdo JSON.

Quando o WCF usa JSON, o cenário usual é que o <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> é conectado automaticamente pelo <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> comportamento ou pelo <xref:System.ServiceModel.Description.WebHttpBehavior> comportamento quando apropriado. O <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> compreende o mapeamento entre JSON e o XML infoset e atua como se ele estiver lidando diretamente com o JSON. (É possível usar o <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> com qualquer leitor ou gravador XML, sabendo que o XML está em conformidade com o mapeamento a seguir.)

Em cenários avançados, pode ser necessário acessar diretamente o mapeamento a seguir. Esses cenários ocorrem quando você deseja serializar e desserializar JSON de maneiras personalizadas, sem depender do <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> ou ao lidar com o <xref:System.ServiceModel.Channels.Message> tipo diretamente para mensagens que contêm JSON. O mapeamento JSON-XML também é usado para o log de mensagens. Ao usar o recurso de log de mensagens no WCF, as mensagens JSON são registradas como XML de acordo com o mapeamento descrito na próxima seção.

Para esclarecer o conceito de mapeamento, o exemplo a seguir é de um documento JSON.

```json
{"product":"pencil","price":12}
```

Para ler este documento JSON usando um dos leitores mencionados anteriormente, use a mesma sequência de <xref:System.Xml.XmlDictionaryReader> chamadas que você usaria para ler o documento XML a seguir.

```xml
<root type="object">
    <product type="string">pencil</product>
    <price type="number">12</price>
</root>
```

Além disso, se a mensagem JSON no exemplo for recebida pelo WCF e registrada, você verá o fragmento XML no log anterior.

## <a name="mapping-between-json-and-the-xml-infoset"></a>Mapeamento entre JSON e o XML infoset

Formalmente, o mapeamento está entre JSON, conforme descrito em [RFC 4627](https://www.ietf.org/rfc/rfc4627.txt) (exceto com determinadas restrições relaxadas e determinadas outras restrições) e o XML Infoset (e não texto XML), conforme descrito em [conjunto de informações XML](https://www.w3.org/TR/2004/REC-xml-infoset-20040204/). Consulte este tópico para obter as definições de *itens de informações* e campos em [colchetes].

Um documento JSON em branco é mapeado para um documento XML em branco e um documento XML em branco é mapeado para um documento JSON em branco. No mapeamento de XML para JSON, o espaço em branco precedente e o espaço em branco à direita após o documento não são permitidos.

O mapeamento é definido entre um item de informações de documento (DII) ou um item de informações de elemento (EII) e JSON. O EII, ou a propriedade [Document Element] do DII, é referido como o elemento JSON raiz. Observe que os fragmentos de documento (XML com vários elementos raiz) não têm suporte neste mapeamento.

Exemplo: o seguinte documento:

```xml
<?xml version="1.0"?>
<root type="number">42</root>
```

E o seguinte elemento:

```xml
<root type="number">42</root>
```

Ambos têm um mapeamento para JSON. O `root` elemento <> é o elemento JSON raiz em ambos os casos.

Além disso, no caso de um DII, o seguinte deve ser considerado:

- Alguns itens na lista [filhos] não devem estar presentes. Não confie nesse fato ao ler XML mapeado do JSON.

- A lista [Children] não contém itens de informações de comentário.

- A lista [Children] não contém nenhum item de informações de DTD.

- A lista [Children] não contém itens de informação de informações pessoais (PI) (a `<?xml…>` declaração não é considerada um item de informações de PI)

- O conjunto de [notações] está vazio.

- O conjunto [entidades não analisadas] está vazio.

Exemplo: o documento a seguir não tem mapeamento para JSON porque [Children] contém um PI e um comentário.

```xml
<?xml version="1.0"?>
<!--comment--><?pi?>
<root type="number">42</root>
```

O EII para o elemento JSON raiz tem as seguintes características:

- [nome local] tem o valor "root".

- [nome do namespace] não tem valor.

- [prefix] não tem valor.

- [Children] pode conter EIIs (que representam elementos internos conforme descrito mais adiante) ou CIIs (itens de informações de caractere, conforme descrito mais adiante) ou nenhum deles, mas não ambos.

- [Attributes] pode conter os seguintes itens de informação de atributo opcionais (AIIs)

- O atributo de tipo JSON ("Type"), conforme descrito mais adiante. Esse atributo é usado para preservar o tipo JSON (cadeia de caracteres, número, booliano, objeto, matriz ou NULL) no XML mapeado.

- O atributo de nome do contrato de dados (" \_ \_ tipo"), conforme descrito mais adiante. Esse atributo só poderá estar presente se o atributo de tipo JSON também estiver presente e seu [valor normalizado] for "Object". Esse atributo é usado pelo `DataContractJsonSerializer` para preservar informações de tipo de contrato de dados – por exemplo, em casos polimórficos em que um tipo derivado é serializado e onde um tipo base é esperado. Se você não estiver trabalhando com o `DataContractJsonSerializer` , na maioria dos casos, esse atributo será ignorado.

- [namespaces no escopo] contém a associação de "XML" a `http://www.w3.org/XML/1998/namespace` , conforme exigido pela especificação infoset.

- [Children], [Attributes] e [namespaces no escopo] não devem ter nenhum item além do especificado anteriormente e [atributos de namespace] não devem ter nenhum membro, mas não dependem desses fatos ao ler XML mapeado de JSON.

Exemplo: o documento a seguir não tem mapeamento para JSON porque [atributos de namespace] não está vazio.

```xml
<?xml version="1.0"?>
<root xmlns:a="myattributevalue">42</root>
```

O todos para o atributo de tipo JSON tem as seguintes características:

- [nome do namespace] não tem valor.
- [prefix] não tem valor.
- [nome local] é "tipo".
- [valor normalizado] é um dos valores de tipo possíveis descritos na seção a seguir.
- [especificado] é `true` .
- [tipo de atributo] não tem valor.
- [References] não tem valor.

O todos para o atributo de nome de contrato de dados tem as seguintes características:

- [nome do namespace] não tem valor.
- [prefix] não tem valor.
- [nome local] é " \_ \_ tipo" (dois sublinhados e, em seguida, "tipo").
- [valor normalizado] é qualquer cadeia de caracteres Unicode válida – o mapeamento dessa cadeia de caracteres para JSON é descrito na seção a seguir.
- [especificado] é `true` .
- [tipo de atributo] não tem valor.
- [References] não tem valor.

Os elementos internos contidos no elemento JSON raiz ou outros elementos internos têm as seguintes características:

- [nome local] pode ter qualquer valor, conforme descrito mais.
- [nome do namespace], [prefixo], [filhos], [atributos], [atributos de namespace] e [namespaces no escopo] estão sujeitos às mesmas regras que o elemento JSON raiz.

No elemento JSON raiz e nos elementos internos, o atributo de tipo JSON define o mapeamento para JSON e o possível [Children] e sua interpretação. O [valor normalizado] do atributo diferencia maiúsculas de minúsculas e deve estar em minúsculas e não pode conter espaço em branco.

|[valor normalizado] do todos do atributo do tipo JSON|Permitido [Children] do EII correspondente|Mapeando para JSON|
|---------------------------------------------------------|---------------------------------------------------|---------------------|
|`string` (ou ausência do tipo JSON todos)<br /><br /> R `string` e a ausência do tipo JSON todos são as mesmas torna `string` o padrão.<br /><br /> Portanto, `<root> string1</root>` o mapeia para o JSON `string` "seqüência1".|0 ou mais CIIs|Um JSON `string` (JSON RFC, seção 2,5). Cada `char` um é um caractere que corresponde ao [código de caractere] da CII. Se não houver nenhum CIIs, ele será mapeado para um JSON vazio `string` .<br /><br /> Exemplo: o seguinte elemento é mapeado para um fragmento JSON:<br /><br /> `<root type="string">42</root>`<br /><br /> O fragmento JSON é "42".<br /><br /> No mapeamento de XML para JSON, os caracteres que devem ser mapeados de escape para caracteres de escape, todos os outros mapeam para caracteres que não são de escape. O caractere "/" é especial – ele é escapado mesmo que não precise ser (escrito como " \\ /").<br /><br /> Exemplo: o elemento a seguir mapeia para um fragmento JSON.<br /><br /> `<root type="string">the "da/ta"</root>`<br /><br /> O fragmento JSON é "o \\ " da \\ /ta \\ "".<br /><br /> No mapeamento de JSON para XML, qualquer caractere de escape e caracteres que não são mapeados corretamente para o [código de caractere] correspondente.<br /><br /> Exemplo: o fragmento JSON "\u0041BC", é mapeado para o elemento XML a seguir.<br /><br /> `<root type="string">ABC</root>`<br /><br /> A cadeia de caracteres pode estar entre espaços em branco (' WS ' na seção 2 da RFC JSON) que não é mapeada para XML.<br /><br /> Exemplo: o fragmento JSON "ABC", (há espaços antes da primeira aspa dupla), é mapeado para o elemento XML a seguir.<br /><br /> `<root type="string">ABC</root>`<br /><br /> Qualquer espaço em branco em mapas XML para o espaço em branco em JSON.<br /><br /> Exemplo: o elemento XML a seguir é mapeado para um fragmento JSON.<br /><br /> `<root type="string">  A BC      </root>`<br /><br /> O fragmento JSON é "A BC".|
|`number`|1 ou mais CIIs|Um JSON `number` (JSON RFC, seção 2,4), possivelmente rodeado por um espaço em branco. Cada caractere na combinação número/espaço em branco é um caractere que corresponde ao [código de caractere] da CII.<br /><br /> Exemplo: o elemento a seguir mapeia para um fragmento JSON.<br /><br /> `<root type="number">    42</root>`<br /><br /> O fragmento JSON é 42<br /><br /> (O espaço em branco é preservado).|
|`boolean`|4 ou 5 CIIs (que corresponde a `true` ou `false` ), possivelmente cercados por CIIs de espaço em branco adicional.|Uma sequência CII que corresponde à cadeia de caracteres "true" é mapeada para o literal `true` e uma sequência CII que corresponde à cadeia de caracteres "false" é mapeada para o literal `false` . O espaço em branco ao redor é preservado.<br /><br /> Exemplo: o elemento a seguir mapeia para um fragmento JSON.<br /><br /> `<root type="boolean"> false</root>`<br /><br /> O fragmento JSON é `false` .|
|`null`|Nenhum permitido.|O literal `null` . No mapeamento JSON para XML, o `null` pode estar entre espaços em branco (' WS ' na seção 2) que não é mapeado para XML.<br /><br /> Exemplo: o elemento a seguir mapeia para um fragmento JSON.<br /><br /> `<root type="null"/>`<br /><br /> ou<br /><br /> `<root type="null"></root>`<br /><br /> :<br /><br /> O fragmento JSON em ambos os casos é `Null` .|
|`object`|0 ou mais EIIs.|A `begin-object` (chave esquerda) como na seção 2,2 da RFC JSON, seguida por um registro de membro para cada EII, conforme descrito mais adiante. Se houver mais de um EII, haverá separadores de valor (vírgulas) entre os registros de membro. Tudo isso é seguido por um objeto final (chave direita).<br /><br /> Exemplo: o elemento a seguir mapeia para o fragmento JSON.<br /><br /> `<root type="object">`<br /><br /> `<type1 type="string">aaa\</type1>`<br /><br /> `<type2 type="string">bbb\</type2>`<br /><br /> `</root >`<br /><br /> O fragmento JSON é `{"type1":"aaa","type2":"bbb"}` .<br /><br /> Se o atributo de tipo de contrato de dados estiver presente no mapeamento de XML para JSON, um registro de membro adicional será inserido no início. Seu nome é o [nome local] do atributo de tipo de contrato de dados (" \_ \_ tipo") e seu valor é o [valor normalizado] do atributo. Por outro lado, no mapeamento de JSON para XML, se o nome do primeiro registro de membro for o [nome local] do atributo de tipo de contrato de dados (ou seja, " \_ \_ tipo"), um atributo de tipo de contrato de dados correspondente estará presente no XML mapeado, mas um EII correspondente não estará presente. Observe que esse registro de membro deve ocorrer primeiro no objeto JSON para que esse mapeamento especial seja aplicado. Isso representa uma partida do processamento comum de JSON, em que a ordem dos registros de membros não é significativa.<br /><br /> Exemplo:<br /><br /> O fragmento JSON a seguir mapeia para XML.<br /><br /> `{"__type":"Person","name":"John"}`<br /><br /> O XML é o código a seguir.<br /><br /> `<root type="object" __type="Person">   <name type="string">John</name> </root>`<br /><br /> Observe que o \_ \_ tipo todos está presente, mas não há nenhum \_ \_ tipo EIi.<br /><br /> No entanto, se a ordem no JSON for revertida, conforme mostrado no exemplo a seguir.<br /><br /> `{"name":"John","\_\_type":"Person"}`<br /><br /> O XML correspondente é mostrado.<br /><br /> `<root type="object">   <name type="string">John</name>   <__type type="string">Person</__type> </root>`<br /><br /> Ou seja, \_ _type deixa de ter um significado especial e é mapeado para um EII como de costume, não todos.<br /><br /> As regras de escape/saída para o [valor normalizado] do todos quando mapeadas para um valor JSON são iguais às cadeias de caracteres JSON, especificadas na linha "String" dessa tabela.<br /><br /> Exemplo:<br /><br /> `<root type="object" __type="\abc" />`<br /><br /> para o exemplo anterior, é possível mapear para o JSON a seguir.<br /><br /> `{"__type":"\\abc"}`<br /><br /> Em um mapeamento de XML para JSON, o primeiro [nome local] do EII não deve ser " \_ \_ Type".<br /><br /> O espaço em branco ( `ws` ) nunca é gerado em mapeamento de XML para JSON para objetos e é ignorado no mapeamento de JSON para XML.<br /><br /> Exemplo: o fragmento JSON a seguir mapeia para um elemento XML.<br /><br /> `{ "ccc" : "aaa", "ddd" :"bbb"}`<br /><br /> O elemento XML é mostrado no código a seguir.<br /><br /> `<root type="object">    <ccc type="string">aaa</ccc>    <ddd type="string">bbb</bar> </root >`|
|array|0 ou mais EIIs|Um Begin-array (colchete esquerdo) como na seção 2,3 da RFC JSON, seguido por um registro de matriz para cada EII, conforme descrito mais adiante. Se houver mais de um EII, haverá separadores de valor (vírgulas) entre os registros de matriz. Tudo isso é seguido por uma matriz final.<br /><br /> Exemplo: o elemento XML a seguir é mapeado para um fragmento JSON.<br /><br /> `<root type="array"/>    <item type="string">aaa</item>    <item type="string">bbb</item> </root >`<br /><br /> O fragmento JSON é `["aaa","bbb"]`<br /><br /> O espaço em branco ( `ws` ) nunca é gerado no mapeamento de XML para JSON para matrizes e é ignorado no mapeamento de JSON para XML.<br /><br /> Exemplo: um fragmento JSON.<br /><br />`["aaa", "bbb"]`<br /><br /> O elemento XML para o qual ele é mapeado.<br /><br /> `<root type="array"/>    <item type="string">aaa</item>    <item type="string">bbb</item> </root >`|

Os registros de membro funcionam da seguinte maneira:

- O [nome local] do elemento interno é mapeado para a `string` parte do `member` conforme definido na seção 2,2 da RFC JSON.

Exemplo: o elemento a seguir mapeia para um fragmento JSON.

```xml
<root type="object">
    <myLocalName type="string">aaa</myLocalName>
</root>
```

O fragmento JSON a seguir é exibido.

```json
{"myLocalName":"aaa"}
```

- No mapeamento de XML para JSON, os caracteres que devem ser ignorados em JSON são ignorados e os outros não são de escape. O caractere "/", embora não seja um caractere que deva ser escapado, tenha um escape de saída, no entanto (não precisa ser ignorado em mapeamento de JSON para XML). Isso é necessário para dar suporte ao formato ASP.NET AJAX para `DateTime` dados em JSON.

- No mapeamento JSON para XML, todos os caracteres (incluindo os caracteres sem escape, se necessário) são usados para formar um `string` que produza um [nome local].

- Os elementos internos [filhos] são mapeados para o valor na seção 2,2, de acordo com o que é `JSON Type Attribute` assim para o `Root JSON Element` . São permitidos vários níveis de aninhamento de EIIs (incluindo aninhamento dentro de matrizes).

Exemplo: o elemento a seguir mapeia para um fragmento JSON.

```xml
<root type="object">
    <myLocalName1 type="string">myValue1</myLocalName1>
    <myLocalName2 type="number">2</myLocalName2>
    <myLocalName3 type="object">
        <myNestedName1 type="boolean">true</myNestedName1>
        <myNestedName2 type="null"/>
    </myLocalName3>
</root >
```

O fragmento JSON a seguir é o que ele mapeia.

```json
{"myLocalName1":"myValue1","myLocalName2":2,"myLocalName3":{"myNestedName1":true,"myNestedName2":null}}
```

> [!NOTE]
> Não há nenhuma etapa de codificação XML no mapeamento anterior. Portanto, o WCF dá suporte apenas a documentos JSON, onde todos os caracteres em nomes de chave são caracteres válidos em nomes de elementos XML. Por exemplo, o documento JSON {"<": "a"} não tem suporte porque < não é um nome válido para um elemento XML.

A situação inversa (caracteres válidos em XML, mas não em JSON) não causa problemas porque o mapeamento anterior inclui etapas de escape/saída JSON.

Os registros de matriz funcionam da seguinte maneira:

- O [nome local] do elemento interno é "item".

- O mapa [Children] do elemento interno é mapeado para o valor na seção 2,3, de acordo com o atributo de tipo JSON, como se encontra para o elemento JSON raiz. São permitidos vários níveis de aninhamento de EIIs (incluindo aninhamento dentro de objetos).

Exemplo: o elemento a seguir mapeia para um fragmento JSON.

```xml
<root type="array">
    <item type="string">myValue1</item>
    <item type="number">2</item>
    <item type="array">
    <item type="boolean">true</item>
    <item type="null"/></item>
</root>
```

Este é o fragmento JSON.

```json
["myValue1",2,[true,null]]
```

## <a name="see-also"></a>Consulte também

- <xref:System.Runtime.Serialization.Json.JsonReaderWriterFactory>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>
- [Serialização JSON autônoma](stand-alone-json-serialization.md)
