---
description: 'Saiba mais sobre: <remove> elemento para BypassList (configurações de rede)'
title: Elemento <remove> para bypasslist (Configurações de Rede)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist/remove
- http://schemas.microsoft.com/.NetConfiguration/v2.0#remove
helpviewer_keywords:
- <bypasslist>, remove element
- remove element, bypasslist
- bypasslist, remove element
- remove element, bypasslist
ms.assetid: 61dcfb4a-e3d9-4abf-a2cd-7d685fe2f64b
ms.openlocfilehash: 48441f1b402b339a1bd2ea069678afb4b1d5f2e1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99740282"
---
# <a name="remove-element-for-bypasslist-network-settings"></a>Elemento \<remove> para bypasslist (Configurações de Rede)

Remove um endereço IP ou nome DNS da lista de bypass de proxy.

[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)  
&nbsp;&nbsp;&nbsp;&nbsp;[**\<defaultProxy>**](defaultproxy-element-network-settings.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<bypasslist>**](bypasslist-element-network-settings.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<remove>**  

## <a name="syntax"></a>Syntax

```xml
<remove
  address="regular expression"
/>
```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|**Atributo**|**Descrição**|
|-------------------|---------------------|
|`address`|Uma expressão regular que descreve um endereço IP ou nome DNS.|

### <a name="child-elements"></a>Elementos filho

Nenhum.

### <a name="parent-elements"></a>Elementos pai

|**Element**|**Descrição**|
|-----------------|---------------------|
|[bypasslist](bypasslist-element-network-settings.md)|Fornece um conjunto de expressões regulares que descrevem endereços que não usam um proxy.|

## <a name="remarks"></a>Comentários

O `remove` elemento remove expressões regulares que descrevem endereços IP ou nomes de servidores DNS da lista de endereços que ignoram um servidor proxy. Os endereços foram definidos anteriormente no arquivo de configuração ou em um nível superior na hierarquia de configuração.

O valor do `address` atributo deve ser uma expressão regular que descreve um conjunto de endereços IP ou nomes de host.

Para obter mais informações sobre expressões regulares, consulte. [.NET Framework expressões regulares](../../../../standard/base-types/regular-expressions.md).

## <a name="configuration-files"></a>Arquivos de Configuração

Esse elemento pode ser usado no arquivo de configuração do aplicativo ou no arquivo de configuração do computador (Machine.config).

## <a name="example"></a>Exemplo

O exemplo a seguir remove qualquer definição anterior para o domínio adventure-works.com e, em seguida, adiciona o domínio contoso.com à lista de bypass.

```xml
<configuration>
  <system.net>
    <defaultProxy>
      <bypasslist>
        <remove address="[a-z]+\.adventure-works\.com$" />
        <add address="[a-z]+\.contoso\.com$" />
      </bypasslist>
    </defaultProxy>
  </system.net>
</configuration>
```

## <a name="see-also"></a>Consulte também

- <xref:System.Net.WebProxy?displayProperty=nameWithType>
- [Esquema de configurações de rede](index.md)
