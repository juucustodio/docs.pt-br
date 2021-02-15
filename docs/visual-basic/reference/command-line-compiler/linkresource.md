---
description: Saiba mais sobre:-linkresource (Visual Basic)
title: -linkresource
ms.date: 03/10/2018
helpviewer_keywords:
- /linkresource compiler option [Visual Basic]
- -linkresource compiler option [Visual Basic]
- linkresource compiler option [Visual Basic]
- /linkres compiler option [Visual Basic]
- linkres compiler option [Visual Basic]
- -linkres compiler option [Visual Basic]
ms.assetid: cf4dcad8-17b7-404c-9184-29358aa05b15
ms.openlocfilehash: 21fc47ecff44230bda0f445bc695706b5ae91eff
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100463695"
---
# <a name="-linkresource-visual-basic"></a>-linkresource (Visual Basic)

Cria um link a um recurso gerenciado.  
  
## <a name="syntax"></a>Syntax  
  
```console  
-linkresource:filename[,identifier[,public|private]]  
```

ou  

```console
-linkres:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>Argumentos  

 `filename`  
 Obrigatório. O arquivo de recurso a ser vinculado ao assembly. Se o nome do arquivo contiver um espaço, coloque o nome entre aspas ("").  
  
 `identifier`  
 Opcional. O nome lógico do recurso. O nome usado para carregar o recurso. O padrão é o nome do arquivo. Opcionalmente, você pode especificar se o arquivo é público ou privado no manifesto do assembly, por exemplo: `-linkres:filename.res,myname.res,public` . Por padrão, `filename` é público no assembly.  
  
## <a name="remarks"></a>Comentários  

 A `-linkresource` opção não incorpora o arquivo de recurso no arquivo de saída; use a `-resource` opção para fazer isso.  
  
 A `-linkresource` opção requer uma das `-target` opções diferentes de `-target:module` .  
  
 Se `filename` for um arquivo de recurso .NET Framework criado, por exemplo, pelo [Resgen.exe (gerador de arquivo de recurso)](../../../framework/tools/resgen-exe-resource-file-generator.md) ou no ambiente de desenvolvimento, ele poderá ser acessado com membros no <xref:System.Resources> namespace. (Para obter mais informações, consulte <xref:System.Resources.ResourceManager> .) Para acessar todos os outros recursos em tempo de execução, use os métodos que começam com `GetManifestResource` na <xref:System.Reflection.Assembly> classe.  
  
 O nome do arquivo pode ser qualquer formato de arquivo. Por exemplo, crie uma parte DLL nativa do assembly de maneira que possa ser instalada no cache de assembly global e acessado no código gerenciado no assembly.  
  
 A forma abreviada de `-linkresource` é `-linkres`.  
  
> [!NOTE]
> A `-linkresource` opção não está disponível no ambiente de desenvolvimento do Visual Studio; ela está disponível somente quando você compila a partir da linha de comando.  
  
## <a name="example"></a>Exemplo  

 O código a seguir compila `in.vb` e vincula ao arquivo de recurso `rf.resource` .  
  
```console  
vbc -linkresource:rf.resource in.vb  
```  
  
## <a name="see-also"></a>Consulte também

- [Compilador de linha de comando do Visual Basic](index.md)
- [-Target (Visual Basic)](target.md)
- [-recurso (Visual Basic)](resource.md)
- [Linhas de Comando de Compilação de Exemplo](sample-compilation-command-lines.md)
