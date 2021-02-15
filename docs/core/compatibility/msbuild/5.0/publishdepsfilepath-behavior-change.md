---
title: 'Alteração significativa: alteração de comportamento de PublishDepsFilePath'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que a Propriedade MSBuild do PublishDepsFilePath está vazia para aplicativos de arquivo único.
ms.date: 09/17/2020
ms.openlocfilehash: 70631beff31aa3388e59f3b79875ef437351451a
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760550"
---
# <a name="publishdepsfilepath-behavior-change"></a>Alteração de comportamento de PublishDepsFilePath

A `PublishDepsFilePath` Propriedade MSBuild está vazia para aplicativos de arquivo único. Além disso, para aplicativos que não são de arquivo único, o *deps.jsno* arquivo pode não ser copiado para o diretório de saída até mais tarde na compilação.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, a `PublishDepsFilePath` Propriedade MSBuild é o caminho para a *deps.js* do aplicativo no arquivo no diretório de saída para aplicativos que não são de arquivo único e um caminho no diretório intermediário para aplicativos de arquivo único.

A partir do .NET 5,0, `PublishDepsFilePath` está vazio para aplicativos de arquivo único e uma nova `IntermediateDepsFilePath` propriedade especifica o *deps.jsno* local no diretório intermediário. Além disso, para aplicativos que não são de arquivo único, o *deps.jsno* arquivo pode não ser copiado para o diretório de saída (ou seja, o caminho especificado por `PublishDepsFilePath` ) até mais tarde na compilação.

## <a name="reason-for-change"></a>Motivo da alteração

Essa alteração foi feita por alguns motivos:

- Devido a uma refatoração da lógica de publicação a fim de dar suporte a [aplicativos de arquivo único aprimorados](https://github.com/dotnet/designs/blob/master/accepted/2020/single-file/design.md) no .NET 5.

- Em aplicativos de arquivo único, para ajudar a proteger contra destinos que tentam regravar o *deps.jsno* arquivo depois que *deps.jsno* já foi agrupado, portanto, sem afetar o aplicativo silenciosamente. Por esse motivo, o `PublishDepsFilePath` está vazio para aplicativos de arquivo único.

## <a name="recommended-action"></a>Ação recomendada

Os destinos que reescrevem o *deps.jsno* arquivo geralmente devem fazer isso usando a `IntermediateDepsFilePath` propriedade.

## <a name="affected-apis"></a>APIs afetadas

N/D

<!--

### Affected APIs

Not detectable via API analysis.

### Category

MSBuild

-->
