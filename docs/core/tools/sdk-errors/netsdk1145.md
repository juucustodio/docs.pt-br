---
title: 'NETSDK1145: destino ou pacote de appHost ausente'
description: Como resolver o problema do pacote de direcionamento ausente enquanto a restauração do pacote NuGet não é suportada
author: wli3
ms.topic: error-reference
ms.date: 09/14/2020
f1_keywords:
- NETSDK1145
ms.openlocfilehash: c343952582cafb63eae388fd216769e6c67d4741
ms.sourcegitcommit: 636af37170ae75a11c4f7d1ecd770820e7dfe7bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91805317"
---
# <a name="netsdk1145-targeting-or-apphost-pack-missing"></a>NETSDK1145: destino ou pacote de appHost ausente

**Este artigo aplica-se a:** ✔️ o SDK do .NET 5.0.100 e versões posteriores

Quando o SDK do .NET emite o erro NETSDK1145, o pacote de destino ou appHost não está instalado e não há suporte para a restauração do pacote NuGet. Isso geralmente é causado por ter um SDK mais recente do que aquele incluído no Visual Studio para projetos C++/CLI. Atualize o Visual Studio, remova _global.js_ se ele especificar uma determinada versão do SDK e desinstale o SDK mais recente. Como alternativa, você pode substituir a versão de destino ou appHost. Localize a versão que existe no diretório do pacote a partir da mensagem de erro e corresponde à estrutura de destino do projeto. Adicione o seguinte ao projeto:

Para APPHOST Pack

```xml
<ItemGroup>
  <KnownAppHostPack Update="@(KnownAppHostPack)">
    <AppHostPackVersion Condition="'%(TargetFramework)' == 'TARGETFRAMEWORK'">EXISTINGVERSION</AppHostPackVersion>
  </KnownAppHostPack>
</ItemGroup>
```

Para o pacote de direcionamento

```xml
<ItemGroup>
  <KnownAppHostPack Update="@(KnownAppHostPack)">
    <AppHostPackVersion Condition="'%(TargetFramework)' == 'TARGETFRAMEWORK'">EXISTINGVERSION</AppHostPackVersion>
  </KnownAppHostPack>
</ItemGroup>
```
