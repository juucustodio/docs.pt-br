---
description: 'Saiba mais sobre: filtros personalizados'
title: Filtros personalizados
ms.date: 03/30/2017
ms.assetid: 97cf247d-be0a-4057-bba9-3be5c45029d5
ms.openlocfilehash: 95a419823cf69575f951c0984e2136f9e7afca56
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99704973"
---
# <a name="custom-filters"></a>Filtros personalizados

Os filtros personalizados permitem que você defina a lógica correspondente que não pode ser realizada usando os filtros de mensagens fornecidos pelo sistema. Por exemplo, você pode criar um filtro personalizado que faz hash de um determinado elemento de mensagem e, em seguida, examina o valor para determinar se o filtro deve retornar true ou false.  
  
## <a name="implementation"></a>Implementação  

 Um filtro personalizado é uma implementação da <xref:System.ServiceModel.Dispatcher.MessageFilter> classe base abstrata. Ao implementar seu filtro personalizado, o construtor pode opcionalmente aceitar um único parâmetro de cadeia de caracteres. Esse parâmetro contém as informações de configuração que são passadas para o Construtor MessageFilter para fornecer qualquer valor ou configuração que o filtro precisa em tempo de execução para executar correspondências. Por exemplo, isso pode ser usado para fornecer um valor que o filtro Procure dentro da mensagem que está sendo avaliada. O exemplo a seguir demonstra uma implementação básica de um filtro de mensagem personalizado que aceita um parâmetro de cadeia de caracteres:  
  
```csharp  
public class MyMessageFilter: MessageFilter  
{  
    string filterData;  
    public MyMessageFilter(string filterData)  
    {  
        if(string.IsNullOrEmpty(filterData)  
            throw new ArgumentNullException("filterData");  
        this.filterData=filterData;  
    }  
    public override bool Match(System.ServiceModel.Channels.Message message)  
    {  
        ...  
        return retValue;  
    }  
    public override bool Match(System.ServiceModel.Channels.MessageBuffer buffer)  
    {  
        ...  
        return retValue;  
    }  
}  
```  
  
> [!NOTE]
> Em uma implementação real, os métodos de correspondência contêm a lógica que examinará a mensagem para determinar se esse filtro de mensagem deve retornar **verdadeiro** ou **falso**.  
  
### <a name="performance"></a>Desempenho  

 Ao implementar um filtro personalizado, é importante levar em consideração o período máximo de tempo necessário para que o filtro conclua a avaliação de uma mensagem. Uma vez que uma mensagem pode ser avaliada em vários filtros antes que uma correspondência seja encontrada, é importante garantir que a solicitação do cliente não expire antes que todos os filtros possam ser avaliados. Portanto, um filtro personalizado deve conter apenas o código necessário para avaliar o conteúdo ou os atributos de uma mensagem a fim de determinar se ele corresponde aos critérios de filtro.  
  
 Em geral, você deve evitar o seguinte ao implementar um filtro personalizado:  
  
- E/s, como salvar dados em disco ou em um banco de dados.  
  
- Processamento desnecessário, como looping sobre vários registros em um documento.  
  
- Operações de bloqueio, como chamadas que envolvem a obtenção de um bloqueio em recursos compartilhados ou a execução de pesquisas em um banco de dados.  
  
 Antes de usar um filtro personalizado em um ambiente de produção, você deve executar testes de desempenho para determinar a duração média de tempo que o filtro leva para avaliar uma mensagem. Quando combinado com o tempo médio de processamento dos outros filtros usados na tabela de filtro, isso permitirá que você determine com precisão o valor de tempo limite máximo que deve ser especificado pelo aplicativo cliente.  
  
## <a name="usage"></a>Uso  

 Para usar o filtro personalizado com o serviço de roteamento, você deve adicioná-lo à tabela de filtros especificando uma nova entrada de filtro do tipo "Custom", o nome do tipo totalmente qualificado do filtro de mensagem e o nome do seu assembly.  Assim como ocorre com outros MessageFilters, você pode especificar a cadeia de caracteres filterData que será passada para o construtor do filtro personalizado.  
  
 Os exemplos a seguir demonstram como usar um filtro personalizado com o serviço de roteamento:  
  
```xml  
<!--ROUTING SECTION -->  
<routing>  
  <filters>  
    <filter name="CustomFilter1" filterType="Custom"
            customType="CustomAssembly.MyMessageFilter,
            CustomAssembly" filterData="custom data" />  
  </filters>  
  <filterTables>  
    <table name="routingTable1">  
      <filters>  
        <add filterName="CustomFilter1" endpointName="CalculatorService" />  
      </filters>  
    </table>  
  </filterTables>  
</routing>  
```  
  
```csharp  
RoutingConfiguration rc = new RoutingConfiguration();  
List<ServiceEndpoint> endpointList = new List<ServiceEndpoint>();  
endpointList.Add(client);  
rc.FilterTable.Add(new MyMessageFilter("CustomData"), endpointList);  
```
