---
description: "Saiba mais sobre: a função ' dir ' deve ser chamada primeiro com um argumento ' PathName '"
title: A função 'Dir' deve ser chamada primeiro com um argumento 'PathName'
ms.date: 07/20/2015
f1_keywords:
- vbrDIR_IllegalCall
ms.assetid: 7b5d149f-be91-4ac3-8262-86a360894e7d
ms.openlocfilehash: 076828978b27911a97a4767cde1b1d7b04317a31
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100479966"
---
# <a name="dir-function-must-first-be-called-with-a-pathname-argument"></a>A função 'Dir' deve ser chamada primeiro com um argumento 'PathName'

Uma chamada inicial para a `Dir` função não inclui o `PathName` argumento. A primeira chamada para `Dir` deve incluir uma `PathName` , mas as chamadas subsequentes para não `Dir` precisam incluir parâmetros para recuperar o próximo item.

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Forneça um `PathName` argumento na chamada de função.

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualBasic.FileSystem.Dir%2A>
