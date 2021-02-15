---
description: 'Saiba mais sobre: criação de serviços interoperáveis 1,1 do WS-I Basic Profile'
title: Criando serviços interoperáveis de perfil básico de WS-I 1.1
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- configuration [WCF], interoperable services
ms.assetid: 91b70a21-8f5c-4679-808c-2ed5fa6b2013
ms.openlocfilehash: 46e2d925dfe431957198b1d53b40d28adf6fb1c4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646173"
---
# <a name="creating-ws-i-basic-profile-11-interoperable-services"></a>Criando serviços interoperáveis de perfil básico de WS-I 1.1

Para configurar um ponto de extremidade de serviço WCF para ser interoperável com clientes do serviço Web ASP.NET:  
  
- Use o <xref:System.ServiceModel.BasicHttpBinding?displayProperty=nameWithType> tipo como o tipo de associação para o ponto de extremidade de serviço.  
  
- Não usar recursos de retorno de chamada e de contrato de sessão ou comportamentos de transação em seu ponto de extremidade de serviço  
  
Opcionalmente, você pode habilitar o suporte para HTTPS e autenticação de cliente de nível de transporte na associação.  
  
Os seguintes recursos da <xref:System.ServiceModel.BasicHttpBinding> classe exigem funcionalidade além do WS-I Basic Profile 1,1:  
  
- Codificação de mensagem MTOM (mecanismo de otimização de transmissão de mensagens) controlada pela <xref:System.ServiceModel.BasicHttpBinding.MessageEncoding%2A?displayProperty=nameWithType> propriedade. Deixe essa propriedade em seu valor padrão, que é <xref:System.ServiceModel.WSMessageEncoding.Text?displayProperty=nameWithType> não usar MTOM.  
  
- A segurança de mensagem controlada pelo <xref:System.ServiceModel.BasicHttpBinding.Security%2A?displayProperty=nameWithType> valor fornece WS-Security suporte compatível com o perfil de segurança básico WS-I 1,0. Deixe essa propriedade em seu valor padrão, que é <xref:System.ServiceModel.SecurityMode.Transport?displayProperty=nameWithType> para não usar o WS-Security.  
  
Para disponibilizar os metadados de um serviço WCF para o ASP.NET, use a ferramenta de geração de cliente do serviço Web: [Web Services Description Language Tool (Wsdl.exe)](/previous-versions/dotnet/netframework-4.0/7h3ystb6(v=vs.100)), [Web Services Discovery Tool (Disco.exe)](/previous-versions/dotnet/netframework-4.0/cy2a3ybs(v=vs.100))e o recurso **Add Web Reference** no Visual Studio. Habilitar publicação de metadados. Para obter mais informações, consulte [publicando pontos de extremidade de metadados](publishing-metadata-endpoints.md).  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  

 O código de exemplo a seguir demonstra como adicionar um ponto de extremidade WCF compatível com clientes de serviço Web ASP.NET em código e, como alternativa, em um arquivo de configuração.  
  
### <a name="code"></a>Código  

 [!code-csharp[C_HowTo-WCFServiceAndASMXClient#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/cs/program.cs#0)]
 [!code-vb[C_HowTo-WCFServiceAndASMXClient#0](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/vb/program.vb#0)]  
 [!code-xml[C_HowTo-WCFServiceAndASMXClient#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/common/app.config#1)]  
  
## <a name="see-also"></a>Consulte também

- [Interoperabilidade com serviços Web do ASP.NET](./feature-details/interop-with-aspnet-web-services.md)
