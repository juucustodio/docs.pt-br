---
description: 'Saiba mais sobre: função InitDbgTransportManager'
title: Função InitDbgTransportManager
ms.date: 03/30/2017
api_name:
- InitDbgTransportManager
api_location:
- mscordbi_macx86.dll
api_type:
- COM
f1_keywords:
- InitDbgTransportManager
helpviewer_keywords:
- remote debugging API [Silverlight]
- InitDbgTransportManager function
- Silverlight, remote debugging
ms.assetid: a30102ff-c52e-48c9-b3a9-aa14286a42b2
topic_type:
- apiref
ms.openlocfilehash: 19cdfcbe3a5b120c11fc781476410833997b8c6e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790432"
---
# <a name="initdbgtransportmanager-function"></a>Função InitDbgTransportManager

Inicializa o Gerenciador de transporte para se conectar a um destino remoto para enumeração de processo e tempo de execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT InitDbgTransportManager ();  
```  
  
## <a name="return-value"></a>Valor retornado  

 S_OK  
 Sucesso.  
  
 E_OUTOFMEMORY  
 A função não pôde alocar memória para um Gerenciador de transporte.  
  
 E_FAIL (ou outros códigos de retorno de E_)  
 Outras falhas.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CoreClrRemoteDebuggingInterfaces. h  
  
 **Biblioteca:** mscordbi_macx86.dll  
  
 **Versões do .NET Framework:** 3,5 SP1
