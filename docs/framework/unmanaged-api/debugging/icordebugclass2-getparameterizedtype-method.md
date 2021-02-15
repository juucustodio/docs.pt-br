---
description: 'Saiba mais sobre o método: ICorDebugClass2:: GetParameterizedType'
title: Método ICorDebugClass2::GetParameterizedType
ms.date: 03/30/2017
api_name:
- ICorDebugClass2.GetParameterizedType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass2::GetParameterizedType
helpviewer_keywords:
- GetParameterizedType method [.NET Framework debugging]
- ICorDebugClass2::GetParameterizedType method [.NET Framework debugging]
ms.assetid: 94b591c4-9302-4af2-a510-089496afb036
topic_type:
- apiref
ms.openlocfilehash: 4810e10e88af9256a466579ee607c0ef314d984b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765016"
---
# <a name="icordebugclass2getparameterizedtype-method"></a>Método ICorDebugClass2::GetParameterizedType

Obtém a declaração de tipo para esta classe.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetParameterizedType (  
    [in] CorElementType                      elementType,  
    [in] ULONG32                             nTypeArgs,  
    [in, size_is(nTypeArgs)] ICorDebugType  *ppTypeArgs[],  
    [out] ICorDebugType                    **ppType  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `elementType`  
 no Um valor da enumeração CorElementType que especifica o tipo de elemento para esta classe: defina esse valor como ELEMENT_TYPE_VALUETYPE se esse ICorDebugClass2 representar um tipo de valor. Defina esse valor como ELEMENT_TYPE_CLASS se isso `ICorDebugClass2` representar um tipo complexo.  
  
 `nTypeArgs`  
 no O número de parâmetros de tipo, se o tipo for genérico. O número de parâmetros de tipo (se houver) deve corresponder ao número exigido pela classe.  
  
 `ppTypeArgs`  
 no Uma matriz de ponteiros, cada um dos quais aponta para um objeto ICorDebugType que representa um parâmetro de tipo. Se a classe for não genérica, esse valor será NULL.  
  
 `ppType`  
 fora Um ponteiro para o endereço de um `ICorDebugType` objeto que representa a declaração de tipo. Este objeto é equivalente a um <xref:System.Type> objeto no código gerenciado.  
  
## <a name="remarks"></a>Comentários  

 Se a classe for não genérica, ou seja, se ela não tiver parâmetros de tipo, `GetParameterizedType` simplesmente obtém o objeto de tipo de tempo de execução correspondente à classe. O `elementType` parâmetro deve ser definido como o tipo de elemento correto para a classe: ELEMENT_TYPE_VALUETYPE se a classe for um tipo de valor; caso contrário, ELEMENT_TYPE_CLASS.  
  
 Se a classe aceita parâmetros de tipo (por exemplo, `ArrayList<T>` ), você pode usar `GetParameterizedType` para construir um objeto de tipo para um tipo instanciado, como `ArrayList<int>` .  
  
## <a name="background-information"></a>Informações gerais  

 No .NET Framework versões 1,0 e 1,1, todos os tipos nos metadados podem ser mapeados diretamente para um tipo no processo em execução. Assim, um tipo de metadados e um tipo de tempo de execução tinham uma única representação no processo em execução. No entanto, um tipo genérico em metadados pode ser mapeado para várias instanciações diferentes do tipo no processo em execução. Por exemplo, o tipo de metadados `SortedList<K,V>` pode ser mapeado para `SortedList<String, EmployeeRecord>` , `SortedList<Int32, String>` , `SortedList<String,Array<Int32>>` e assim por diante. Portanto, você precisa de uma maneira de tratar a instanciação de tipo.  
  
 O .NET Framework versão 2,0 apresenta a `ICorDebugType` interface. Para um tipo genérico, um `ICorDebugClass` `ICorDebugClass2` objeto ou representa o tipo não instanciado ( `SortedList<K,V>` ), e um `ICorDebugType` objeto representa os vários tipos instanciados. Dado um `ICorDebugClass` `ICorDebugClass2` objeto ou, você pode criar um `ICorDebugType` objeto para qualquer instanciação chamando o `ICorDebugClass2::GetParameterizedType` método. Você também pode criar um `ICorDebugType` objeto para um tipo simples, como Int32, ou para um tipo não genérico.  
  
 A introdução do `ICorDebugType` objeto para representar a noção de tempo de execução de um tipo tem um efeito de ondulação em toda a API. As funções que anteriormente levaram `ICorDebugClass` um `ICorDebugClass2` objeto ou ou até um `CorElementType` valor são generalizadas para pegar um `ICorDebugType` objeto.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
