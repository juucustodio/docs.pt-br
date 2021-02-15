---
description: -codepage (opções do compilador C#)
title: -codepage (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /codepage
helpviewer_keywords:
- /codepage compiler option [C#]
- codepage compiler option [C#]
- -codepage compiler option [C#]
ms.assetid: 75942989-b69a-4308-90a0-840c73d2c478
ms.openlocfilehash: eda4ce5604beb25ae2d72ac94fbbe7dde9695820
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91196800"
---
# <a name="-codepage-c-compiler-options"></a>-codepage (opções do compilador C#)

Esta opção especifica qual página de código deve ser usada durante a compilação caso a página necessária não seja a página de código padrão atual do sistema.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-codepage:id  
```  
  
## <a name="arguments"></a>Argumentos  

 `id`  
 Especifica a ID da página de código a ser usada para todos os arquivos de código-fonte na compilação.  
  
## <a name="remarks"></a>Comentários  

 O compilador tentará primeiro interpretar todos os arquivos de origem como UTF-8. Se seus arquivos de código-fonte estiverem em uma codificação diferente de UTF-8 e usarem caracteres diferentes de caracteres ASCII de 7 bits, use a opção **-codepage** para especificar qual página de código deve ser usada. **-codepage** se aplica a todos os arquivos de código-fonte na compilação.  

 Consulte [GetCPInfo](/windows/desktop/api/winnls/nf-winnls-getcpinfo) para obter informações sobre como localizar quais páginas de código têm suporte do sistema.  
  
 Essa opção do compilador não está disponível no Visual Studio e não pode ser alterada programaticamente.  
  
## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
