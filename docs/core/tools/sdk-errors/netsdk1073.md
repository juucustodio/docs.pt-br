---
title: 'NETSDK1073: o FrameworkReference não foi reconhecido'
description: Como resolver o problema em que o FrameworkReference não pode ser encontrado.
author: marcpopMSFT
ms.topic: error-reference
ms.date: 10/9/2020
f1_keywords:
- NETSDK1073
ms.openlocfilehash: 2b2dbf2a0d3e13dca4fe634529b7951f2333ce28
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95713022"
---
# <a name="netsdk1073-the-frameworkreference-was-not-recognized"></a>NETSDK1073: o FrameworkReference não foi reconhecido

**Este artigo aplica-se a:** ✔️ SDK 2.1.100 do .NET Core e versões posteriores

Esse erro normalmente significa que há uma versão de um determinado FrameworkReference que o SDK não pode localizar. Tente excluir as pastas *obj* e *bin* e execute `dotnet restore` para baixar novamente os pacotes de direcionamento mais recentes.

Como alternativa, pode haver um problema com a instalação, portanto, verifique se você está nas versões mais recentes do .NET e do Visual Studio
