---
ms.openlocfilehash: 85488de561a2298f2ff4009ec78b9a6e294053f3
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89598171"
---
### <a name="threadabort-is-obsolete"></a>Thread. Abort é obsoleto

As <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> APIs estão obsoletas. Os projetos direcionados ao .NET 5,0 ou uma versão posterior encontrarão avisos de tempo de compilação se esses métodos forem chamados. Se você suprimir os avisos, um <xref:System.PlatformNotSupportedException> será lançado em tempo de execução.

#### <a name="change-description"></a>Descrição das alterações

Anteriormente, as chamadas para <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> não produziram avisos de tempo de compilação, no entanto, o método lançou um <xref:System.PlatformNotSupportedException> em tempo de execução.

A partir do .NET 5,0, <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> é marcado como obsoleto como aviso. Chamar esse método produz o aviso do compilador `SYSLIB0006` . A implementação do método permanece inalterada e continua lançando um <xref:System.PlatformNotSupportedException> .

#### <a name="reason-for-change"></a>Motivo da alteração

Considerando que <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> o sempre lança um <xref:System.PlatformNotSupportedException> em todas as implementações do .net, exceto .NET Framework, <xref:System.ObsoleteAttribute> foi adicionado ao método para chamar a atenção para locais onde ele é chamado.

#### <a name="version-introduced"></a>Versão introduzida

5,0 RC 1

#### <a name="recommended-action"></a>Ação recomendada

- Use um <xref:System.Threading.CancellationToken> para anular o processamento de uma unidade de trabalho em vez de chamar <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> . O exemplo a seguir ilustra o uso de <xref:System.Threading.CancellationToken> .

  ```csharp
  void ProcessPendingWorkItemsNew(CancellationToken cancellationToken)
  {
      if (QueryIsMoreWorkPending())
      {
          // If the CancellationToken is marked as "needs to cancel",
          // this will throw the appropriate exception.
          cancellationToken.ThrowIfCancellationRequested();

          WorkItem work = DequeueWorkItem();
          ProcessWorkItem(work);
      }
  }
  ```

  Para saber mais, confira [Cancelamento em threads gerenciados](../../../../docs/standard/threading/cancellation-in-managed-threads.md).

- Para suprimir o aviso de tempo de compilação, suprime o código de aviso `SYSLIB0006` . O código de aviso é específico para <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> e a supressão dele não elimina outros avisos de obsoletion em seu código. No entanto, recomendamos que você remova <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> as chamadas para, em vez de suprimir o aviso.

  ```csharp
  void MyMethod()
  {
  #pragma warning disable SYSLIB0006
      Thread.CurrentThread.Abort();
  #pragma warning restore SYSLIB0006
  }
  ```

  Você também pode suprimir o aviso no arquivo de projeto.

  ```xml
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>
    <!-- Disable "Thread.Abort is obsolete" warnings for entire project. -->
    <NoWarn>$(NoWarn);SYSLIB0006</NoWarn>
  </PropertyGroup>
  ```

#### <a name="category"></a>Categoria

- Bibliotecas principais do .NET

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName>

<!--

#### Affected APIs

- `Overload:System.Threading.Thread.Abort`

-->
