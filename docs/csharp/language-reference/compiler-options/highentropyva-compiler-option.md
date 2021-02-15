---
description: -highentropyva (opções do compilador C#)
title: -highentropyva (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /highentropyva
helpviewer_keywords:
- /highentropyva compiler option [C#]
- -highentropyva compiler option [C#]
- highentropyva compiler option [C#]
ms.assetid: eaf409b3-384e-49dd-9417-62453658f421
ms.openlocfilehash: f3cdeb5e63d632fecbbd94501558cc53c28a918a
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91173198"
---
# <a name="-highentropyva-c-compiler-options"></a>-highentropyva (opções do compilador C#)

A opção do compilador **-highentropyva** informa ao kernel do Windows se um determinado executável é compatível com ASLR (Address Space Layout Randomization) de alta entropia.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-highentropyva[+ | -]  
```  
  
## <a name="arguments"></a>Argumentos  

 `+` &#124; `-`  
 Essa opção especifica que um executável de 64 bits ou um executável que está marcado com a opção do compilador [-platform:anycpu](./platform-compiler-option.md) é compatível com um espaço de endereço virtual de alta entropia. A opção está desabilitada por padrão. Use **-highentropyva+** ou **-highentropyva** para habilitá-la.  
  
## <a name="remarks"></a>Comentários  

 A opção **-highentropyva** permite que as versões compatíveis do kernel do Windows usem níveis mais altos de entropia ao randomizar o layout do espaço de endereço de um processo como parte da ASLR. O uso de níveis mais altos de entropia significa que um número maior de endereços pode ser alocado para regiões de memória como pilhas e heaps. Como resultado, é mais difícil adivinhar a localização de uma região específica da memória.  
  
 Quando a opção do compilador **-highentropyva** é especificada, o executável de destino e todos os módulos dos quais ele depende devem ser capazes de manipular valores de ponteiro que sejam maiores que 4 GB (gigabytes) quando eles estiverem em execução como um processo de 64 bits.
