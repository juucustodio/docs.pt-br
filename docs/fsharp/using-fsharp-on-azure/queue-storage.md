---
title: 'Introdução ao armazenamento de filas do Azure usando F #'
description: As filas do Azure fornecem uma mensagem assíncrona e confiável entre os componentes do aplicativo. A mensagem na nuvem permite que os componentes do aplicativo se dimensionem de modo independente.
author: sylvanc
ms.date: 09/20/2016
ms.custom: devx-track-fsharp
ms.openlocfilehash: 0ab131647e37985d45073966ffc01b9a7f379e2f
ms.sourcegitcommit: 8299abfbd5c49b596d61f1e4d09bc6b8ba055b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/27/2021
ms.locfileid: "98899289"
---
# <a name="get-started-with-azure-queue-storage-using-f"></a>Introdução ao armazenamento de filas do Azure usando F\#

O armazenamento de filas do Azure fornece mensagens de nuvem entre componentes do aplicativo. Na criação de aplicativos para escala, os componentes do aplicativo geralmente são desassociados, para que possam ser redimensionados independentemente. O armazenamento de filas fornece mensagens assíncronas para a comunicação entre os componentes do aplicativo, estando eles em execução na nuvem, na área de trabalho, em um servidor local ou em um dispositivo móvel. O armazenamento de Fila também dá suporte ao gerenciamento de tarefas assíncronas e à criação de fluxos de trabalho do processo.

### <a name="about-this-tutorial"></a>Sobre este tutorial

Este tutorial mostra como escrever código F # para algumas tarefas comuns usando o armazenamento de filas do Azure. As tarefas cobertas incluem criar e excluir filas e adicionar, ler e excluir mensagens da fila.

Para obter uma visão geral conceitual do armazenamento de filas, consulte [o guia .net para armazenamento de filas](/azure/storage/storage-dotnet-how-to-use-queues).

## <a name="prerequisites"></a>Pré-requisitos

Para usar este guia, você deve primeiro [criar uma conta de armazenamento do Azure](/azure/storage/storage-create-storage-account).
Você também precisará da sua chave de acesso de armazenamento para essa conta.

## <a name="create-an-f-script-and-start-f-interactive"></a>Criar um script F # e iniciar o F# Interativo

Os exemplos neste artigo podem ser usados em um aplicativo F # ou em um script F #. Para criar um script F #, crie um arquivo com a `.fsx` extensão, por exemplo `queues.fsx` , em seu ambiente de desenvolvimento em F #.

Em seguida, use um [Gerenciador de pacotes](package-management.md) , como [paket](https://fsprojects.github.io/Paket/) ou [NuGet](https://www.nuget.org/) , para instalar o `WindowsAzure.Storage` pacote e a referência `WindowsAzure.Storage.dll` em seu script usando uma `#r` diretiva.

### <a name="add-namespace-declarations"></a>Adicionar declarações do namespace

Adicione as seguintes instruções `open` à parte superior do arquivo `queues.fsx`:

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L1-L3)]

### <a name="get-your-connection-string"></a>Obter a cadeia de conexão

Você precisará de uma cadeia de conexão de armazenamento do Azure para este tutorial. Para obter mais informações sobre cadeias de conexão, consulte [Configurar cadeias de conexão de armazenamento](/azure/storage/storage-configure-connection-string).

Para o tutorial, você inserirá sua cadeia de conexão em seu script, da seguinte maneira:

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L9-L9)]

No entanto, isso **não é recomendado** para projetos reais. Sua chave de conta de armazenamento é semelhante para a senha raiz da sua conta de armazenamento. Sempre tenha cuidado para proteger a chave de sua conta de armazenamento. Evite distribuí-la a outros usuários, embuti-la no código ou salvá-lo em um arquivo de texto sem formatação que esteja acessível a outras pessoas. Você pode regenerar sua chave usando o portal do Azure se acreditar que ele pode ter sido comprometido.

Para aplicativos reais, a melhor maneira de manter a cadeia de conexão de armazenamento está em um arquivo de configuração. Para buscar a cadeia de conexão de um arquivo de configuração, você pode fazer isso:

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L11-L13)]

O uso do Gerenciador de Configurações do Azure é opcional. Você também pode usar uma API como o tipo de .NET Framework `ConfigurationManager` .

### <a name="parse-the-connection-string"></a>Analisar a cadeia de conexão

Para analisar a cadeia de conexão, use:

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L19-L20)]

Isso retornará um `CloudStorageAccount` .

### <a name="create-the-queue-service-client"></a>Criar o cliente do serviço Fila

A `CloudQueueClient` classe permite que você recupere filas armazenadas no armazenamento de filas. Veja uma maneira de criar o cliente de serviço:

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L26-L26)]

Agora você está pronto para escrever um código que lê e grava dados no Armazenamento de Filas.

## <a name="create-a-queue"></a>Criar uma fila

Este exemplo mostra como criar uma fila, caso ela ainda não exista:

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L32-L36)]

## <a name="insert-a-message-into-a-queue"></a>Inserir uma mensagem em uma fila

