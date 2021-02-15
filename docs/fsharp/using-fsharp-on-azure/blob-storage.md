---
title: 'Introdução ao armazenamento de BLOBs do Azure usando o F #'
description: Armazene dados não estruturados na nuvem com o armazenamento de BLOBs do Azure.
author: sylvanc
ms.date: 09/20/2016
ms.custom: devx-track-fsharp
ms.openlocfilehash: 58c120c26a1e99481b49ae3a0fb096a2188f359e
ms.sourcegitcommit: 4d5e25a46aa7cd0d29b4b9227b92987354d444c4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98794806"
---
# <a name="get-started-with-azure-blob-storage-using-f"></a>Introdução ao armazenamento de BLOBs do Azure usando o F\#

O armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados na nuvem como objetos/BLOBs. O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo. O Armazenamento de Blobs também é chamado de armazenamento de objeto.

Este artigo mostra como executar tarefas comuns usando o armazenamento de BLOBs. Os exemplos são escritos usando F # usando a biblioteca de cliente de armazenamento do Azure para .NET. As tarefas abordadas incluem como carregar, listar, baixar e excluir BLOBs.

Para obter uma visão geral conceitual do armazenamento de BLOBs, consulte [o guia .net para armazenamento de BLOBs](/azure/storage/blobs/storage-quickstart-blobs-dotnet).

## <a name="prerequisites"></a>Pré-requisitos

Para usar este guia, você deve primeiro [criar uma conta de armazenamento do Azure](/azure/storage/common/storage-account-create). Você também precisa da sua chave de acesso de armazenamento para essa conta.

## <a name="create-an-f-script-and-start-f-interactive"></a>Criar um script F # e iniciar o F# Interativo

Os exemplos neste artigo podem ser usados em um aplicativo F # ou em um script F #. Para criar um script F #, crie um arquivo com a `.fsx` extensão, por exemplo `blobs.fsx` , em seu ambiente de desenvolvimento em F #.

Em seguida, use um [Gerenciador de pacotes](package-management.md) , como [paket](https://fsprojects.github.io/Paket/) ou [NuGet](https://www.nuget.org/) , para instalar os `WindowsAzure.Storage` pacotes e a `Microsoft.WindowsAzure.ConfigurationManager` referência e `WindowsAzure.Storage.dll` `Microsoft.WindowsAzure.Configuration.dll` em seu script usando uma `#r` diretiva.

### <a name="add-namespace-declarations"></a>Adicionar declarações do namespace

Adicione as seguintes instruções `open` à parte superior do arquivo `blobs.fsx`:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L1-L5)]

### <a name="get-your-connection-string"></a>Obter a cadeia de conexão

Você precisa de uma cadeia de conexão de armazenamento do Azure para este tutorial. Para obter mais informações sobre cadeias de conexão, consulte [Configurar cadeias de conexão de armazenamento](/azure/storage/storage-configure-connection-string).

Para o tutorial, insira a cadeia de conexão em seu script, da seguinte maneira:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L11-L11)]

No entanto, isso **não é recomendado** para projetos reais. Sua chave de conta de armazenamento é semelhante para a senha raiz da sua conta de armazenamento. Sempre tenha cuidado para proteger a chave de sua conta de armazenamento. Evite distribuí-la a outros usuários, embuti-la no código ou salvá-lo em um arquivo de texto sem formatação que esteja acessível a outras pessoas. Você pode regenerar sua chave usando o portal do Azure se acreditar que ele pode ter sido comprometido.

Para aplicativos reais, a melhor maneira de manter a cadeia de conexão de armazenamento está em um arquivo de configuração. Para buscar a cadeia de conexão de um arquivo de configuração, você pode fazer isso:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L13-L15)]

O uso do Gerenciador de Configurações do Azure é opcional. Você também pode usar uma API como o tipo de .NET Framework `ConfigurationManager` .

### <a name="parse-the-connection-string"></a>Analisar a cadeia de conexão

Para analisar a cadeia de conexão, use:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L21-L22)]

Isso retorna um `CloudStorageAccount` .

