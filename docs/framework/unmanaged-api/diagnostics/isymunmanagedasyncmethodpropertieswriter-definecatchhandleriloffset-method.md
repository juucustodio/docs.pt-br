---
description: 'Saiba mais sobre: ISymUnmanagedAsyncMethodPropertiesWriter: método efineCatchHandlerILOffset de:D'
title: Método ISymUnmanagedAsyncMethodPropertiesWriter::DefineCatchHandlerILOffset
ms.date: 03/30/2017
ms.assetid: 92af7896-2201-408d-8b1b-23e28001eeac
ms.openlocfilehash: fcb2c6efa7ea83252a46a9b08cdfa7b2c14f09d1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737786"
---
# <a name="isymunmanagedasyncmethodpropertieswriterdefinecatchhandleriloffset-method"></a>Método ISymUnmanagedAsyncMethodPropertiesWriter::DefineCatchHandlerILOffset

Define o deslocamento de IL para o manipulador catch gerado pelo compilador que encapsula um método assíncrono.  
  
 O deslocamento de IL do catch gerado é usado pelo depurador para lidar com o Catch como se fosse um código não-usuário, embora possa ocorrer em um método de código de usuário. Em particular, ele é usado em resposta a um evento de exceção **CatchHandlerFound** .  
  
## <a name="syntax"></a>Sintaxe  
  
```idl  
HRESULT DefineCatchHandlerILOffset(    [in] ULONG32 catchHandlerOffset);  
```  
  
## <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`catchHandlerOffset`||  
  
## <a name="return-value"></a>Valor retornado  

 Retorna `HRESULT`.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedAsyncMethodPropertiesWriter](isymunmanagedasyncmethodpropertieswriter-interface.md)
