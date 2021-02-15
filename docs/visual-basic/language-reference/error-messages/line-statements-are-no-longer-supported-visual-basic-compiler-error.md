---
description: "Saiba mais sobre: BC30830: não há mais suporte para instruções ' line '"
title: Instruções 'Line' não são mais compatíveis (erro de compilador do Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- bc30830
- vbc30830
helpviewer_keywords:
- BC30830
ms.assetid: 4734bc1d-882e-4555-b498-1f1ec0399d16
ms.openlocfilehash: 16696856cee365171000e7b0abc206c42d3f3174
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795866"
---
# <a name="bc30830-line-statements-are-no-longer-supported"></a>BC30830: não há mais suporte para instruções ' line '

Não há mais suporte para instruções de linha. A funcionalidade de e/s de arquivo está disponível `Microsoft.VisualBasic.FileSystem.LineInput` e a funcionalidade de gráficos está disponível como `System.Drawing.Graphics.DrawLine` .

 **ID do erro:** BC30830

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Se estiver executando o acesso ao arquivo, use `Microsoft.VisualBasic.FileSystem.LineInput` .

- Se estiver executando gráficos, use `System.Drawing.Graphics.Drawline` .

## <a name="see-also"></a>Consulte também

- <xref:System.IO>
- <xref:System.Drawing>
- [Access de arquivo com o Visual Basic](../../developing-apps/programming/drives-directories-files/file-access.md)
