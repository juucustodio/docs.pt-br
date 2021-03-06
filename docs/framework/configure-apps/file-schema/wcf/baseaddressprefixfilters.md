---
title: <baseAddressPrefixFilters>
ms.date: 03/30/2017
ms.assetid: 8cab2a9a-c51f-4283-bb60-2ad0c274fd46
ms.openlocfilehash: 635e4f02f4d286b63c4f4845563ba1953d23592a
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88811893"
---
# \<baseAddressPrefixFilters>
Representa uma coleção de elementos de configuração que especificam filtros de passagem, que fornecem um mecanismo para escolher as associações de Serviços de Informações da Internet (IIS) apropriadas ao hospedar o aplicativo de Windows Communication Foundation (WCF) no IIS.  
  
> [!WARNING]
> \<baseAddressPrefixFilters> Não reconhece "localhost"; em vez disso, use o nome do computador totalmente qualificado.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceHostingEnvironment>**](servicehostingenvironment.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<baseAddressPrefixFilters>**  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<serviceHostingEnvironment>
  <baseAddressPrefixFilters>
    <add prefix="String" />
   </baseAddressPrefixFilters>
</serviceHostingEnvironment>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
 Nenhum.  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<add>](add-of-baseaddressprefixfilter.md)|Adiciona um elemento de configuração que especifica um filtro de prefixo para os endereços base usados pelo host de serviço.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<serviceHostingEnvironment>](servicehostingenvironment.md)|Define o tipo que o ambiente de Hospedagem de serviço instancia para um transporte específico.|  
  
## <a name="remarks"></a>Comentários  
 Um filtro de prefixo fornece uma maneira de provedores de hospedagem compartilhados especificar quais URIs devem ser usados pelo serviço. Ele permite que hosts compartilhados hospedem vários aplicativos com endereços base diferentes para o mesmo esquema no mesmo site.  
  
 Os sites da Web do IIS são contêineres para aplicativos virtuais que contêm diretórios virtuais. O aplicativo em um site pode ser acessado por meio de uma ou mais associações do IIS. As associações do IIS fornecem duas informações: vinculação de protocolo e informações de associação. O protocolo de associação (por exemplo, HTTP) define o esquema sobre o qual ocorre a comunicação e as informações de associação (por exemplo, endereço IP, porta, cabeçalho) contêm os dados usados para acessar o site.  
  
 O IIS dá suporte à especificação de várias associações IIS para cada site, o que resulta em vários endereços base para cada esquema. Como um serviço WCF hospedado em um site permite a associação a apenas um endereço base para cada esquema, você pode usar o recurso de filtro de prefixo para escolher o endereço base necessário do serviço hospedado. Os endereços base de entrada, fornecidos pelo IIS, são filtrados com base no filtro de lista de prefixo opcional.  
  
 Por exemplo, seu site pode conter os seguintes endereços base:
  
```http
http://testl.fabrikam.com/Service.svc  
http://test2.fabrikam.com/Service.svc  
```  
  
 Você pode usar o arquivo de configuração a seguir para especificar um filtro de prefixo no nível do AppDomain.  
  
```xml  
<system.serviceModel>
  <serviceHostingEnvironment>
    <baseAddressPrefixFilters>
      <add prefix="net.tcp://test1.fabrikam.com:8000" />
      <add prefix="http://test2.fabrikam.com:9000" />
    </baseAddressPrefixFilters>
  </serviceHostingEnvironment>
</system.serviceModel>
```  
  
 Neste exemplo, `net.tcp://test1.fabrikam.com:8000` e `http://test2.fabrikam.com:9000` são os únicos endereços base para seus respectivos esquemas, que têm permissão para serem passados.  
  
 Por padrão, quando o prefixo não é especificado, todos os endereços são passados. A especificação do prefixo só permite que o endereço de base correspondente para esse esquema seja passado.  
  
> [!NOTE]
> O filtro não oferece suporte a caracteres curinga. Além disso, os baseAddresss fornecidos pelo IIS podem ter endereços associados a outros esquemas que não estão presentes na `baseAddressPrefixFilters` lista. Esses endereços não são filtrados.  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.Configuration.BaseAddressPrefixFilterElementCollection>
- <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>
- <xref:System.ServiceModel.ServiceHostingEnvironment>
- [Hosting](../../../wcf/feature-details/hosting.md)
