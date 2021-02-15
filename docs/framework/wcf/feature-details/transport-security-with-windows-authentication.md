---
title: Segurança de transporte com autenticação do Windows
description: Examine este cenário, que mostra um cliente/serviço WCF protegido pela segurança do Windows. Neste exemplo, um serviço de intranet exibe informações de recursos humanos.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 96dd26e2-46e7-4de0-9a29-4fcb05bf187b
ms.openlocfilehash: 47f5a2a3b2c8815e2ccb0cc4d4bf3c408f4992e2
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96251731"
---
# <a name="transport-security-with-windows-authentication"></a>Segurança de transporte com autenticação do Windows

O cenário a seguir mostra um cliente Windows Communication Foundation (WCF) e um serviço protegido pela segurança do Windows. Para obter mais informações sobre programação, consulte [como proteger um serviço com credenciais do Windows](../how-to-secure-a-service-with-windows-credentials.md).  
  
 Um serviço Web de intranet exibe informações de recursos humanos. O cliente é um aplicativo do Windows Form. O aplicativo é implantado em um domínio com um controlador Kerberos protegendo o domínio.  
  
 ![Segurança de transporte com autenticação do Windows](./media/transport-security-with-windows-authentication/secured-windows-authentication.gif)  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Modo de segurança|Transport|  
|Interoperabilidade|Somente WCF|  
|Autenticação (servidor)<br /><br /> Autenticação (cliente)|Sim (usando a autenticação integrada do Windows)<br /><br /> Sim (usando a autenticação integrada do Windows)|  
|Integridade|Sim|  
|Confidencialidade|Yes|  
|Transport|Virtual. Protocol|  
|Associação|<xref:System.ServiceModel.NetTcpBinding>|  
  
## <a name="service"></a>Serviço  

 O código e a configuração a seguir devem ser executados de forma independente. Realize uma destas ações:  
  
- Crie um serviço autônomo usando o código sem configuração.  
  
- Crie um serviço usando a configuração fornecida, mas não defina nenhum ponto de extremidade.  
  
### <a name="code"></a>Código  

 O código a seguir mostra como criar um ponto de extremidade de serviço que usa uma segurança do Windows.  
  
 [!code-csharp[C_SecurityScenarios#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#3)]
 [!code-vb[C_SecurityScenarios#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#3)]  
  
### <a name="configuration"></a>Configuração  

 A configuração a seguir pode ser usada em vez do código para configurar o ponto de extremidade de serviço:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors />  
    <services>  
      <service behaviorConfiguration="" name="ServiceModel.Calculator">  
        <endpoint address="net.tcp://localhost:8008/Calculator"
                  binding="netTcpBinding"  
          bindingConfiguration="WindowsClientOverTcp"
                  name="WindowsClientOverTcp"  
                  contract="ServiceModel.ICalculator" />  
      </service>  
    </services>  
    <bindings>  
      <netTcpBinding>  
        <binding name="WindowsClientOverTcp">  
          <security mode="Transport">  
            <transport clientCredentialType="Windows" />  
          </security>  
        </binding>  
      </netTcpBinding>  
    </bindings>  
    <client />  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a>Cliente  

 O código e a configuração a seguir devem ser executados de forma independente. Realize uma destas ações:  
  
- Crie um cliente autônomo usando o código (e o código do cliente).  
  
- Crie um cliente que não defina nenhum endereço de ponto de extremidade. Em vez disso, use o construtor do cliente que usa o nome da configuração como um argumento. Por exemplo:  
  
     [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
     [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]  
  
### <a name="code"></a>Código  

 O código a seguir cria o cliente. A associação é configurada para usar a segurança do modo de transporte, com o transporte TCP, com o tipo de credencial do cliente definido como Windows.  
  
 [!code-csharp[C_SecurityScenarios#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#4)]
 [!code-vb[C_SecurityScenarios#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#4)]  
  
### <a name="configuration"></a>Configuração  

 A configuração a seguir pode ser usada em vez do código para criar o cliente.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <netTcpBinding>  
        <binding name="NetTcpBinding_ICalculator" >  
          <security mode="Transport">  
            <transport clientCredentialType="Windows" />  
          </security>  
        </binding>  
      </netTcpBinding>  
    </bindings>  
    <client>  
      <endpoint address="net.tcp://localhost:8008/Calculator"
                binding="netTcpBinding"
                bindingConfiguration="NetTcpBinding_ICalculator"
                contract="ICalculator"  
                name="NetTcpBinding_ICalculator">  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>Veja também

- [Visão geral de segurança](security-overview.md)
- [Como: proteger um serviço com credenciais do Windows](../how-to-secure-a-service-with-windows-credentials.md)
- [Modelo de segurança para o Windows Server app Fabric](/previous-versions/appfabric/ee677202(v=azure.10))
