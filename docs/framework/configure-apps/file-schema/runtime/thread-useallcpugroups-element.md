---
description: 'Saiba mais sobre: <Thread_UseAllCpuGroups elemento>'
title: Elemento <Thread_UseAllCpuGroups>
ms.date: 03/30/2017
ms.assetid: d30fe7c5-8469-46e2-b804-e3eec7b24256
ms.openlocfilehash: 3f11ba6855caab25bd261de71c80c78232f2690f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802405"
---
# <a name="thread_useallcpugroups-element"></a>Elemento \<Thread_UseAllCpuGroups>

Especifica se o runtime distribui threads gerenciados entre todos os grupos de CPU.

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<Thread_UseAllCpuGroups>**  

## <a name="syntax"></a>Syntax

```xml
<Thread_UseAllCpuGroups
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|`enabled`|Atributo obrigatório.<br /><br /> Especifica se o runtime distribui threads gerenciados entre todos os grupos de CPU.|

## <a name="enabled-attribute"></a>Atributo habilitado

|Valor|Descrição|
|-----------|-----------------|
|`false`|O tempo de execução não distribui threads gerenciados entre vários grupos de CPU. Este é o padrão.|
|`true`|O tempo de execução distribui threads gerenciados entre vários grupos de CPU, se o computador tiver vários grupos de CPU e o [\<GCCpuGroup>](gccpugroup-element.md) elemento estiver habilitado.|

### <a name="child-elements"></a>Elementos filho

Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|`configuration`|O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework.|
|`runtime`|Contém informações sobre associação do assembly e coleta de lixo.|

## <a name="remarks"></a>Comentários

Quando um computador tem vários grupos de CPU, a habilitação desse elemento faz com que o tempo de execução distribua threads gerenciados em todos os grupos de CPU. Para usar esse recurso, você também deve habilitar o [\<GCCpuGroup>](gccpugroup-element.md) elemento, que estende a coleta de lixo para todos os grupos de CPU e leva todos os núcleos em conta ao criar e balancear heaps. Habilitar o [\<GCCpuGroup>](gccpugroup-element.md) elemento requer a habilitação do [\<gcServer>](gcserver-element.md) elemento. Se esses elementos não estiverem habilitados, a habilitação do `<Thread_UseAllCpuGroups>` elemento não terá nenhum efeito.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra como habilitar o suporte para vários grupos de CPU.

```xml
<configuration>
   <runtime>
      <Thread_UseAllCpuGroups enabled="true"/>
      <GCCpuGroup enabled="true"/>
      <gcServer enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>Consulte também

- [Esquema de configurações do runtime](index.md)
- [Esquema do arquivo de configuração](../index.md)
- [\<GCCpuGroup> Elementos](gccpugroup-element.md)
