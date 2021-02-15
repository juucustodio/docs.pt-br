---
description: 'Saiba mais sobre: <service>'
title: <service>
ms.date: 03/30/2017
ms.assetid: 13123dd6-c4a9-4a04-a984-df184b851788
ms.openlocfilehash: c3870a170847d773996625235c75591ced75e315
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786779"
---
# \<service>

O `service` elemento contém as configurações para um serviço Windows Communication Foundation (WCF). Ele também contém pontos de extremidade que expõem o serviço.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<services>**](services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<service>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<service behaviorConfiguration="String"
         name="String">
</service>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|behaviorConfiguration|Uma cadeia de caracteres que contém o nome do comportamento do comportamento a ser usado para instanciar o serviço. O nome do comportamento deve estar no escopo no ponto em que o serviço é definido. O valor padrão é uma cadeia de caracteres vazia.|  
|name|Atributo de cadeia de caracteres necessário que especifica o tipo de serviço a ser instanciado. Essa configuração deve ser igual a um tipo válido. O formato deve ser `Namespace.Class.`|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<endpoint>](endpoint-element.md)|Uma coleção de `endpoint` elementos que expõe este serviço.|  
|[\<host>](host.md)|Especifica o host dessa instância de serviço. Esse elemento é do tipo <xref:System.ServiceModel.Configuration.HostElement> .|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<services>](services.md)|O elemento raiz de todos os elementos de configuração do WCF.|  
  
## <a name="remarks"></a>Comentários  

 Os serviços são definidos na `services` seção do arquivo de configuração. Um assembly pode conter qualquer número de serviços. Cada serviço tem sua própria `service` seção de configuração. Esta seção e seu conteúdo definem o contrato de serviço, o comportamento e os pontos de extremidade do serviço específico.  
  
 O `behaviorConfiguration` elemento também é opcional. Ele identifica o comportamento usado pelo serviço. O comportamento especificado neste atributo deve ser vinculado a um comportamento no escopo no mesmo arquivo de configuração.  
  
 Cada serviço expõe um ou mais pontos de extremidade, que tem seu próprio endereço e associação. Todas as associações usadas no arquivo de configuração devem ser definidas no escopo do arquivo. A associação é vinculada aos pontos de extremidade por meio da combinação dos atributos `name` e `bindingConfiguration` . O `name` atributo descreve a seção em que a associação é definida. O `bindingConfiguration` atributo define qual configuração dentro da seção de associação é usada. Uma seção de associação pode definir várias configurações.  
  
## <a name="example"></a>Exemplo  

 Este é um exemplo de uma configuração de serviço.  
  
```xml  
<service behaviorConfiguration="testChannelBehavior"
         name="HelloWorld">
  <endpoint address="/HelloWorld2/"
            name="test"
            bindingNamespace="http://www.cohowinery.com/"
            binding="basicHttpBinding"
            contract="IHelloWorld" />
</service>
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Configuration.ServiceElement>
- [Configurando serviços](../../../wcf/configuring-services.md)
