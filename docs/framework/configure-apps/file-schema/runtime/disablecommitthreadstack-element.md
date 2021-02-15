---
description: 'Saiba mais sobre: <disableCommitThreadStack> elemento'
title: Elemento <disableCommitThreadStack>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/disableCommitThreadStack
- http://schemas.microsoft.com/.NetConfiguration/v2.0#disableCommitThreadStack
helpviewer_keywords:
- <disableCommitThreadStack> element
- disableCommitThreadStack element
ms.assetid: 3559d46a-7640-4c72-9a11-7e980768929e
ms.openlocfilehash: f80a23b12f67b9f3df1ddb010edb735225f6f7a8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787091"
---
# <a name="disablecommitthreadstack-element"></a>Elemento \<disableCommitThreadStack>

Especifica se a pilha de threads completa é confirmada quando um thread é iniciado.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<disableCommitThreadStack>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<disableCommitThreadStack enabled="0|1"/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|Habilitado|Atributo obrigatório.<br /><br /> Especifica se a confirmação da pilha de threads completa na inicialização do thread (o comportamento padrão) está desabilitada.|  
  
## <a name="enabled-attribute"></a>Atributo habilitado  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|Não desabilite o comportamento padrão do Common Language Runtime, que é confirmar a pilha de threads completa quando um thread é iniciado.|  
|1|Desabilite o comportamento padrão do Common Language Runtime, que é confirmar a pilha de threads completa quando um thread é iniciado.|  
  
### <a name="child-elements"></a>Elementos filho  

 Nenhum.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`configuration`|O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework.|  
|`runtime`|Contém informações sobre associação do assembly e coleta de lixo.|  
  
## <a name="remarks"></a>Comentários  

 O comportamento padrão da Common Language Runtime é confirmar a pilha de threads completa quando um thread é iniciado. Se um grande número de threads precisar ser criado em um servidor com memória limitada e a maioria desses threads usarem muito pouco espaço de pilha, o servidor poderá executar melhor se o Common Language Runtime não confirmar a pilha de thread completa imediatamente quando um thread for iniciado.  
  
> [!NOTE]
> Os hosts não gerenciados podem usar o `STARTUP_DISABLE_COMMITTHREADSTACK` sinalizador de inicialização na enumeração de [STARTUP_FLAGS](../../../unmanaged-api/hosting/startup-flags-enumeration.md) para realizar o mesmo resultado.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como desabilitar o comportamento padrão do Common Language Runtime, que é confirmar a pilha de threads completa na inicialização do thread.  
  
```xml  
<configuration>  
   <runtime>  
      <disableCommitThreadStack enabled="1" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também

- [Esquema de configurações do runtime](index.md)
- [Esquema do arquivo de configuração](../index.md)
