---
description: 'Saiba mais sobre: como: chamar APIs do Windows (Visual Basic)'
title: 'Como: Chamar APIs do Windows'
ms.date: 07/20/2015
helpviewer_keywords:
- API calls [Visual Basic]
- Windows API, calling
- API calls [Visual Basic], platform invoke
- calls [Visual Basic], stored procedures
ms.assetid: 27d75f0a-54ab-4ee1-b91d-43513a19b12d
ms.openlocfilehash: ec25df3715b1f8a4612c1575b5f7192d0a133c4b
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100464905"
---
# <a name="how-to-call-windows-apis-visual-basic"></a>Como chamar APIs do Windows (Visual Basic)

Este exemplo define e chama a `MessageBox` função em user32.dll e, em seguida, passa uma cadeia de caracteres para ela.  
  
## <a name="example"></a>Exemplo  

 [!code-vb[VbVbalrInterop#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#1)]  
  
## <a name="compile-the-code"></a>Compilar o código  

 Este exemplo requer:  
  
- Uma referência ao <xref:System> namespace.  
  
## <a name="robust-programming"></a>Programação robusta  

 As seguintes condições podem causar uma exceção:  
  
- O método não é estático, é abstrato ou foi definido anteriormente. O tipo de pai é uma interface ou o comprimento de *Name* ou *DllName* é zero. (<xref:System.ArgumentException>)  
  
- O *nome* ou *DllName* é `Nothing` . (<xref:System.ArgumentNullException>)  
  
- O tipo recipiente foi criado anteriormente usando `CreateType`. (<xref:System.InvalidOperationException>)  
  
## <a name="see-also"></a>Consulte também

- [Um olhar detalhado sobre invocação de plataforma](../../../framework/interop/consuming-unmanaged-dll-functions.md#a-closer-look-at-platform-invoke)
- [Exemplos de invocação de plataforma](../../../framework/interop/platform-invoke-examples.md)
- [Consumindo funções de DLL não gerenciadas](../../../framework/interop/consuming-unmanaged-dll-functions.md)
- [Definindo um método com a emissão de reflexão](/previous-versions/dotnet/netframework-4.0/w63y4d4f(v=vs.100))
- [Passo a passo: Fazer chamadas de APIs do Windows](walkthrough-calling-windows-apis.md)
- [Interoperabilidade COM](index.md)
