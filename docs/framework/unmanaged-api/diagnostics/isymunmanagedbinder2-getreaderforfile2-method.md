---
description: 'Saiba mais sobre o método: ISymUnmanagedBinder2:: GetReaderForFile2'
title: Método ISymUnmanagedBinder2::GetReaderForFile2
ms.date: 03/30/2017
api_name:
- ISymUnmanagedBinder2.GetReaderForFile2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedBinder2::GetReaderForFile2
helpviewer_keywords:
- ISymUnmanagedBinder2::GetReaderForFile2 method [.NET Framework debugging]
- GetReaderForFile2 method [.NET Framework debugging]
ms.assetid: dd92dcaf-403c-464d-a254-21594985dddd
topic_type:
- apiref
ms.openlocfilehash: c1a180ceec07c3087150613365acfce646adc34e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689931"
---
# <a name="isymunmanagedbinder2getreaderforfile2-method"></a>Método ISymUnmanagedBinder2::GetReaderForFile2

Dada uma interface de metadados e um nome de arquivo, retorna a interface [ISymUnmanagedReader](isymunmanagedreader-interface.md) correta que lerá os símbolos de depuração associados ao módulo.  
  
 Esse método fornece uma pesquisa mais abrangente para o arquivo de banco de dados do programa (PDB) do que o método [ISymUnmanagedBinder:: GetReaderForFile](isymunmanagedbinder-getreaderforfile-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetReaderForFile2(  
    [in]  IUnknown     *importer,  
    [in]  const WCHAR  *fileName,  
    [in]  const WCHAR  *searchPath,  
    [in]  ULONG32      searchPolicy,  
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
  
 `pRetVal`  
 fora Um ponteiro que é definido para a interface [ISymUnmanagedReader](isymunmanagedreader-interface.md) retornada.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso; caso contrário, E_FAIL ou algum outro código de erro.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="remarks"></a>Comentários  

 Esta versão do método pode pesquisar o arquivo PDB em áreas diferentes da direita ao lado do módulo. A política de pesquisa pode ser controlada pela combinação de [CorSymSearchPolicyAttributes](corsymsearchpolicyattributes-enumeration.md). Por exemplo, `AllowReferencePathAccess | AllowSymbolServerAccess` procura o PDB ao lado do arquivo executável e em um servidor de símbolos, mas não consulta o registro nem usa o caminho no arquivo executável. Se o `searchPath` parâmetro for fornecido, esses diretórios sempre serão pesquisados.  
  
## <a name="see-also"></a>Consulte também

- [Interface ISymUnmanagedBinder2](isymunmanagedbinder2-interface.md)
- [Método GetReaderForFile](isymunmanagedbinder-getreaderforfile-method.md)
