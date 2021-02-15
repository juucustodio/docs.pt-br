---
title: 'Alteração significativa: não há suporte para a instanciação de implementações padrão de abstrações criptográficas'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que as sobrecargas de criação sem parâmetros () em abstrações criptográficas são obsoletas.
ms.date: 10/16/2020
ms.openlocfilehash: 8ed7d0b72347ec41ec65ccd9e4004266619c84f7
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760484"
---
# <a name="instantiating-default-implementations-of-cryptographic-abstractions-is-not-supported"></a>Não há suporte para a instanciação de implementações padrão de abstrações criptográficas

As `Create()` sobrecargas sem parâmetros em abstrações criptográficas são obsoletas como aviso a partir do .net 5,0.

## <a name="change-description"></a>Descrição das alterações

No .NET Framework 2,0-4,8, as fábricas de primitiva de criptografia abstratas, como, <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> podem ser configuradas para retornar algoritmos diferentes. Por exemplo, em uma instalação padrão do .NET Framework 4,8, o método estático sem parâmetros <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> retorna uma instância do algoritmo SHA1, conforme mostrado no trecho a seguir.

**Somente .NET Framework**

```csharp
// Return an instance of the default hash algorithm (SHA1).
HashAlgorithm alg = HashAlgorithm.Create();
// Prints 'System.Security.Cryptography.SHA1CryptoServiceProvider'.
Console.WriteLine(alg.GetType());

// Change the default algorithm to be SHA256, not SHA1.
CryptoConfig.AddAlgorithm(typeof(SHA256CryptoServiceProvider), typeof(HashAlgorithm).FullName);
alg = HashAlgorithm.Create();
// Prints 'System.Security.Cryptography.SHA256CryptoServiceProvider'.
Console.WriteLine(alg.GetType());
```

Você também pode usar a [configuração em todo o computador](../../../../framework/configure-apps/map-algorithm-names-to-cryptography-classes.md) para alterar o algoritmo padrão sem a necessidade de chamar de `CryptoConfig` forma programática.

No .NET Core 2,0-3,1, abstratos de extensão primitiva de criptografia, como o <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> Always throw a <xref:System.PlatformNotSupportedException> .

```csharp
// Throws PlatformNotSupportedException on .NET Core.
HashAlgorithm alg = HashAlgorithm.Create();
```

No .NET 5,0 e versões posteriores, as fábricas primitivas de criptografia abstratas como <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> estão marcadas como obsoletas e produzem um aviso de tempo de compilação com a ID `SYSLIB0007` . Em tempo de execução, esses métodos continuam lançando um <xref:System.PlatformNotSupportedException> .

```csharp
// Throws PlatformNotSupportedException.
// Also produces compile-time warning SYSLIB0007 on .NET 5+.
HashAlgorithm alg = HashAlgorithm.Create();
```

Essa é uma alteração somente em tempo de compilação. Não há nenhuma alteração de tempo de execução de versões anteriores do .NET Core.

> [!NOTE]
>
> - Somente as sobrecargas sem parâmetros dos `Create()` métodos são obsoletas. Sobrecargas parametrizadas não são obsoletas e continuam funcionando conforme o esperado.
>
>   ```csharp
>   // Call Create(string), providing an explicit algorithm family name.
>   // Works in .NET Framework, .NET Core, and .NET 5.0+.
>   HashAlgorithm hashAlg = HashAlgorithm.Create("SHA256");
>   ```
>
> - Sobrecargas sem parâmetros de famílias de algoritmos *específicas* (não abstrações) não são obsoletas e continuarão a funcionar conforme o esperado.
>
>   ```csharp
>   // Call a specific algorithm family's parameterless Create() ctor.
>   // Works in .NET Framework, .NET Core, and .NET 5.0+.
>   Aes aesAlg = Aes.Create();
>   ```

## <a name="reason-for-change"></a>Motivo da alteração

O sistema de configuração criptográfica presente no .NET Framework não está mais presente no .NET Core e no .NET 5.0 +, já que esse sistema herdado não permite uma agilidade de criptografia adequada. Os requisitos de compatibilidade com versões anteriores do .NET também proíbem a estrutura de atualizar determinadas APIs de criptografia para acompanhar os avanços em criptografia. Por exemplo, o <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> método foi introduzido no .NET Framework 1,0, quando o algoritmo de hash SHA-1 era de ponta. Vinte anos passaram e agora o SHA-1 é considerado desfeito, mas não podemos mudar <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> para retornar um algoritmo diferente. Isso introduziria uma alteração significativa inaceitável no consumo de aplicativos.

