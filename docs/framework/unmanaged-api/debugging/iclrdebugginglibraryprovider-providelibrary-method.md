---
description: 'Saiba mais sobre: ICLRDebuggingLibraryProvider: método rovideLibrary de:P'
title: Método ICLRDebuggingLibraryProvider::ProvideLibrary
ms.date: 03/30/2017
api_name:
- ICLRDebuggingLibraryProvider.ProvideLibrary Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDebuggingLibraryProvider::ProvideLibrary
helpviewer_keywords:
- ProvideLibrary method [.NET Framework debugging]
- ICLRDebuggingLibraryProvider::ProvideLibrary method [.NET Framework debugging]
ms.assetid: 86f06245-9517-49be-8d8c-ca5deaf34c02
topic_type:
- apiref
ms.openlocfilehash: 624061fb9b23af7a69616d4565586ac0fd129860
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99772609"
---
# <a name="iclrdebugginglibraryproviderprovidelibrary-method"></a>Método ICLRDebuggingLibraryProvider::ProvideLibrary

Obtém uma interface de retorno de chamada do provedor de biblioteca que permite que bibliotecas de depuração específicas à versão Common Language Runtime (CLR) sejam localizadas e carregadas sob demanda.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT ProvideLibrary(
     [in] const WCHAR* pwszFileName,
     [in] DWORD dwTimestamp,
     [in] DWORD dwSizeOfImage,
     [out] HMODULE* hModule);
```

## <a name="parameters"></a>Parâmetros

`pwszFilename` \
no O nome do módulo que está sendo solicitado.

`dwTimestamp` \
no O carimbo de data/hora armazenado no cabeçalho de arquivo COFF de arquivos PE.

`pLibraryProvider` \
no O `SizeOfImage` campo armazenado no cabeçalho de arquivo opcional COFF de arquivos PE.

`hModule` \
fora O identificador para o módulo solicitado.

## <a name="return-value"></a>Valor retornado

Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.

|HRESULT|Descrição|
|-------------|-----------------|
|S_OK|O método foi concluído com êxito.|

## <a name="exceptions"></a>Exceções

## <a name="remarks"></a>Comentários

`ProvideLibrary` permite que o depurador forneça módulos que são necessários para depurar arquivos CLR específicos, como mscordbi.dll e mscordacwks.dll. Os identificadores de módulo precisam permanecer válidos até que uma chamada para o método [ICLRDebugging:: CanUnloadNow](iclrdebugging-canunloadnow-method.md) indique que eles podem ser liberados. nesse ponto, é responsabilidade do chamador liberar os identificadores.

O depurador pode usar qualquer meio disponível para localizar ou adquirir o módulo de depuração.

> [!IMPORTANT]
> Esse recurso permite que o chamador da API forneça módulos que contêm um código executável e possivelmente mal-intencionado. Como uma precaução de segurança, o chamador não deve usar o `ProvideLibrary` para distribuir nenhum código que não esteja disposto a ser executado.
>
> Se um problema de segurança sério for descoberto em uma biblioteca já liberada, como mscordbi.dll ou mscordacwks.dll, o Shim poderá ser corrigido para reconhecer as versões inadequadas dos arquivos. O Shim pode emitir solicitações para as versões com patches dos arquivos e rejeitar as versões inadequadas se elas forem fornecidas em resposta a qualquer solicitação. Isso só poderá ocorrer se o usuário tiver corrigido o patch para uma nova versão do Shim. As versões sem patch continuarão vulneráveis.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** CorDebug.idl, CorDebug.h

**Biblioteca:** CorGuids.lib

**.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]

## <a name="see-also"></a>Consulte também

- [Depurando interfaces](debugging-interfaces.md)
- [Depuração](index.md)
