---
description: 'Saiba mais sobre: como percorrer uma árvore binária com tarefas paralelas'
title: 'Como: percorrer uma árvore binária com tarefas paralelas'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to traverse a tree
ms.assetid: 4265d169-6c69-4f36-b10d-b7ae7f72f4df
ms.openlocfilehash: f6b053bb9b480e85698dcd098a750d38d2ef403a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99629533"
---
# <a name="how-to-traverse-a-binary-tree-with-parallel-tasks"></a>Como: percorrer uma árvore binária com tarefas paralelas

O exemplo a seguir mostra duas maneiras pelas quais tarefas paralelas podem ser usadas para percorrer uma estrutura de dados de árvore. A criação da árvore em si permanece como um exercício.  
  
## <a name="example"></a>Exemplo  

 [!code-csharp[TPL#16](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/tpl.cs#16)]
 [!code-vb[TPL#16](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/treewalk.vb#16)]  
  
 Os dois métodos mostrados são funcionalmente equivalentes. Usando o método <xref:System.Threading.Tasks.TaskFactory.StartNew%2A> para criar e executar as tarefas, você obter um identificador de tarefas que pode ser usado para aguardar as tarefas e manipular exceções.  
  
## <a name="see-also"></a>Consulte também

- [Biblioteca de tarefas paralelas (TPL)](task-parallel-library-tpl.md)
