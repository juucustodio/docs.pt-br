---
description: 'Saiba mais sobre: método GetWin32ResBlob'
title: Método GetWin32ResBlob
ms.date: 03/30/2017
api_name:
- IALink.GetWin32ResBlob
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- GetWin32ResBlob
helpviewer_keywords:
- GetWin32ResBlob method
ms.assetid: 36997e04-f9f6-4254-a041-6767ac6c51d9
topic_type:
- apiref
ms.openlocfilehash: e1140b14bfba56dfac03c443a537d6d2188575b8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99718259"
---
# <a name="getwin32resblob-method"></a>Método GetWin32ResBlob

Recupera o blob de recursos do Win32. Chame esse método depois de definir as opções de assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetWin32ResBlob(  
    mdAssembly    AssemblyID,  
    mdToken       FileToken,  
    BOOL          fDll,  
    LPCWSTR       pszIconFile,  
    const void**  ppResBlob,  
    DWORD*        pcbResBlob  
) PURE;  
```  
  
## <a name="parameters"></a>Parâmetros  

 `AssemblyID`  
 ID do assembly.  
  
 `FileToken`  
 O token de arquivo usado para recuperar o nome de o FileName a ser usado ao construir o recurso de versão do Win32  
  
 `fDll`  
 TRUE se o arquivo for uma DLL, false para um EXE.  
  
 `pszIconFile`  
 Ícone opcional para inserir no blob de recursos.  
  
 `ppResBlob`  
 Recebe o blob de recursos.  
  
 `pcbResBlob`  
 Recebe o tamanho do blob.  
  
## <a name="return-value"></a>Valor retornado  

 Retorna S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 Requer ALink. h  
  
## <a name="see-also"></a>Consulte também

- [Interface IALink](ialink-interface.md)
- [Interface IALink2](ialink2-interface.md)
- [API do ALink](index.md)
