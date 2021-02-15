---
description: '#pragma checksum – Referência de C#'
title: '#pragma checksum – Referência de C#'
ms.date: 07/20/2015
f1_keywords:
- '#pragma checksum'
helpviewer_keywords:
- '#pragma checksum [C#]'
ms.assetid: 3673e4ca-6098-4ec1-890f-8fceb2a794a2
ms.openlocfilehash: df665704ac813adbbf6473e81fad0a1c7ff616d0
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91168563"
---
# <a name="pragma-checksum-c-reference"></a>#pragma checksum (Referência de C#)

Gera somas de verificação para os arquivos de origem para ajudar na depuração de páginas do ASP.NET.  
  
## <a name="syntax"></a>Sintaxe  
  
```csharp
#pragma checksum "filename" "{guid}" "checksum bytes"  
```  
  
## <a name="parameters"></a>Parâmetros  

 `"filename"`  
 O nome do arquivo que exige o monitoramento de alterações ou atualizações.  
  
 `"{guid}"`  
 O GUID (identificador global exclusivo) do algoritmo de hash.  
  
 `"checksum_bytes"`  
 A cadeia de caracteres de dígitos hexadecimais que representa os bytes da soma de verificação. Deve ser um número par de dígitos hexadecimais. Um número ímpar de dígitos resulta em um aviso em tempo de compilação e a diretiva é ignorada.  
  
## <a name="remarks"></a>Comentários  

 O depurador do Visual Studio usa uma soma de verificação para certificar-se de sempre encontrar a fonte correta. O compilador calcula a soma de verificação para um arquivo de origem e, em seguida, emite a saída no arquivo PDB (banco de dados do programa). Em seguida, o depurador usa o PDB para comparar com a soma de verificação que ele calcula para o arquivo de origem.  
  
 Essa solução não funciona para projetos do ASP.NET, porque é a soma de verificação calculada é para o arquivo de origem gerado e não para o arquivo .aspx. Para resolver esse problema, a `#pragma checksum` fornece suporte à soma de verificação para páginas do ASP.NET.  
  
 Quando você cria um projeto do ASP.NET em Visual C#, o arquivo de origem gerado contém uma soma de verificação para o arquivo .aspx, do qual a fonte é gerada. Então, o compilador grava essas informações no arquivo PDB.  
  
 Se o compilador não encontrar uma diretiva `#pragma checksum` no arquivo, ele calcula a soma de verificação e grava o valor no arquivo PDB.  
  
## <a name="example"></a>Exemplo  
  
```csharp
class TestClass  
{  
    static int Main()  
    {  
        #pragma checksum "file.cs" "{406EA660-64CF-4C82-B6F0-42D48172A799}" "ab007f1d23d9" // New checksum  
    }  
}  
```  
  
## <a name="see-also"></a>Confira também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Diretivas de pré-processador do C#](./index.md)
