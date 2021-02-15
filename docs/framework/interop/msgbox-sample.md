---
title: Exemplo de MsgBox
description: Veja um exemplo de passagem de tipos de cadeia de caracteres por valores como parâmetros usando MsgBox. Ele mostra quando usar os campos EntryPoint, CharSet e ExactSpelling no .NET.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- marshaling, MsgBox sample
- data marshaling, MsgBox sample
ms.assetid: 9e0edff6-cc0d-4d5c-a445-aecf283d9c3a
ms.openlocfilehash: 024ed612115ce73646596651fe454238418446db
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96242013"
---
# <a name="msgbox-sample"></a>Exemplo de MsgBox

Esta amostra demonstra como passar tipos de cadeia de caracteres por valor como parâmetros In e quando usar os campos <xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint>, <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet> e <xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling>.  
  
 A amostra de MsgBox usa a seguinte função não gerenciada, mostrada com a respectiva declaração de função original:  
  
- **MessageBox** exportada de User32.dll.  
  
    ```cpp
    int MessageBox(HWND hWnd, LPCTSTR lpText, LPCTSTR lpCaption,
       UINT uType);  
    ```  
  
 Nesta amostra, a classe `NativeMethods` contém um protótipo gerenciado para cada função não gerenciada chamado pela classe `MsgBoxSample`. Os métodos de protótipo gerenciado `MsgBox`, `MsgBox2` e `MsgBox3` têm declarações diferentes para a mesma função não gerenciada.  
  
 A declaração para `MsgBox2` produz uma saída incorreta na caixa de mensagem porque o tipo de caractere, especificado como ANSI, é incompatível com o ponto de entrada `MessageBoxW`, que é o nome da função Unicode. A declaração `MsgBox3` cria uma incompatibilidade entre os campos **EntryPoint**, **CharSet** e **ExactSpelling**. Quando chamado, `MsgBox3` gera uma exceção. Para obter informações detalhadas sobre a nomeação de cadeia de caracteres e marshaling de nome, consulte [Especificando um conjunto de caracteres](specifying-a-character-set.md).  
  
## <a name="declaring-prototypes"></a>Declarando Protótipos  

 [!code-cpp[Conceptual.Interop.Marshaling#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/msgbox.cpp#5)]
 [!code-csharp[Conceptual.Interop.Marshaling#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/msgbox.cs#5)]
 [!code-vb[Conceptual.Interop.Marshaling#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/msgbox.vb#5)]  
  
## <a name="calling-functions"></a>Chamando Funções  

 [!code-cpp[Conceptual.Interop.Marshaling#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/msgbox.cpp#6)]
 [!code-csharp[Conceptual.Interop.Marshaling#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/msgbox.cs#6)]
 [!code-vb[Conceptual.Interop.Marshaling#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/msgbox.vb#6)]  
  
## <a name="see-also"></a>Veja também

- [Realizando marshaling de cadeias de caracteres](marshaling-strings.md)
- [Marshaling padrão para cadeias de caracteres](default-marshaling-for-strings.md)
- [Criando protótipos em código gerenciado](creating-prototypes-in-managed-code.md)
- [Especificando um conjunto de caracteres](specifying-a-character-set.md)
