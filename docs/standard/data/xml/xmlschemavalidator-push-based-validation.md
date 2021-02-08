---
description: 'Saiba mais sobre: validação de Push-Based de XmlSchemaValidator'
title: XmlSchemaValidator Envio- de validação
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 911d4460-dd91-4958-85b2-2ca3299f9ec6
ms.openlocfilehash: 6492285b26659fabbc72bf56304c5f24790af170
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99782605"
---
# <a name="xmlschemavalidator-push-based-validation"></a>XmlSchemaValidator Envio- de validação

A classe de <xref:System.Xml.Schema.XmlSchemaValidator> fornece um mecanismo eficiente, de alto desempenho validar dados XML com esquemas XML de uma maneira envio- base. Por exemplo, a classe de <xref:System.Xml.Schema.XmlSchemaValidator> permite que você valide um infoset XML no local sem ter que para serializá-lo como um documento XML e então um nova análise o documento usando um leitor validando XML.

A classe de <xref:System.Xml.Schema.XmlSchemaValidator> pode ser usada em cenários avançados como mecanismos de validação de compilação sobre fontes de dados XML personalizados ou como uma maneira de criar um gravador validando XML.

A seguir está um exemplo de uso da classe de <xref:System.Xml.Schema.XmlSchemaValidator> para validar o arquivo de `contosoBooks.xml` com o esquema de `contosoBooks.xsd` . O exemplo usa a classe de <xref:System.Xml.Serialization.XmlSerializer> para desserializar o arquivo de `contosoBooks.xml` e passar o valor de nós métodos de classe de <xref:System.Xml.Schema.XmlSchemaValidator> .

> [!NOTE]
> Este exemplo é usado em todo as seções deste tópico.