### <a name="create-some-local-dummy-data"></a>Criar alguns dados fictícios locais

Antes de começar, crie alguns dados locais fictícios no diretório do nosso script. Posteriormente, você carregará esses dados.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L28-L30)]

### <a name="create-the-blob-service-client"></a>Criar o cliente do serviço Blob

O `CloudBlobClient` tipo permite que você recupere contêineres e blobs armazenados no armazenamento de BLOBs. Veja uma maneira de criar o cliente de serviço:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L36-L36)]

Agora você está pronto para escrever um código que lê e grava dados no Armazenamento de Blobs.

## <a name="create-a-container"></a>Criar um contêiner

Este exemplo mostra como criar um contêiner caso ele ainda não exista:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L42-L46)]

Por padrão, o novo contêiner é privado, o que significa que você deve especificar sua chave de acesso de armazenamento para baixar blobs desse contêiner. Para disponibilizar os arquivos do contêiner para todos, você pode definir o contêiner como público usando o seguinte código:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L48-L49)]

Qualquer pessoa na Internet pode ver os blobs em um contêiner público, mas você só poderá modificá-los ou excluí-los se tiver a chave de acesso ou a assinatura de acesso compartilhado adequada.

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob em um contêiner

O Armazenamento de Blob do Azure oferece suporte a blobs de blocos e a blobs de páginas. Na maioria dos casos, um blob de blocos é o tipo recomendado a ser usado.

Para carregar um arquivo em um blob de blocos, obtenha uma referência de contêiner e use-a para obter uma referência de blob de blocos. Depois de ter uma referência de BLOB, você pode carregar qualquer fluxo de dados para ele chamando o `UploadFromFile` método. Essa operação criará o blob se ele não existir anteriormente ou substituirá-o se existir.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L55-L59)]

## <a name="list-the-blobs-in-a-container"></a>Listar os blobs em um contêiner

Para listar blobs em um contêiner, primeiro obtenha uma referência ao contêiner. Em seguida, você pode usar o `ListBlobs` método do contêiner para recuperar os BLOBs e/ou diretórios dentro dele. Para acessar o rico conjunto de propriedades e métodos para um retornado `IListBlobItem` , você deve convertê-lo em um `CloudBlockBlob` `CloudPageBlob` objeto, ou `CloudBlobDirectory` . Se o tipo for desconhecido, você poderá usar uma verificação de tipo para determinar no qual convertê-lo. O código a seguir demonstra como recuperar e apresentar a saída do URI de cada item no contêiner `mydata` :

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L67-L80)]

Você também pode nomear BLOBs com informações de caminho em seus nomes. Isso cria uma estrutura de diretório virtual que você pode organizar e percorrer como faria com um sistema de arquivos tradicional. A estrutura de diretório é virtual somente-os únicos recursos disponíveis no armazenamento de BLOBs são contêineres e blobs. No entanto, a biblioteca de cliente de armazenamento oferece um `CloudBlobDirectory` objeto para se referir a um diretório virtual e simplificar o processo de trabalho com blobs que são organizados dessa maneira.

Por exemplo, considere o seguinte conjunto de blobs de blocos em um contêiner chamado `photos`:

*photo1.jpg*\
*2015/arquitetura/description.txt*\
*2015/arquitetura/photo3.jpg*\
*2015/arquitetura/photo4.jpg*\
*2016/arquitetura/photo5.jpg*\
*2016/arquitetura/photo6.jpg*\
*2016/arquitetura/description.txt*\
*2016/photo7.jpg*\

Quando você chama `ListBlobs` em um contêiner (como no exemplo acima), uma listagem hierárquica é retornada. Se ele contiver ambos os `CloudBlobDirectory` `CloudBlockBlob` objetos e, representando os diretórios e blobs no contêiner, respectivamente, a saída resultante será semelhante a esta:

