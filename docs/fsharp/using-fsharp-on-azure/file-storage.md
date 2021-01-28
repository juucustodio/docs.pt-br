---
title: 'Introdução ao armazenamento de arquivos do Azure usando o F #'
description: Armazene dados de arquivo na nuvem com o armazenamento de arquivos do Azure e monte o compartilhamento de arquivos de nuvem de uma VM (máquina virtual) do Azure ou de um aplicativo local que executa o Windows.
author: sylvanc
ms.date: 09/20/2016
ms.custom: devx-track-fsharp
ms.openlocfilehash: bcea58b4bf756fc9d696cd5a1010b0feffb127a7
ms.sourcegitcommit: 8299abfbd5c49b596d61f1e4d09bc6b8ba055b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/27/2021
ms.locfileid: "98899417"
---
# <a name="get-started-with-azure-file-storage-using-f"></a>Introdução ao armazenamento de arquivos do Azure usando o F\#

O armazenamento de arquivos do Azure é um serviço que oferece compartilhamentos de arquivos na nuvem usando o [protocolo SMB (Server Message Block)](/windows/win32/fileio/microsoft-smb-protocol-and-cifs-protocol-overview)padrão. Há suporte ao SMB 2.1 e ao 3.0 SMB. Com o armazenamento de arquivos do Azure, você pode migrar aplicativos herdados que dependem de compartilhamentos de arquivos para o Azure rapidamente e sem regravações dispendiosas. Os aplicativos executados em máquinas virtuais do Azure ou serviços de nuvem ou em clientes locais podem montar um compartilhamento de arquivos na nuvem, exatamente como um aplicativo de desktop monta um compartilhamento SMB típico. Qualquer quantidade de componentes de aplicativos pode montar e acessar o compartilhamento de armazenamento de arquivos simultaneamente.

Para obter uma visão geral conceitual do armazenamento de arquivos, consulte [o guia .net para armazenamento de arquivos](/azure/storage/storage-dotnet-how-to-use-files).

## <a name="prerequisites"></a>Pré-requisitos

Para usar este guia, você deve primeiro [criar uma conta de armazenamento do Azure](/azure/storage/storage-create-storage-account).
Você também precisará da sua chave de acesso de armazenamento para essa conta.

## <a name="create-an-f-script-and-start-f-interactive"></a>Criar um script F # e iniciar o F# Interativo

Os exemplos neste artigo podem ser usados em um aplicativo F # ou em um script F #. Para criar um script F #, crie um arquivo com a `.fsx` extensão, por exemplo `files.fsx` , em seu ambiente de desenvolvimento em F #.

Em seguida, use um [Gerenciador de pacotes](package-management.md) , como [paket](https://fsprojects.github.io/Paket/) ou [NuGet](https://www.nuget.org/) , para instalar o `WindowsAzure.Storage` pacote e a referência `WindowsAzure.Storage.dll` em seu script usando uma `#r` diretiva.

### <a name="add-namespace-declarations"></a>Adicionar declarações do namespace

Adicione as seguintes instruções `open` à parte superior do arquivo `files.fsx`:

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L1-L5)]

### <a name="get-your-connection-string"></a>Obter a cadeia de conexão

Você precisará de uma cadeia de conexão de armazenamento do Azure para este tutorial. Para obter mais informações sobre cadeias de conexão, consulte [Configurar cadeias de conexão de armazenamento](/azure/storage/storage-configure-connection-string).

Para o tutorial, você inserirá sua cadeia de conexão em seu script, da seguinte maneira:

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L11-L11)]

No entanto, isso **não é recomendado** para projetos reais. Sua chave de conta de armazenamento é semelhante para a senha raiz da sua conta de armazenamento. Sempre tenha cuidado para proteger a chave de sua conta de armazenamento. Evite distribuí-la a outros usuários, embuti-la no código ou salvá-lo em um arquivo de texto sem formatação que esteja acessível a outras pessoas. Você pode regenerar sua chave usando o portal do Azure se acreditar que ele pode ter sido comprometido.

Para aplicativos reais, a melhor maneira de manter a cadeia de conexão de armazenamento está em um arquivo de configuração. Para buscar a cadeia de conexão de um arquivo de configuração, você pode fazer isso:

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L13-L15)]

O uso do Gerenciador de Configurações do Azure é opcional. Você também pode usar uma API como o tipo de .NET Framework `ConfigurationManager` .

### <a name="parse-the-connection-string"></a>Analisar a cadeia de conexão

Para analisar a cadeia de conexão, use:

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L21-L22)]

Isso retornará um `CloudStorageAccount` .

### <a name="create-the-file-service-client"></a>Criar o cliente do serviço de arquivo

O `CloudFileClient` tipo permite que você use programaticamente arquivos armazenados no armazenamento de arquivos. Veja uma maneira de criar o cliente de serviço:

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L28-L28)]

Agora você está pronto para escrever código que lê e grava dados no armazenamento de arquivos.

## <a name="create-a-file-share"></a>Criar um compartilhamento de arquivo

Este exemplo mostra como criar um compartilhamento de arquivos se ele ainda não existir:

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L34-L35)]

## <a name="create-a-root-directory-and-a-subdirectory"></a>Criar um diretório raiz e um subdiretório

Aqui, você obtém o diretório raiz e Obtém um subdiretório da raiz. Você cria ambos se eles ainda não existirem.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L41-L43)]

