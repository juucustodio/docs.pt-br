---
description: 'Saiba mais sobre: interface ISymUnmanagedWriter'
title: Interface ISymUnmanagedWriter
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter
helpviewer_keywords:
- ISymUnmanagedWriter interface [.NET Framework debugging]
ms.assetid: 7d6733ec-f081-4166-bc17-de09e16dc304
topic_type:
- apiref
ms.openlocfilehash: 20fc0fd9b76b1aae4090582fe48a8a8e77d77c9f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99762234"
---
# <a name="isymunmanagedwriter-interface"></a>Interface ISymUnmanagedWriter

Representa um gravador de símbolo e fornece métodos para definir documentos, pontos de sequência, escopos lexicais e variáveis.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Abort](isymunmanagedwriter-abort-method.md)|Fecha o gravador de símbolo sem confirmar os símbolos para o repositório de símbolos.|  
|[Método Close](isymunmanagedwriter-close-method.md)|Fecha o gravador de símbolo depois de confirmar os símbolos para o repositório de símbolos.|  
|[Método CloseMethod](isymunmanagedwriter-closemethod-method.md)|Fecha o método atual. Depois que um método é fechado, nenhum símbolo pode ser definido dentro dele.|  
|[Método CloseNamespace](isymunmanagedwriter-closenamespace-method.md)|Fecha o namespace aberto mais recentemente.|  
|[Método CloseScope](isymunmanagedwriter-closescope-method.md)|Fecha o escopo léxico atual.|  
|[Método DefineConstant](isymunmanagedwriter-defineconstant-method.md)|Define um nome para um valor constante.|  
|[Método DefineDocument](isymunmanagedwriter-definedocument-method.md)|Define um documento de origem.|  
|[Método DefineField](isymunmanagedwriter-definefield-method.md)|Define uma única variável que não está dentro de um método.|  
|[Método DefineGlobalVariable](isymunmanagedwriter-defineglobalvariable-method.md)|Define uma única variável global.|  
|[Método DefineLocalVariable](isymunmanagedwriter-definelocalvariable-method.md)|Define uma única variável no escopo léxico atual.|  
|[Método DefineParameter](isymunmanagedwriter-defineparameter-method.md)|Define um único parâmetro no método atual.|  
|[Método DefineSequencePoints](isymunmanagedwriter-definesequencepoints-method.md)|Define um grupo de pontos de sequência dentro do método atual.|  
|[Método GetDebugInfo](isymunmanagedwriter-getdebuginfo-method.md)|Retorna as informações necessárias para um compilador gravar a entrada do diretório de depuração no cabeçalho do arquivo PE (executável portátil).|  
|[Método Initialize](isymunmanagedwriter-initialize-method.md)|Define a interface do emissor de metadados com a qual esse gravador será associado e define o nome do arquivo de saída para o qual os símbolos de depuração serão gravados.|  
|[Método Initialize2](isymunmanagedwriter-initialize2-method.md)|Define a interface do emissor de metadados com a qual este gravador será associado, define o nome do arquivo de saída para o qual os símbolos de depuração serão gravados e define o local final do arquivo de banco de dados do programa (PDB).|  
|[Método OpenMethod](isymunmanagedwriter-openmethod-method.md)|Abre um método no qual as informações de símbolo são emitidas.|  
|[Método OpenNamespace](isymunmanagedwriter-opennamespace-method.md)|Abre um novo namespace.|  
|[Método OpenScope](isymunmanagedwriter-openscope-method.md)|Abre um novo escopo léxico no método atual.|  
|[Método RemapToken](isymunmanagedwriter-remaptoken-method.md)|Notifica o gravador de símbolo de que um token de metadados foi remapeado conforme os metadados foram emitidos.|  
|[Método SetMethodSourceRange](isymunmanagedwriter-setmethodsourcerange-method.md)|Especifica os verdadeiros início e término de um método de dentro de um arquivo de origem.|  
|[Método SetScopeRange](isymunmanagedwriter-setscoperange-method.md)|Define o intervalo de deslocamento do escopo léxico especificado.|  
|[Método SetSymAttribute](isymunmanagedwriter-setsymattribute-method.md)|Define um atributo personalizado com base no seu nome.|  
|[Método SetUserEntryPoint](isymunmanagedwriter-setuserentrypoint-method.md)|Especifica o método definido pelo usuário que é o ponto de entrada para este módulo.|  
|[Método UsingNamespace](isymunmanagedwriter-usingnamespace-method.md)|Especifica que o nome de namespace totalmente qualificado fornecido está sendo usado dentro do escopo léxico aberto no momento.|  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de armazenamento de símbolo de diagnóstico](diagnostics-symbol-store-interfaces.md)
- [Interface ISymUnmanagedWriter2](isymunmanagedwriter2-interface.md)
- [Interface ISymUnmanagedWriter3](isymunmanagedwriter3-interface.md)
