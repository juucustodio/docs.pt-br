---
description: 'Saiba mais sobre: tipos preteridos no Windows Workflow Foundation'
title: Substituído em Windows Workflow Foundation
ms.date: 03/30/2017
ms.assetid: 4aebe928-a964-4c1c-abf7-0dbbd3604b13
ms.openlocfilehash: a536f67708c5913040848df52f178dcc2a361f6c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99742427"
---
# <a name="deprecated-types-in-windows-workflow-foundation"></a>Substituído em Windows Workflow Foundation

Em .NET 4 a equipe de fluxo de trabalho liberou qualquer novo mecanismo de fluxo de trabalho no espaço de <xref:System.Activities> . Com o lançamento do .NET Framework 4,5 Beta, estamos marcando a maioria dos tipos no "WF 3" <xref:System.Workflow.Activities> , <xref:System.Workflow.ComponentModel> e  <xref:System.Workflow.Runtime> namespaces como obsoletos.

## <a name="obsolete-namespaces-and-tools"></a>Namespaces e ferramentas obsoletas

 Os seguintes conjuntos possuem um ou mais tipos públicos que serão substituídos:

- System.Workflow.Activities.dll

- System.Workflow.ComponentModel.dll

- System.Workflow.Runtime.dll

- System.WorkflowServices.dll

- Microsoft.Workflow.DebugController.dll

- Microsoft.Workflow.Compiler.exe

- Wfc.exe

 Como resultado, os clientes que são substituídos usando APIs de WF 3 encontrarão avisos de compilação com uma mensagem semelhante ao seguinte:

 **Aviso BC40000: X é obsoleto: tipos do WF 3 são preteridos. Em vez disso, use o WF 4.** Nós removeremos os tipos do.NET Framework em uma versão futura, mas nós não determinamos ainda esse o prazo (não em 4,5). Esta etapa atual permite que nós comuniquem a direção a nossos clientes e permitam-lhes a abundância hora de mover para o novo modelo WF4. Certamente, continuaremos a oferecer suporte a esses tipos do WF 3 na [política de ciclo de vida suporte da Microsoft](/lifecycle/). Os aplicativos WF3 existentes serão executados sem problemas no .NET Framework 4,5, e o Visual Studio 2012 dará suporte a soluções baseadas em WF3 novas e existentes.

 As regras tipos relacionados ao espaço de <xref:System.Workflow.Activities.Rules> , que não têm uma substituição em WF 4,5, não foram substituídas dentro.

 Os clientes que desejarem migrar seus aplicativos para o WF 4 encontrarão ajuda nas [diretrizes de migração do fluxo de trabalho 4](migration-guidance.md).