```console
Directory: https://<accountname>.blob.core.windows.net/photos/2015/
Directory: https://<accountname>.blob.core.windows.net/photos/2016/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

Opcionalmente, você pode definir o `UseFlatBlobListing` parâmetro do `ListBlobs` método como `true` . Nesse caso, cada blob no contêiner é retornado como um `CloudBlockBlob` objeto. A chamada para `ListBlobs` para retornar uma listagem simples é parecida com esta:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L82-L89)]

e, dependendo do conteúdo atual do seu contêiner, os resultados têm a seguinte aparência:

```console
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2015/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2015/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2015/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2016/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2016/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2016/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2016/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a>Baixar blobs

Para baixar BLOBs, primeiro recupere uma referência de BLOB e, em seguida, chame o `DownloadToStream` método. O exemplo a seguir usa o `DownloadToStream` método para transferir o conteúdo do blob para um objeto de fluxo que você pode persistir em um arquivo local.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L95-L101)]

Você também pode usar o `DownloadToStream` método para baixar o conteúdo de um blob como uma cadeia de texto.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L103-L106)]

## <a name="delete-blobs"></a>Excluir blobs

Para excluir um blob, primeiro obtenha uma referência de BLOB e, em seguida, chame o `Delete` método nele.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L112-L116)]

## <a name="list-blobs-in-pages-asynchronously"></a>Listar blobs em páginas de maneira assíncrona

Se você está listando uma grande quantidade de blobs ou se deseja controlar o número de resultados retornados em uma operação de listagem, pode listar os blobs em páginas de resultados. Este exemplo mostra como retornar resultados em páginas de forma assíncrona, para que a execução não fique bloqueada enquanto espera para retornar um grande conjunto de resultados.

Este exemplo mostra uma listagem de blob simples, mas você também pode executar uma listagem hierárquica, definindo o `useFlatBlobListing` parâmetro do `ListBlobsSegmentedAsync` método como `false` .

O exemplo define um método assíncrono, usando um `async` bloco. A ``let!`` palavra-chave suspende a execução do método de exemplo até que a tarefa de listagem seja concluída.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L122-L160)]

Agora podemos usar essa rotina assíncrona da seguinte maneira. Primeiro, você carrega alguns dados fictícios (usando o arquivo local criado anteriormente neste tutorial).

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L162-L166)]

Agora, chame a rotina. Você usa `Async.RunSynchronously` para forçar a execução da operação assíncrona.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L168-L168)]

## <a name="writing-to-an-append-blob"></a>Gravar um blob de acréscimo

Um blob de acréscimo é otimizado para operações de acréscimo, como o registro em log. Como um blob de blocos, um blob de acréscimo é composto por blocos, mas quando você adiciona um novo bloco a um blob de acréscimo, ele é sempre acrescentado ao final do blob. Não é possível atualizar ou excluir um bloco existente em um blob de acréscimo. As IDs de bloco de um blob de acréscimo não ficam expostas como em um blob de blocos.

Cada bloco em um blob de acréscimo pode ter um tamanho diferente, até no máximo 4 MB, e um blob de acréscimo pode incluir no máximo 50.000 blocos. O tamanho máximo de um blob de acréscimo, portanto, é de pouco mais de 195 GB (4 MB x 50.000 blocos).

O exemplo a seguir cria um novo BLOB de acréscimo e acrescenta alguns dados a ele, simulando uma operação de log simples.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L174-L203)]

Para saber mais sobre as diferenças entre os três tipos de blobs, confira [Noções gerais sobre blobs de blocos, blobs de páginas e blobs de acréscimo](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) .

## <a name="concurrent-access"></a>Acesso simultâneo

Para suportar o acesso simultâneo a uma blob por meio de vários clientes ou várias instâncias do processo, você pode usar **ETags** ou **concessões**.

- **Etag** – fornece uma maneira de detectar se o blob ou o contêiner foi modificado por outro processo

- **Concessão** -fornece uma maneira de obter acesso exclusivo, renovável, gravar ou excluir a um blob por um período de tempo

Para obter mais informações, consulte [Gerenciando a simultaneidade no armazenamento do Microsoft Azure](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/).

## <a name="naming-containers"></a>Contêineres de nomenclatura

