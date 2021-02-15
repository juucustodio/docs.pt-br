---
title: 'Alteração significativa: os arquivos Directory. Packages. props são importados por padrão'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que os arquivos. props do NuGet importam automaticamente um arquivo chamado Directory. Packages. props, caso ele seja encontrado na pasta do projeto.
ms.date: 09/17/2020
ms.openlocfilehash: ee8a2999b801e81750d96a0bc985e3c8169224a9
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760367"
---
# <a name="directorypackagesprops-files-is-imported-by-default"></a>Os arquivos Directory. Packages. props são importados por padrão

Os arquivos *. props* do NuGet importam automaticamente um arquivo chamado *Directory. Packages. props* , caso ele seja encontrado na pasta do projeto ou em qualquer um de seus ancestrais.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, você poderia ter um arquivo chamado *Directory. Packages. props* no seu arquivo de projeto e ele não seria importado automaticamente pelo arquivo *. props* do NuGet no momento da compilação.

A partir do .NET 5,0, tal arquivo *é* importado automaticamente se ele existir na pasta do projeto ou em qualquer um de seus ancestrais. Se você tiver um arquivo com esse nome na pasta do projeto, essa importação automática poderá alterar o comportamento da compilação. Por exemplo, o arquivo será importado, mas não estava antes, ou a ordem de quando for importado poderá ser alterada se você a importar especificamente.

## <a name="reason-for-change"></a>Motivo da alteração

Essa alteração foi feita para dar suporte ao [controle de versão de pacote central](https://github.com/NuGet/Home/wiki/Centrally-managing-NuGet-package-versions) para NuGet.

## <a name="recommended-action"></a>Ação recomendada

Renomeie o arquivo *Directory. Packages. props* existente se ele não deve ser importado automaticamente.

## <a name="affected-apis"></a>APIs afetadas

N/D

<!--

### Affected APIs

Not detectable via API analysis.

### Category

MSBuild

-->
