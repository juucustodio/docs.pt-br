---
title: Aviso de SYSLIB0004
description: Saiba mais sobre o obsoletions que gera SYSLIB0004 de aviso de tempo de compilação.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 03be8bb54f71f74ed94ee2c3f8489397ae1e99b5
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596430"
---
# <a name="syslib0004-the-constrained-execution-region-cer-feature-is-not-supported"></a>SYSLIB0004: não há suporte para o recurso CER (região de execução restrita)

Há suporte para o recurso [cer (regiões de execução restrita)](../../../framework/performance/constrained-execution-regions.md) somente no .NET Framework. Assim, várias APIs relacionadas à CER são marcadas como obsoletas, começando no .NET 5,0. O uso dessas APIs gera aviso `SYSLIB0004` no momento da compilação.

As seguintes APIs relacionadas a CER são obsoletas:

- <xref:System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup(System.Runtime.CompilerServices.RuntimeHelpers.TryCode,System.Runtime.CompilerServices.RuntimeHelpers.CleanupCode,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegionsNoOP?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareContractedDelegate(System.Delegate)?displayProperty=nameWithType>
- <xref:System.Runtime.CompilerServices.RuntimeHelpers.ProbeForSufficientStack?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.Cer?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.Consistency?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.PrePrepareMethodAttribute?displayProperty=nameWithType>
- <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute?displayProperty=nameWithType>

## <a name="workarounds"></a>Soluções Alternativas

- Se você aplicou um atributo CER a um método, remova o atributo. Esses atributos não têm nenhum efeito no .NET 5,0 e versões posteriores.

  ```csharp
  // REMOVE the attribute below.
  [ReliabilityContract(Consistency.WillNotCorruptState, Cer.Success)]
  public void DoSomething()
  {
  }

  // REMOVE the attribute below.
  [PrePrepareMethod]
  public void DoSomething()
  {
  }
  ```

- Se você estiver chamando `RuntimeHelpers.ProbeForSufficientStack` ou `RuntimeHelpers.PrepareContractedDelegate` , remova a chamada. Essas chamadas não têm nenhum efeito no .NET 5,0 e versões posteriores.

  ```csharp
  public void DoSomething()
  {
      // REMOVE the call below.
      RuntimeHelpers.ProbeForSufficientStack();

      // (Remainder of your method logic here.)
  }
  ```

- Se você estiver chamando `RuntimeHelpers.PrepareConstrainedRegions` , remova a chamada. Essa chamada não tem nenhum efeito no .NET 5,0 e versões posteriores.

  ```csharp
  public void DoSomething_Old()
  {
      // REMOVE the call below.
      RuntimeHelpers.PrepareConstrainedRegions();
      try
      {
          // try code
      }
      finally
      {
          // cleanup code
      }
  }

  public void DoSomething_Corrected()
  {
      // There is no call to PrepareConstrainedRegions. It's a normal try / finally block.

      try
      {
          // try code
      }
      finally
      {
          // cleanup code
      }
  }
  ```

- Se você estiver chamando `RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup` , substitua a chamada por um bloco _try/catch/finally_ padrão.

  ```csharp
  // The sample below produces warning SYSLIB0004.
  public void DoSomething_Old()
  {
      RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup(MyTryCode, MyCleanupCode, null);
  }
  public void MyTryCode(object state) { /* try code */ }
  public void MyCleanupCode(object state, bool exceptionThrown) { /* cleanup code */ }

  // The corrected sample below does not produce warning SYSLIB0004.
  public void DoSomething_Corrected()
  {
      try
      {
          // try code
      }
      catch (Exception ex)
      {
          // exception handling code
      }
      finally
      {
          // cleanup code
      }
  }
  ```

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a>Confira também

- [Regiões de execução restrita](../../../framework/performance/constrained-execution-regions.md)
