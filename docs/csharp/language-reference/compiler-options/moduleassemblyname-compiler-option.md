---
description: -moduleassemblyname (opção do compilador C#)
title: -moduleassemblyname (opção do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /moduleassemblyname
helpviewer_keywords:
- moduleassemblyname compiler option [C#]
- /moduleassemblyname compiler option [C#]
- .moduleassemblyname compiler option [C#]
ms.assetid: d464d9b9-f18d-423b-95e9-66c7878fd53a
ms.openlocfilehash: 9131db17d767c76fe6a57f5d5353474153e0c269
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91194083"
---
# <a name="-moduleassemblyname-c-compiler-option"></a>-moduleassemblyname (opção do compilador C#)

Especifica um assembly cujos tipos não públicos podem ser acessados por um .netmodule.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-moduleassemblyname:assembly_name  
```  
  
## <a name="arguments"></a>Argumentos  

 `assembly_name`  
 O nome do assembly cujos tipos não públicos podem ser acessados por um .netmodule.  
  
## <a name="remarks"></a>Comentários  

 O **-moduleassemblyname** deverá ser usado ao compilar um .netmodule e quando as condições a seguir forem true:  
  
- O .netmodule precisa acessar tipos não públicos em um assembly existente.  
  
- Você sabe o nome do assembly no qual o .netmodule será compilado.  
  
- O assembly existente concedeu acesso de assembly amigável ao assembly no qual o .netmodule será compilado.  
  
 Para obter mais informações sobre a compilação de um .netmodule, consulte [-target:module (Opções do compilador do C#)](./target-module-compiler-option.md).  
  
 Para obter mais informações sobre assemblies amigos, consulte [Assemblies Amigáveis](../../../standard/assembly/friend.md).  
  
 Essa opção não está disponível de dentro do ambiente de desenvolvimento; ela só está disponível quando se compila na linha de comando.  
  
 Essa opção do compilador não está disponível no Visual Studio e não pode ser alterada programaticamente.  
  
## <a name="example"></a>Exemplo  

 Este exemplo compila um assembly com um tipo privado que concede acesso de assembly amigável a um assembly denominado csman_an_assembly.  
  
```csharp  
// moduleassemblyname_1.cs  
// compile with: -target:library  
using System;  
using System.Runtime.CompilerServices;  
  
[assembly:InternalsVisibleTo ("csman_an_assembly")]  
  
class An_Internal_Class
{  
    public void Test()
    {
        Console.WriteLine("An_Internal_Class.Test called");
    }  
}  
```  
  
## <a name="example"></a>Exemplo  

 Este exemplo compila um .netmodule que acessa um tipo não público no assembly moduleassemblyname_1.dll. Sabendo que esse. netmodule será criado em um assembly chamado csman_an_assembly, podemos especificar **-moduleassemblyname**, permitindo que o. netmodule acesse tipos não públicos em um assembly que tenha concedido acesso de assembly friend a csman_an_assembly.  
  
```csharp  
// moduleassemblyname_2.cs  
// compile with: -moduleassemblyname:csman_an_assembly -target:module -reference:moduleassemblyname_1.dll  
class B {  
    public void Test() {  
        An_Internal_Class x = new An_Internal_Class();  
        x.Test();  
    }  
}  
```  
  
## <a name="example"></a>Exemplo  

 Este exemplo de código compila o assembly csman_an_assembly, referenciando o assembly compilado anteriormente e o .netmodule.  
  
```csharp  
// csman_an_assembly.cs  
// compile with: -addmodule:moduleassemblyname_2.netmodule -reference:moduleassemblyname_1.dll  
class A {  
    public static void Main() {  
        B bb = new B();  
        bb.Test();  
    }  
}  
```  
  
**An_Internal_Class.Test foi chamado**

## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
- [Gerenciando propriedades de solução e de projeto](/visualstudio/ide/managing-project-and-solution-properties)
