---
description: 'Saiba mais sobre: _CorDllMain função'
title: Função _CorDllMain
ms.date: 03/30/2017
api_name:
- _CorDllMain
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- _CorDllMain
helpviewer_keywords:
- _CorDllMain function [.NET Framework hosting]
ms.assetid: bc7b51cf-39d3-48ec-a5cb-2f179fbefff8
topic_type:
- apiref
ms.openlocfilehash: 442afae3a627eb684a86c02fbc6e546aa804b7a5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99717141"
---
# <a name="_cordllmain-function"></a>\_Função CorDllMain

Inicializa o Common Language Runtime (CLR), localiza o ponto de entrada gerenciado no cabeçalho CLR do assembly de DLL e começa a execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
BOOL STDMETHODCALLTYPE _CorDllMain (  
   [in] HINSTANCE hInst,  
   [in] DWORD     dwReason,  
   [in] LPVOID    lpReserved  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `hInst`  
 no O identificador de instância do módulo carregado.  
  
 `dwReason`  
 no Indica por que a função de ponto de entrada de DLL está sendo chamada. Esse parâmetro pode ser um dos seguintes valores: DLL \_ PROCESS_ATTACH, dll de \_ thread \_ Attach, dll \_ \_ de anexação de thread \_ ou \_ reanexação de processo de dll. Para obter descrições desses valores, consulte a `DllMain` documentação no Platform SDK.  
  
 `lpReserved`  
 no Não utilizado.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna `true` para êxito e `false` se ocorre um erro.  
  
## <a name="remarks"></a>Comentários  

 Essa função é chamada pelo carregador do sistema operacional para assemblies DLL. Para assemblies executáveis, o carregador chama a função [ \_ CorExeMain](corexemain-function.md) em vez disso.  
  
 O carregador do sistema operacional chama esse método, independentemente do ponto de entrada especificado no arquivo DLL.  
  
A `_CorDllMain` função é chamada diretamente pelo carregador do sistema operacional.
  
 Para obter informações adicionais, consulte a seção comentários no tópico [ \_ CorValidateImage](corvalidateimage-function.md) .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Incluído como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções estáticas globais de metadados](../metadata/metadata-global-static-functions.md)
