---
description: 'Saiba mais sobre: interface ISymUnmanagedReader'
title: Interface ISymUnmanagedReader
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader
helpviewer_keywords:
- ISymUnmanagedReader interface [.NET Framework debugging]
ms.assetid: aa3cc15d-058e-4e6f-b03e-39569646ba47
topic_type:
- apiref
ms.openlocfilehash: bad4fdbac3bf6f03fa0db79ce54a5b0ca897028f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99763794"
---
# <a name="isymunmanagedreader-interface"></a>Interface ISymUnmanagedReader

Representa um leitor de símbolo que fornece acesso a documentos, métodos e variáveis em um repositório de símbolos.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método GetDocument](isymunmanagedreader-getdocument-method.md)|Localiza um documento.|  
|[Método GetDocuments](isymunmanagedreader-getdocuments-method.md)|Retorna uma matriz de todos os documentos definidos no repositório de símbolos.|  
|[Método GetDocumentVersion](isymunmanagedreader-getdocumentversion-method.md)|Obtém a versão especificada do documento especificado.|  
|[Método GetGlobalVariables](isymunmanagedreader-getglobalvariables-method.md)|Retorna todas as variáveis globais.|  
|[Método GetMethod](isymunmanagedreader-getmethod-method.md)|Obtém um método de leitor de símbolo, dado um token de método.|  
|[Método GetMethodByVersion](isymunmanagedreader-getmethodbyversion-method.md)|Obtém um método de leitor de símbolo, dado um token de método e um número de versão de edição e cópia.|  
|[Método GetMethodFromDocumentPosition](isymunmanagedreader-getmethodfromdocumentposition-method.md)|Retorna o método que contém o ponto de interrupção na posição especificada em um documento.|  
|[Método GetMethodsFromDocumentPosition](isymunmanagedreader-getmethodsfromdocumentposition-method.md)|Retorna uma matriz de métodos, cada um contendo o ponto de interrupção na posição especificada em um documento.|  
|[Método GetMethodVersion](isymunmanagedreader-getmethodversion-method.md)|Obtém a versão do método.|  
|[Método GetNamespaces](isymunmanagedreader-getnamespaces-method.md)|Obtém os namespaces definidos no escopo global dentro deste armazenamento de símbolos.|  
|[Método GetSymAttribute](isymunmanagedreader-getsymattribute-method.md)|Obtém um atributo personalizado com base no seu nome.|  
|[Método GetSymbolStoreFileName](isymunmanagedreader-getsymbolstorefilename-method.md)|Fornece o nome de arquivo em disco do repositório de símbolos.|  
|[Método GetUserEntryPoint](isymunmanagedreader-getuserentrypoint-method.md)|Retorna o método que foi especificado como o ponto de entrada do usuário para o módulo, se houver.|  
|[Método GetVariables](isymunmanagedreader-getvariables-method.md)|Retornar uma variável não local, dado seu pai e nome.|  
|[Método Initialize](isymunmanagedreader-initialize-method.md)|Inicializa o leitor de símbolos com a interface de importador de metadados à qual esse leitor será associado, juntamente com o nome de arquivo do módulo.|  
|[Método ReplaceSymbolStore](isymunmanagedreader-replacesymbolstore-method.md)|Substitui o repositório de símbolos existente por um repositório de símbolos delta.|  
|[Método UpdateSymbolStore](isymunmanagedreader-updatesymbolstore-method.md)|Atualiza o repositório de símbolos existente com um repositório de símbolos delta.|  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de armazenamento de símbolo de diagnóstico](diagnostics-symbol-store-interfaces.md)
- [Interface ISymUnmanagedReader2](isymunmanagedreader2-interface.md)
