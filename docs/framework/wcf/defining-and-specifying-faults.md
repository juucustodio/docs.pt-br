---
description: 'Saiba mais sobre: definindo e especificando falhas'
title: Definindo e especificando falhas
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- handling faults [WCF], specifying
- handling faults [WCF], defining
ms.assetid: c00c84f1-962d-46a7-b07f-ebc4f80fbfc1
ms.openlocfilehash: cf8c4dafaf3958cbb0be6fd096049d13f70685bd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646108"
---
# <a name="defining-and-specifying-faults"></a>Definindo e especificando falhas

Falhas de SOAP transmitem informações de condição de erro de um serviço para um cliente e, no caso duplex, de um cliente para um serviço de forma interoperável. Este tópico discute quando e como definir o conteúdo de falha personalizado e especificar quais operações podem retorná-los. Para obter mais informações sobre como um serviço, ou cliente duplex, pode enviar essas falhas e como um aplicativo cliente ou de serviço lida com essas falhas, consulte [enviando e recebendo falhas](sending-and-receiving-faults.md). Para obter uma visão geral do tratamento de erros em aplicativos Windows Communication Foundation (WCF), consulte [especificando e manipulando falhas em contratos e serviços](specifying-and-handling-faults-in-contracts-and-services.md).  
  
## <a name="overview"></a>Visão geral  

 As falhas de SOAP declaradas são aquelas em que uma operação tem um <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType> que especifica um tipo de falha SOAP personalizado. As falhas de SOAP não declaradas são aquelas que não são especificadas no contrato para uma operação. Este tópico ajuda você a identificar essas condições de erro e a criar um contrato de falha para o serviço que os clientes podem usar para lidar corretamente com essas condições de erro quando notificado por falhas de SOAP personalizadas. As tarefas básicas são, em ordem:  
  
1. Defina as condições de erro sobre as quais um cliente do seu serviço deve saber.  
  
2. Defina o conteúdo personalizado das falhas de SOAP para essas condições de erro.  
  
3. Marque suas operações para que as falhas SOAP específicas que elas lançam sejam expostas aos clientes em WSDL.  
  
### <a name="defining-error-conditions-that-clients-should-know-about"></a>Definindo condições de erro que os clientes devem saber sobre  

 Falhas de SOAP são mensagens descritas publicamente que contêm informações de falha para uma operação específica. Como eles são descritos junto com outras mensagens de operação em WSDL, os clientes sabem e, portanto, esperam lidar com essas falhas ao invocar uma operação. Mas como os serviços WCF são escritos em código gerenciado, decidir quais condições de erro no código gerenciado devem ser convertidas em falhas e retornadas ao cliente oferece a oportunidade de separar as condições de erro e os bugs em seu serviço da conversa de erro formal que você tem com um cliente.  
  
 Por exemplo, o exemplo de código a seguir mostra uma operação que usa dois inteiros e retorna outro inteiro. Várias exceções podem ser lançadas aqui, portanto, ao criar o contrato de falha, você deve determinar quais condições de erro são importantes para o cliente. Nesse caso, o serviço deve detectar a <xref:System.DivideByZeroException?displayProperty=nameWithType> exceção.  
  
```csharp  
[ServiceContract]  
public class CalculatorService  
{  
    [OperationContract]
    int Divide(int a, int b)  
    {  
      if (b==0) throw new Exception("Division by zero!");  
      return a/b;  
    }  
}  
```  
  
```vb
<ServiceContract> _
Public Class CalculatorService
    <OperationContract> _
    Public Function Divide(a As Integer, b As Integer) As Integer
        If b = 0 Then Throw New DivideByZeroException("Division by zero!")
        Return a / b
    End Function
End Class
```
  
 No exemplo anterior, a operação pode retornar uma falha de SOAP personalizada que é específica para dividir por zero, uma falha personalizada específica para operações matemáticas, mas que contém informações específicas para dividir por zero, várias falhas para várias situações de erro diferentes ou nenhuma falha SOAP.  
  
