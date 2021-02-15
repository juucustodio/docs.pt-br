---
description: 'Saiba mais sobre: como usar o moniker do serviço Windows Communication Foundation sem registro'
title: 'Como: usar o moniker de serviço do Windows Communication Foundation sem registro'
ms.date: 03/30/2017
helpviewer_keywords:
- COM [WCF], service monikers without registration
ms.assetid: ee3cf5c0-24f0-4ae7-81da-73a60de4a1a8
ms.openlocfilehash: ed3ea221bc32c4334f609b6740fa10bb63cb2830
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99632380"
---
# <a name="how-to-use-the-windows-communication-foundation-service-moniker-without-registration"></a>Como: usar o moniker de serviço do Windows Communication Foundation sem registro

Para se conectar e se comunicar com um serviço Windows Communication Foundation (WCF), um aplicativo cliente WCF deve ter os detalhes do endereço de serviço, a configuração de associação e o contrato de serviço.  
  
 O moniker do serviço WCF normalmente Obtém o contrato necessário por meio do registro anterior dos tipos de atributo necessários, mas pode haver casos em que isso não é viável. No lugar do registro, o moniker pode obter a definição do contrato na forma de um documento WSDL (Web Services Definition Language), por meio do uso do `wsdl` parâmetro ou da troca de metadados, por meio do uso do `mexAddress` parâmetro.  
  
 Isso permite cenários como a distribuição de uma planilha do Excel em que alguns dos valores de célula são calculados por meio de interações de serviço Web. Nesse cenário, talvez não seja possível registrar o assembly do contrato de serviço em todos os clientes que possam abrir o documento. O `wsdl` parâmetro ou o `mexAddress` parâmetro habilita uma solução independente.  
  
> [!NOTE]
> A autenticação mútua deve ser usada para proteger contra violação ou falsificação de solicitação e resposta. Especificamente, é importante que os clientes tenham certeza de que o ponto de extremidade de troca de metadados que está respondendo é a parte confiável pretendida.  
  
## <a name="example"></a>Exemplo  

 Este exemplo mostra o uso do moniker de serviço com um contrato MEX. Um serviço com o contrato a seguir é exposto com uma wsHttpBinding.  
  
```csharp
using System.ServiceModel;  
  
// ...
  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Demo")]  
public interface IAffiliate  
{  
    [OperationContract]  
    bool NewAffiliate(string ID, string company, string fullname, string accountsCode);  
    [OperationContract]  
    bool RemoveAffiliate(string ID);  
    [OperationContract]  
    double RevenueCheckMonthly(ref string ID);  
    [OperationContract]  
    double RevenueCheckTotal(ref string ID);  
}  
```  
  
 Para construir um cliente WCF para o serviço remoto, o seguinte exemplo de cadeia de caracteres do moniker pode ser usado.  
  
```
service4:mexAddress="http://servername/Affiliates/service.svc/mex",  
address="http://servername/Affiliates/service.svc",  
contract=IAffiliate, contractNamespace=http://Microsoft.ServiceModel.Demo,  
binding=WSHttpBinding_IAffiliate, bindingNamespace=http://tempuri.org/  
```  
  
 Durante a execução do aplicativo cliente, o cliente executa um `WS-MetadataExchange` com o fornecido `mexAddress` . Isso pode retornar os detalhes de endereço, associação e contrato para vários serviços. Os `address` `contract` parâmetros,, e `contractNamespace` `binding` `bindingNamespace` são usados para identificar o serviço pretendido. Depois que esses parâmetros forem correspondidos, o moniker construirá um cliente WCF com a definição de contrato apropriada e as chamadas poderão ser feitas usando o cliente WCF, como com o contrato tipado.  
  
> [!NOTE]
> Se o moniker estiver malformado ou se o serviço estiver indisponível, a chamada para `GetObject` retornará um erro dizendo "sintaxe inválida". Se você receber esse erro, verifique se o moniker que você está usando está correto e se o serviço está disponível.  
  
## <a name="see-also"></a>Consulte também

- [Como: registrar e configurar um moniker de serviço](how-to-register-and-configure-a-service-moniker.md)
