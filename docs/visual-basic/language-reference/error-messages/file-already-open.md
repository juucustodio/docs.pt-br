---
description: 'Saiba mais sobre: o arquivo já está aberto'
title: Arquivo já aberto
ms.date: 07/20/2015
f1_keywords:
- vbrID55
ms.assetid: d674a0fb-ef16-4cc2-9da7-709a8a07dbea
ms.openlocfilehash: 2f3345c15f4a3095a8e733c2c8424edb25b4dee6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796295"
---
# <a name="file-already-open"></a>Arquivo já aberto

Às vezes, um arquivo deve ser fechado antes que outra `FileOpen` ou outra operação possa ocorrer. Entre as possíveis causas desse erro estão:

- Uma operação de modo de saída sequencial `FileOpen` foi executada para um arquivo que já está aberto

- Uma instrução refere-se a um arquivo aberto.

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Feche o arquivo antes de executar a instrução.

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualBasic.FileSystem.FileOpen%2A>
