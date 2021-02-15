---
title: Assemblies e execução lado a lado
description: Saiba mais sobre a execução lado a lado, que é a capacidade de armazenar e executar várias versões de um aplicativo ou componente no mesmo computador.
ms.date: 08/20/2019
helpviewer_keywords:
- side-by-side execution [.NET]
- assemblies [.NET], side-by-side execution
ms.assetid: e42036ee-7590-47d1-b884-cc856e39bd5d
ms.openlocfilehash: 7bedd5a384ceace014412eb894adad5c92c00b05
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687985"
---
# <a name="assemblies-and-side-by-side-execution"></a>Assemblies e execução lado a lado

Execução lado a lado é a capacidade de armazenar e executar várias versões de um aplicativo ou componente no mesmo computador. Isso significa que você pode ter várias versões do runtime e várias versões de aplicativos e componentes que usam uma versão do runtime no mesmo computador ao mesmo tempo. A execução lado a lado confere mais controle sobre a quais versões de um componente um aplicativo está associado e mais controle sobre qual versão do runtime um aplicativo usa.  
  
O suporte para armazenamento lado a lado e execução de diferentes versões do mesmo assembly é uma parte integrante da nomenclatura forte e está integrada à infraestrutura do runtime. Como o número de versão do assembly de nome forte faz parte de sua identidade, o runtime pode armazenar várias versões do mesmo assembly no cache de assembly global e carregar esses módulos em runtime.  
  
Embora o runtime ofereça a capacidade de criar aplicativos lado a lado, a execução lado a lado não é automática. Para obter mais informações sobre como criar aplicativos para execução lado a lado, consulte [diretrizes para criar componentes para execução lado a lado](../../framework/deployment/guidelines-for-creating-components-for-side-by-side-execution.md).  
  
## <a name="see-also"></a>Veja também

- [Como o tempo de execução localiza assemblies](../../framework/deployment/how-the-runtime-locates-assemblies.md)
- [Assemblies no .NET](index.md)
