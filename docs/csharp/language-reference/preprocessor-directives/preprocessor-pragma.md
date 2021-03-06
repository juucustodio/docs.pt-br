---
description: '#pragma – Referência de C#'
title: '#pragma – Referência de C#'
ms.date: 07/20/2015
f1_keywords:
- '#pragma'
helpviewer_keywords:
- '#pragma directive [C#]'
ms.assetid: 5b7944cd-d402-46a1-ad8f-feffb2d83673
ms.openlocfilehash: 97d7a786c83a8be21f7fd38873061dba0f9278ae
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2020
ms.locfileid: "89137949"
---
# <a name="pragma-c-reference"></a>#pragma (Referência de C#)
O `#pragma` fornece ao compilador instruções especiais para a compilação do arquivo no qual ele é exibido. O compilador deve dar suporte às instruções. Em outras palavras, não é possível usar `#pragma` para criar instruções personalizadas de pré-processamento. O compilador Microsoft C# dá suporte a estas duas `#pragma` instruções:  
  
 [aviso de #pragma](./preprocessor-pragma-warning.md)  
  
 [soma de verificação de #pragma](./preprocessor-pragma-checksum.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```csharp
#pragma pragma-name pragma-arguments  
```  
  
## <a name="parameters"></a>Parâmetros  
 `pragma-name`  
 O nome de um pragma reconhecido.  
  
 `pragma-arguments`  
 Argumentos específicos do pragma.  
  
## <a name="see-also"></a>Confira também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Diretivas de pré-processador do C#](./index.md)
- [aviso de #pragma](./preprocessor-pragma-warning.md)
- [soma de verificação de #pragma](./preprocessor-pragma-checksum.md)
