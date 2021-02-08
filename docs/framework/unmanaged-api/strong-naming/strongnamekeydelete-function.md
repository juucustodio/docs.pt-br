---
description: 'Saiba mais sobre: função StrongNameKeyDelete'
title: Função StrongNameKeyDelete
ms.date: 03/30/2017
api_name:
- StrongNameKeyDelete
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameKeyDelete
helpviewer_keywords:
- StrongNameKeyDelete function [.NET Framework strong naming]
ms.assetid: 313e71e4-1790-4d2f-b68b-5040ebd1c149
topic_type:
- apiref
ms.openlocfilehash: 9314d961f79e673925125c2362308f9ab4533e75
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781201"
---
# <a name="strongnamekeydelete-function"></a>Função StrongNameKeyDelete

Exclui o contêiner de chave especificado.

Esta função foi preterida. Em vez disso, use o método [ICLRStrongName:: StrongNameKeyDelete](../hosting/iclrstrongname-strongnamekeydelete-method.md) .

## <a name="syntax"></a>Sintaxe

```cpp
BOOLEAN StrongNameKeyDelete (
    [in]  LPCWSTR   wszKeyContainer
);
```

## <a name="parameters"></a>Parâmetros

`wszKeyContainer`\
no O nome do contêiner de chave a ser excluído.

## <a name="return-value"></a>Valor retornado

`true` após a conclusão bem-sucedida; caso contrário, `false` .

## <a name="remarks"></a>Comentários

Use a função [StrongNameKeyInstall](strongnamekeyinstall-function.md) para importar um par de chaves pública/privada para um contêiner.

Se a `StrongNameKeyDelete` função não for concluída com êxito, chame a função [StrongNameErrorInfo](strongnameerrorinfo-function.md) para recuperar o último erro gerado.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** StrongName. h

**Biblioteca:** Incluído como um recurso no MsCorEE.dll

**.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

## <a name="see-also"></a>Consulte também

- [Método StrongNameKeyDelete](../hosting/iclrstrongname-strongnamekeydelete-method.md)
- [Método StrongNameKeyInstall](../hosting/iclrstrongname-strongnamekeyinstall-method.md)
- [Interface ICLRStrongName](../hosting/iclrstrongname-interface.md)
