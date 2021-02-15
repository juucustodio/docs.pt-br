---
description: 'Saiba mais sobre o método: ISymUnmanagedENCUpdate:: UpdateSymbolStore2'
title: Método ISymUnmanagedENCUpdate::UpdateSymbolStore2
ms.date: 03/30/2017
api_name:
- ISymUnmanagedENCUpdate.UpdateSymbolStore2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedENCUpdate::UpdateSymbolStore2
helpviewer_keywords:
- ISymUnmanagedENCUpdate::UpdateSymbolStore2 method [.NET Framework debugging]
- UpdateSymbolStore2 method [.NET Framework debugging]
ms.assetid: 35588317-6184-485c-ab41-4b15fc1765d9
topic_type:
- apiref
ms.openlocfilehash: f2e5cbf51c1bab3a538fbf5a3e5824739fa3b250
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790133"
---
# <a name="isymunmanagedencupdateupdatesymbolstore2-method"></a>Método ISymUnmanagedENCUpdate::UpdateSymbolStore2

Permite que um compilador omita funções que não foram modificadas do fluxo do banco de dados do programa (PDB), desde que as informações da linha atendam aos requisitos. As informações de linha corretas podem ser determinadas com as informações da linha PDB antiga e um Delta para todas as linhas na função.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT UpdateSymbolStore2(  
    [in]  IStream      *pIStream,  
    [in]  SYMLINEDELTA* pDeltaLines,  
    [in]  ULONG         cDeltaLines);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pIStream`  
 no Um ponteiro para um [IStream](/windows/desktop/api/objidl/nn-objidl-istream) que contém as informações de linha.  
  
 `pDeltaLines`  
 no Um ponteiro para uma estrutura [SYMLINEDELTA](symlinedelta-structure.md) que contém as linhas que foram alteradas.  
  
 `cDeltaLines`  
 no Um `ULONG` que representa o número de linhas que foram alteradas.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedENCUpdate](isymunmanagedencupdate-interface.md)
