---
title: Como referenciar um assembly de nome forte
description: Este artigo mostra como fazer referência a tipos ou recursos em um assembly .NET de nome forte, seja em tempo de compilação ou em tempo de execução.
ms.date: 08/20/2019
helpviewer_keywords:
- strong-named assemblies, compile-time references
- compile-time assembly referencing
- assemblies [.NET], strong-named
- assembly binding, strong-named
ms.assetid: 4c6a406a-b5eb-44fa-b4ed-4e95bb95a813
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 919e4f4cf467e8fc28c3d007963393dad134ab57
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724046"
---
# <a name="how-to-reference-a-strong-named-assembly"></a>Como referenciar um assembly de nome forte

O processo para referenciar tipos ou recursos em um assembly de nome forte é normalmente transparente. Você pode fazer a referência no tempo de compilação (vinculação inicial) ou no tempo de execução.  
  
Uma referência de tempo de compilação ocorre quando você indica ao compilador que o assembly a ser compilado explicitamente referencia outro assembly. Quando você usa a referência no tempo de compilação, o compilador obtém automaticamente a chave pública do assembly com nome forte direcionado e o coloca na referência de assembly do assembly que está sendo compilado.
  
> [!NOTE]
> Assembly de nome forte só pode usar tipos de outros assemblies de nome forte. Caso contrário, a segurança do assembly de nome forte estaria comprometida.  
  
## <a name="make-a-compile-time-reference-to-a-strong-named-assembly"></a>Fazer uma referência de tempo de compilação a um assembly de nome forte  

Em um prompt de comando, digite o comando a seguir:  

\<*compiler command*>**/Reference:**\<*assembly name*>  

Nesse comando, o *comando do compilador* é o comando do compilador para a linguagem que você está usando, e *nome do assembly* é o nome do assembly de nome forte que está sendo referenciado. Você também pode usar outras opções de compilador, como a opção **/t:library** para criar um assembly de biblioteca.  

O exemplo a seguir cria um assembly chamado *myAssembly.dll* que faz referência a um assembly de nome forte chamado *myLibAssembly.dll* de um módulo de código chamado *myAssembly.cs*.  

```cmd
csc /t:library myAssembly.cs /reference:myLibAssembly.dll  
```  

## <a name="make-a-run-time-reference-to-a-strong-named-assembly"></a>Fazer uma referência de tempo de execução para um assembly de nome forte  
  
Quando você faz uma referência de tempo de execução para um assembly de nome forte, por exemplo, usando <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> o <xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType> método ou, você deve usar o nome de exibição do assembly de nome forte referenciado. A sintaxe de um nome de exibição é a seguinte:  

\<*assembly name*>**,** \<*version number*>**,** \<*culture*>**,** \<*public key token*>  

Por exemplo:  

```console
myDll, Version=1.1.0.0, Culture=en, PublicKeyToken=03689116d3a4ae33
```  

Neste exemplo, `PublicKeyToken` é a forma hexadecimal do token de chave pública. Se não houver valor de cultura, use `Culture=neutral`.  

O exemplo de código a seguir mostra como usar essas informações com o método <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType>.  

```cpp
Assembly^ myDll =
    Assembly::Load("myDll, Version=1.0.0.1, Culture=neutral, PublicKeyToken=9b35aa32c18d4fb1");
```

```csharp
Assembly myDll =
    Assembly.Load("myDll, Version=1.0.0.1, Culture=neutral, PublicKeyToken=9b35aa32c18d4fb1");
```

```vb
Dim myDll As Assembly = _
    Assembly.Load("myDll, Version=1.0.0.1, Culture=neutral, PublicKeyToken=9b35aa32c18d4fb1")
```

Você pode imprimir o formato hexadecimal da chave pública e do token de chave pública para um assembly específico usando o seguinte comando [Nome Forte (Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md):  

**SN-TP \<** *assembly* **>**  

Se você tiver um arquivo de chave pública, use o comando a seguir (observe a diferença no caso da opção de linha de comando):  

**SN-TP \<** *public key file* **>**  

## <a name="see-also"></a>Confira também

- [Criar e usar assemblies com nome forte](create-use-strong-named.md)
