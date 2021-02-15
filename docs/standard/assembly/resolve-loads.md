---
title: Resolver carregamentos de assembly
description: Este artigo descreve o evento .NET AppDomain. AssemblyResolve. Use esse evento para aplicativos que exigem controle sobre o carregamento de assembly.
ms.date: 12/15/2020
helpviewer_keywords:
- assemblies [.NET], resolving loads
- application domains, loading assemblies
- resolving assembly loads
- assemblies [.NET], loading
- application domains, resolving assembly loads
ms.assetid: 5099e549-f4fd-49fb-a290-549edd456c6a
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 63545db31a4290ce933da45c0957dfdb2a00701c
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593858"
---
# <a name="resolve-assembly-loads"></a>Resolver carregamentos de assembly

O .NET fornece o <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> evento para aplicativos que exigem maior controle sobre o carregamento de assembly. Ao tratar esse evento, seu aplicativo pode carregar um assembly no contexto de carga de fora dos caminhos normais de investigação, selecionar qual das várias versões de assembly carregar, emitir um assembly dinâmico e retorná-lo, etc. Este tópico fornece orientação para a manipulação do evento <xref:System.AppDomain.AssemblyResolve>.

> [!NOTE]
> Para resolver carregamentos de assembly no contexto de somente reflexão, use o evento <xref:System.AppDomain.ReflectionOnlyAssemblyResolve?displayProperty=nameWithType> em vez disso.

## <a name="how-the-assemblyresolve-event-works"></a>Como o evento AssemblyResolve funciona

Quando você registra um manipulador para o evento <xref:System.AppDomain.AssemblyResolve>, o manipulador é invocado sempre que o runtime falha ao se associar a um assembly por nome. Por exemplo, chamar os seguintes métodos usando o código do usuário pode fazer com que o evento <xref:System.AppDomain.AssemblyResolve> seja gerado:

- Uma sobrecarga de método <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> ou uma sobrecarga de método <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> cujo primeiro argumento é uma cadeia de caracteres que representa o nome de exibição do assembly a ser carregado (ou seja, a cadeia de caracteres retornada pela propriedade <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType>).

- Uma sobrecarga de método <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> ou uma sobrecarga de método <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> cujo primeiro argumento é um objeto <xref:System.Reflection.AssemblyName> que identifica o assembly a ser carregado.

- Uma sobrecarga de método <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType>.

- Uma sobrecarga de método <xref:System.AppDomain.CreateInstance%2A?displayProperty=nameWithType> ou <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=nameWithType> que cria uma instância de um objeto em outro domínio de aplicativo.

## <a name="what-the-event-handler-does"></a>O que o manipulador de eventos faz

