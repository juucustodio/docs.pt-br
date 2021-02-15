---
description: 'Saiba mais sobre: <clear> elemento para NameValueSectionHandler e DictionarySectionHandler'
title: <clear> elemento para NameValueSectionHandler e DictionarySectionHandler
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/sectionName/clear
helpviewer_keywords:
- clear Element
- <clear> Element
ms.assetid: ff2294ec-fb82-4b0c-933e-ae185433fc7b
ms.openlocfilehash: 896aa7e8f0e3b41574538fcd9e4be9d6155da889
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99699227"
---
# <a name="clear-element-for-namevaluesectionhandler-and-dictionarysectionhandler"></a>\<clear> elemento para NameValueSectionHandler e DictionarySectionHandler

Limpa todas as configurações definidas anteriormente em uma seção.

[**\<configuration>**](configuration-element.md)\
&nbsp;&nbsp;[**\<sectionName>**](custom-element-2.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<clear>**

## <a name="syntax"></a>Syntax

```xml
<clear />
```

## <a name="attributes"></a>Atributos

Nenhum

## <a name="parent-element"></a>Elemento pai

|     | Descrição |
| --- | ------------|
| [**\<sectionName>** Elementos](custom-element-2.md) | Define as configurações para seções de configuração personalizadas que usam as <xref:System.Configuration.NameValueSectionHandler> <xref:System.Configuration.DictionarySectionHandler> classes e. |

## <a name="child-elements"></a>Elementos filho

Nenhum

## <a name="remarks"></a>Comentários

Você pode usar o **\<clear>** elemento para remover todas as configurações do aplicativo que foram definidas em um nível mais alto na hierarquia do arquivo de configuração.

## <a name="example"></a>Exemplo

Este exemplo define um arquivo de configuração de computador e um arquivo de configuração de aplicativo e mostra como usar o **\<clear>** elemento em um arquivo de configuração de aplicativo para limpar as seções definidas anteriormente no arquivo de configuração de computador.

O código do arquivo de configuração do computador a seguir declara a seção **\<mySection>** :

```xml
<!-- Machine.config file -->
<configuration>
  <configSections>
    <section name="mySection" type="System.Configuration.NameValueSectionHandler,System" />
  </configSections>
  <mySection>
    <add key="key1" value="value1" />
    <add key="key2" value="value2" />
  </mySection>
</configuration>
```

O código do arquivo de configuração de aplicativo a seguir remove todas as configurações de **\<mySection>** . O aplicativo não pode recuperar nenhuma das configurações que foram declaradas no na **\<mySection>** seção do arquivo de configuração do computador.

```xml
<!-- Application configuration file -->
<configuration>
  <mySection>
    <clear/>
  </mySection>
</configuration>
```

## <a name="configuration-file"></a>Arquivo de configuração

Esse elemento pode ser usado no arquivo de configuração do aplicativo, no arquivo de configuração do computador (*Machine.config*) e *Web.config* arquivos que não estão no nível do diretório do aplicativo.

## <a name="see-also"></a>Consulte também

- [Esquema do arquivo de configuração para o .NET Framework](index.md)
