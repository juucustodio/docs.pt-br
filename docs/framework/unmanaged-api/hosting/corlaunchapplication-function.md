---
description: 'Saiba mais sobre: função CorLaunchApplication'
title: Função CorLaunchApplication
ms.date: 03/30/2017
api_name:
- CorLaunchApplication
api_location:
- mscoree.dll
- clr.dll
api_type:
- COM
f1_keywords:
- CorLaunchApplication
helpviewer_keywords:
- CorLaunchApplication function [.NET Framework hosting]
ms.assetid: 71f362a9-8fe2-47ce-9302-05a645cf3d7d
topic_type:
- apiref
ms.openlocfilehash: 89f1f37ddde69fb5ecc24fd9dfd0d0c27d5fac40
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99716946"
---
# <a name="corlaunchapplication-function"></a>Função CorLaunchApplication

Inicia o aplicativo no caminho de rede especificado, usando os manifestos especificados e outros dados de aplicativo.  
  
 Essa função foi preterida no .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CorLaunchApplication (  
    [in]  HOST_TYPE                dwClickOnceHost,  
    [in]  LPCWSTR                  pwzAppFullName,  
    [in]  DWORD                    dwManifestPaths,  
    [in]  LPCWSTR                 *ppwzManifestPaths,  
    [in]  DWORD                    dwActivationData,  
    [in]  LPCWSTR                 *ppwzActivationData,  
    [out] LPPROCESS_INFORMATION    lpProcessInformation  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwClickOnceHost`  
 no Um valor da enumeração [HOST_TYPE](host-type-enumeration.md) que especifica o tipo de host que está iniciando o aplicativo.  
  
 `pwzAppFullName`  
 no O nome completo do aplicativo que está sendo iniciado.  
  
 `dwManifestPaths`  
 no O número de caminhos de manifesto para o aplicativo.  
  
 `ppwzManifestPaths`  
 no Uma matriz de cadeias de caracteres, cada uma delas especifica um caminho para um manifesto para o aplicativo que está sendo iniciado.  
  
 `dwActivationData`  
 no O número de itens de dados de ativação para o aplicativo que está sendo iniciado.  
  
 `ppwzActivationData`  
 no Uma matriz de cadeias de caracteres, cada uma delas é um item de dados de ativação para o aplicativo que está sendo iniciado.  
  
 `lpProcessInformation`  
 fora Um ponteiro para informações sobre o processo no qual o aplicativo foi carregado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Funções de hospedagem CLR reprovadas](deprecated-clr-hosting-functions.md)
