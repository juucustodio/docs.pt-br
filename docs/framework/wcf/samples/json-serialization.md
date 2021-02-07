---
description: 'Saiba mais sobre: exemplo de DataContractJsonSerializer'
title: Exemplo de DataContractJsonSerializer
ms.date: 03/30/2017
ms.assetid: 3c2c4747-7510-4bdf-b4fe-64f98428ef4a
ms.openlocfilehash: 258cd38f9ee532e5d750b4cabaa4214366835be7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99726345"
---
# <a name="datacontractjsonserializer-sample"></a>Exemplo de DataContractJsonSerializer

> [!NOTE]
> Este exemplo é para <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> . Para a maioria dos cenários que envolvem a serialização e desserialização do JSON, recomendamos as APIs na [System.Text.Jsno namespace](../../../standard/serialization/system-text-json-overview.md).

O <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> dá suporte aos mesmos tipos que o <xref:System.Runtime.Serialization.DataContractSerializer>. O formato de dados JSON é especialmente útil ao escrever aplicativos Web de estilo AJAX (Asynchronous JavaScript and XML). O suporte ao AJAX no Windows Communication Foundation (WCF) é otimizado para uso com o ASP.NET AJAX por meio do controle ScriptManager. Para obter exemplos de como usar o Windows Communication Foundation (WCF) com o ASP.NET AJAX, consulte os [exemplos do AJAX](ajax.md).  
  
Os procedimentos de instalação e as instruções de compilação para esse exemplo estão localizadas no final deste tópico.  
  
Este exemplo usa um contrato de dados `Person` para demonstrar a serialização e a desserialização.  

```csharp
[DataContract]
class Person
{
    [DataMember]
    internal string name;

    [DataMember]
    internal int age;
}
```

 Para serializar uma instância do tipo `Person` para JSON, crie primeiro o <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> e use o método `WriteObject` para gravar dados JSON em um fluxo.  

```csharp
Person p = new Person();
//Set up Person object...
MemoryStream stream1 = new MemoryStream();
DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(Person));
ser.WriteObject(stream1, p);
```

 O fluxo de memória contém dados JSON válidos.
  
```json  
{"age":42,"name":"John"}  
```  
  
 O exemplo demonstra a desserialização de dados JSON em um objeto. Em seguida, você volta o fluxo e chama `ReadObject`.  

```csharp
Person p2 = (Person)ser.ReadObject(stream1);
```

 Examinar o objeto `p2` revela que os dados JSON foram desserializados corretamente.  
  
> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Ajax\JsonSerialization`  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar e executar o exemplo  
  
1. Crie a solução JsonSerialization. sln, conforme descrito em [criando os exemplos de Windows Communication Foundation](building-the-samples.md).  
  
2. Execute o aplicativo de console resultante.  
