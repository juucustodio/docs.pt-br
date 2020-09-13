---
title: 'Como: gravar e ler mensagens de um bloco de fluxo de base'
ms.date: 09/10/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Task Parallel Library, dataflows
- TPL dataflow library, reading and writing messages
ms.assetid: 1a9bf078-aa82-46eb-b95a-f87237f028c5
ms.openlocfilehash: 8eb92d917bb2b03c2a505a2ba238598e0c1a450c
ms.sourcegitcommit: 6d4ee46871deb9ea1e45bb5f3784474e240bbc26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2020
ms.locfileid: "90022851"
---
# <a name="how-to-write-and-read-messages-from-a-dataflow-block"></a>Como: gravar e ler mensagens de um bloco de fluxo de base

Este artigo descreve como usar a biblioteca de Dataflow da TPL (biblioteca paralela de tarefas) para gravar e ler mensagens de um bloco de fluxo de mensagens. A Biblioteca de fluxo de dados TPL fornece métodos síncronos e assíncronos para escrever mensagens e ler mensagens de um bloco de fluxo de dados. Este artigo mostra como usar a <xref:System.Threading.Tasks.Dataflow.BufferBlock%601?displayProperty=nameWithType> classe. A <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> classe armazena em buffer as mensagens e se comporta como uma origem de mensagem e um destino de mensagem.

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

## <a name="writing-and-reading-synchronously"></a>Gravando e lendo de forma síncrona

O exemplo a seguir usa o método <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> para gravar em um bloco de fluxo de dados <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> e o método <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Receive%2A> para ler do mesmo objeto.

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs" id="2":::
:::code language="vb" source="../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb" id="2":::

Você também pode usar o método <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> para ler a partir de um bloco de fluxo de dados, como mostrado no exemplo a seguir. O método <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> não bloqueia o thread atual e é útil quando ocasionalmente pesquisa dados.

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs" id="3":::
:::code language="vb" source="../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb" id="3":::

Como o método <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> atua de forma síncrona, o objeto <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> nos exemplos anteriores recebe todos os dados antes do segundo loop ler os dados. O exemplo a seguir amplia o primeiro exemplo usando <xref:System.Threading.Tasks.Task.WhenAll(System.Threading.Tasks.Task[])?displayProperty=nameWithType> para ler e gravar simultaneamente no bloco de mensagens. Como <xref:System.Threading.Tasks.Task.WhenAll%2A> executa ações simultaneamente, os valores não são gravados no objeto <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> em qualquer ordem específica.

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs" id="4":::
:::code language="vb" source="../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb" id="4":::

## <a name="writing-and-reading-asynchronously"></a>Gravando e lendo de forma assíncrona

O exemplo a seguir usa o método <xref:System.Threading.Tasks.Dataflow.DataflowBlock.SendAsync%2A> para gravar de forma assíncrona para um objeto <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> e o método <xref:System.Threading.Tasks.Dataflow.DataflowBlock.ReceiveAsync%2A> para ler de forma assíncrona a partir do mesmo objeto. Este exemplo usa os operadores [async](../../csharp/language-reference/keywords/async.md) e [await](../../csharp/language-reference/operators/await.md) ([Async](../../visual-basic/language-reference/modifiers/async.md) e [Await](../../visual-basic/language-reference/operators/await-operator.md) no Visual Basic) para enviar dados de forma assíncrona e ler dados do bloco de destino. O método <xref:System.Threading.Tasks.Dataflow.DataflowBlock.SendAsync%2A> é útil quando você deve habilitar um bloco de fluxo de dados para adiar mensagens. O método <xref:System.Threading.Tasks.Dataflow.DataflowBlock.ReceiveAsync%2A> é útil quando você deseja atuar nos dados quando esses dados se tornam disponíveis. Para obter mais informações sobre como as mensagens se propagam entre os blocos de mensagens, confira a seção Passagem de mensagem em [Fluxo de dados](dataflow-task-parallel-library.md).

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs" id="5":::
:::code language="vb" source="../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb" id="5":::

## <a name="a-complete-example"></a>Um exemplo completo

O exemplo a seguir mostra todo o código deste artigo.

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_readwrite/cs/dataflowreadwrite.cs" id="1":::
:::code language="vb" source="../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_readwrite/vb/dataflowreadwrite.vb" id="1":::

## <a name="next-steps"></a>Próximas etapas

Esse exemplo mostra como ler e gravar diretamente para um bloco de mensagens. Você também pode conectar blocos de fluxo de dados para formar *pipelines*, que são sequências lineares de blocos de fluxo de dados, ou então *redes*, que são gráficos de blocos de fluxo de dados. Em uma rede ou pipeline, origens propagam dados assincronamente para destinos assim que os dados ficam disponíveis. Para um exemplo que cria um pipeline de fluxo de dados, confira [Passo a passo: criar um pipeline de fluxo de dados](walkthrough-creating-a-dataflow-pipeline.md). Para ver um exemplo que cria uma rede de fluxo de dados mais complexa, confira [Passo a passo: usar o fluxo de dados em um aplicativo do Windows Forms](walkthrough-using-dataflow-in-a-windows-forms-application.md).

## <a name="see-also"></a>Consulte também

- [Fluxo de dados (Task Parallel Library)](dataflow-task-parallel-library.md)
