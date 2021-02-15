---
description: 'Saiba mais sobre: o formato da área de transferência não é válido'
title: Formato inválido de área de transferência
ms.date: 07/20/2015
f1_keywords:
- vbrID460
ms.assetid: 71a4a045-65bb-417d-b3bd-99a9fa3c53f6
ms.openlocfilehash: 58ba6197a14b005cf61d0783e19cb3f957dd2fca
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796750"
---
# <a name="clipboard-format-is-not-valid"></a>Formato inválido de área de transferência

O formato da área de transferência especificado é incompatível com o método que está sendo executado. Entre as possíveis causas desse erro estão:  
  
- Usando o método ou da área de transferência `GetText` `SetText` com um formato de área de transferência diferente de `vbCFText` ou `vbCFLink` .  
  
- Usando o método ou da área de transferência `GetData` `SetData` com um formato de área de transferência diferente de `vbCFBitmap` , `vbCFDIB` ou `vbCFMetafile` .  
  
- Usando os `GetData` `SetData` métodos ou de um `DataObject` com um formato de área de transferência no intervalo reservado pelo Microsoft Windows para formatos registrados (&HC000-&HFFFF), quando esse formato de área de transferência não foi registrado no Microsoft Windows.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Remova o formato inválido e especifique um válido.  
  
## <a name="see-also"></a>Consulte também

- [Área de transferência: adicionando outros formatos](/cpp/mfc/clipboard-adding-other-formats)
