---
description: 'Saiba mais sobre: <appSettings> elemento para <configuration>'
title: Elemento <appSettings> para <configuration>
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/appSettings
helpviewer_keywords:
- appSettings Element
- <appSettings> Element
ms.assetid: 39694cc4-6b84-45a6-9329-385a0d8b48fe
ms.openlocfilehash: 74a25bb0dffd97057cda45575745b6f51ad2a675
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802483"
---
# <a name="appsettings-element-for-configuration"></a>Elemento \<appSettings> para \<configuration>

Contém configurações de aplicativo personalizadas. Esta é uma seção de configuração predefinida fornecida pelo .NET Framework.

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;**\<appSettings>**

## <a name="syntax"></a>Syntax

```xml
<appSettings>
  <!-- Elements to add, clear, or remove configuration settings -->
</appSettings>
```

## <a name="attribute"></a>Atributo

|           | Descrição |
| --------- | ----------- |
| **file**  | Atributo opcional.<br><br>Especifica um caminho relativo para um arquivo externo que contém definições de configuração de aplicativo personalizadas. O arquivo especificado contém o mesmo tipo de configurações que são especificadas nos **\<add>** elementos, e **\<remove>** **\<clear>** e usa o mesmo formato de par chave/valor que esses elementos.<br><br>O caminho especificado é relativo ao arquivo de configuração principal. Para um aplicativo Windows Forms, essa é a pasta binária (como */bin/Debug*), não o local do arquivo de configuração do aplicativo. Para aplicativos Web Forms, o caminho é relativo à raiz do aplicativo, onde o arquivo de *web.config* está localizado.<br><br>O tempo de execução ignora o atributo se o arquivo especificado não puder ser encontrado. |

## <a name="parent-element"></a>Elemento pai

|     | Descrição |
| --- | ----------- |
| [**\<configuration>** Elementos](../configuration-element.md) | O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework. |

## <a name="child-elements"></a>Elementos filho

|     | Descrição |
| --- | ----------- |
| [**\<add>**](add-element-for-appsettings.md) | Adiciona uma configuração de aplicativo personalizada. |
| [**\<clear>**](clear-element-for-appsettings.md) | Limpa todas as configurações de aplicativo definidas anteriormente. |
| [**\<remove>**](remove-element-for-appsettings.md) | Remove uma configuração de aplicativo definida anteriormente. |

## <a name="remarks"></a>Comentários

O **\<appSettings>** elemento armazena informações de configuração de aplicativo personalizadas, como cadeias de conexão de banco de dados, caminhos de arquivo, URLs de serviço Web XML ou qualquer outra informação de configuração personalizada para um aplicativo. Os pares de chave/valor especificados no **\<appSettings>** elemento são acessados no código usando a <xref:System.Configuration.ConfigurationSettings> classe.

Você pode usar o atributo **File** no **\<appSettings>** elemento da *Web.config* e dos arquivos de configuração do aplicativo. Esse atributo especifica um arquivo de configuração que fornece configurações adicionais ou substitui as configurações especificadas no **\<appSettings>** elemento. O atributo de **arquivo** pode ser usado em cenários de desenvolvimento de equipe de controle do código-fonte, como quando um usuário deseja substituir as configurações de projeto especificadas em um arquivo de configuração de aplicativo.

Os arquivos de configuração especificados pelo atributo de **arquivo** devem ter um nó raiz **\<appSettings>** em vez de **\<configuration>** .

## <a name="example"></a>Exemplo

O exemplo a seguir mostra um arquivo de configurações de aplicativo externo (*custom.config*) que define uma configuração de aplicativo personalizada:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<appSettings>
  <add key="MyCustomSetting" value="MyCustomSettingValue" />
</appSettings>
```

O exemplo a seguir mostra um arquivo de configuração de aplicativo que consome a configuração no arquivo de configurações externas e define sua própria configuração de aplicativo:

```xml
<configuration>
  <appSettings file="custom.config">
    <add key="ApplicationName" value="MyApplication" />
  </appSettings>
</configuration>
```

## <a name="configuration-file"></a>Arquivo de configuração

Esse elemento pode ser usado no arquivo de configuração do aplicativo, no arquivo de configuração do computador (*Machine.config*) e *Web.config* arquivos que não estão no nível do diretório do aplicativo.

## <a name="see-also"></a>Consulte também

- [Esquema do arquivo de configuração para o .NET Framework](../index.md)
