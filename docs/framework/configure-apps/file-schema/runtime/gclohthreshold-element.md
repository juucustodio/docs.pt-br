---
description: 'Saiba mais sobre: elemento GCLOHThreshold'
title: Elemento GCLOHThreshold
ms.date: 11/20/2019
helpviewer_keywords:
- GCLOHThreshold element
- <GCLOHThreshold> element
ms.openlocfilehash: 5d4ef4e6aaf44642c2307dc27ac2e99e966d3ad0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652803"
---
# <a name="gclohthreshold-element"></a>Elemento GCLOHThreshold

Especifica o tamanho do limite, em bytes, que faz com que o coletor de lixo coloque objetos na LOH (Large Object heap).

[\<configuration>](../configuration-element.md)\
&nbsp;&nbsp;[\<runtime>](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;\<GCLOHThreshold>

## <a name="syntax"></a>Syntax

```xml
<GCLOHThreshold
   enabled="nnnn"/>
```

## <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|`enabled`|Atributo obrigatório.<br /><br />Especifica o tamanho do limite que faz com que os objetos vá para a heap de objeto grande.|

### <a name="enabled-attribute"></a>atributo habilitado

|Valor|Descrição|
|-----------|-----------------|
|`nnnn`|O tamanho do limite, em bytes, que faz com que os objetos vá para a heap de objeto grande.|

## <a name="child-elements"></a>Elementos filho

Nenhum.

## <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|`configuration`|O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework.|
|`runtime`|Contém informações sobre associação do assembly e coleta de lixo.|

## <a name="remarks"></a>Comentários

Essa configuração foi introduzida no .NET Framework 4,8.

## <a name="see-also"></a>Consulte também

- [Esquema de configurações de tempo de execução](index.md)
- [Esquema do arquivo de configuração](../index.md)
- [Conceitos básicos da coleta de lixo](../../../../standard/garbage-collection/fundamentals.md)
- [Opções de configuração de tempo de execução do NET Core para GC](../../../../core/run-time-config/garbage-collector.md)
