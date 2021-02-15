---
description: 'Saiba mais sobre: método ISymUnmanagedReader:: Initialize'
title: Método ISymUnmanagedReader::Initialize
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.Initialize
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::Initialize
helpviewer_keywords:
- ISymUnmanagedReader::Initialize method [.NET Framework debugging]
- Initialize method, ISymUnmanagedReader interface [.NET Framework debugging]
ms.assetid: 8f0dd2fe-7df7-464e-91f4-5518c586bb5f
topic_type:
- apiref
ms.openlocfilehash: cf7f5df3efed7823fc36bd6c9fc56e0c49d17443
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99763872"
---
# <a name="isymunmanagedreaderinitialize-method"></a>Método ISymUnmanagedReader::Initialize

Inicializa o leitor de símbolos com a interface de importador de metadados à qual esse leitor será associado, juntamente com o nome de arquivo do módulo.  
  
> [!NOTE]
> Esse método pode ser chamado apenas uma vez e deve ser chamado antes de qualquer outro método de leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Initialize (  
    [in]  IUnknown     *importer,  
    [in]  const WCHAR  *filename,  
    [in]  const WCHAR  *searchPath,  
    [in]  IStream      *pIStream);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `importer`  
 no A interface de importador de metadados à qual este leitor será associado.  
  
 `filename`  
 no O nome do arquivo do módulo. `pIStream`Em vez disso, você pode usar o parâmetro.  
  
 `searchPath`  
 no O caminho para pesquisar. Esse parâmetro é opcional.  
  
 `pIStream`  
 no O fluxo de arquivos, usado como uma alternativa ao parâmetro filename.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="remarks"></a>Comentários  

 Você precisa especificar apenas um dos `filename` `pIStream` parâmetros ou, não ambos. O `searchPath` é opcional.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedReader](isymunmanagedreader-interface.md)
