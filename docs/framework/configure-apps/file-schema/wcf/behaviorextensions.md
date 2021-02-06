---
description: 'Saiba mais sobre: <behaviorExtensions>'
title: <behaviorExtensions>
ms.date: 03/30/2017
ms.assetid: 59f2791a-c78f-40d7-aa80-0d9cd10135d9
ms.openlocfilehash: 0bd641f8e26d309c592c07bcc19ff02897fe71cd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99639517"
---
# \<behaviorExtensions>

As extensões de comportamento permitem que o usuário crie elementos de comportamento definidos pelo usuário. Esses elementos podem ser usados junto com os elementos de comportamento padrão do Windows Communication Foundation (WCF). A `behaviorExtensions` seção define o elemento de modo que ele possa ser usado na configuração. Aqui está um exemplo de uma extensão de comportamento típica.  
  
```xml  
<system.serviceModel>
  <extensions>
    <behaviorExtensions>
      <add name="myBehavior"
           type="Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
                 Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    </behaviorExtensions>
  </extensions>
</system.serviceModel>
```  
  
 Para adicionar habilidades de configuração ao elemento, você precisa escrever e registrar um elemento de configuração. Para obter mais informações sobre isso, consulte a <xref:System.Configuration> documentação.  
  
 Depois que o elemento e seu tipo de configuração são definidos, a extensão pode ser usada, conforme mostrado no exemplo a seguir.  
  
```xml  
<behaviors>
  <behavior configurationName="testChannelBehavior">
    <myBehavior />
    <channelSecurity cacheCookies="false"
                     detectReplays="false"
                     maxCachedNonces="9"
                     maxClockSkew="00:00:03"
                     maxCookieCachingTime="00:07:24"
                     replayWindow="00:07:22.2190000" />
  </behavior>
</behaviors>
```  
  
## <a name="security"></a>Segurança  

 É altamente recomendável que você use nomes de assembly totalmente qualificados ao registrar tipos nos `machine.config` arquivos e `app.config` . Se o tipo não for definido exclusivamente, o carregador de tipo CLR pesquisará nos seguintes locais na ordem especificada:  
  
 Se o assembly do tipo for conhecido, o carregador pesquisará os locais de redirecionamento do arquivo de configuração, o GAC, o assembly atual usando as informações de configuração e o diretório base do aplicativo. Se o assembly for desconhecido, o carregador pesquisará o assembly atual, mscorlib e o local retornado pelo `TypeResolve` manipulador de eventos. Essa ordem de pesquisa do CLR pode ser modificada com ganchos como o mecanismo de encaminhamento de tipo e o evento AppDomain. TypeResolve.  
  
 Um invasor pode explorar a ordem de pesquisa do CLR e executar código não autorizado. Usar nomes totalmente qualificados (fortes) identifica exclusivamente um tipo e aumenta ainda mais a segurança do sistema.  
  
 Para obter mais informações, consulte [como o tempo de execução localiza assemblies](../../../deployment/how-the-runtime-locates-assemblies.md) e <xref:System.AppDomain.TypeResolve> .  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>
- [Configurando e estendendo o runtime com comportamentos](../../../wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)
