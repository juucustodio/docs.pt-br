---
description: 'Saiba mais sobre: implementação de contratos de serviço'
title: Implementando contratos de serviço
ms.date: 03/30/2017
helpviewer_keywords:
- implementing service contracts [WCF]
ms.assetid: aefb6f56-47e3-4f24-ab0a-9bc07bf9885f
ms.openlocfilehash: 4510c9e7b9ea3a98a37d528af4064f0e73bea89b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99752490"
---
# <a name="implementing-service-contracts"></a>Implementando contratos de serviço

Um serviço é uma classe que expõe a funcionalidade disponível para clientes em um ou mais pontos de extremidade. Para criar um serviço, escreva uma classe que implemente um contrato de Windows Communication Foundation (WCF). É possível fazer isso de duas formas. Você pode definir o contrato separadamente como uma interface e, em seguida, criar uma classe que implementa essa interface. Como alternativa, você pode criar a classe e o contrato diretamente colocando o <xref:System.ServiceModel.ServiceContractAttribute> atributo na própria classe e o <xref:System.ServiceModel.OperationContractAttribute> atributo nos métodos disponíveis para os clientes do serviço.  
  
## <a name="creating-a-service-class"></a>Criando uma classe de serviço  

 Veja a seguir um exemplo de um serviço que implementa um `IMath` contrato que foi definido separadamente.  
  
```csharp  
// Define the IMath contract.  
[ServiceContract]  
public interface IMath  
{  
    [OperationContract]
    double Add(double A, double B);  
  
    [OperationContract]  
    double Multiply (double A, double B);  
}  
  
// Implement the IMath contract in the MathService class.  
public class MathService : IMath  
{  
    public double Add (double A, double B) { return A + B; }  
    public double Multiply (double A, double B) { return A * B; }  
}  
```  
  
 Como alternativa, um serviço pode expor um contrato diretamente. Veja a seguir um exemplo de uma classe de serviço que define e implementa um `MathService` contrato.  
  
```csharp  
// Define the MathService contract directly on the service class.  
[ServiceContract]  
class MathService  
{  
    [OperationContract]  
    public double Add(double A, double B) { return A + B; }  
    [OperationContract]  
    private double Multiply (double A, double B) { return A * B; }  
}  
```  
  
 Observe que os serviços anteriores expõem contratos diferentes porque os nomes de contrato são diferentes. No primeiro caso, o contrato exposto é denominado " `IMath` " enquanto, no segundo caso, o contrato é denominado " `MathService` ".  
  
 Você pode definir algumas coisas nos níveis de implementação de serviço e operação, como simultaneidade e instanciação. Para obter mais informações, consulte [projetando e implementando serviços](designing-and-implementing-services.md).  
  
 Depois de implementar um contrato de serviço, você deve criar um ou mais pontos de extremidade para o serviço. Para obter mais informações, consulte [visão geral da criação de ponto de extremidade](endpoint-creation-overview.md). Para obter mais informações sobre como executar um serviço, consulte [serviços de hospedagem](hosting-services.md).  
  
## <a name="see-also"></a>Consulte também

- [Serviços de implantação e projeção](designing-and-implementing-services.md)
- [Como: criar um serviço com uma classe de contrato](./feature-details/how-to-create-a-wcf-contract-with-a-class.md)
- [Como: criar um serviço com interface de contrato](./feature-details/how-to-create-a-service-with-a-contract-interface.md)
- [Especificando comportamento de tempo de execução de serviço](specifying-service-run-time-behavior.md)
