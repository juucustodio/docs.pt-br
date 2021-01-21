---
description: -doc (opções do compilador C#)
title: -doc (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- FileProperties.BuildAction
- /doc
helpviewer_keywords:
- comments, C# code
- XML documentation [C#], comments in source files
- doc compiler option [C#]
- Visual C#, XML documentation for
- -doc compiler option [C#]
- /doc compiler option [C#]
ms.assetid: 849eea59-c936-4311-bad8-d07404480f2a
ms.openlocfilehash: e55b86e5b028fb871f309d80217477cfd164c106
ms.sourcegitcommit: f0eb7eeedf3ceec726499fa678786d03083214ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/21/2021
ms.locfileid: "98629248"
---
# <a name="-doc-c-compiler-options"></a>-doc (opções do compilador C#)

A opção **-doc** permite colocar comentários de documentação em um arquivo XML.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-doc:file  
```  
  
## <a name="arguments"></a>Argumentos  

 `file`  
 O arquivo de saída para XML, que é populado com os comentários nos arquivos de código-fonte da compilação.  
  
## <a name="remarks"></a>Comentários  

 Nos arquivos de código-fonte, os comentários de documentação que precedem o seguinte podem ser processados e adicionados ao arquivo XML:  
  
- Tipos definidos pelo usuário, como [classe](../keywords/class.md), [delegado](../builtin-types/reference-types.md#the-delegate-type) ou [interface](../keywords/interface.md)  
  
- Membros como um campo, [evento](../keywords/event.md), [propriedade](../../programming-guide/classes-and-structs/using-properties.md) ou método  
  
 O arquivo de código-fonte que contém Main é gerado primeiro no XML.  
  
 Para usar o arquivo .xml gerado para uso com o recurso [IntelliSense](/visualstudio/ide/using-intellisense), deixe o nome do arquivo .xml igual ao do assembly a que você deseja dar suporte e, em seguida, verifique se o arquivo .xml está no mesmo diretório que o assembly. Sendo assim, quando o assembly for referenciado no projeto do Visual Studio, o arquivo .xml também será encontrado. Consulte [Fornecendo comentários de código](/visualstudio/ide/reference/generate-xml-documentation-comments) para obter mais informações.  
  
 A menos que você compile com o [módulo-target:](./target-module-compiler-option.md), conterá `file` \<assembly> \</assembly> marcas especificando o nome do arquivo que contém o manifesto do assembly para o arquivo de saída da compilação.  
  
> [!NOTE]
> A opção -doc se aplica a todos os arquivos de entrada ou, se definida nas Configurações do Projeto, todos os arquivos no projeto. Para desabilitar avisos relacionados aos comentários de documentação para um arquivo ou uma seção específica do código, use [#pragma warning](../preprocessor-directives/preprocessor-pragma-warning.md).  
  
 Consulte [Marcas recomendadas para comentários de documentação](../../programming-guide/xmldoc/recommended-tags-for-documentation-comments.md) para ver maneiras de gerar a documentação dos comentários em seu código.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-2019-development-environment"></a>Para definir essa opção de compilador no ambiente de desenvolvimento do Visual Studio 2019  

1. Abra a página **Propriedades** do projeto.  
2. Clique na guia **Build**.
3. Modifique a propriedade **Arquivo de documentação XML**.
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-for-mac-development-environment"></a>Para definir essa opção de compilador no ambiente de desenvolvimento de Visual Studio para Mac  
  
1. Abra a página **Opções** do projeto.
2. Selecione a guia **compilador** .
3. Selecione **gerar documentação XML** e insira o nome do arquivo na caixa de texto.

Para obter informações sobre como definir essa opção do compilador programaticamente, consulte <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DocumentationFile%2A>.  
  
## <a name="see-also"></a>Veja também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
