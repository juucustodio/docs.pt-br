---
description: 'Saiba mais sobre: referências a objetos interoperáveis'
title: Referências de objeto interoperável
ms.date: 04/15/2019
ms.assetid: cb8da4c8-08ca-4220-a16b-e04c8f527f1b
ms.openlocfilehash: 27c801fb3954c7ea3f821a6588a2229502702989
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802678"
---
# <a name="interoperable-object-references"></a>Referências de objeto interoperável

Por padrão, o <xref:System.Runtime.Serialization.DataContractSerializer> serializa objetos por valor. Você pode usar a <xref:System.Runtime.Serialization.DataContractAttribute.IsReference%2A> propriedade para instruir o serializador de contrato de dados a preservar referências de objeto ao serializar objetos.  
  
## <a name="generated-xml"></a>XML gerado  

 Como exemplo, considere o seguinte objeto:  
  
```csharp  
[DataContract]  
public class X  
{  
    SomeClass someInstance = new SomeClass();  
    [DataMember]  
    public SomeClass A = someInstance;  
    [DataMember]  
    public SomeClass B = someInstance;  
}  
  
public class SomeClass
{  
}  
```  
  
 Com <xref:System.Runtime.Serialization.DataContractSerializer.PreserveObjectReferences%2A> definido como `false` (o padrão), o seguinte XML é gerado:  
  
```xml  
<X>  
   <A>contents of someInstance</A>  
   <B>contents of someInstance</B>  
</X>  
```  
  
 Com <xref:System.Runtime.Serialization.DataContractSerializer.PreserveObjectReferences%2A> definido como `true` , o seguinte XML é gerado:  
  
```xml  
<X>  
   <A id="1">contents of someInstance</A>  
   <B ref="1"></B>  
</X>  
```  
  
 No entanto, <xref:System.Runtime.Serialization.XsdDataContractExporter> o não descreve os `id` `ref` atributos e em seu esquema, mesmo quando a `preserveObjectReferences` propriedade é definida como `true` .  
  
## <a name="using-isreference"></a>Usando IsReference  

 Para gerar informações de referência de objeto que são válidas de acordo com o esquema que a descreve, aplique o <xref:System.Runtime.Serialization.DataContractAttribute> atributo a um tipo e defina o <xref:System.Runtime.Serialization.DataContractAttribute.IsReference%2A> sinalizador como `true` . O exemplo a seguir modifica a classe `X` no exemplo anterior adicionando `IsReference` :  
  
```csharp
[DataContract(IsReference=true)]
public class X
{  
     SomeClass someInstance = new SomeClass();
     [DataMember]
     public SomeClass A = someInstance;
     [DataMember]
     public SomeClass B = someInstance;
}
  
public class SomeClass
{
}  
````

 O XML gerado é o seguinte:  

```xml
<X>  
    <A id="1">
        <Value>contents of A</Value>  
    </A>
    <B ref="1"></B>  
</X>
```  
  
 O uso `IsReference` de garante a conformidade com o ida e volta da mensagem. Sem ele, quando um tipo é gerado a partir do esquema, a saída XML para esse tipo não é necessariamente compatível com o esquema assumido originalmente. Em outras palavras, embora os `id` `ref` atributos e tenham sido serializados, o esquema original poderia ter bloqueado esses atributos (ou todos os atributos) da ocorrência no XML. Com `IsReference` aplicado a um membro de dados, o membro continua a ser reconhecido como *referenciable* quando movimentado por ida e volta.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.CollectionDataContractAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute.IsReference?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.CollectionDataContractAttribute.IsReference?displayProperty=nameWithType>
