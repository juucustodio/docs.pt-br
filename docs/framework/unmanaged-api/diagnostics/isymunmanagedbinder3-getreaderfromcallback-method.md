---
description: 'Saiba mais sobre o método: ISymUnmanagedBinder3:: GetReaderFromCallback'
title: Método ISymUnmanagedBinder3::GetReaderFromCallback
ms.date: 03/30/2017
api_name:
- ISymUnmanagedBinder3.GetReaderFromCallback
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedBinder3::GetReaderFromCallback
helpviewer_keywords:
- GetReaderFromCallback method [.NET Framework debugging]
- ISymUnmanagedBinder3::GetReaderFromCallback method [.NET Framework debugging]
ms.assetid: 4ef83bd2-3d8e-499e-8a12-d9d6fd6ced30
topic_type:
- apiref
ms.openlocfilehash: ba7c819678fee7625f3cddb29d99f5d7f4c6f991
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689866"
---
# <a name="isymunmanagedbinder3getreaderfromcallback-method"></a>Método ISymUnmanagedBinder3::GetReaderFromCallback

Permite que o usuário implemente ou forneça por meio de um retorno de chamada `IID_IDiaReadExeAtRVACallback` ou `IID_IDiaReadExeAtOffsetCallback` para obter as informações do diretório de depuração da memória.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetReaderFromCallback(  
    [in]  IUnknown     *importer,  
    [in]  const WCHAR  *fileName,  
    [in]  const WCHAR  *searchPath,  
    [in]  ULONG32      searchPolicy,  
    [in]  IUnknown     *callback,  
    [out,retval] ISymUnmanagedReader  **pRetVal);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `importer`  
 no Um ponteiro para a interface de importação de metadados.  
  
 `fileName`  
 no Um ponteiro para o nome do arquivo.  
  
 `searchPath`  
 no Um ponteiro para o caminho de pesquisa.  
  
 `searchPolicy`  
 no Um valor da enumeração [CorSymSearchPolicyAttributes](corsymsearchpolicyattributes-enumeration.md) que especifica a política a ser usada ao fazer uma pesquisa por um leitor de símbolo.  
  
 `callback`  
 no Um ponteiro para a função de retorno de chamada.  
  
 `pRetVal`  
 fora Um ponteiro que é definido para a interface [ISymUnmanagedReader](isymunmanagedreader-interface.md) retornada.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedBinder3](isymunmanagedbinder3-interface.md)