Todos os blobs no armazenamento do Azure devem residir em um contêiner. O contêiner faz parte do nome do blob. Por exemplo, `mydata` é o nome do contêiner nesses URIs do blob de exemplo:

- `https://storagesample.blob.core.windows.net/mydata/blob1.txt`
- `https://storagesample.blob.core.windows.net/mydata/photos/myphoto.jpg`

Um nome de contêiner deve ser um nome DNS válido e estar em conformidade com as seguintes regras de nomenclatura:

1. Os nomes de contêiner devem começar com uma letra ou número e podem conter apenas letras, números e o caractere traço (-).
1. Cada caractere traço (-) deve ser imediatamente precedido e seguido por uma letra ou número. Não são permitidos traços consecutivos em nomes de contêiner.
1. Todas as letras do nome de um contêiner devem ser minúsculas.
1. Os nomes de contêiner devem ter de 3 a 63 caracteres.

O nome de um contêiner deve estar sempre em minúsculas. Se você incluir uma letra maiúscula em um nome de contêiner ou de alguma forma violar as regras de nomenclatura do contêiner, você receberá um erro 400 (solicitação incorreta).

## <a name="managing-security-for-blobs"></a>Gerenciamento da segurança de blobs

Por padrão, o Armazenamento do Azure mantém seus dados seguros limitando o acesso ao proprietário da conta, que possui as chaves de acesso à conta. Quando você precisa compartilhar dados de blob em sua conta de armazenamento, é importante fazer isso sem comprometer a segurança de suas chaves de acesso à conta. Além disso, você pode criptografar os dados de blob para garantir que eles fiquem seguros durante a transmissão e no Armazenamento do Azure.

### <a name="controlling-access-to-blob-data"></a>Controle do acesso a dados de blob

Por padrão, os dados de blob em sua conta de armazenamento só podem ser acessados pelo proprietário da conta de armazenamento. A autenticação de solicitações no Armazenamento de Blobs requer a chave de acesso da conta, por padrão. No entanto, talvez você queira disponibilizar determinados dados de BLOB para outros usuários.

### <a name="encrypting-blob-data"></a>Criptografia de dados de blobs

O armazenamento do Azure dá suporte à criptografia de dados de blob no cliente e no servidor.

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu os conceitos básicos do armazenamento de Blobs, siga estes links para saber mais.

### <a name="tools"></a>Ferramentas

- [AzureStorageTypeProvider F #](https://fsprojects.github.io/AzureStorageTypeProvider/)\
Um provedor de tipo F # que pode ser usado para explorar os ativos de armazenamento de BLOBs, tabelas e filas do Azure e aplicar facilmente as operações CRUD neles.

- [FSharp. Azure. Storage](https://github.com/fsprojects/FSharp.Azure.Storage)\
Uma API F # para usar Microsoft Azure serviço de armazenamento de tabelas

- [Gerenciador de Armazenamento do Microsoft Azure (MASE)](/azure/vs-azure-tools-storage-manage-with-storage-explorer)\
Um aplicativo autônomo e gratuito da Microsoft que permite que você trabalhe visualmente com os dados do armazenamento do Azure no Windows, no OS X e no Linux.

### <a name="blob-storage-reference"></a>Referência do Armazenamento de Blobs

- [APIs do Armazenamento do Azure para .NET](/dotnet/api/overview/azure/storage)
- [Referência de API REST dos Serviços de Armazenamento do Azure](/rest/api/storageservices/)

### <a name="related-guides"></a>Guias relacionados

- [Exemplos de armazenamento de Blobs do Azure para .NET](/samples/azure-samples/storage-blob-dotnet-getting-started/storage-blob-dotnet-getting-started/)
- [Introdução ao AzCopy](/azure/storage/common/storage-use-azcopy-v10)
- [Configurar cadeias de conexão do Armazenamento do Azure](/azure/storage/common/storage-configure-connection-string)
- [Blog da equipe de Armazenamento do Azure](/archive/blogs/windowsazurestorage/)
- [Início rápido: usar o .NET para criar um blob no armazenamento de objetos](/azure/storage/blobs/storage-quickstart-blobs-dotnet)
