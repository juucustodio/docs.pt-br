---
description: 'Saiba mais sobre: _CorExeMain2 função'
title: Função _CorExeMain2
ms.date: 03/30/2017
api_name:
- _CorExeMain2
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- _CorExeMain2
helpviewer_keywords:
- _CorExeMain2 function [.NET Framework hosting]
ms.assetid: 72ea68b4-689f-4733-9416-9664b75e8892
topic_type:
- apiref
ms.openlocfilehash: 4629ea2f6c2ba13351c409bc382077eea926b507
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99717089"
---
# <a name="_corexemain2-function"></a>Função _CorExeMain2

Executa o ponto de entrada no código mapeado de memória especificado. Essa função é chamada pelo carregador do sistema operacional.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
__int32 STDMETHODCALLTYPE _CorExeMain2 (  
   [in] PBYTE           pUnmappedPE,  
   [in] DWORD           cUnmappedPE,  
   [in] __in LPWSTR     pImageNameIn,  
   [in] __in LPWSTR     pLoadersFileName,  
   [in] __in LPWSTR     pCmdLine  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pUnmappedPE`  
 no Um ponteiro para o código de memória mapeada.  
  
 `cUnmappedPE`  
 no O número de elementos `pUnmappedPE` pode conter.  
  
 `pImageNameIn`  
 no Um ponteiro para o nome da imagem executável.  
  
 `pLoadersFileName`  
 no O nome do arquivo do carregador.  
  
 `pCmdLine`  
 no Parâmetros de linha de comando, se houver.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções estáticas globais de metadados](../metadata/metadata-global-static-functions.md)
