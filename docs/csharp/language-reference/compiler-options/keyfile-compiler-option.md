---
description: -keyfile (opções do compilador C#)
title: -keyfile (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /keyfile
helpviewer_keywords:
- /keyfile compiler option [C#]
- -keyfile compiler option [C#]
- keyfile compiler option [C#]
ms.assetid: 0815f9de-ace4-4e98-b4c6-13c55dea40c2
ms.openlocfilehash: 5af40da18895d47933cb809d710e31a40f14513b
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91152423"
---
# <a name="-keyfile-c-compiler-options"></a>-keyfile (opções do compilador C#)

Especifica o nome de arquivo que contém a chave de criptografia.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-keyfile:file  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Termo|Definição|  
|----------|----------------|  
|`file`|O nome do arquivo que contém a chave de nome forte.|  
  
## <a name="remarks"></a>Comentários  

 Quando esta opção é usada, o compilador insere a chave pública da linha especificada no manifesto do assembly e, em seguida, assina o assembly definitivo com a chave privada. Para gerar um arquivo de chave, digite sn -k `file` na linha de comando.  
  
 Se você compilar com **-target:module**, o nome do arquivo de chave será mantido no módulo e incorporado no assembly, criado quando você compila um assembly com [-addmodule](./addmodule-compiler-option.md).  
  
 Também é possível passar suas informações de criptografia para o compilador com [-keycontainer](./keycontainer-compiler-option.md). Use [-delaysign](./delaysign-compiler-option.md) se quiser um assembly parcialmente assinado.  
  
 Caso -keyfile e -keycontainer sejam especificados (pela opção de linha de comando ou pelo atributo personalizado) na mesma compilação, o compilador tentará primeiro o contêiner de chaves. Se isso ocorrer, o assembly será assinado com as informações no contêiner de chaves. Se o compilador não localizar o contêiner de chaves, ele tentará o arquivo especificado com -keyfile. Se isso ocorrer, o assembly será assinado com as informações no arquivo de chave e as informações da chave serão instaladas no contêiner de chaves (semelhante a sn -i), de forma que, na próxima compilação, o contêiner de chaves será válido.  
  
 Observe que um arquivo de chave pode conter somente a chave pública.  
  
 Para obter mais informações, consulte [Criando e usando assemblies de nomes fortes](../../../standard/assembly/create-use-strong-named.md) e [Atraso na Assinatura de um Assembly](../../../standard/assembly/delay-sign.md).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio  
  
1. Abra a página **Propriedades** do projeto.  
  
2. Clique na página de propriedades **Assinatura**.  
  
3. Modifique a propriedade **Escolha um arquivo de chave de nome forte**.  
  
 Você pode acessar programaticamente essa opção do compilador com <xref:VSLangProj.ProjectProperties.AssemblyOriginatorKeyFile%2A>.  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
