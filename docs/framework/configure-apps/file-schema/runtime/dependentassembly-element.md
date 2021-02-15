---
description: 'Saiba mais sobre: <dependentAssembly> elemento'
title: Elemento <dependentAssembly>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly
- http://schemas.microsoft.com/.NetConfiguration/v2.0#dependentAssembly
helpviewer_keywords:
- container tags, <dependentAssembly> element
- dependentAssembly element
- <dependentAssembly> element
ms.assetid: 14e95627-dd79-4b82-ac85-e682aa3a31d8
ms.openlocfilehash: c804920de961fc609fd04a0853ecbdbc9202e5be
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99719078"
---
# <a name="dependentassembly-element"></a>Elemento \<dependentAssembly>

Encapsula local do assembly e política de associação para cada assembly. Use um `dependentAssembly` elemento para cada assembly.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<assemblyBinding>**](assemblybinding-element-for-runtime.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<dependentAssembly>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<dependentAssembly>
</dependentAssembly>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  

 Nenhum.  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`assemblyIdentity`|Contém informações de identificação sobre o assembly. Esse elemento deve ser incluído em cada `dependentAssembly` elemento.|  
|`codeBase`|Especifica onde o tempo de execução pode encontrar um assembly compartilhado se ele não estiver instalado no computador.|  
|`bindingRedirect`|Redireciona uma versão do assembly para outra.|  
|`publisherPolicy`|Especifica se o tempo de execução aplica a política de Publicador para este assembly.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`assemblyBinding`|Contém informações sobre o redirecionamento de versão e os locais dos assemblies.|  
|`configuration`|O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework.|  
|`runtime`|Contém informações sobre associação do assembly e coleta de lixo.|  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como encapsular informações de assembly para dois assemblies.  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <!--Redirection and codeBase policy for myAssembly.-->  
         </dependentAssembly>  
         <dependentAssembly>  
            <assemblyIdentity name="mySecondAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <!--Redirection and codeBase policy for mySecondAssembly.-->  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também

- [Esquema de configurações do runtime](index.md)
- [Esquema do arquivo de configuração](../index.md)
- [Redirecionando versões de assembly](../../redirect-assembly-versions.md)
