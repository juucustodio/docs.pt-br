---
description: 'Saiba mais sobre: função CreateHistoryReader'
title: Função CreateHistoryReader
ms.date: 03/30/2017
api_name:
- CreateHistoryReader
api_location:
- fusion.dll
api_type:
- DLLExport
f1_keywords:
- CreateHistoryReader
helpviewer_keywords:
- CreateHistoryReader function [.NET Framework fusion]
ms.assetid: 66a89acf-8c32-44c0-8787-960c99c7b3ec
topic_type:
- apiref
ms.openlocfilehash: 0943f3d0f3322d34ed92c0a96b909e4d63ec5e7f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99761116"
---
# <a name="createhistoryreader-function"></a>Função CreateHistoryReader

Cria um leitor de histórico para o arquivo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateHistoryReader (  
    [in]  LPCWSTR        wzFilePath,  
    [out] IHistoryReader **ppHistoryReader  
 );  
```  
  
## <a name="parameters"></a>Parâmetros  

 `wzFilePath`  
 no O caminho do arquivo.  
  
 `ppHistoryReader`  
 fora Após a conclusão bem-sucedida, contém um ponteiro para o leitor de histórico.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna códigos de erro COM padrão, conforme definido no WinError. h, além dos valores descritos na tabela a seguir.  
  
|Código de retorno|Descrição|  
|-----------------|-----------------|  
|S_OK|Indica que o método foi concluído com êxito.|  
|E_INVALIDARG|Indica se `wzFilePath` or `ppHistoryReader` está definido como uma referência nula.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Biblioteca:** Fusion.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções estáticas globais de fusão](fusion-global-static-functions.md)
