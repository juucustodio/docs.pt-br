---
title: 'Alteração significativa: CA1416: compatibilidade de plataforma'
description: Saiba mais sobre a alteração significativa no .NET 5,0 causada pela habilitação da regra de análise de código CA1416.
ms.date: 09/29/2020
ms.openlocfilehash: ec3fc809b8de382a2093fc9f2d33c2f96b91613d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760309"
---
# <a name="warning-ca1416-platform-compatibility"></a>Aviso CA1416: compatibilidade de plataforma

A regra do analisador de código .NET [CA1416](/visualstudio/code-quality/ca1416) está habilitada, por padrão, a partir do .NET 5,0. Ele produz um aviso de compilação para chamadas a APIs específicas da plataforma de sites de chamada que não verificam o sistema operacional.

## <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../fundamentals/code-analysis/overview.md). Várias dessas regras estão habilitadas, por padrão, incluindo [CA1416](/visualstudio/code-quality/ca1416). Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação. A regra CA1416 informa quando você está usando APIs específicas da plataforma de locais onde o contexto da plataforma não é verificado.

A regra [CA1416](/visualstudio/code-quality/ca1416), o analisador de compatibilidade de plataforma, trabalha em conjunto com alguns outros recursos que são novos no .NET 5,0. O .NET 5,0 apresenta o <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> e o <xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> , que permitem especificar as plataformas nas quais uma API *é* ou *não* tem suporte. Na ausência desses atributos, pressupõe-se que uma API tenha suporte em todas as plataformas. Esses atributos foram aplicados a APIs específicas da plataforma nas principais bibliotecas do .NET.

Em projetos que visam plataformas para as quais as APIs que eles usam não estão disponíveis, a regra [CA1416](/visualstudio/code-quality/ca1416) sinaliza qualquer chamada de API específica da plataforma onde o contexto da plataforma não é verificado. A maioria das APIs que agora estão decoradas com <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> os <xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> atributos e gera <xref:System.PlatformNotSupportedException> exceções quando elas são invocadas em um sistema operacional sem suporte. Agora que essas APIs estão marcadas como específicas da plataforma, a regra [CA1416](/visualstudio/code-quality/ca1416) ajuda você a evitar exceções em tempo de execução <xref:System.PlatformNotSupportedException> adicionando verificações do sistema operacional aos seus sites de chamada.

## <a name="examples"></a>Exemplos

- O <xref:System.Console.Beep(System.Int32,System.Int32)?displayProperty=nameWithType> método só tem suporte no Windows e é decorado com `[SupportedOSPlatform("windows")]` . O código a seguir produzirá um aviso de CA1416 no momento da compilação se o projeto tiver como [destino](../../../../standard/frameworks.md) `net5.0` (mas não `net5.0-windows` ). Para ações que você pode executar para evitar o aviso, consulte a [ação recomendada](#recommended-action).

  ```csharp
  public void PlayCMajor()
  {
      Console.Beep(261, 1000);
  }
  ```

- O <xref:System.Drawing.Image.FromFile(System.String)?displayProperty=nameWithType> método não tem suporte no navegador e é decorado com `[UnsupportedOSPlatform("browser")]` . O código a seguir produzirá um aviso de CA1416 no momento da compilação se o projeto der suporte à plataforma do navegador.

  ```csharp
  public void CreateImage()
  {
      Image newImage = Image.FromFile("SampImag.jpg");
  }
  ```

  > [!TIP]
  >
  > - Os projetos de Webassembly mais incrivelmente e projetos de biblioteca de classes Razor incluem suporte de navegador automaticamente.
  > - Para adicionar manualmente o navegador como uma plataforma com suporte para seu projeto, adicione a seguinte entrada ao arquivo de projeto:
  >
  >  ```xml
  >  <ItemGroup>
  >    <SupportedPlatform Include="browser" />
  >  </ItemGroup>
  >  ```

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Verifique se as APIs específicas da plataforma são chamadas apenas quando o código está sendo executado em uma plataforma apropriada. Você pode verificar o sistema operacional atual usando um dos `Is<Platform>` métodos na classe, <xref:System.OperatingSystem?displayProperty=nameWithType> por exemplo,, <xref:System.OperatingSystem.IsWindows?displayProperty=nameWithType> antes de chamar uma API específica da plataforma.

Você pode usar um dos `Is<Platform>` métodos na condição de uma `if` instrução:

```csharp
public void PlayCMajor()
{
    if (OperatingSystem.IsWindows())
    {
        Console.Beep(261, 1000);
    }
}
```

Ou, se você não quiser a sobrecarga de uma `if` instrução adicional em tempo de execução, chame <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType> :

```csharp
public void PlayCMajor()
{
    Debug.Assert(OperatingSystem.IsWindows());
    Console.Beep(261, 1000);
}
```

Se você estiver criando uma biblioteca, poderá marcar sua API como específica da plataforma. Nesse caso, a carga dos requisitos de verificação cai nos seus chamadores. Você pode marcar métodos ou tipos específicos ou um assembly inteiro.

```csharp
[SupportedOSPlatform("windows")]
public void PlayCMajor()
{
    Console.Beep(261, 1000);
}
```

Se você não quiser corrigir todos os seus sites de chamada, poderá escolher uma das seguintes opções para suprimir o aviso:

- Para suprimir a regra CA1416, você pode fazer isso usando `#pragma` o ou o sinalizador do compilador [-nowarn](../../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md) ou [definindo a severidade da regra](../../../../fundamentals/code-analysis/configuration-options.md#severity-level) como `none` em um arquivo. editorconfig.

  ```csharp
  public void PlayCMajor()
  {
  #pragma warning disable CA1416
      Console.Beep(261, 1000);
  #pragma warning restore CA1416
  }
  ```

- Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto. Para obter mais informações, consulte [EnableNETAnalyzers](../../../project-sdk/msbuild-props.md#enablenetanalyzers).

## <a name="affected-apis"></a>APIs afetadas

Para a plataforma Windows:

- Todas as APIs listadas em <https://github.com/dotnet/designs/blob/master/accepted/2020/windows-specific-apis/windows-specific-apis.md> .
- <xref:System.Security.Cryptography.DSAOpenSsl?displayProperty=fullName>
- <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl?displayProperty=fullName>
- <xref:System.Security.Cryptography.ECDsaOpenSsl?displayProperty=fullName>
- <xref:System.Security.Cryptography.RSAOpenSsl?displayProperty=fullName>

Para a plataforma Webassembly mais incrivelmente:

- Todas as APIs listadas em <https://github.com/dotnet/runtime/issues/41087> .

<!--

### Affected APIs

- ``

### Category

- Code analysis
- Core .NET libraries

-->

## <a name="see-also"></a>Confira também

- [CA1416: validar a compatibilidade da plataforma](/visualstudio/code-quality/ca1416)
- [Analisador de API do .NET](../../../../standard/analyzers/api-analyzer.md)
