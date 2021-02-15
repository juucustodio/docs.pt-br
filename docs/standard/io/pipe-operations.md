---
title: Operações básicas de pipe no .NET
description: 'Saiba mais sobre as operações de pipe no .NET. Os pipes fornecem um meio de comunicação entre processos. Há dois tipos de Pipes: Pipes anônimos e pipes nomeados.'
ms.date: 03/30/2017
helpviewer_keywords:
- pipes [.NET]
- pipe operations [.NET]
- interprocess communication [.NET], pipes
- I/O [.NET], pipes
ms.assetid: 7b964ebd-7a4f-4d28-8194-7841f9e4c702
ms.openlocfilehash: bb8804c32b9f2b54b05298779bddae117c10dcf5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95734797"
---
# <a name="pipe-operations-in-net"></a>Operações básicas de pipe no .NET

Os pipes fornecem um meio de comunicação entre processos. Existem dois tipos de pipes:  
  
- Pipes anônimos.  
  
     Os pipes anônimos fornecem comunicação entre processos em um computador local. Os pipes anônimos exigem menos sobrecarga do que os pipes nomeados mas oferecem serviços limitados. Os pipes anônimos são unidirecionais e não podem ser usados em uma rede. Eles oferecem suporte a apenas uma única instância de servidor. Os pipes anônimos são úteis para a comunicação entre threads ou entre processos pai e filho em que os identificadores de pipe podem ser facilmente passados para o processo filho quando ele é criado.  
  
     No .NET, você implementa pipes anônimos usando as classes <xref:System.IO.Pipes.AnonymousPipeServerStream> e <xref:System.IO.Pipes.AnonymousPipeClientStream>.  
  
     Veja [Como usar pipes anônimos para a comunicação entre processos locais](how-to-use-anonymous-pipes-for-local-interprocess-communication.md).  
  
- Pipes nomeados.  
  
     Os pipes nomeados fornecem a comunicação entre processos entre um servidor de pipe e um ou mais clientes pipe. Os pipes nomeados podem ser unidirecionais ou bidirecionais. Eles oferecem suporte à comunicação baseada em mensagens e permitem que vários clientes se conectem simultaneamente ao processo do servidor usando o mesmo nome de pipe. Os pipes nomeados também oferecem suporte à representação, que permite aos processos de conexão usar suas próprias permissões em servidores remotos.  
  
     No .NET, você implementa pipes nomeados usando as classes <xref:System.IO.Pipes.NamedPipeServerStream> e <xref:System.IO.Pipes.NamedPipeClientStream>.  
  
     Veja [Como usar pipes nomeados para comunicação entre processos na rede](how-to-use-named-pipes-for-network-interprocess-communication.md).  
  
## <a name="see-also"></a>Confira também

- [Arquivo e e/s de fluxo](index.md)
- [Como: Usar pipes anônimos para comunicação entre processos locais](how-to-use-anonymous-pipes-for-local-interprocess-communication.md)
- [Como: Usar pipes nomeados para comunicação entre processos na rede](how-to-use-named-pipes-for-network-interprocess-communication.md)
