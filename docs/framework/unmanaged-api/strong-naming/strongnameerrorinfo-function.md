---
description: 'Saiba mais sobre: Função StrongNameErrorInfo'
title: Função StrongNameErrorInfo
ms.date: 03/30/2017
api_name:
- StrongNameErrorInfo
api_location:
- mscoree.dll
- mscorsn.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameErrorInfo
helpviewer_keywords:
- StrongNameErrorInfo function [.NET Framework strong naming]
ms.assetid: e91bf8c3-7c26-4732-938e-2e5b04abfc99
topic_type:
- apiref
ms.openlocfilehash: a02e5f3d101a34c8ed13cb0f70fd2e95d945cb4e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646394"
---
# <a name="strongnameerrorinfo-function"></a>Função StrongNameErrorInfo

Obtém o último código de erro que foi gerado por uma das funções de nome forte.  
  
 Esta função foi preterida.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT StrongNameErrorInfo ();
```  
  
## <a name="return-value"></a>Valor retornado  

 O último código de erro COM definido por uma das funções de nome forte.  
  
## <a name="remarks"></a>Comentários  

 A maioria dos métodos de nome forte retorna uma simples `true` ou uma `false` indicação de conclusão bem-sucedida. Use a `StrongNameErrorInfo` função para recuperar um HRESULT que especifica o último erro gerado pelas funções de nome forte.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** StrongName. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
