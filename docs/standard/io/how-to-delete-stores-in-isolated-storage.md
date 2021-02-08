---
description: 'Saiba mais sobre: como excluir repositórios no armazenamento isolado'
title: 'Como: Excluir repositórios no armazenamento isolado'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- stores, deleting
- data stores, deleting
- deleting stores
- removing stores
- isolated storage, deleting stores
- storing data using isolated storage, deleting stores
- data storage using isolated storage, deleting stores
ms.assetid: 3947e333-5af6-4601-b2f1-24d4d6129cf3
ms.openlocfilehash: 3e454492c6a6e24feb57acf20afe1073d7ffbb4e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99775637"
---
# <a name="how-to-delete-stores-in-isolated-storage"></a>Como: Excluir repositórios no armazenamento isolado

A classe <xref:System.IO.IsolatedStorage.IsolatedStorageFile> fornece dois métodos para excluir arquivos de armazenamento isolado:  
  
- O método de instância <xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove> não recebe qualquer argumento e exclui o armazenamento que o chama. Nenhuma permissão é necessária para essa operação. Qualquer código que possa acessar o armazenamento pode excluir qualquer ou todos os dados dentro dele.  
  
- O método estático <xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove%28System.IO.IsolatedStorage.IsolatedStorageScope%29> usa o valor de enumeração <xref:System.IO.IsolatedStorage.IsolatedStorageScope.User> e exclui todos os armazenamentos para o usuário que está executando o código. Esta operação exige a permissão <xref:System.Security.Permissions.IsolatedStorageFilePermission> para o valor <xref:System.Security.Permissions.IsolatedStorageContainment.AdministerIsolatedStorageByUser>.  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir demonstra o uso dos métodos <xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove%2A> estático e de instância . A classe obtém dois armazenamentos; uma é isolado para o usuário e o assembly, e o outro é isolado para o usuário, domínio e assembly. O armazenamento de usuário, domínio e assembly é excluído chamando o método <xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove> do arquivo de armazenamento isolado `isoStore1`. Em seguida, todos os armazenamentos restantes para o usuário são excluídos chamando o método estático <xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove%28System.IO.IsolatedStorage.IsolatedStorageScope%29>.  
  
 [!code-cpp[Conceptual.IsolatedStorage#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source3.cpp#3)]
 [!code-csharp[Conceptual.IsolatedStorage#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source3.cs#3)]
 [!code-vb[Conceptual.IsolatedStorage#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source3.vb#3)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>
- [Armazenamentos isolado](isolated-storage.md)