O manipulador do evento <xref:System.AppDomain.AssemblyResolve> recebe o nome de exibição do assembly a ser carregado na propriedade <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType>. Se o manipulador não reconhecer o nome do assembly, ele retornará `null` (C#), `Nothing` (Visual Basic) ou `nullptr` (Visual C++).

Se o manipulador reconhecer o nome do assembly, ele poderá carregar e retornar um assembly que atende à solicitação. A lista a seguir descreve alguns cenários de exemplo.

- Se o manipulador conhecer o local de uma versão do assembly, ele poderá carregar o assembly usando o método <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> ou <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType> e poderá retornar o assembly carregado se tiver êxito.

- Se o manipulador tiver acesso a um banco de dados de assemblies armazenados como matrizes de bytes, ele poderá carregar uma matriz de bytes usando uma das sobrecargas do método <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> que usa uma matriz de bytes.

- O manipulador pode gerar um assembly dinâmico e retorná-lo.

> [!NOTE]
> O manipulador deve carregar o assembly no contexto de carga, no contexto de carga ou sem contexto. Se o manipulador carregar o assembly no contexto somente de reflexão usando o <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=nameWithType> método ou, a tentativa de carregamento que gerou o <xref:System.AppDomain.AssemblyResolve> evento falhará.

É responsabilidade do manipulador de eventos retornar um assembly adequado. O manipulador pode analisar o nome de exibição do assembly solicitado passando o valor da propriedade <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> para o construtor <xref:System.Reflection.AssemblyName.%23ctor%28System.String%29>. A partir do .NET Framework 4, o manipulador pode usar a propriedade <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> para determinar se a solicitação atual é uma dependência de outro assembly. Essas informações podem ajudar a identificar um assembly que atenderá à dependência.

O manipulador de eventos pode retornar uma versão diferente do assembly do que a versão que foi solicitada.

Na maioria dos casos, o assembly que é retornado pelo manipulador aparece no contexto de carga, independentemente do contexto em que o manipulador o carrega. Por exemplo, se o manipulador usar o método <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> para carregar um assembly no contexto de origem de carga, o assembly aparecerá no contexto de carga quando o manipulador o retornar. No entanto, no seguinte caso, o assembly aparece sem contexto quando o manipulador o retorna:

- O manipulador carrega um assembly sem contexto.

- A propriedade <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> não é nula.

- O assembly solicitante (ou seja, o assembly que é retornado pela propriedade <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType>) foi carregado sem contexto.

Para obter informações sobre os contextos, consulte a sobrecarga de método <xref:System.Reflection.Assembly.LoadFrom%28System.String%29?displayProperty=nameWithType>.

Várias versões do mesmo assembly podem ser carregadas no mesmo domínio do aplicativo. Essa prática não é recomendada, pois ela pode levar a problemas de atribuição de tipo. Consulte [práticas recomendadas para o carregamento de assembly](../../framework/deployment/best-practices-for-assembly-loading.md).

## <a name="what-the-event-handler-should-not-do"></a>O que o manipulador de eventos não deve fazer

A regra principal para tratamento do evento <xref:System.AppDomain.AssemblyResolve> é que você não deve tentar retornar um assembly que não reconhece. Ao escrever o manipulador, você deve saber quais assemblies podem fazer com que o evento seja acionado. O manipulador deve retornar nulo para outros assemblies.

> [!IMPORTANT]
> Começando com o .NET Framework 4, o evento <xref:System.AppDomain.AssemblyResolve> é gerado para assemblies satélite. Essa alteração afeta um manipulador de eventos que foi escrito para uma versão anterior do .NET Framework, se o manipulador tenta resolver todas as solicitações de carga do assembly. Manipuladores de eventos que ignoram assemblies que eles não reconhecem não são afetados por essa alteração: eles retornam `null` e mecanismos de fallback normais são seguidos.

Ao carregar um assembly, o manipulador de eventos não deve usar nenhuma das sobrecargas de método <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> ou <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> que possam fazer com que o evento <xref:System.AppDomain.AssemblyResolve> seja gerado recursivamente, pois isso poderia levar a um excedente de pilha. (Consulte a lista fornecida anteriormente neste tópico.) Isso acontece mesmo que você forneça tratamento de exceção para a solicitação de carregamento, porque nenhuma exceção é lançada até que todos os manipuladores de eventos tenham retornado. Desse modo, o seguinte código resultará em um excedente de pilha se `MyAssembly` não for encontrado:

```csharp
using System;
using System.Reflection;

class BadExample
{
    static void Main()
    {
        AppDomain ad = AppDomain.CreateDomain("Test");
        ad.AssemblyResolve += MyHandler;

        try
        {
            object obj = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType");
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

    static Assembly MyHandler(object source, ResolveEventArgs e)
    {
        Console.WriteLine("Resolving {0}", e.Name);
        // DO NOT DO THIS: This causes a StackOverflowException
        return Assembly.Load(e.Name);
    }
}

/* This example produces output similar to the following:

Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
...
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null

Process is terminated due to StackOverflowException.
 */
```

```vb
Imports System.Reflection

Class BadExample

    Shared Sub Main()

        Dim ad As AppDomain = AppDomain.CreateDomain("Test")
        AddHandler ad.AssemblyResolve, AddressOf MyHandler

        Try
            Dim obj As object = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType")
        Catch ex As Exception
            Console.WriteLine(ex.Message)
        End Try
    End Sub

    Shared Function MyHandler(ByVal source As Object, _
                              ByVal e As ResolveEventArgs) As Assembly
        Console.WriteLine("Resolving {0}", e.Name)
        // DO NOT DO THIS: This causes a StackOverflowException
        Return Assembly.Load(e.Name)
    End Function
End Class

' This example produces output similar to the following:
'
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'...
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'
'Process is terminated due to StackOverflowException.
```

```cpp
using namespace System;
using namespace System::Reflection;

ref class Example
{
internal:
    static Assembly^ MyHandler(Object^ source, ResolveEventArgs^ e)
    {
        Console::WriteLine("Resolving {0}", e->Name);
        // DO NOT DO THIS: This causes a StackOverflowException
        return Assembly::Load(e->Name);
    }
};

void main()
{
    AppDomain^ ad = AppDomain::CreateDomain("Test");
    ad->AssemblyResolve += gcnew ResolveEventHandler(&Example::MyHandler);

    try
    {
        Object^ obj = ad->CreateInstanceAndUnwrap(
            "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
            "MyType");
    }
    catch (Exception^ ex)
    {
        Console::WriteLine(ex->Message);
    }
}

/* This example produces output similar to the following:

Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
...
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null

Process is terminated due to StackOverflowException.
*/
```

### <a name="the-correct-way-to-handle-assemblyresolve"></a>A maneira correta de lidar com AssemblyResolve

Ao resolver assemblies do manipulador de <xref:System.AppDomain.AssemblyResolve> eventos, um <xref:System.StackOverflowException> será gerado eventualmente se o manipulador usar as chamadas de <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> método ou. Em vez disso, use <xref:System.Reflection.Assembly.LoadFile%2A> <xref:System.Reflection.Assembly.LoadFrom%2A> métodos ou, pois eles não geram o `AssemblyResolve` evento.

Imagine que `MyAssembly.dll` está localizado próximo ao assembly em execução, em um local conhecido, ele pode ser resolvido usando `Assembly.LoadFile` o caminho fornecido para o assembly.

```csharp
using System;
using System.IO;
using System.Reflection;

class CorrectExample
{
    static void Main()
    {
        AppDomain ad = AppDomain.CreateDomain("Test");
        ad.AssemblyResolve += MyHandler;

        try
        {
            object obj = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType");
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

    static Assembly MyHandler(object source, ResolveEventArgs e)
    {
        Console.WriteLine("Resolving {0}", e.Name);

        var path = Path.GetFullPath("../../MyAssembly.dll");
        return Assembly.LoadFile(path);
     }
}
```

```vb
Imports System.IO
Imports System.Reflection

Class CorrectExample

    Shared Sub Main()

        Dim ad As AppDomain = AppDomain.CreateDomain("Test")
        AddHandler ad.AssemblyResolve, AddressOf MyHandler

        Try
            Dim obj As Object = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType")
        Catch ex As Exception
            Console.WriteLine(ex.Message)
        End Try
    End Sub

    Shared Function MyHandler(ByVal source As Object,
                              ByVal e As ResolveEventArgs) As Assembly
        Console.WriteLine("Resolving {0}", e.Name)

        Dim fullPath = Path.GetFullPath("../../MyAssembly.dll")
        Return Assembly.LoadFile(fullPath)
    End Function
End Class
```

```cpp
using namespace System;
using namespace System::IO;
using namespace System::Reflection;

ref class Example
{
internal:
    static Assembly^ MyHandler(Object^ source, ResolveEventArgs^ e)
    {
        Console::WriteLine("Resolving {0}", e->Name);

        String^ fullPath = Path::GetFullPath("../../MyAssembly.dll");
        return Assembly::LoadFile(fullPath);
    }
};

void main()
{
    AppDomain^ ad = AppDomain::CreateDomain("Test");
    ad->AssemblyResolve += gcnew ResolveEventHandler(&Example::MyHandler);

    try
    {
        Object^ obj = ad->CreateInstanceAndUnwrap(
            "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
            "MyType");
    }
    catch (Exception^ ex)
    {
        Console::WriteLine(ex->Message);
    }
}
```

## <a name="see-also"></a>Confira também

- [Práticas recomendadas para o carregamento de assembly](../../framework/deployment/best-practices-for-assembly-loading.md)
- [Usar domínios de aplicativo](../../framework/app-domains/use.md)