[!code-csharp[XmlSchemaValidatorExamples#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaValidatorExamples/CS/XmlSchemaValidatorExamples.cs#1)]
[!code-vb[XmlSchemaValidatorExamples#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaValidatorExamples/VB/XmlSchemaValidatorExamples.vb#1)]

O exemplo usa o arquivo `contosoBooks.xml` como entrada.

[!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]

O exemplo também usa `contosoBooks.xsd` como entrada.

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" targetNamespace="http://www.contoso.com/books" xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="bookstore">
        <xs:complexType>
            <xs:sequence>
                <xs:element maxOccurs="unbounded" name="book">
                    <xs:complexType>
                        <xs:sequence>
                            <xs:element name="title" type="xs:string" />
                            <xs:element name="author">
                                <xs:complexType>
                                    <xs:sequence>
                                        <xs:element minOccurs="0" name="name" type="xs:string" />
                                        <xs:element minOccurs="0" name="first-name" type="xs:string" />
                                        <xs:element minOccurs="0" name="last-name" type="xs:string" />
                                    </xs:sequence>
                                </xs:complexType>
                            </xs:element>
                            <xs:element name="price" type="xs:decimal" />
                        </xs:sequence>
                        <xs:attribute name="genre" type="xs:string" use="required" />
                        <xs:attribute name="publicationdate" type="xs:date" use="required" />
                        <xs:attribute name="ISBN" type="xs:string" use="required" />
                    </xs:complexType>
                </xs:element>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```

## <a name="validating-xml-data-using-xmlschemavalidator"></a>Validando dados XML usando XmlSchemaValidator

Para iniciar a validar um infoset XML, primeiro você deve inicializar uma nova instância da classe <xref:System.Xml.Schema.XmlSchemaValidator> que usa o construtor de <xref:System.Xml.Schema.XmlSchemaValidator.%23ctor%2A> .

O construtor de <xref:System.Xml.Schema.XmlSchemaValidator.%23ctor%2A> leva <xref:System.Xml.XmlNameTable>, <xref:System.Xml.Schema.XmlSchemaSet>, e objetos de <xref:System.Xml.XmlNamespaceManager> como os parâmetros bem como <xref:System.Xml.Schema.XmlSchemaValidationFlags> avaliada como um parâmetro. O objeto de <xref:System.Xml.XmlNameTable> é usado para atomizar cadeias de caracteres conhecidos de namespace como o namespace do esquema, o namespace XML, e assim por diante, e passado para o método de <xref:System.Xml.Schema.XmlSchemaDatatype.ParseValue%2A> para validar o conteúdo simples. O objeto de <xref:System.Xml.Schema.XmlSchemaSet> contém os esquemas XML usados para validar o infoset XML. O objeto de <xref:System.Xml.XmlNamespaceManager> é usado para resolver namespaces encontrados durante a validação. O valor de <xref:System.Xml.Schema.XmlSchemaValidationFlags> é usado para desativar determinados recursos de validação.

Para obter mais informações sobre o construtor de <xref:System.Xml.Schema.XmlSchemaValidator.%23ctor%2A> , consulte a documentação de referência da classe <xref:System.Xml.Schema.XmlSchemaValidator> .

### <a name="initializing-validation"></a>Inicializando a validação

Depois que um objeto de <xref:System.Xml.Schema.XmlSchemaValidator> foi construído, há dois métodos sobrecarregados de <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> usados para inicializar o estado do objeto de <xref:System.Xml.Schema.XmlSchemaValidator> . Estes são os dois métodos de <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> .

- <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType>

- <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType>

O método de <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType> de opção inicializa um objeto de <xref:System.Xml.Schema.XmlSchemaValidator> ao seu estado inicial, e o método sobrecarregado de <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType> que leva <xref:System.Xml.Schema.XmlSchemaObject> como um parâmetro inicializa um objeto de <xref:System.Xml.Schema.XmlSchemaValidator> ao seu estado inicial para a validação parcial.

Ambos os métodos de <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> só podem ser chamados imediatamente após um objeto de <xref:System.Xml.Schema.XmlSchemaValidator> foi construído ou após uma chamada a <xref:System.Xml.Schema.XmlSchemaValidator.EndValidation%2A>.

Para um exemplo de método <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType> , consulte o exemplo na introdução. Para obter mais informações sobre o método de <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> , consulte a documentação de referência da classe <xref:System.Xml.Schema.XmlSchemaValidator> .

#### <a name="partial-validation"></a>Validação parcial

O método de <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType> que leva <xref:System.Xml.Schema.XmlSchemaObject> como um parâmetro inicializa um objeto de <xref:System.Xml.Schema.XmlSchemaValidator> ao seu estado inicial para a validação parcial.

No exemplo a seguir, <xref:System.Xml.Schema.XmlSchemaObject> é inicializado para validação usando o método parcial de <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType> . O elemento do esquema de `orderNumber` é passado selecionando o elemento de esquema por <xref:System.Xml.XmlQualifiedName> na coleção de <xref:System.Xml.Schema.XmlSchemaObjectTable> retornada pela propriedade de <xref:System.Xml.Schema.XmlSchemaSet.GlobalElements%2A> do objeto de <xref:System.Xml.Schema.XmlSchemaSet> . O objeto de <xref:System.Xml.Schema.XmlSchemaValidator> valida neste elemento específico.

```vb
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()
schemaSet.Add(Nothing, "schema.xsd")
schemaSet.Compile()
Dim nameTable As NameTable = New NameTable()
Dim manager As XmlNamespaceManager = New XmlNamespaceManager(nameTable)

Dim validator As XmlSchemaValidator = New XmlSchemaValidator(nameTable, schemaSet, manager, XmlSchemaValidationFlags.None)
validator.Initialize(schemaSet.GlobalElements.Item(New XmlQualifiedName("orderNumber")))

validator.ValidateElement("orderNumber", "", Nothing)
validator.ValidateEndOfAttributes(Nothing)
validator.ValidateText("123")
validator.ValidateEndElement(Nothing)
```

```csharp
XmlSchemaSet schemaSet = new XmlSchemaSet();
schemaSet.Add(null, "schema.xsd");
schemaSet.Compile();
NameTable nameTable = new NameTable();
XmlNamespaceManager manager = new XmlNamespaceManager(nameTable);

XmlSchemaValidator validator = new XmlSchemaValidator(nameTable, schemaSet, manager, XmlSchemaValidationFlags.None);
validator.Initialize(schemaSet.GlobalElements[new XmlQualifiedName("orderNumber")]);

validator.ValidateElement("orderNumber", "", null);
validator.ValidateEndOfAttributes(null);
validator.ValidateText("123");
validator.ValidateEndElement(null);
```

O exemplo a seguir usa o esquema XML como entrada.

```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="orderNumber" type="xs:int" />
</xs:schema>
```

Para obter mais informações sobre o método de <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> , consulte a documentação de referência da classe <xref:System.Xml.Schema.XmlSchemaValidator> .

### <a name="adding-additional-schemas"></a>Adicionando esquemas adicionais

O método de <xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> da classe de <xref:System.Xml.Schema.XmlSchemaValidator> é usado para adicionar um esquema XML para o conjunto de esquemas usados durante a validação. O método de <xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> pode ser usado para simular o efeito de localizar um esquema XML embutido no infoset XML que está sendo validada.

> [!NOTE]
> O namespace de destino do parâmetro de <xref:System.Xml.Schema.XmlSchema> pode não corresponder de qualquer elemento ou atributo já encontrado pelo objeto de <xref:System.Xml.Schema.XmlSchemaValidator> .
>
> Se o valor de <xref:System.Xml.Schema.XmlSchemaValidationFlags.ProcessInlineSchema?displayProperty=nameWithType> não foi passado como um parâmetro para o construtor de <xref:System.Xml.Schema.XmlSchemaValidator.%23ctor%2A> , o método de <xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> não fará nada.

O resultado de método <xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> é dependente no contexto atual do nó XML que está sendo validada. Para obter mais informações sobre contextos de validação, consulte a seção contexto validação” neste tópico.

Para obter mais informações sobre o método de <xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> , consulte a documentação de referência da classe <xref:System.Xml.Schema.XmlSchemaValidator> .

### <a name="validating-elements-attributes-and-content"></a>Validando elementos, atributos, e conteúdo

A classe de <xref:System.Xml.Schema.XmlSchemaValidator> fornece vários métodos usados para validar elementos, atributos, e o conteúdo em um infoset XML com esquemas XML. A tabela a seguir descreve cada um desses métodos.

|Método|Descrição|
|------------|-----------------|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A>|Valida o nome do elemento no contexto atual.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>|Valida o atributo no contexto do elemento atual ou contra o objeto de <xref:System.Xml.Schema.XmlSchemaAttribute> passado como um parâmetro para o método de <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> .|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndOfAttributes%2A>|Verifica se todos os atributos necessários no contexto do elemento entram presente e prepara o objeto de <xref:System.Xml.Schema.XmlSchemaValidator> para validar o conteúdo filho do elemento.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A>|Valida se o texto é permitido no contexto do elemento atual, e acumula o texto para validação se o elemento atual tem conteúdo simples.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateWhitespace%2A>|Valida se o espaço em branco é permitido no contexto do elemento atual, e acumula o espaço em branco para validação se o elemento atual tem conteúdo simples.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A>|Verifica se o conteúdo de texto do elemento é válida de acordo com seu tipo de dados para elementos com conteúdo simples, e verifica se o conteúdo do elemento atual seja concluída para elementos com conteúdo complexo.|
|<xref:System.Xml.Schema.XmlSchemaValidator.SkipToEndElement%2A>|Ignora a validação de conteúdo do elemento atual e prepara o objeto de <xref:System.Xml.Schema.XmlSchemaValidator> para validar o conteúdo no contexto do elemento pai.|
|<xref:System.Xml.Schema.XmlSchemaValidator.EndValidation%2A>|Termina a validação verifica e restrições de identidade para o documento inteiro XML se a opção de validação de <xref:System.Xml.Schema.XmlSchemaValidationFlags.ProcessIdentityConstraints> é definida.|

> [!NOTE]
> A classe de <xref:System.Xml.Schema.XmlSchemaValidator> tiver definido uma transição de estado que aplica a sequência e a ocorrência de chamadas feitas a cada um dos métodos descritos na tabela anterior. A transição específica do estado da classe de <xref:System.Xml.Schema.XmlSchemaValidator> é descrita da seção “de transição de estado XmlSchemaValidator” neste tópico.

Para um exemplo dos métodos usados para validar elementos, atributos, e o conteúdo em um infoset XML, consulte o exemplo na seção anterior. Para obter mais informações sobre estes métodos, consulte a documentação de referência da classe <xref:System.Xml.Schema.XmlSchemaValidator> .

#### <a name="validating-content-using-an-xmlvaluegetter"></a>Validando conteúdo usando um XmlValueGetter

<xref:System.Xml.Schema.XmlValueGetter>`delegate` pode ser usado para passar o valor do atributo, texto, ou de nós de espaço em branco como o Common Language Runtime (CLR) tipos compatível com o tipo de idioma de XSD (XSD) de atributo, texto, ou o nó de espaço em branco. <xref:System.Xml.Schema.XmlValueGetter>`delegate` é útil se o valor de CLR de um atributo, um texto, ou um nó de espaço em branco já estiver disponível, e evita o custo de convertê-los em `string` e dos reparsing novamente para validação.

<xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>, <xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A>, e os métodos de <xref:System.Xml.Schema.XmlSchemaValidator.ValidateWhitespace%2A> são sobrecarregados e aceitar o valor do atributo, texto, ou de nós de espaço em branco como `string` ou <xref:System.Xml.Schema.XmlValueGetter>`delegate`.

Os seguintes métodos da classe <xref:System.Xml.Schema.XmlSchemaValidator> aceitam <xref:System.Xml.Schema.XmlValueGetter>`delegate` como um parâmetro.

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateWhitespace%2A>

A seguir está um exemplo <xref:System.Xml.Schema.XmlValueGetter>`delegate` extraído do exemplo de classe de <xref:System.Xml.Schema.XmlSchemaValidator> na introdução. <xref:System.Xml.Schema.XmlValueGetter>`delegate` retorna o valor de um atributo como um objeto de <xref:System.DateTime> . Para validar este objeto de <xref:System.DateTime> retornado por <xref:System.Xml.Schema.XmlValueGetter>, converte o objeto de <xref:System.Xml.Schema.XmlSchemaValidator> ele para o primeiro ValueType (ValueType é CLR padrão que mapeia para o tipo XSD) para o tipo de dados de atributo e então verifica facetas o valor convertido.

```vb
Shared dateTimeGetterContent As Object

Shared Function DateTimeGetterHandle() As Object
    Return dateTimeGetterContent
End Function

Shared Function DateTimeGetter(dateTime As DateTime) As XmlValueGetter
    dateTimeGetterContent = dateTime
    Return New XmlValueGetter(AddressOf DateTimeGetterHandle)
End Function
```

```csharp
static object dateTimeGetterContent;

static object DateTimeGetterHandle()
{
    return dateTimeGetterContent;
}

static XmlValueGetter DateTimeGetter(DateTime dateTime)
{
    dateTimeGetterContent = dateTime;
    return new XmlValueGetter(dateTimeGetterHandle);
}
```

Para um exemplo completo de <xref:System.Xml.Schema.XmlValueGetter>`delegate`, consulte o exemplo na introdução. Para obter mais informações sobre <xref:System.Xml.Schema.XmlValueGetter> de `delegate`, consulte <xref:System.Xml.Schema.XmlValueGetter>, e documentação de referência da classe <xref:System.Xml.Schema.XmlSchemaValidator> .

#### <a name="post-schema-validation-information"></a>POST-Esquema-Validação-informações

A classe de <xref:System.Xml.Schema.XmlSchemaInfo> representa algumas de POST-Esquema-Validação- informações de um nó XML validado pela classe de <xref:System.Xml.Schema.XmlSchemaValidator> . Os vários métodos da classe <xref:System.Xml.Schema.XmlSchemaValidator> aceitar um objeto de <xref:System.Xml.Schema.XmlSchemaInfo> como um opcional), (`null`parâmetro de `out` .

Em cima de validação com êxito, as propriedades do objeto de <xref:System.Xml.Schema.XmlSchemaInfo> são definidas com os resultados de validação. Por exemplo, em cima de validação com êxito de um atributo usando o método de <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A> , <xref:System.Xml.Schema.XmlSchemaInfo>do objeto de <xref:System.Xml.Schema.XmlSchemaInfo.SchemaAttribute%2A> (se especificado), <xref:System.Xml.Schema.XmlSchemaInfo.SchemaType%2A>, <xref:System.Xml.Schema.XmlSchemaInfo.MemberType%2A>, e as propriedades de <xref:System.Xml.Schema.XmlSchemaInfo.Validity%2A> são especificados com os resultados de validação.

Os seguintes métodos da classe <xref:System.Xml.Schema.XmlSchemaValidator> aceitar um objeto de <xref:System.Xml.Schema.XmlSchemaInfo> como um parâmetro de saída.

- <xref:System.Xml.Schema.XmlSchemaValidator.SkipToEndElement%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndOfAttributes%2A>

Para um exemplo completo da classe de <xref:System.Xml.Schema.XmlSchemaInfo> , consulte o exemplo na introdução. Para obter mais informações sobre a classe de <xref:System.Xml.Schema.XmlSchemaInfo> , consulte a documentação de referência da classe <xref:System.Xml.Schema.XmlSchemaInfo> .

### <a name="retrieving-expected-particles-attributes-and-unspecified-default-attributes"></a>Recuperando partículas previstas, atributos, e atributos padrão não especificado

A classe de <xref:System.Xml.Schema.XmlSchemaValidator> fornece <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>, e métodos de <xref:System.Xml.Schema.XmlSchemaValidator.GetUnspecifiedDefaultAttributes%2A> para recuperar as partículas previstas, atributos, e atributos padrão não especificado no contexto atual de validação.

#### <a name="retrieving-expected-particles"></a>Recuperando partículas previstas

O método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna uma matriz de objetos de <xref:System.Xml.Schema.XmlSchemaParticle> que contêm as partículas previstas no contexto do elemento atual. As partículas válidas que podem ser retornadas pelo método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> são instâncias de classes de <xref:System.Xml.Schema.XmlSchemaElement> e de <xref:System.Xml.Schema.XmlSchemaAny> .

Quando o compositor para o modelo de conteúdo for `xs:sequence`, somente a partícula seguir na sequência é retornada. Se o compositor para o modelo de conteúdo é `xs:all` ou `xs:choice`, todas as partículas válidos que podem seguir no contexto do elemento atual são retornadas.

> [!NOTE]
> Se o método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> é chamado imediatamente depois de chamar o método de <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> , o método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna todos os elementos globais.

Por exemplo, no esquema e o documento XML de idioma de XSD (XSD) que seguem, após validar o elemento de `book` , o elemento de `book` é o contexto do elemento atual. O método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna uma matriz que contém um único objeto de <xref:System.Xml.Schema.XmlSchemaElement> que representa o elemento de `title` . Quando o contexto de validação é o elemento de `title` , o método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna uma matriz vazia. Se o método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> é chamado depois que o elemento de `title` foi validado mas antes do elemento de `description` está validado, retorna uma matriz que contém um único objeto de <xref:System.Xml.Schema.XmlSchemaElement> que representa o elemento de `description` . Se o método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> é chamado depois que o elemento de `description` já foi validado então retorna uma matriz que contém um único objeto de <xref:System.Xml.Schema.XmlSchemaAny> que representa a curinga.

```vb
Dim reader As XmlReader =  XmlReader.Create("input.xml")

Dim schemaSet As New XmlSchemaSet()
schemaSet.Add(Nothing, "schema.xsd")
Dim manager As New XmlNamespaceManager(reader.NameTable)

Dim validator As New XmlSchemaValidator(reader.NameTable,schemaSet,manager,XmlSchemaValidationFlags.None)
validator.Initialize()

validator.ValidateElement("book", "", Nothing)

validator.ValidateEndOfAttributes(Nothing)
For Each element As XmlSchemaElement In validator.GetExpectedParticles()
    Console.WriteLine(element.Name)
Next

validator.ValidateElement("title", "", Nothing)
validator.ValidateEndOfAttributes(Nothing)
For Each element As XmlSchemaElement In validator.GetExpectedParticles()
    Console.WriteLine(element.Name)
Next
validator.ValidateEndElement(Nothing)

For Each element As XmlSchemaElement In validator.GetExpectedParticles()
    Console.WriteLine(element.Name)
Next

validator.ValidateElement("description", "", Nothing)
validator.ValidateEndOfAttributes(Nothing)
validator.ValidateEndElement(Nothing)

For Each particle As XmlSchemaParticle In validator.GetExpectedParticles()
    Console.WriteLine(particle.GetType())
Next

validator.ValidateElement("namespace", "", Nothing)
validator.ValidateEndOfAttributes(Nothing)
validator.ValidateEndElement(Nothing)

validator.ValidateEndElement(Nothing)
```

```csharp
XmlReader reader = XmlReader.Create("input.xml");

var schemaSet = new XmlSchemaSet();
schemaSet.Add(null, "schema.xsd");
var manager = new XmlNamespaceManager(reader.NameTable);

var validator = new XmlSchemaValidator(reader.NameTable, schemaSet, manager, XmlSchemaValidationFlags.None);
validator.Initialize();

validator.ValidateElement("book", "", null);

validator.ValidateEndOfAttributes(null);
foreach (XmlSchemaElement element in validator.GetExpectedParticles())
{
    Console.WriteLine(element.Name);
}

validator.ValidateElement("title", "", null);
validator.ValidateEndOfAttributes(null);
foreach (XmlSchemaElement element in validator.GetExpectedParticles())
{
    Console.WriteLine(element.Name);
}
validator.ValidateEndElement(null);

foreach (XmlSchemaElement element in validator.GetExpectedParticles())
{
    Console.WriteLine(element.Name);
}

validator.ValidateElement("description", "", null);
validator.ValidateEndOfAttributes(null);
validator.ValidateEndElement(null);

foreach (XmlSchemaParticle particle in validator.GetExpectedParticles())
{
    Console.WriteLine(particle.GetType());
}

validator.ValidateElement("namespace", "", null);
validator.ValidateEndOfAttributes(null);
validator.ValidateEndElement(null);

validator.ValidateEndElement(null);
```

 O exemplo usa o seguinte XML como entrada:

```xml
<xs:schema xmlns:xs="http://www.w3c.org/2001/XMLSchema">
  <xs:element name="book">
    <xs:sequence>
      <xs:element name="title" type="xs:string" />
      <xs:element name="description" type="xs:string" />
      <xs:any processContent="lax" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:element>
</xs:schema>
```

O exemplo usa o seguinte esquema XSD como entrada:

```xml
<book>
  <title>My Book</title>
  <description>My Book's Description</description>
  <namespace>System.Xml.Schema</namespace>
</book>
```

> [!NOTE]
> Os resultados de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>, de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>, e métodos de <xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> da classe de <xref:System.Xml.Schema.XmlSchemaValidator> são dependentes no contexto atual sendo validada. Para obter mais informações, consulte a seção contexto validação” neste tópico.

Para um exemplo de método <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> , consulte o exemplo na introdução. Para obter mais informações sobre o método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> , consulte a documentação de referência da classe <xref:System.Xml.Schema.XmlSchemaValidator> .

#### <a name="retrieving-expected-attributes"></a>Recuperando atributos esperados

O método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna uma matriz de objetos de <xref:System.Xml.Schema.XmlSchemaAttribute> que contêm os atributos esperados no contexto do elemento atual.

Por exemplo, no exemplo na introdução, o método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> é usado para recuperar todos os atributos do elemento de `book` .

Se você chamar o método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> imediatamente após o método de <xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A> , todos os atributos que podem aparecer no documento XML são retornados. No entanto, se você chamar o método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> depois que um ou mais chamadas para o método de <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A> , os atributos que não foram validados ainda para o elemento atual são retornados.

> [!NOTE]
> Os resultados de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>, de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>, e métodos de <xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> da classe de <xref:System.Xml.Schema.XmlSchemaValidator> são dependentes no contexto atual sendo validada. Para obter mais informações, consulte a seção contexto validação” neste tópico.

Para um exemplo de método <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> , consulte o exemplo na introdução. Para obter mais informações sobre o método de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> , consulte a documentação de referência da classe <xref:System.Xml.Schema.XmlSchemaValidator> .

#### <a name="retrieving-unspecified-default-attributes"></a>Recuperando atributos padrão não especificado

O método de <xref:System.Xml.Schema.XmlSchemaValidator.GetUnspecifiedDefaultAttributes%2A> preenche <xref:System.Collections.ArrayList> especificado com objetos de <xref:System.Xml.Schema.XmlSchemaAttribute> para todos os atributos com valores padrão que não foram validados anteriormente usando o método de <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A> no contexto do elemento. O método de <xref:System.Xml.Schema.XmlSchemaValidator.GetUnspecifiedDefaultAttributes%2A> deve ser chamado após o método chamado de <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A> em cada atributo no contexto do elemento. O método de <xref:System.Xml.Schema.XmlSchemaValidator.GetUnspecifiedDefaultAttributes%2A> deve ser usado para determinar quais atributos padrão devem ser inseridos no documento XML que está sendo validada.

Para obter mais informações sobre o método de <xref:System.Xml.Schema.XmlSchemaValidator.GetUnspecifiedDefaultAttributes%2A> , consulte a documentação de referência da classe <xref:System.Xml.Schema.XmlSchemaValidator> .

### <a name="handling-schema-validation-events"></a>Eventos de validação do esquema de tratamento

Os avisos e os erros de validação de esquema encontrados durante a validação são tratadas pelo evento de <xref:System.Xml.Schema.XmlSchemaValidator.ValidationEventHandler> da classe de <xref:System.Xml.Schema.XmlSchemaValidator> .

Os avisos de validação de esquema têm um valor de <xref:System.Xml.Schema.XmlSeverityType> de <xref:System.Xml.Schema.XmlSeverityType.Warning> e os erros de validação de esquema têm um valor de <xref:System.Xml.Schema.XmlSeverityType> de <xref:System.Xml.Schema.XmlSeverityType.Error>. Se nenhum <xref:System.Xml.Schema.XmlSchemaValidator.ValidationEventHandler> foi atribuído, <xref:System.Xml.Schema.XmlSchemaValidationException> é acionada para todos os erros de validação de esquema com um valor de <xref:System.Xml.Schema.XmlSeverityType> de <xref:System.Xml.Schema.XmlSeverityType.Error>. No entanto, <xref:System.Xml.Schema.XmlSchemaValidationException> não é lançada para avisos de validação de esquema com um valor de <xref:System.Xml.Schema.XmlSeverityType> de <xref:System.Xml.Schema.XmlSeverityType.Warning>.

O código a seguir é um exemplo de <xref:System.Xml.Schema.ValidationEventHandler> que receberá os avisos e os erros de validação de esquema encontrados durante a validação de esquema tomada de exemplo na introdução.

```vb
Shared Sub SchemaValidationEventHandler(sender As Object, e As ValidationEventArgs)

    Select Case e.Severity
        Case XmlSeverityType.Error
            Console.WriteLine(vbCrLf & "Error: {0}", e.Message)
            Exit Sub
        Case XmlSeverityType.Warning
            Console.WriteLine(vbCrLf & "Warning: {0}", e.Message)
            Exit Sub
    End Select
End Sub
```

```csharp
static void SchemaValidationEventHandler(object sender, ValidationEventArgs e)
{
    switch (e.Severity)
    {
        case XmlSeverityType.Error:
            Console.WriteLine("\nError: {0}", e.Message);
            break;
        case XmlSeverityType.Warning:
            Console.WriteLine("\nWarning: {0}", e.Message);
            break;
    }
}
```

Para um exemplo completo de <xref:System.Xml.Schema.ValidationEventHandler>, consulte o exemplo na introdução. Para obter mais informações, consulte a documentação de referência da classe <xref:System.Xml.Schema.XmlSchemaInfo> .

## <a name="xmlschemavalidator-state-transition"></a>Transição de estado de XmlSchemaValidator

A classe de <xref:System.Xml.Schema.XmlSchemaValidator> tiver definido uma transição de estado que aplica a sequência e a ocorrência de chamadas feitas a cada um dos métodos usados para validar elementos, atributos, e o conteúdo em um infoset XML.

A tabela a seguir descreve a transição de estado da classe de <xref:System.Xml.Schema.XmlSchemaValidator> , e a sequência e a ocorrência de chamadas de método que podem ser feitas em cada estado.

|Estado|Transição|
|-----------|----------------|
|Validar|<xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> (<xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A> &#124; TopLevel*) <xref:System.Xml.Schema.XmlSchemaValidator.EndValidation%2A>|
|TopLevel|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateWhitespace%2A> &#124; <xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A> &#124; Element|
|Elemento|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A><xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>* ( <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndOfAttributes%2A> Conteúdo \* )? <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A> &#124;<br /><br /> <xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A><xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>\* <xref:System.Xml.Schema.XmlSchemaValidator.SkipToEndElement%2A> &#124;<br /><br /> <xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A><xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>\* <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndOfAttributes%2A> &#124; de conteúdo \* <xref:System.Xml.Schema.XmlSchemaValidator.SkipToEndElement%2A>|
|Conteúdo|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateWhitespace%2A> &#124; <xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A> &#124; Element|

> [!NOTE]
> <xref:System.InvalidOperationException> é acionada por cada um dos métodos na tabela acima quando a chamada para o método é feito na sequência incorreta de acordo com o estado atual de um objeto de <xref:System.Xml.Schema.XmlSchemaValidator> .

A tabela de transição de estado anterior de símbolos de pontuação usos para descrever os métodos e outros estados que podem ser chamados para cada estado de transição de estado da classe de <xref:System.Xml.Schema.XmlSchemaValidator> . Os símbolos usados são os mesmos símbolos localizados na referência de padrões XML para o Document type definition (DTD).

A tabela a seguir descreve como símbolos de pontuação localizados na tabela de transição de estado anterior afetam os métodos e outros estados que podem ser chamados para cada estado na transição de estado da classe de <xref:System.Xml.Schema.XmlSchemaValidator> .

|Símbolo|Descrição|
|------------|-----------------|
|&#124;|O método ou o estado (aquele antes de barra ou esse após ele) podem ser chamados.|
|?|O método ou indica que antes do ponto de interrogação é opcional mas se é chamado pode ser chamado somente uma vez.|
|\*|O método ou estado que precede o \* símbolo é opcional e pode ser chamado mais de uma vez.|

## <a name="validation-context"></a>Contexto de validação

Os métodos da classe <xref:System.Xml.Schema.XmlSchemaValidator> usada para validar elementos, atributos, e o conteúdo em um infoset XML, alterar o contexto de validação de um objeto de <xref:System.Xml.Schema.XmlSchemaValidator> . Por exemplo, a validação ignora do método de <xref:System.Xml.Schema.XmlSchemaValidator.SkipToEndElement%2A> de conteúdo do elemento atual e prepara o objeto de <xref:System.Xml.Schema.XmlSchemaValidator> para validar o conteúdo no contexto do elemento pai; é equivalente à validação de ir para todos os filhos do elemento atual e de chamar o método de <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A> .

Os resultados de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>, de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>, e métodos de <xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> da classe de <xref:System.Xml.Schema.XmlSchemaValidator> são dependentes no contexto atual sendo validada.

A tabela a seguir descreve os resultados de chamar esses métodos após chamando um dos métodos da classe <xref:System.Xml.Schema.XmlSchemaValidator> usada para validar elementos, atributos, e o conteúdo em um infoset XML.

|Método|GetExpectedParticles|GetExpectedAttributes|AddSchema|
|------------|--------------------------|---------------------------|---------------|
|<xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A>|Se o método de <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> padrão é chamado, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna uma matriz que contém todos os elementos globais.<br /><br /> Se o método sobrecarregado que leva <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> como um parâmetro é chamado para inicializar a validação parcial de um elemento, <xref:System.Xml.Schema.XmlSchemaObject> de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna somente o elemento ao qual o objeto de <xref:System.Xml.Schema.XmlSchemaValidator> foi inicializado.|Se o método de <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> padrão é chamado, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna uma matriz vazia.<br /><br /> Se a sobrecarga de método que usa <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> como um parâmetro é chamado para inicializar a validação parcial de um atributo, <xref:System.Xml.Schema.XmlSchemaObject> de <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna somente o atributo para que o objeto de <xref:System.Xml.Schema.XmlSchemaValidator> foi inicializado.|Adiciona o esquema a <xref:System.Xml.Schema.XmlSchemaSet> do objeto de <xref:System.Xml.Schema.XmlSchemaValidator> se não tem nenhum erro de pré-processamento.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A>|Se o elemento de contexto é válido, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna a sequência de elementos esperado como filhos do elemento de contexto.<br /><br /> Se o elemento de contexto é inválido, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna uma matriz vazia.|Se o elemento de contexto é válido, e se nenhuma chamada a <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A> tiver sido feito anteriormente, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna uma lista de todos os atributos definidos no elemento de contexto.<br /><br /> Se alguns atributos já foram validados, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna uma lista dos outros atributos a ser validados.<br /><br /> Se o elemento de contexto é inválido, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna uma matriz vazia.|Mesmo que acima.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>|Se o atributo de contexto é um atributo de nível superior, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna uma matriz vazia.<br /><br /> Se não <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna a sequência de elementos esperado como o primeiro filho do elemento de contexto.|Se o atributo de contexto é um atributo de nível superior, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna uma matriz vazia.<br /><br /> Se não <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna a lista dos outros atributos a ser validados.|Mesmo que acima.|
|<xref:System.Xml.Schema.XmlSchemaValidator.GetUnspecifiedDefaultAttributes%2A>|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna a sequência de elementos esperado como o primeiro filho do elemento de contexto.|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna uma lista de atributos necessários e opcionais que devem ser validados ainda para o elemento de contexto.|Mesmo que acima.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndOfAttributes%2A>|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna a sequência de elementos esperado como o primeiro filho do elemento de contexto.|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna uma matriz vazia.|Mesmo que acima.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A>|Se o contentType do elemento de contexto é misturado, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna a sequência de elementos esperado na próxima posição.<br /><br /> Se o contentType do elemento de contexto é TextOnly ou Empty, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna uma matriz vazia.<br /><br /> Se o contentType do elemento de contexto é ElementOnly, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna a sequência de elementos esperado na próxima posição mas um erro de validação tem ocorreu.|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna a lista de elemento do contexto de atributos não validados.|Mesmo que acima.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateWhitespace%2A>|Se o espaço em branco de contexto é o espaço em branco de nível superior, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna uma matriz vazia.<br /><br /> Se não o comportamento de método <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> é o mesmo que em <xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A>.|Se o espaço em branco de contexto é o espaço em branco de nível superior, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna uma matriz vazia.<br /><br /> Se não o comportamento de método <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> é o mesmo que em <xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A>.|Mesmo que acima.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A>|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> retorna a sequência de elementos esperado após o elemento de contexto (irmãos possíveis).|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna a lista de elemento do contexto de atributos não validados.<br /><br /> Se o elemento de contexto não tem nenhum pai em <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> retorna uma lista vazia (o elemento de contexto é o pai do elemento atual em <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A> que foi chamado.)|Mesmo que acima.|
|<xref:System.Xml.Schema.XmlSchemaValidator.SkipToEndElement%2A>|Mesmo que <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A>.|Mesmo que <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A>.|Mesmo que acima.|
|<xref:System.Xml.Schema.XmlSchemaValidator.EndValidation%2A>|Retorna uma matriz vazia.|Retorna uma matriz vazia.|Mesmo que acima.|

> [!NOTE]
> Os valores retornados por várias propriedades da classe de <xref:System.Xml.Schema.XmlSchemaValidator> não são alterados chamando os métodos na tabela anterior.

## <a name="see-also"></a>Confira também

- <xref:System.Xml.Schema.XmlSchemaValidator>