A prática recomendada determina que as bibliotecas que consomem primitivos criptográficos (como AES, SHA-* e RSA) devem estar em controle total sobre como elas consomem esses primitivos. Os aplicativos que exigem a futura verificação devem utilizar bibliotecas de nível superior que encapsulam esses primitivos e adicionem recursos de agilidade de gerenciamento e de chave. Essas bibliotecas são geralmente fornecidas pelo ambiente de hospedagem. Um exemplo é o [ASP. A biblioteca de proteção de dados da rede](/aspnet/core/security/data-protection/), que lida com essas preocupações em nome do aplicativo de chamada.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

- O curso de ação recomendado é substituir as chamadas para as APIs agora obsoletas por chamadas para métodos de fábrica para algoritmos específicos, por exemplo, <xref:System.Security.Cryptography.Aes.Create?displayProperty=nameWithType> . Isso lhe dá controle total sobre quais algoritmos são instanciados.

- Se você precisar manter a compatibilidade com as cargas existentes geradas por .NET Framework aplicativos que usam as APIs agora obsoletas, use as substituições sugeridas na tabela a seguir. A tabela fornece um mapeamento de .NET Framework algoritmos padrão para seus equivalentes do .NET 5 +.

  | .NET Framework | .NET Core/.NET 5.0 + substituição compatível | Comentários |
  | - | - | - |
  | <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.RSA.Create?displayProperty=nameWithType> | |
  | <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.SHA1.Create?displayProperty=nameWithType> | O algoritmo SHA-1 é considerado desfeito. Considere o uso de um algoritmo mais forte, se possível. Consulte seu supervisor de segurança para obter mais diretrizes. |
  | <xref:System.Security.Cryptography.HMAC.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.HMACSHA1.%23ctor> | O algoritmo HMACSHA1 não é recomendado para a maioria dos aplicativos modernos. Considere o uso de um algoritmo mais forte, se possível. Consulte seu supervisor de segurança para obter mais diretrizes. |
  | <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.HMACSHA1.%23ctor> | O algoritmo HMACSHA1 não é recomendado para a maioria dos aplicativos modernos. Considere o uso de um algoritmo mais forte, se possível. Consulte seu supervisor de segurança para obter mais diretrizes. |
  | <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.Aes.Create?displayProperty=nameWithType> |

- Se você precisar continuar chamando as sobrecargas sem parâmetros obsoletos `Create()` , poderá suprimir o `SYSLIB0007` aviso no código.

  ```csharp
  #pragma warning disable SYSLIB0007 // Disable the warning.
  HashAlgorithm alg = HashAlgorithm.Create(); // Still throws PNSE.
  #pragma warning restore SYSLIB0007 // Re-enable the warning.
  ```

  Você também pode suprimir o aviso em seu arquivo de projeto. Isso desabilita o aviso para todos os arquivos de origem dentro do projeto.

  ```xml
  <Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
     <TargetFramework>net5.0</TargetFramework>
     <!-- NoWarn below suppresses SYSLIB0007 project-wide -->
     <NoWarn>$(NoWarn);SYSLIB0007</NoWarn>
    </PropertyGroup>
  </Project>
  ```

  > [!NOTE]
  > Suprimir `SYSLIB0007` desabilita apenas os avisos obsoletion para as APIs de criptografia listadas aqui. Ele não desabilita nenhum outro aviso. Além disso, mesmo se você suprimir o aviso, essas APIs obsoletas ainda serão lançadas <xref:System.PlatformNotSupportedException> em tempo de execução.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.HMAC.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=fullName>

<!--

### Affected APIs

- `M:System.Security.Cryptography.AsymmetricAlgorithm.Create`
- `M:System.Security.Cryptography.HashAlgorithm.Create`
- `M:System.Security.Cryptography.HMAC.Create`
- `M:System.Security.Cryptography.KeyedHashAlgorithm.Create`
- `M:System.Security.Cryptography.SymmetricAlgorithm.Create`

### Category

- Cryptography

-->
