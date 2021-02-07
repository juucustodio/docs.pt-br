---
description: 'Saiba mais sobre: critérios de localização personalizados'
title: Critérios de localização personalizados
ms.date: 03/30/2017
ms.assetid: b2723929-8829-424d-8015-a37ba2ab4f68
ms.openlocfilehash: 71082f303e3464e27e1bad3995d20b5f6cf7d647
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99732560"
---
# <a name="custom-find-criteria"></a>Critérios de localização personalizados

Este exemplo demonstra como criar uma correspondência de escopo personalizada usando a lógica e como implementar um serviço de descoberta personalizado. Os clientes usam a funcionalidade de correspondência de escopo personalizada para refinar e criar mais sobre a funcionalidade localizar fornecida pelo sistema da descoberta do WCF. O cenário abordado por este exemplo é o seguinte:  
  
1. Um cliente está procurando um serviço de calculadora.  
  
2. Para refinar sua pesquisa, o cliente deve usar uma regra de correspondência de escopo personalizada.  
  
3. De acordo com essa regra, um serviço responde ao cliente se seu ponto de extremidade corresponde a qualquer um dos escopos especificados pelo cliente.  
  
## <a name="demonstrates"></a>Demonstra  
  
- Criando um serviço de descoberta personalizado.  
  
- Implementando uma correspondência de escopo personalizado por algoritmo.  
  
## <a name="discussion"></a>Discussão  

 O cliente está procurando "ou" critérios de correspondência de tipo. Um serviço responde de volta se os escopos em seus pontos de extremidade corresponderem a qualquer um dos escopos fornecidos pelo cliente. Nesse caso, o cliente está procurando um serviço de calculadora que tenha qualquer um dos escopos na lista a seguir:  
  
1. `net.tcp://Microsoft.Samples.Discovery/RedmondLocation`  
  
2. `net.tcp://Microsoft.Samples.Discovery/SeattleLocation`  
  
3. `net.tcp://Microsoft.Samples.Discovery/PortlandLocation`  
  
 Para fazer isso, o cliente direciona os serviços para usar uma regra de correspondência de escopo personalizada, passando uma correspondência de escopo personalizado por URI. Para facilitar a correspondência de escopo personalizado, o serviço deve usar um serviço de descoberta personalizado que entenda a regra de correspondência de escopo personalizada e implemente a lógica correspondente associada.  
  
 No projeto cliente, abra o arquivo Program.cs. Observe que o `ScopeMatchBy` campo do `FindCriteria` objeto é definido como um URI específico. Esse identificador é enviado para o serviço. Se o serviço não entender essa regra, ele ignorará a solicitação de localização do cliente.  
  
 Abra o projeto de serviço. Três arquivos são usados para implementar o serviço de descoberta personalizado:  
  
1. **AsyncResult.cs**: essa é a implementação do `AsyncResult` que é exigida pelos métodos de descoberta.  
  
2. **CustomDiscoveryService.cs**: esse arquivo implementa o serviço de descoberta personalizado. A implementação estende a <xref:System.ServiceModel.Discovery.DiscoveryService> classe e substitui os métodos necessários. Observe a implementação do <xref:System.ServiceModel.Discovery.DiscoveryService.OnBeginFind%2A> método. O método verifica se a correspondência de escopo personalizado por regra foi especificada pelo cliente. Esse é o mesmo URI personalizado que o cliente especificou anteriormente. Se a regra personalizada for especificada, o caminho de código que implementa a lógica de correspondência "ou" é seguido.  
  
     Essa lógica personalizada passa por todos os escopos em cada um dos pontos de extremidade que o serviço tem. Se qualquer um dos escopos do ponto de extremidade corresponder a qualquer um dos escopos fornecidos pelo cliente, o serviço de descoberta adicionará esse ponto de extremidade à resposta que é enviada de volta para o cliente.  
  
3. **CustomDiscoveryExtension.cs**: a última etapa da implementação do serviço de descoberta é conectar essa implementação do serviço de descoberta personalizado ao host de serviço. A classe auxiliar usada aqui é a `CustomDiscoveryExtension` classe. Essa classe estende a <xref:System.ServiceModel.Discovery.DiscoveryServiceExtension> classe. O usuário deve substituir o <xref:System.ServiceModel.Discovery.DiscoveryServiceExtension.GetDiscoveryService%2A> método. Nesse caso, o método retorna uma instância do serviço de descoberta personalizado que foi criado antes. `PublishedEndpoints` é um <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> que contém todos os pontos de extremidade do aplicativo que são adicionados ao <xref:System.ServiceModel.ServiceHost> . O serviço de descoberta personalizado usa isso para preencher sua lista interna. Um usuário também pode adicionar outros metadados de ponto de extremidade.  
  
 Por fim, abra Program.cs. Observe que <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> e `CustomDiscoveryExtension` são adicionados ao host. Depois que isso for feito e o host tiver um ponto de extremidade sobre o qual receber mensagens de descoberta, o aplicativo poderá usar o serviço de descoberta personalizado.  
  
 Observe que o cliente é capaz de encontrar o serviço sem saber seu endereço.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo  
  
1. Abra a solução que contém o projeto.  
  
2. Compile o projeto.  
  
3. Execute o aplicativo de serviço.  
  
4. Execute o aplicativo cliente.  
  
> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Discovery\CustomFindCriteria`
