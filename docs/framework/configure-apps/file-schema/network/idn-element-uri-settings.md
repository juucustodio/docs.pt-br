---
description: 'Saiba mais sobre: <idn> elemento (configurações de URI)'
title: Elemento <idn> (Configurações de URI)
ms.date: 03/30/2017
ms.assetid: 16c8e869-1791-4cf5-9244-3d3c738f60ec
ms.openlocfilehash: a53afd59b713a804d5b969521f468000dbbad6e8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802470"
---
# <a name="idn-element-uri-settings"></a>Elemento \<idn> (Configurações de URI)

Especifica se a análise de IDN (nome de domínio internacionalizado) é aplicada a um nome de domínio.
  
[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;[**\<uri>**](uri-element-uri-settings.md)  
&nbsp;&nbsp;&nbsp;&nbsp;**\<idn>**  
  
## <a name="syntax"></a>Syntax  
  
```xml
<idn
  enabled="All|AllExceptIntranet|None"
/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  

 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  

|**Element**|**Descrição**|  
|-----------------|---------------------|  
|`enabled`|Especifica se a análise de IDN (nome de domínio internacionalizado) é aplicada a um nome de domínio, o valor padrão é nenhum.|  

### <a name="child-elements"></a>Elementos filho

Nenhum
  
### <a name="parent-elements"></a>Elementos pai

|**Element**|**Descrição**|  
|-----------------|---------------------|  
|[uri](uri-element-uri-settings.md)|Contém configurações que especificam como o .NET Framework trata os endereços da Web expressos usando URIs (identificadores de recursos uniformes).|  

## <a name="remarks"></a>Comentários

A <xref:System.Uri> classe existente foi estendida no .NET Framework 3,5. 3,0 SP1 e 2,0 SP1 com suporte para IRI (identificadores de recursos internacionais) e IDNs (nomes de domínio internacionalizados). Os usuários atuais não verão nenhuma alteração do comportamento .NET Framework 2,0, a menos que eles especificamente habilitem o suporte a IRI e IDN. Isso garante a compatibilidade do aplicativo com versões anteriores do .NET Framework.

Para habilitar o suporte para IRI, as duas alterações a seguir são necessárias:

1. Adicione a seguinte linha ao arquivo de machine.config no diretório .NET Framework 2,0:
  
    ```xml  
    <section name="uri" type="System.Configuration.UriSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
    ```  
  
2. Especifique se você deseja a análise de nome de domínio internacionalizado (IDN) aplicada ao nome de domínio e se as regras de análise de IRI devem ser aplicadas. Isso pode ser feito no arquivo machine.config ou em app.config.

 Há três valores possíveis para IDN, dependendo dos servidores DNS que são usados:

- IDN habilitado = todos  

     Esse valor converterá todos os nomes de domínio Unicode em seus equivalentes do Punycode (nomes IDN).

- IDN habilitado = AllExceptIntranet

     Esse valor converterá todos os nomes de domínio Unicode que não estão na intranet local para usar os equivalentes Punycode (nomes IDN). Nesse caso, para lidar com nomes internacionais na intranet local, os servidores DNS que são usados para a intranet devem dar suporte à resolução de nomes Unicode.

- IDN habilitado = nenhum

     Esse valor não converterá nenhum nome de domínio Unicode para usar o Punycode. Esse é o valor padrão, que é consistente com o comportamento do .NET Framework 2.0.

 Habilitar o IDN converterá todos os rótulos Unicode de um nome de domínio para seus equivalentes em Punycode. Os nomes Punycode contêm apenas caracteres ASCII e sempre começam com o prefixo xn--. A razão para isso é dar suporte a servidores DNS existentes na Internet, pois a maioria dos servidores DNS dá suporte somente a caracteres ASCII (consulte RFC 3940).

### <a name="configuration-files"></a>Arquivos de configuração

Esse elemento pode ser usado no arquivo de configuração do aplicativo ou no arquivo de configuração do computador (Machine.config).

## <a name="example"></a>Exemplo

O exemplo a seguir mostra uma configuração usada pela <xref:System.Uri> classe para dar suporte a análise de IRI e nomes IDN:

```xml
<configuration>
  <uri>
    <idn enabled="All" />
    <iriParsing enabled="true" />
  </uri>
</configuration>
```

## <a name="see-also"></a>Consulte também

- <xref:System.Configuration.IdnElement?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection?displayProperty=nameWithType>
- [Esquema de configurações de rede](index.md)
