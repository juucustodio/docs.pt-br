---
description: 'Saiba mais sobre: <switches> elemento'
title: Elemento <switches>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/switches
- http://schemas.microsoft.com/.NetConfiguration/v2.0#switches
helpviewer_keywords:
- <switches> element
- switches element
- trace switches, <switches> element
ms.assetid: 4cf36786-b89a-40e2-a0f1-86bb9b783343
ms.openlocfilehash: d0ffdf2bdc4dacd157d09d34c40063b687595e3d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99750514"
---
# <a name="switches-element"></a>Elemento \<switches>

Contém opções de rastreamento e o nível em que as opções de rastreamento são definidas.  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<switches>**

## <a name="syntax"></a>Syntax  
  
```xml  
      <switches>
</switches>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  

 Nenhum.  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<add>](add-element-for-switches.md)|Especifica o nível em que uma opção de rastreamento é definida.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`configuration`|O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework.|  
|`System.diagnostics`|Especifica os ouvintes de rastreamento que coletam, armazenam e roteiam mensagens e o nível em que uma opção de rastreamento é definida.|  
  
## <a name="remarks"></a>Comentários  

 Você pode alterar o nível de uma opção de rastreamento colocando-a em um arquivo de configuração. Se o comutador for um <xref:System.Diagnostics.BooleanSwitch> , você poderá ativá-lo e desligá-lo. Se o comutador for um <xref:System.Diagnostics.TraceSwitch> , você poderá atribuir diferentes níveis a ele para especificar os tipos de mensagens de rastreamento ou de depuração que o aplicativo gera.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como usar o **\<switch>** elemento para definir a `General` opção de rastreamento para o <xref:System.Diagnostics.TraceLevel> nível e habilitar a `Data` opção de rastreamento booliano.  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <switches>  
         <add name="General" value="4" />  
         <add name="Data" value="1" />  
      </switches>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Diagnostics.Switch>
- <xref:System.Diagnostics.TraceSwitch>
- <xref:System.Diagnostics.BooleanSwitch>
- [Esquema de configurações de rastreamento e depuração](index.md)
