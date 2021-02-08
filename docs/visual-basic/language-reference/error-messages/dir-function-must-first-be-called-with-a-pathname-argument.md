---
description: "Saiba mais sobre a função: dir ' deve ser chamada primeiro com um argumento ' PathName '"
title: A função 'Dir' deve ser chamada primeiro com um argumento 'PathName'
ms.date: 07/20/2015
f1_keywords:
- vbrDIR_IllegalCall
ms.assetid: 7b5d149f-be91-4ac3-8262-86a360894e7d
ms.openlocfilehash: ee492a269d41e8c9fe1fddbd59210b59fbe8618c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796581"
---
# <a name="dir-function-must-first-be-called-with-a-pathname-argument"></a>A função 'Dir' deve ser chamada primeiro com um argumento 'PathName'

Uma chamada inicial para a `Dir` função não inclui o `PathName` argumento. A primeira chamada para `Dir` deve incluir uma `PathName` , mas as chamadas subsequentes para não `Dir` precisam incluir parâmetros para recuperar o próximo item.

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Forneça um `PathName` argumento na chamada de função.

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualBasic.FileSystem.Dir%2A>