Para inserir uma mensagem em uma fila existente, primeiro crie uma nova `CloudQueueMessage` . Em seguida, chame o `AddMessage` método. Um `CloudQueueMessage` pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma `byte` matriz, como esta:

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L42-L44)]

## <a name="peek-at-the-next-message"></a>Espiar a próxima mensagem

Você pode inspecionar a mensagem na frente de uma fila, sem removê-la da fila, chamando o `PeekMessage` método.

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L50-L52)]

## <a name="get-the-next-message-for-processing"></a>Obter a próxima mensagem para processamento

Você pode recuperar a mensagem na frente de uma fila para processamento chamando o `GetMessage` método.

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L58-L59)]

Posteriormente, você indicará o processamento bem-sucedido da mensagem usando `DeleteMessage` .

## <a name="change-the-contents-of-a-queued-message"></a>Alterar o conteúdo de uma mensagem na fila

Você pode alterar o conteúdo de uma mensagem recuperada in-loco na fila. Se a mensagem representar uma tarefa de trabalho, você poderá usar esse recurso para atualizar o status da tarefa de trabalho. O código a seguir atualiza a mensagem da fila com novo conteúdo e define o tempo limite de visibilidade para estender mais 60 segundos. Isso salva o estado do trabalho associado à mensagem e dá ao cliente mais um minuto para continuar trabalhando na mensagem. Você pode usar essa técnica para acompanhar fluxos de trabalho de várias etapas em mensagens em fila, sem a necessidade de começar desde o início, caso uma etapa de processamento falhar devido a uma falha de hardware ou de software. Normalmente, você manteria uma contagem de repetições também e, se a mensagem for repetida mais do que um número de vezes, você a excluiria. Isso protege contra uma mensagem que dispara um erro do aplicativo sempre que for processada.

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L65-L69)]

## <a name="de-queue-the-next-message"></a>Remover a próxima mensagem da fila

Seu código remove uma mensagem de um fila em duas etapas. Ao chamar `GetMessage` , você receberá a próxima mensagem em uma fila. Uma mensagem retornada de `GetMessage` torna-se invisível para todas as outras mensagens de leitura de código da fila. Por padrão, essa mensagem permanece invisível por 30 segundos. Para concluir a remoção da mensagem da fila, você também deve chamar `DeleteMessage` . Este processo de duas etapas de remover uma mensagem garante que quando o código não processa uma mensagem devido à falhas de hardware ou de software, outra instância do seu código pode receber a mesma mensagem e tentar novamente. Seu código chama `DeleteMessage` logo após a mensagem ser processada.

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L75-L76)]

## <a name="use-async-workflows-with-common-queue-storage-apis"></a>Usar fluxos de trabalho assíncronos com APIs de armazenamento de fila comuns

Este exemplo mostra como usar um fluxo de trabalho assíncrono com APIs de armazenamento de fila comuns.

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L82-L91)]

## <a name="additional-options-for-de-queuing-messages"></a>Opções adicionais para remover mensagens da fila

Há duas maneiras de personalizar a recuperação da mensagem de uma fila.
Primeiro, você pode obter um lote de mensagens (até 32). Segundo, você pode definir um tempo limite de invisibilidade mais longo ou mais curto, permitindo mais ou menos tempo para seu código processar totalmente cada mensagem. O exemplo de código a seguir usa `GetMessages` para obter 20 mensagens em uma chamada e, em seguida, processa cada mensagem. Ele também define o tempo limite de invisibilidade de cinco minutos para cada mensagem. Os 5 minutos começam para todas as mensagens ao mesmo tempo; portanto, depois de 5 minutos desde a chamada para `GetMessages` , todas as mensagens que não foram excluídas ficarão visíveis novamente.

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L97-L99)]

## <a name="get-the-queue-length"></a>Obter o tamanho da fila

Você pode obter uma estimativa do número de mensagens em uma fila. O `FetchAttributes` método solicita ao serviço fila recuperar os atributos da fila, incluindo a contagem de mensagens. A `ApproximateMessageCount` propriedade retorna o último valor recuperado pelo `FetchAttributes` método, sem chamar o serviço fila.

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L105-L106)]

## <a name="delete-a-queue"></a>Excluir uma fila

Para excluir uma fila e todas as mensagens contidas nela, chame o `Delete` método no objeto de fila.

[!code-fsharp[QueueStorage](~/samples/snippets/fsharp/azure/queue-storage.fsx#L112-L113)]

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu os conceitos básicos do armazenamento de Fila, siga estes links para saber mais sobre tarefas de armazenamento mais complexas.

- [APIs do Armazenamento do Azure para .NET](/dotnet/api/overview/azure/storage)
- [Provedor de tipo de armazenamento do Azure](https://github.com/fsprojects/AzureStorageTypeProvider)
- [Blog da equipe de Armazenamento do Azure](/archive/blogs/windowsazurestorage/)
- [Configurar cadeias de conexão do Armazenamento do Azure](/azure/storage/common/storage-configure-connection-string)
- [Referência de API REST dos Serviços de Armazenamento do Azure](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference)
