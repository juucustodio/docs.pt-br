---
description: Saiba mais sobre:-sdkpath
title: -sdkpath
ms.date: 07/20/2015
f1_keywords:
- sdkpath
- -sdkpath
helpviewer_keywords:
- -sdkpath compiler option [Visual Basic]
- /sdkpath compiler option [Visual Basic]
- sdkpath compiler option [Visual Basic]
ms.assetid: fec8a3f1-b791-4a37-8af7-344859f8212d
ms.openlocfilehash: 3c593d56924f4b903540b2392cb86b31cae09cc8
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100473986"
---
# <a name="-sdkpath"></a>-sdkpath

Especifica o local de mscorlib.dll e Microsoft.VisualBasic.dll.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-sdkpath:path  
```  
  
## <a name="arguments"></a>Argumentos  

 `path`  
 O diretório que contém as versões de mscorlib.dll e Microsoft.VisualBasic.dll a serem usadas para compilação. Esse caminho não é verificado até que seja carregado. Coloque o nome do diretório entre aspas ("") se ele contiver um espaço.  
  
## <a name="remarks"></a>Comentários  

 Essa opção informa o compilador de Visual Basic para carregar os arquivos de mscorlib.dll e Microsoft.VisualBasic.dll de um local não padrão. A `-sdkpath` opção foi projetada para ser usada com [-netcf](netcf.md). O .NET Compact Framework usa versões diferentes dessas bibliotecas de suporte para evitar o uso de tipos e recursos de idioma não encontrados nos dispositivos.  
  
> [!NOTE]
> A `-sdkpath` opção não está disponível no ambiente de desenvolvimento do Visual Studio; ela está disponível somente durante a compilação na linha de comando. A `-sdkpath` opção é definida quando um projeto de dispositivo Visual Basic é carregado.  
  
 Você pode especificar que o compilador deve compilar sem uma referência para a biblioteca de tempo de execução Visual Basic usando a `-vbruntime` opção do compilador. Para obter mais informações, consulte [-vbruntime](vbruntime.md).  
  
## <a name="example"></a>Exemplo  

 O código a seguir é compilado `Myfile.vb` com o .NET Compact Framework, usando as versões do Mscorlib.dll e Microsoft.VisualBasic.dll encontradas no diretório de instalação padrão do .NET Compact Framework na unidade C. Normalmente, você usaria a versão mais recente do .NET Compact Framework.  
  
```console
vbc -netcf -sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb  
```  
  
## <a name="see-also"></a>Consulte também

- [Compilador de linha de comando do Visual Basic](index.md)
- [Linhas de Comando de Compilação de Exemplo](sample-compilation-command-lines.md)
- [-netcf](netcf.md)
- [-vbruntime](vbruntime.md)
