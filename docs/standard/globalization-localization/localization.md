---
description: 'Saiba mais sobre: localização'
title: Localização
ms.date: 03/30/2017
helpviewer_keywords:
- culture, localization
- application development [.NET], localization
- globalization [.NET], localization
- code blocks
- international applications [.NET], localization
- global applications, localization
- world-ready applications, localization
- user interface blocks
- localization [.NET], about localization
- localizing resources
ms.assetid: 49d520d7-92d7-44ee-bb24-8b615db1d41b
ms.openlocfilehash: 0f84e406e35eb75cacf6daac32bbe26b4750738b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99675787"
---
# <a name="localization"></a>Localização

Localização é o processo de traduzir os recursos do aplicativo em versões localizadas para cada cultura à qual o aplicativo dará suporte. Você deve prosseguir para a etapa de localização somente após concluir a etapa de [Revisão de Capacidade de Localização](localizability-review.md) para verificar se o aplicativo globalizado está pronto para a localização.

Um aplicativo que está pronto para a localização é separado em dois blocos conceituais: um bloco que contém todos os elementos de interface do usuário e um bloco que contém o código executável. O bloco de interface do usuário contém apenas os elementos de interface de usuário localizáveis, como cadeias de caracteres, mensagens de erro, caixas de diálogo, menus, recursos de objetos inseridos e assim por diante para a cultura neutra. O bloco de código contém apenas o código do aplicativo a ser usado por todas as culturas com suporte. O common language runtime dá suporte a um modelo de recurso de assembly satélite que separa o código executável do aplicativo de seus recursos. Para obter mais informações de como implementar esse modelo, confira [Recursos no .NET](../../framework/resources/index.md).

Para cada versão localizada do aplicativo, adicione um novo assembly satélite que contenha o bloco de interface do usuário localizada traduzido para o idioma apropriado para a cultura de destino. O bloco de código para todas as culturas deve permanecer o mesmo. A combinação de uma versão localizada do bloco de interface de usuário com o bloco de código produz uma versão localizada do aplicativo.

O SDK (Software Development Kit) do Windows fornece o Editor de Recursos do Windows Forms (Winres.exe), que permite localizar rapidamente o Windows Forms para as culturas de destino. Para saber mais sobre como usar essa ferramenta, confira [Winres.exe (Windows Forms Resource Editor)](../../framework/tools/winres-exe-windows-forms-resource-editor.md).

## <a name="see-also"></a>Consulte também

- [Globalização e localização](index.md)
- [Revisão de possibilidade de localização](localizability-review.md)
- [Globalização](globalization.md)
- [Recursos em aplicativos da área de trabalho](../../framework/resources/index.md)
