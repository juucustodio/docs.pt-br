---
title: Como fornecer uma caixa de diálogo de progresso para operações de arquivo – guia de programação C#
description: Saiba como fornecer uma caixa de diálogo de progresso para operações de arquivo usando o método CopyFile (String, String, UIOption).
ms.date: 07/20/2015
helpviewer_keywords:
- progress dialog [C#]
ms.assetid: 01b71fe7-8178-4dc8-aeb1-12053be7b51c
ms.openlocfilehash: 5d16aeb3a5394ca250e4a5e26074db797c54216d
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91185880"
---
# <a name="how-to-provide-a-progress-dialog-box-for-file-operations-c-programming-guide"></a>Como fornecer uma caixa de diálogo de progresso para operações de arquivo (guia de programação C#)

Você pode fornecer uma caixa de diálogo padrão que mostra o andamento em operações de arquivos no Windows se você usar o método <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%28System.String%2CSystem.String%2CMicrosoft.VisualBasic.FileIO.UIOption%29> no namespace <xref:Microsoft.VisualBasic?displayProperty=nameWithType>.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-add-a-reference-in-visual-studio"></a>Para adicionar uma referência no Visual Studio  
  
1. Na barra de menus, escolha **Projeto**, **Adicionar Referência**.  
  
     A caixa de diálogo **Gerenciador de Referências** é exibida.  
  
2. Na área **Assemblies**, escolha **Framework** se ele ainda não estiver escolhido.  
  
3. Na lista de nomes, marque a caixa de seleção **Microsoft.VisualBasic** e, em seguida, escolha o botão **OK** para fechar a caixa de diálogo.  
  
## <a name="example"></a>Exemplo  

 O código a seguir copia o diretório que `sourcePath` especifica, para o diretório que `destinationPath` especifica. Esse código também fornece uma caixa de diálogo padrão que mostra a quantidade estimada de tempo que resta antes da conclusão da operação.  
  
 [!code-csharp[csFilesandFolders#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#11)]  
  
## <a name="see-also"></a>Veja também

- [Sistema de arquivos e o Registro (Guia de Programação em C#)](./index.md)