### <a name="define-the-content-of-error-conditions"></a>Definir o conteúdo das condições de erro  

 Depois que uma condição de erro for identificada como uma que possa retornar de forma útil uma falha de SOAP personalizada, a próxima etapa será definir o conteúdo dessa falha e garantir que a estrutura de conteúdo possa ser serializada. O exemplo de código na seção anterior mostra um erro específico para uma `Divide` operação, mas se houver outras operações no `Calculator` serviço, uma única falha SOAP personalizada poderá informar ao cliente de todas as condições de erro da calculadora, `Divide` incluídas. O exemplo de código a seguir mostra a criação de uma falha de SOAP personalizada, `MathFault` , que pode relatar erros feitos usando todas as operações matemáticas, incluindo `Divide` . Embora a classe possa especificar uma operação (a `Operation` Propriedade) e um valor que descreva o problema (a `ProblemType` Propriedade), a classe e essas propriedades devem ser serializáveis para serem transferidas para o cliente em uma falha de SOAP personalizada. Portanto, os <xref:System.Runtime.Serialization.DataContractAttribute?displayProperty=nameWithType> <xref:System.Runtime.Serialization.DataMemberAttribute?displayProperty=nameWithType> atributos e são usados para tornar o tipo e suas propriedades serializáveis e o mais interoperável possível.  
  
 [!code-csharp[Faults#2](../../../samples/snippets/csharp/VS_Snippets_CFX/faults/cs/service.cs#2)]
 [!code-vb[Faults#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faults/vb/service.vb#2)]  
  
 Para obter mais informações sobre como garantir que seus dados sejam serializáveis, consulte [especificando transferência de dados em contratos de serviço](./feature-details/specifying-data-transfer-in-service-contracts.md). Para obter uma lista do suporte de serialização que o <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> fornece, consulte [tipos com suporte pelo serializador de contrato de dados](./feature-details/types-supported-by-the-data-contract-serializer.md).  
  
### <a name="mark-operations-to-establish-the-fault-contract"></a>Marcar operações para estabelecer o contrato de falha  

 Quando uma estrutura de dados serializável que é retornada como parte de uma falha de SOAP personalizada é definida, a última etapa é marcar o contrato de operação como lançar uma falha SOAP desse tipo. Para fazer isso, use o <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType> atributo e passe o tipo do tipo de dados personalizado que você criou. O exemplo de código a seguir mostra como usar o <xref:System.ServiceModel.FaultContractAttribute> atributo para especificar que a `Divide` operação pode retornar uma falha SOAP do tipo `MathFault` . Outras operações com base em matemática agora também podem especificar que podem retornar um `MathFault` .  
  
 [!code-csharp[Faults#1](../../../samples/snippets/csharp/VS_Snippets_CFX/faults/cs/service.cs#1)]
 [!code-vb[Faults#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faults/vb/service.vb#1)]  
  
 Uma operação pode especificar que ela retorna mais de uma falha personalizada marcando essa operação com mais de um <xref:System.ServiceModel.FaultContractAttribute> atributo.  
  
 A próxima etapa, para implementar o contrato de falha na implementação da operação, é descrita no tópico [envio e recebimento de falhas](sending-and-receiving-faults.md).  
  
#### <a name="soap-wsdl-and-interoperability-considerations"></a>Considerações sobre SOAP, WSDL e interoperabilidade  

 Em algumas circunstâncias, especialmente ao interoperar com outras plataformas, pode ser importante controlar a maneira como uma falha aparece em uma mensagem SOAP ou como ela é descrita nos metadados WSDL.  
  
 O <xref:System.ServiceModel.FaultContractAttribute> atributo tem uma <xref:System.ServiceModel.FaultContractAttribute.Name%2A> propriedade que permite o controle do nome do elemento de falha WSDL que é gerado nos metadados para essa falha.  
  
 De acordo com o padrão SOAP, uma falha pode ter um `Action` , um `Code` e um `Reason` . O `Action` é controlado pela <xref:System.ServiceModel.FaultContractAttribute.Action%2A> propriedade. A <xref:System.ServiceModel.FaultException.Code%2A> propriedade e a <xref:System.ServiceModel.FaultException.Reason%2A> propriedade são ambas propriedades da <xref:System.ServiceModel.FaultException?displayProperty=nameWithType> classe, que é a classe pai do genérico <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType> . A `Code` propriedade inclui um <xref:System.ServiceModel.FaultCode.SubCode%2A> membro.  
  
 Ao acessar não-serviços que geram falhas, existem algumas limitações. O WCF dá suporte apenas a falhas com tipos detalhados que o esquema descreve e que são compatíveis com os contratos de dados. Por exemplo, como mencionado acima, o WCF não oferece suporte a falhas que usam atributos XML em seus tipos de detalhes ou falhas com mais de um elemento de nível superior na seção de detalhes.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.FaultContractAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [Especificando e lidando com falhas em contratos e serviços](specifying-and-handling-faults-in-contracts-and-services.md)
- [Enviando e recebendo falhas](sending-and-receiving-faults.md)
- [Como: declarar falhas em contratos de serviço](how-to-declare-faults-in-service-contracts.md)
- [Noções básicas de nível de proteção](understanding-protection-level.md)
- [Como: definir a propriedade ProtectionLevel](how-to-set-the-protectionlevel-property.md)
- [Especificando transferência de dados em contratos de serviço](./feature-details/specifying-data-transfer-in-service-contracts.md)
