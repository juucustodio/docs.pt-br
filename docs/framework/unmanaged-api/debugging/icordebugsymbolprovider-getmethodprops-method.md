---
description: 'Saiba mais sobre o método: ICorDebugSymbolProvider:: GetMethodProps'
title: 'Método ICorDebugSymbolProvider:: GetMethodProps'
ms.date: 03/30/2017
ms.assetid: 8f836b80-b7a5-460b-bf76-5f0e45652aea
ms.openlocfilehash: 53a329426ecadfe5559c0e6a08ffbd250163e177
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99659719"
---
# <a name="icordebugsymbolprovidergetmethodprops-method"></a>Método ICorDebugSymbolProvider:: GetMethodProps

Retorna informações sobre as propriedades do método, como o token de metadados do método e informações sobre seus parâmetros genéricos, considerando um endereço virtual relativo (RVA) nesse método.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetMethodProps(  
   [in]  ULONG32 codeRva,  
   [out] mdToken *pMethodToken,  
   [out] ULONG32 *pcGenericParams,  
   [in]  ULONG32 cbSignature,  
   [out] ULONG32 *pcbSignature,  
   [out, size_is(cbSignature), length_is(*pcbSignature)] BYTE signature[]  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `codeRVA`  
 no Um endereço virtual relativo no método sobre quais informações serão recuperadas.  
  
 `pMethodToken`  
 fora Um ponteiro para o token de metadados do método.  
  
 `pcGenericParams`  
 fora Um ponteiro para o número de parâmetros genéricos associados a este método.  
  
 `cbSignature`  
 no O tamanho da `signature` matriz. Consulte a seção Comentários.  
  
 `pcbSignature`  
 fora Um ponteiro para o tamanho da matriz retornada `signature` .  
  
 `signature`  
 fora Um buffer que contém as assinaturas TypeSpec de todos os parâmetros genéricos.  
  
## <a name="remarks"></a>Comentários  

 Para obter o tamanho necessário da matriz do método `signature` , defina o `cbSignature` argumento como 0 e `signature` como **nulo**. Quando o método retornar, `pcbSignature` conterá o número de bytes necessários para a `signature` matriz.  
  
> [!NOTE]
> Esse método está disponível somente com .NET Native.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Método GetTypeProps](icordebugsymbolprovider-gettypeprops-method.md)
- [Interface ICorDebugSymbolProvider](icordebugsymbolprovider-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
