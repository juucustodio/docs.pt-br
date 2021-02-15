---
description: 'Saiba mais sobre: interface ISymUnmanagedDocument'
title: Interface ISymUnmanagedDocument
ms.date: 03/30/2017
api_name:
- ISymUnmanagedDocument
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedDocument
helpviewer_keywords:
- ISymUnmanagedDocument interface [.NET Framework debugging]
ms.assetid: 5c26b366-6e81-467c-9dd0-02dd26fee0a3
topic_type:
- apiref
ms.openlocfilehash: cd1907e570dd15ebcac3ee12aa09c626c9bb7787
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99710134"
---
# <a name="isymunmanageddocument-interface"></a>Interface ISymUnmanagedDocument

Representa um documento referenciado por um repositório de símbolos. Um documento é definido por um Uniform Resource Locator (URL) e um GUID de tipo de documento. Você pode localizar o documento independentemente de como ele é armazenado usando a URL e o tipo de documento GUID. Você pode armazenar a origem do documento no repositório de símbolos e recuperá-lo por meio desta interface.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método FindClosestLine](isymunmanageddocument-findclosestline-method.md)|Retorna a linha mais próxima que é um ponto de sequência, dada uma linha neste documento que pode ou não ser um ponto de sequência.|  
|[Método GetCheckSum](isymunmanageddocument-getchecksum-method.md)|Obtém a soma de verificação.|  
|[Método GetCheckSumAlgorithmId](isymunmanageddocument-getchecksumalgorithmid-method.md)|Obtém o identificador de algoritmo de soma de verificação ou retorna um GUID de todos os zeros se não houver nenhuma soma de verificação.|  
|[Método GetDocumentType](isymunmanageddocument-getdocumenttype-method.md)|Obtém o tipo de documento deste documento.|  
|[Método GetLanguage](isymunmanageddocument-getlanguage-method.md)|Obtém o identificador de idioma deste documento.|  
|[Método GetLanguageVendor](isymunmanageddocument-getlanguagevendor-method.md)|Obtém o fornecedor do idioma deste documento.|  
|[Método GetSourceLength](isymunmanageddocument-getsourcelength-method.md)|Obtém o comprimento, em bytes, da origem inserida.|  
|[Método GetSourceRange](isymunmanageddocument-getsourcerange-method.md)|Retorna o intervalo especificado da fonte inserida para o buffer fornecido.|  
|[Método GetURL](isymunmanageddocument-geturl-method.md)|Retorna a URL deste documento.|  
|[Método HasEmbeddedSource](isymunmanageddocument-hasembeddedsource-method.md)|Retorna `true` se o documento tem origem inserida nos símbolos de depuração; caso contrário, retorna `false` .|  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de armazenamento de símbolo de diagnóstico](diagnostics-symbol-store-interfaces.md)
