---
description: 'Saiba mais sobre: _CorExeMain função'
title: Função _CorExeMain
ms.date: 03/30/2017
api_name:
- _CorExeMain
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- _CorExeMain
helpviewer_keywords:
- _CorExeMain function [.NET Framework hosting]
ms.assetid: 898f76e2-16f4-4a63-b7d9-dad2d3824d8a
topic_type:
- apiref
ms.openlocfilehash: f94197598d01255c35712aa682f83ca9be1fb377
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99717115"
---
# <a name="_corexemain-function"></a>Função _CorExeMain

Inicializa o Common Language Runtime (CLR), localiza o ponto de entrada gerenciado no cabeçalho CLR do assembly executável e começa a execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
__int32 STDMETHODCALLTYPE _CorExeMain ();  
```  
  
## <a name="remarks"></a>Comentários  

 Essa função é chamada pelo carregador em processos criados a partir de assemblies executáveis gerenciados. Para assemblies DLL, o carregador chama a função [_CorDllMain](cordllmain-function.md) em vez disso.  
  
 O carregador do sistema operacional chama esse método, independentemente do ponto de entrada especificado no arquivo de imagem.  
  
 No Windows 98, Windows ME, Windows NT e Windows 2000, a `_CorExeMain` função é chamada indiretamente por meio de uma correção no carregador do sistema operacional. Em todas as outras versões do Windows, ele é chamado diretamente pelo carregador do sistema operacional.  
  
 Para obter informações adicionais, consulte a seção comentários no tópico [_CorValidateImage](corvalidateimage-function.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções estáticas globais de metadados](../metadata/metadata-global-static-functions.md)
