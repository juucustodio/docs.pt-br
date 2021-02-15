---
description: 'Saiba mais sobre: como especificar uma associação de serviço no código'
title: 'Como: especificar uma associação de serviço no código'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 67ab5dd8-79c1-4e62-aa75-828ea918a53a
ms.openlocfilehash: 744919fee4ec28d7df4581ac1d608d1fa9e99a29
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755935"
---
# <a name="how-to-specify-a-service-binding-in-code"></a>Como: especificar uma associação de serviço no código

Neste exemplo, um `ICalculator` contrato é definido para um serviço de calculadora, o serviço é implementado na `CalculatorService` classe e, em seguida, seu ponto de extremidade é definido no código, onde é especificado que o serviço deve usar a <xref:System.ServiceModel.BasicHttpBinding> classe.  
  
 Geralmente, é a prática recomendada especificar a associação e as informações de endereço de forma declarativa na configuração, em vez de imperativa no código. A definição de pontos de extremidade no código geralmente não é prática porque as associações e os endereços para um serviço implantado são normalmente diferentes daqueles usados enquanto o serviço está sendo desenvolvido. Em geral, manter as informações de vinculação e endereçamento do código permite que elas sejam alteradas sem a necessidade de recompilar ou reimplantar o aplicativo.  
  
 Para obter uma descrição de como configurar esse serviço usando elementos de configuração em vez de código, consulte [como especificar uma associação de serviço na configuração](how-to-specify-a-service-binding-in-configuration.md).  
  
### <a name="to-specify-in-code-to-use-the-basichttpbinding-for-the-service"></a>Para especificar no código usar o BasicHttpBinding para o serviço  
  
1. Defina um contrato de serviço para o tipo de serviço.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#1)]
     [!code-vb[C_HowTo_CodeServiceBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#1)]  
  
2. Implemente o contrato de serviço em uma classe de serviço.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#2)]
     [!code-vb[C_HowTo_CodeServiceBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#2)]  
  
3. No aplicativo de hospedagem, crie o endereço base para o serviço e a associação a ser usada com o serviço.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#3)]
     [!code-vb[C_HowTo_CodeServiceBinding#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#3)]  
  
4. Crie o host para o serviço, adicione o ponto de extremidade e, em seguida, abra o host.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#4)]
     [!code-vb[C_HowTo_CodeServiceBinding#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#4)]  
  
### <a name="to-modify-the-default-values-of-the-binding-properties"></a>Para modificar os valores padrão das propriedades de associação  
  
1. Para modificar um dos valores de propriedade padrão da <xref:System.ServiceModel.BasicHttpBinding> classe, defina o valor da propriedade na associação ao novo valor antes de criar o host. Por exemplo, para alterar os valores de tempo limite de abertura e fechamento padrão de 1 minuto para 2 minutos, use o seguinte.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#5)]
     [!code-vb[C_HowTo_CodeServiceBinding#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#5)]  
  
## <a name="see-also"></a>Consulte também

- [Usando associações para configurar serviços e clientes](using-bindings-to-configure-services-and-clients.md)
- [Especificando um endereço de ponto de extremidade](specifying-an-endpoint-address.md)
