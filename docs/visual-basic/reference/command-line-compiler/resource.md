---
description: Saiba mais sobre:-Resource (Visual Basic)
title: -resource
ms.date: 03/13/2018
helpviewer_keywords:
- /resource compiler option [Visual Basic]
- -resource compiler option [Visual Basic]
- /res compiler option [Visual Basic]
- res compiler option [Visual Basic]
- -res compiler option [Visual Basic]
- resource compiler option [Visual Basic]
ms.assetid: eee2f227-91f2-4f2b-a9d6-1c51c5320858
ms.openlocfilehash: 830d89ab4f4063aa12d12a5206b76e49c5355708
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100474103"
---
# <a name="-resource-visual-basic"></a>-recurso (Visual Basic)

Insere um recurso gerenciado em um assembly.  
  
## <a name="syntax"></a>Syntax  
  
```console  
-resource:filename[,identifier[,public|private]]  
```

ou  

```console
-res:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Termo|Definição|  
|---|---|  
|`filename`|Obrigatório. O nome do arquivo de recurso a ser inserido no arquivo de saída. Por padrão, `filename` é público no assembly. Coloque o nome de arquivo entre aspas ("") se ele contiver um espaço.|  
|`identifier`|Opcional. O nome lógico do recurso; o nome usado para carregá-lo. O padrão é o nome do arquivo. Opcionalmente, você pode especificar se o recurso é público ou privado no manifesto do assembly, como com o seguinte: `-res:filename.res, myname.res, public`|  
  
## <a name="remarks"></a>Comentários  

 Use `-linkresource` para vincular um recurso a um assembly sem colocar o arquivo de recurso no arquivo de saída.  
  
 Se `filename` for um arquivo de recurso .NET Framework criado, por exemplo, pelo [Resgen.exe (gerador de arquivo de recurso)](../../../framework/tools/resgen-exe-resource-file-generator.md) ou no ambiente de desenvolvimento, ele poderá ser acessado com membros no <xref:System.Resources> namespace (consulte <xref:System.Resources.ResourceManager> para obter mais informações). Para acessar todos os outros recursos em tempo de execução, use um dos seguintes métodos: <xref:System.Reflection.Assembly.GetManifestResourceInfo%2A> , <xref:System.Reflection.Assembly.GetManifestResourceNames%2A> ou <xref:System.Reflection.Assembly.GetManifestResourceStream%2A> .  
  
 A forma abreviada de `-resource` é `-res`.  
  
 Para obter informações sobre como definir `-resource` no IDE do Visual Studio, consulte [Gerenciando recursos de aplicativos (.net)](/visualstudio/ide/managing-application-resources-dotnet).  
  
## <a name="example"></a>Exemplo  

 O código a seguir compila `In.vb` e anexa o arquivo de recurso `Rf.resource` .  
  
```console
vbc -res:rf.resource in.vb  
```  
  
## <a name="see-also"></a>Consulte também

- [Compilador de linha de comando do Visual Basic](index.md)
- [-win32resource](win32resource.md)
- [-linkresource (Visual Basic)](linkresource.md)
- [-Target (Visual Basic)](target.md)
- [Linhas de Comando de Compilação de Exemplo](sample-compilation-command-lines.md)
