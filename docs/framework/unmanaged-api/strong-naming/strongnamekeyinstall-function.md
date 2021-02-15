---
description: 'Saiba mais sobre: função StrongNameKeyInstall'
title: Função StrongNameKeyInstall
ms.date: 03/30/2017
api_name:
- StrongNameKeyInstall
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameKeyInstall
helpviewer_keywords:
- StrongNameKeyInstall function [.NET Framework strong naming]
ms.assetid: e32fd546-7757-4681-be3d-658e93281e50
topic_type:
- apiref
ms.openlocfilehash: 0a5d3971ac0927dda7066405adc01a5c80b7faca
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99670535"
---
# <a name="strongnamekeyinstall-function"></a>Função StrongNameKeyInstall

Importa um par de chaves públicas/privadas em um contêiner.

Esta função foi preterida. Em vez disso, use o método [ICLRStrongName:: StrongNameKeyInstall](../hosting/iclrstrongname-strongnamekeyinstall-method.md) .

## <a name="syntax"></a>Sintaxe

```cpp
BOOLEAN StrongNameKeyInstall (
    [in]  LPCWSTR   wszKeyContainer,
    [in]  BYTE      *pbKeyBlob,
    [in]  ULONG     cbKeyBlob
);
```

## <a name="parameters"></a>Parâmetros

`wszKeyContainer`\
no O nome do contêiner de chave. `wszKeyContainer` deve ser uma cadeia de caracteres não vazia.

`pbKeyBlob`\
no O par de chaves binárias.

`cbKeyBlob`\
no O tamanho, em bytes, de `pbKeyBlob` .

## <a name="return-value"></a>Valor retornado

`true` após a conclusão bem-sucedida; caso contrário, `false` .

## <a name="remarks"></a>Comentários

Use a função [StrongNameKeyDelete](strongnamekeydelete-function.md) para excluir o contêiner de chave.

Se a `StrongNameKeyInstall` função não for concluída com êxito, chame a função [StrongNameErrorInfo](strongnameerrorinfo-function.md) para recuperar o último erro gerado.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** StrongName. h

**Biblioteca:** Incluído como um recurso no MsCorEE.dll

**.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

## <a name="see-also"></a>Consulte também

- [Método StrongNameKeyInstall](../hosting/iclrstrongname-strongnamekeyinstall-method.md)
- [Método StrongNameKeyDelete](../hosting/iclrstrongname-strongnamekeydelete-method.md)
- [Interface ICLRStrongName](../hosting/iclrstrongname-interface.md)
