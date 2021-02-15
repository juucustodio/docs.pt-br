---
description: -appconfig (opções do compilador C#)
title: -appconfig (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /appconfig
helpviewer_keywords:
- /appconfig compiler option [C#]
- -appconfig compiler option [C#]
- appconfig compiler option [C#]
ms.assetid: 1cdbcbcc-7813-4010-b5b8-e67c107c5a98
ms.openlocfilehash: 8ee481851dc02bed5eb0a7c26fa8893e52d54a9f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91157961"
---
# <a name="-appconfig-c-compiler-options"></a>-appconfig (opções do compilador C#)

A opção do compilador **-appconfig** permite que um aplicativo em C# especifique o local de um arquivo de configuração de aplicativo (app.config) de um assembly para o CLR (Common Language Runtime) em tempo de associação do assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-appconfig:file  
```  
  
## <a name="arguments"></a>Argumentos  

 `file`  
 Necessário. O arquivo de configuração de aplicativo que contém as configurações de associação de assembly.  
  
## <a name="remarks"></a>Comentários  

 O **-appconfig** pode ser usado em cenários avançados, nos quais é necessário que um assembly referencie, ao mesmo temo, tanto a versão do .NET Framework quanto a versão do .NET Framework para a versão do Silverlight de um assembly de referência específico. Por exemplo, um designer XAML gravado no Windows Presentation Foundation (WPF) pode ter que referenciar a Área de Trabalho do WPF, para a interface do usuário do designer e o subconjunto do WPF incluído no Silverlight. O mesmo assembly do designer deve acessar ambos os assemblies. Por padrão, as referências separadas causam um erro do compilador, pois a associação de assembly considera os dois assemblies equivalentes.  
  
 A opção do compilador **-appconfig** permite a especificação do local de um arquivo app.config que desabilita o comportamento padrão por meio de uma marcação `<supportPortability>`, conforme mostrado no exemplo a seguir.  
  
 `<supportPortability PKT="7cec85d7bea7798e" enable="false"/>`  
  
 O compilador passa o local do arquivo para a lógica de associação de assembly do CLR.  
  
> [!NOTE]
> Caso o MSBuild (Microsoft Build Engine) seja usado para compilar o aplicativo, é possível definir a opção do compilador **-appconfig** adicionando uma marcação de propriedade ao arquivo .csproj. Para usar o arquivo app.config que já está definido no projeto, adicione a marca de propriedade `<UseAppConfigForCompiler>` ao arquivo .csproj e defina seu valor para `true`. Para especificar um arquivo app.config diferente, adicione a marca de propriedade `<AppConfigForCompiler>` e defina seu valor para o local do arquivo.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra um arquivo app.config que habilita um aplicativo a referenciar as implementações do .NET Framework e do .NET Framework para Silverlight de qualquer assembly do .NET Framework que exista em ambas as implementações. A opção do compilador **-appconfig** especifica o local desse arquivo app.config.  
  
```xml  
<configuration>  
      <runtime>  
      <assemblyBinding>  
            <supportPortability PKT="7cec85d7bea7798e" enable="false"/>  
            <supportPortability PKT="31bf3856ad364e35" enable="false"/>  
      </assemblyBinding>  
      </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Confira também

- [\<supportPortability> Elementos](../../../framework/configure-apps/file-schema/runtime/supportportability-element.md)
- [Opções do compilador de C# listadas em ordem alfabética](./listed-alphabetically.md)
