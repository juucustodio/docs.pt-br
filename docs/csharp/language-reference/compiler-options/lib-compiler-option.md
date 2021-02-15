---
description: -lib (opções do compilador C#)
title: -lib (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /lib
helpviewer_keywords:
- lib compiler option [C#]
- -lib compiler option [C#]
- /lib compiler option [C#]
ms.assetid: b0efcc88-e8aa-4df4-a00b-8bdef70b7673
ms.openlocfilehash: 9478501ea98ec1b9d3ec2761bc4ebf3f6bef656c
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91152436"
---
# <a name="-lib-c-compiler-options"></a>-lib (opções do compilador C#)

A opção **-lib** especifica o local dos assemblies referenciados por meio da opção [-Reference (opções do compilador C#)](./reference-compiler-option.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-lib:dir1[,dir2]  
```  
  
## <a name="arguments"></a>Argumentos  

 `dir1`  
 Um diretório para o compilador examinar se um assembly referenciado não foi encontrado no diretório de trabalho atual (o diretório do qual você está invocando o compilador) ou no diretório de sistema do Common Language Runtime.  
  
 `dir2`  
 Um ou mais diretórios adicionais a serem pesquisados para referências de assembly. Separe os nomes de diretório adicionais com uma vírgula e não inclua espaços em branco entre eles.  
  
## <a name="remarks"></a>Comentários  

 O compilador pesquisa referências de assembly que não são totalmente qualificadas na seguinte ordem:  
  
1. Diretório de trabalho atual. Esse é o diretório do qual o compilador é invocado.  
  
2. O diretório de sistema do Common Language Runtime.  
  
3. Diretórios especificados por **-lib**.  
  
4. Diretórios especificados pela variável de ambiente LIB.  
  
 Use **-reference** para especificar uma referência de assembly.  
  
 **-lib** é aditivo; especificá-lo mais de uma vez acrescenta a valores anteriores.  
  
 Uma alternativa ao uso de **-lib** é copiar todos assemblies necessários para o diretório de trabalho; isso permitirá que você simplesmente passe o nome do assembly para **-reference**. Em seguida, é possível excluir os assemblies do diretório de trabalho. Como o caminho para o assembly dependente não foi especificado no manifesto do assembly, o aplicativo pode ser iniciado no computador de destino e localizará e usará o assembly no cache de assembly global.  
  
 O fato de o compilador poder referenciar o assembly não implica que o Common Language Runtime será capaz de localizar e carregar o assembly em tempo de execução. Consulte [Como o tempo de execução localiza assemblies](../../../framework/deployment/how-the-runtime-locates-assemblies.md) para obter detalhes sobre como o runtime pesquisa assemblies referenciados.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio  
  
1. Abra a caixa de diálogo **Páginas de Propriedades** do projeto.  
  
2. Clique na página de propriedades **Caminho de Referências**.  
  
3. Modifique o conteúdo da caixa de listagem.  
  
 Para obter informações sobre como definir essa opção do compilador programaticamente, consulte <xref:VSLangProj80.ProjectProperties3.ReferencePath%2A>.  
  
## <a name="example"></a>Exemplo  

 Compile t2.cs para criar um arquivo .exe. O compilador examinará referências de assembly no diretório de trabalho e no diretório raiz da unidade C.  
  
```console  
csc -lib:c:\ -reference:t2.dll t2.cs  
```  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
