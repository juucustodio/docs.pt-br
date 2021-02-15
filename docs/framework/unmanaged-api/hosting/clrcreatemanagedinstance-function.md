---
description: 'Saiba mais sobre: função ClrCreateManagedInstance'
title: Função ClrCreateManagedInstance
ms.date: 03/30/2017
api_name:
- ClrCreateManagedInstance
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- ClrCreateManagedInstance
helpviewer_keywords:
- ClrCreateManagedInstance function [.NET Framework hosting]
ms.assetid: 58ba42c0-4857-43bf-a039-73a4dc6544c2
topic_type:
- apiref
ms.openlocfilehash: b6d3b014f54dd563e53cd8a4c48907d01945015f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799922"
---
# <a name="clrcreatemanagedinstance-function"></a>Função ClrCreateManagedInstance

Cria uma instância do tipo gerenciado especificado.  
  
 Essa função foi preterida no .NET Framework 4. Use a ativação COM para criar uma instância do tipo gerenciado ou use a hospedagem (consulte [interfaces de hospedagem do CLR adicionadas no .NET Framework 4 e 4,5](clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md)).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
STDAPI ClrCreateManagedInstance (  
    [in]  LPCWSTR  pTypeName,
    [in]  REFIID   riid,
    [out] void     **ppObject  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pTypeName`  
 no Um ponteiro para o nome do tipo de instância que está sendo solicitado.  
  
 `riid`  
 no O `IID` do tipo de instância que está sendo solicitado.  
  
 `ppObject`  
 fora Um ponteiro para um ponteiro para uma instância do tipo gerenciado que foi solicitado pelo chamador.  
  
## <a name="remarks"></a>Comentários  

 O Common Language Runtime já deve estar carregado em um processo. Por exemplo, ele pode ser carregado usando uma chamada para a função [CorBindToRuntimeEx](corbindtoruntimeex-function.md) antes que a `ClrCreateManagedInstance` função seja chamada. Se o tempo de execução não for carregado, o `ClrCreateManagedInstance` primeiro tentará carregar v 1.0.3705 do tempo de execução. Se isso falhar, ele tentará carregar a versão mais recente do tempo de execução.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
- [Hospedagem](index.md)
