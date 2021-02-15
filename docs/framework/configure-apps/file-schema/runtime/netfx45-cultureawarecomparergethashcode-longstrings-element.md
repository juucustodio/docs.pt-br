---
description: 'Saiba mais sobre: <NetFx45_CultureAwareComparerGetHashCode_LongStrings elemento>'
title: Elemento <NetFx45_CultureAwareComparerGetHashCode_LongStrings>
ms.date: 03/30/2017
helpviewer_keywords:
- NetFx45_CultureAwareComparerGetHashCode_LongStrings element
- <NetFx45_CultureAwareComparerGetHashCode_LongStrings> element
- GetHashCode method
- hash codes, calculating
ms.assetid: 3a5f38d1-ebc8-44de-aaeb-2929f6e6b48f
ms.openlocfilehash: ca4099d3bf812cb25e6a611b9b51b3752b1ad361
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99782280"
---
# <a name="netfx45_cultureawarecomparergethashcode_longstrings-element"></a>Elemento \<NetFx45_CultureAwareComparerGetHashCode_LongStrings>

Especifica se o runtime usa uma quantidade fixa de memória para calcular códigos hash para o método <xref:System.StringComparer.GetHashCode%2A?displayProperty=nameWithType>.

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<NetFx45_CultureAwareComparerGetHashCode_LongStrings>**  

## <a name="syntax"></a>Syntax

```xml
<NetFx45_CultureAwareComparerGetHashCode_LongStrings enabled="0|1">
```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|`enabled`|Atributo obrigatório.<br /><br /> Especifica se o Common Language Runtime atribui uma quantidade fixa de memória ao calcular códigos hash.|

## <a name="enabled-attribute"></a>Atributo habilitado

|Valor|Descrição|
|-----------|-----------------|
|0|O Common Language Runtime aloca uma quantidade variável de memória para o método <xref:System.StringComparer.GetHashCode%2A?displayProperty=nameWithType> para calcular códigos hash. Este é o padrão.|
|1|O Common Language Runtime aloca uma quantidade fixa de memória para o método <xref:System.StringComparer.GetHashCode%2A?displayProperty=nameWithType> para calcular códigos hash.|

### <a name="child-elements"></a>Elementos filho

Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|`configuration`|O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework.|
|`runtime`|Contém informações sobre opções de inicialização do runtime.|

## <a name="remarks"></a>Comentários

Por padrão, o Common Language Runtime aloca uma quantidade variável de memória para o método <xref:System.StringComparer.GetHashCode%2A?displayProperty=nameWithType> e um <xref:System.ArgumentException> pode ser disparado quando o método tentar calcular o código hash de cadeias de caracteres muito grandes (com comprimentos superiores a vários milhões de caracteres). Ao adicionar esse elemento a um arquivo de configuração do aplicativo e definir seu atributo `enabled` como "1", você poderá especificar que o método <xref:System.StringComparer.GetHashCode%2A?displayProperty=nameWithType> use um algoritmo alternativo que aloque uma quantidade fixa de memória para o cálculo de códigos hash.

> [!IMPORTANT]
> O `<NetFx45_CultureAwareComparerGetHashCode_LongStrings>` elemento não é usado no Windows 8 e versões posteriores.

## <a name="see-also"></a>Consulte também

- <xref:System.StringComparer.GetHashCode%2A?displayProperty=nameWithType>
- [Esquema de configurações do runtime](index.md)
- [Esquema do arquivo de configuração](../index.md)