## <a name="upload-text-as-a-file"></a>Carregar texto como um arquivo

Este exemplo mostra como carregar texto como um arquivo.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L49-L50)]

### <a name="download-a-file-to-a-local-copy-of-the-file"></a>Baixar um arquivo para uma cópia local do arquivo

Aqui você baixa o arquivo recém-criado, acrescentando o conteúdo a um arquivo local.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L56-L56)]

### <a name="set-the-maximum-size-for-a-file-share"></a>Definir o tamanho máximo de um compartilhamento de arquivos

O exemplo a seguir mostra como verificar o uso atual de um compartilhamento e como definir a cota para o compartilhamento. `FetchAttributes` deve ser chamado para preencher um compartilhamento `Properties` e `SetProperties` para propagar alterações locais para o armazenamento de arquivos do Azure.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L62-L72)]

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Gerar uma assinatura de acesso compartilhado para um arquivo ou compartilhamento de arquivos

Você pode gerar uma SAS (assinatura de acesso compartilhado) para um compartilhamento de arquivo ou para um arquivo individual. Você também pode criar uma política de acesso compartilhado em um compartilhamento de arquivos para gerenciar assinaturas de acesso compartilhado. Recomendamos a criação de uma política de acesso compartilhado, pois ela fornece um meio de revogar o SAS se ele for comprometido.

Aqui, você cria uma política de acesso compartilhado em um compartilhamento e, em seguida, usa essa política para fornecer as restrições para uma SAS em um arquivo no compartilhamento.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L78-L94)]

Para saber mais sobre como criar e usar as assinaturas de acesso compartilhado, confira [Como usar SAS (Assinaturas de Acesso Compartilhado)](/azure/storage/storage-dotnet-shared-access-signature-part-1) e [Criar e usar uma SAS com o Armazenamento de Blobs](/azure/storage/storage-dotnet-shared-access-signature-part-2).

### <a name="copy-files"></a>Copiar arquivos

Você pode copiar um arquivo para outro arquivo ou para um blob, ou um blob para um arquivo. Se você estiver copiando um blob para um arquivo ou um arquivo para um blob, *deverá* usar uma SAS (assinatura de acesso compartilhado) para autenticar o objeto de origem, mesmo que você esteja copiando dentro da mesma conta de armazenamento.

### <a name="copy-a-file-to-another-file"></a>Copiar um arquivo para outro arquivo

Aqui, você copia um arquivo para outro arquivo no mesmo compartilhamento. Como essa operação de cópia realiza a cópia entre arquivos na mesma conta de armazenamento, você pode usar a autenticação de Chave compartilhada para executar a cópia.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L100-L101)]

### <a name="copy-a-file-to-a-blob"></a>Copiar um arquivo em um blob

Aqui, você cria um arquivo e o copia para um blob dentro da mesma conta de armazenamento. Você cria uma SAS para o arquivo de origem, que o serviço usa para autenticar o acesso ao arquivo de origem durante a operação de cópia.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L107-L120)]

Você pode copiar um blob em um arquivo da mesma maneira. Se o objeto de origem for um blob, crie uma SAS para autenticar o acesso ao blob durante a operação de cópia.

## <a name="troubleshooting-file-storage-using-metrics"></a>Solucionando problemas de armazenamento de arquivos usando métricas

O Análise de Armazenamento do Azure dá suporte a métricas para armazenamento de arquivos. Com dados de métricas, você pode rastrear solicitações e diagnosticar problemas.

Você pode habilitar as métricas para o armazenamento de arquivos do [portal do Azure](https://portal.azure.com)ou pode fazer isso em F # como este:

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L126-L140)]

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o armazenamento de arquivos do Azure, consulte esses links.

### <a name="conceptual-articles-and-videos"></a>Artigos e vídeos conceituais

- [Armazenamento de Arquivos do Azure: um sistema de arquivos SMB de nuvem ininterrupto SMB para Windows e Linux](https://azure.microsoft.com/resources/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
- [Como usar o Armazenamento de Arquivos do Azure com o Linux](/azure/storage/storage-how-to-use-files-linux)

### <a name="tooling-support-for-file-storage"></a>Suporte de ferramentas para o armazenamento de arquivos

- [Usando o PowerShell do Azure com o Armazenamento do Azure](/azure/storage/storage-powershell-guide-full)
- [Como usar o AzCopy com o Armazenamento do Microsoft Azure](/azure/storage/storage-use-azcopy)
- [Criar, baixar e listar blobs com a CLI do Azure](/azure/storage/blobs/storage-quickstart-blobs-cli#create-and-manage-file-shares)

### <a name="reference"></a>Referência

- [Referência à Biblioteca de Cliente de Armazenamento para .NET](/dotnet/api/overview/azure/storage)
- [Referência à API REST do serviço de arquivos](/rest/api/storageservices/fileservices/File-Service-REST-API)

### <a name="blog-posts"></a>Postagens no blog

- [O armazenamento de arquivos do Azure já está disponível para o público geral](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
- [Dentro do armazenamento de arquivos do Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)
- [Apresentando o serviço de arquivo do Microsoft Azure](/archive/blogs/windowsazurestorage/introducing-microsoft-azure-file-service)
- [Persistindo conexões para arquivos do Microsoft Azure](/archive/blogs/windowsazurestorage/persisting-connections-to-microsoft-azure-files)
