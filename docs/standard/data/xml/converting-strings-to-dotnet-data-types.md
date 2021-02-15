---
description: 'Saiba mais sobre: converter cadeias de caracteres em tipos de dados .NET'
title: Convertendo cadeias de caracteres em tipos de dados .NET
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 65455ef3-9120-412c-819b-d0f59f88ac09
ms.openlocfilehash: 2960657dc4d4a31eed85a9b8af04976692a4dc9f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99713930"
---
# <a name="convert-strings-to-net-data-types"></a>Converter cadeias de caracteres em tipos de dados .NET

Se você quiser converter uma cadeia de caracteres em um tipo de dados .NET, use o método **XmlConvert** que atenda aos requisitos do aplicativo. Para obter uma lista de todos os métodos de conversão disponíveis na classe **XmlConvert**, confira <xref:System.Xml.XmlConvert>.  
  
 A cadeia de caracteres retornada do método **ToString** é uma versão da cadeia de caracteres dos dados que são passados. Além disso, há vários tipos .NET que são convertidos usando a classe **XmlConvert** , ainda que não usem os métodos na classe **System. Convert** . A classe **XmlConvert** segue a especificação do tipo de dados XSD (XML Schema) e tem um tipo de dados para o qual o **XmlConvert** pode ser mapeado.  
  
 A tabela a seguir lista os tipos de dados do .NET e os tipos de cadeia de caracteres que são retornados usando o mapeamento de tipo de dados XSD (esquema XML). Esses tipos .NET não podem ser processados usando **System. Convert**.  
  
|Tipo .NET|Cadeia de caracteres retornada|  
|-------------------------|---------------------|  
|Boolean|"true", "false"|  
|Single.PositiveInfinity|"INF"|  
|Single.NegativeInfinity|"-INF"|  
|Double.PositiveInfinity|"INF"|  
|Double.NegativeInfinity|"-INF"|  
|Datetime|O formato é "yyyy-MM-ddTHH:mm:sszzzzzz" e seus subconjuntos.|  
|Timespan|O formato é PnYnMnTnHnMnS isto é, `P2Y10M15DT10H30M20S` é uma duração de 2 anos, 10 meses, 15 dias, 10 horas, 30 minutos e 20 segundos.|  
  
> [!NOTE]
> Se estiver convertendo qualquer um dos tipos .NET listados na tabela para uma cadeia de caracteres usando o método **ToString** , a cadeia de caracteres retornada não será o tipo base, mas o tipo de cadeia de caracteres XSD (esquema XML).  
  
 O tipo de valor **DateTime** e **Timespan** diferem porque **DateTime** representa um momento no tempo, enquanto **TimeSpan** representa um intervalo de tempo. Os formatos **DateTime** e **Timespan** são definidos na especificação dos tipos de dados do esquema XML (XSD). Por exemplo:  
  
```vb  
Dim writer As New XmlTextWriter("myfile.xml", Nothing)  
Dim [date] As New DateTime(2001, 8, 4)  
writer.WriteElementString("Date", XmlConvert.ToString([date]))  
```  
  
```csharp  
XmlTextWriter writer = new XmlTextWriter("myfile.xml", null);  
DateTime date = new DateTime (2001, 08, 04);  
writer.WriteElementString("Date", XmlConvert.ToString(date));  
```  
  
 **Saída**  
  
 `<Date>2001-08-04T00:00:00</Date>`.  
  
 O código a seguir converte um inteiro para uma cadeia de caracteres:  
  
```vb  
Dim writer As New XmlTextWriter("myfile.xml", Nothing)  
Dim value As Int32 = 200  
writer.WriteElementString("Number", XmlConvert.ToString(value))  
```  
  
```csharp  
XmlTextWriter writer = new XmlTextWriter("myfile.xml", null);  
Int32 value = 200;  
writer.WriteElementString("Number", XmlConvert.ToString(value));  
```  
  
 **Saída**  
  
 `<Number>200</Number>`  
  
 No entanto, se você estiver convertendo uma cadeia de caracteres em **booliano**, **única** ou **dupla**, o tipo do .net retornado não será o mesmo que o tipo retornado ao usar a classe **System. Convert** .  
  
## <a name="string-to-boolean"></a>String para Boolean  

 A tabela a seguir mostra qual o tipo gerado para cadeias de caracteres de entradas consideradas, ao converter uma cadeia de caracteres para **Boolean** usando o método **ToBoolean**.  
  
|Parâmetro de entrada válida de cadeia de caracteres|Tipo de saída do .NET|  
|----------------------------------|--------------------------------|  
|"true"|Boolean.True|  
|"1"|Boolean.True|  
|"false"|Boolean.False|  
|"0"|Boolean.False|  
  
 Por exemplo, considerando o seguinte XML:  
  
 **Entrada**  
  
```xml  
<Boolean>true</Boolean>  
<Boolean>1</Boolean>
```  
  
 Ambos podem ser compreendidos pelo código a seguir e **bvalue** é **System.Boolean.True**:  
  
```vb  
Dim bvalue As Boolean = _  
   XmlConvert.ToBoolean(reader.ReadElementString())  
Console.WriteLine(bvalue)  
```  
  
```csharp  
Boolean bvalue = XmlConvert.ToBoolean(reader.ReadElementString());  
Console.WriteLine(bvalue);  
```  
  
## <a name="string-to-single"></a>String para Single  

 A tabela a seguir mostra qual o tipo gerado para cadeias de caracteres de entradas consideradas, ao converter uma cadeia de caracteres para **Single** usando o método **ToSingle**.  
  
|Parâmetro de entrada válida de cadeia de caracteres|Tipo de saída do .NET|  
|----------------------------------|--------------------------------|  
|"INF"|Single.PositiveInfinity|  
|"-INF"|Single.NegativeInfinity|  
  
## <a name="string-to-double"></a>String para Double  

 A tabela a seguir mostra qual o tipo gerado para cadeias de caracteres de entradas consideradas, ao converter uma cadeia de caracteres para **Single** usando o método **ToDouble**.  
  
|Parâmetro de entrada válida de cadeia de caracteres|Tipo de saída do .NET|  
|----------------------------------|--------------------------------|  
|"INF"|Double.PositiveInfinity|  
|"-INF"|Double.NegativeInfinity|  
  
 O código a seguir grava `<Infinity>INF</Infinity>`:  
  
```vb  
Dim value As Double = Double.PositiveInfinity  
writer.WriteElementString("Infinity", XmlConvert.ToString(value))  
```  
  
```csharp  
Double value = Double.PositiveInfinity;  
writer.WriteElementString("Infinity", XmlConvert.ToString(value));  
```  
  
## <a name="see-also"></a>Consulte também

- [Conversão de tipos de dados XML](conversion-of-xml-data-types.md)
- [Convertendo tipos .NET em cadeias de caracteres](converting-dotnet-types-to-strings.md)
