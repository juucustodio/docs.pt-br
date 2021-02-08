---
description: 'Saiba mais sobre: como ler e gravar em arquivos no armazenamento isolado'
title: 'Como: Ler e gravar em arquivos no armazenamento isolado'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- files, isolated storage
- reading data
- storing data using isolated storage, reading and writing to files
- writing to files within store
- data storage using isolated storage, reading and writing to files
- reading files within store
- isolated storage, reading and writing to files
- data stores, reading and writing to files
- stores, reading and writing to files
ms.assetid: f977ebdc-1b55-475a-bc3d-3376470b08ae
ms.openlocfilehash: 6e88cc4c590c44394768472ce8bd5fd89ac99d38
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99775533"
---
# <a name="how-to-read-and-write-to-files-in-isolated-storage"></a>Como: Ler e gravar em arquivos no armazenamento isolado

Para ler ou gravar de um arquivo em um armazenamento isolado, use um objeto <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> com um leitor de fluxo (objeto <xref:System.IO.StreamReader>) ou o gravador do fluxo (objeto <xref:System.IO.StreamWriter>).  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir obtém um repositório isolado e verifica se existe um arquivo chamado TestStore.txt no repositório. Se não existir, ele cria o arquivo e grava "Armazenamento Isolado do Hello" no arquivo. Se TestStore.txt já existir, o código de exemplo será lido a partir do arquivo.  
  
 [!code-csharp[Conceptual.IsolatedStorage#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source5.cs#5)]
 [!code-vb[Conceptual.IsolatedStorage#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source5.vb#5)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>
- <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>
- <xref:System.IO.FileMode?displayProperty=nameWithType>
- <xref:System.IO.FileAccess?displayProperty=nameWithType>
- <xref:System.IO.StreamReader?displayProperty=nameWithType>
- <xref:System.IO.StreamWriter?displayProperty=nameWithType>
- [Arquivo e e/s de fluxo](index.md)
- [Armazenamentos isolado](isolated-storage.md)
