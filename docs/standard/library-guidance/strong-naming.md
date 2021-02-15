---
title: Nomenclatura forte e bibliotecas do .NET
description: Recomendações de melhores práticas para dar um nome forte a bibliotecas do .NET.
ms.date: 10/16/2018
ms.openlocfilehash: 6f9533d768331964a8e640243536b12ddde158e5
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2020
ms.locfileid: "93189206"
---
# <a name="strong-naming"></a>Nomenclatura forte

Nomenclatura forte refere-se a assinar um assembly com uma chave, produzindo um [assembly de nome forte](../assembly/strong-named.md). Quando um assembly tem um nome forte, ele cria uma identidade exclusiva com base no número de versão de nome e assembly e pode ajudar a evitar conflitos de assembly.

A desvantagem da nomenclatura forte é que .NET Framework no Windows permite o carregamento estrito de assemblies quando um assembly tem um nome forte. Uma referência de assembly de nome forte deve corresponder exatamente à versão do assembly carregado, forçando os desenvolvedores a [Configurar redirecionamentos de associação](../../framework/configure-apps/redirect-assembly-versions.md) ao usar o assembly:

```xml
<configuration>
   <runtime>
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
         <dependentAssembly>
            <assemblyIdentity name="myAssembly" publicKeyToken="32ab4ba45e0a69a1" culture="neutral" />
            <bindingRedirect oldVersion="1.0.0.0" newVersion="2.0.0.0"/>
         </dependentAssembly>
      </assemblyBinding>
   </runtime>
</configuration>
```

Quando os desenvolvedores do .NET reclamam sobre nomenclatura forte, eles normalmente reclamam de carregamento estrito do assembly. Felizmente, esse problema é isolado para .NET Framework. O .NET 5 +, o .NET Core, o Xamarin, o UWP e a maioria das outras implementações do .NET não têm o carregamento estrito do assembly, que é a principal desvantagem da nomeação forte.

Um aspecto importante da nomenclatura forte é que ele é viral: um assembly de nome forte só pode fazer referência outros assemblies de nome forte. Se a biblioteca não tiver um nome forte, você terá excluído os desenvolvedores que estão criando um aplicativo ou uma biblioteca que precisa de nomenclatura forte para usá-lo.

Os benefícios da nomenclatura forte são:

1. O assembly pode ser referenciado e usado por outros assemblies de nome forte.
2. O assembly pode ser armazenado no GAC (Cache de Assembly Global).
3. O assembly pode ser carregado lado a lado com outras versões do assembly. Carregamento do assembly lado a lado é normalmente exigido por aplicativos com arquiteturas de plug-in.

## <a name="create-strong-named-net-libraries"></a>Crie bibliotecas .NET de nome forte

Você deve dar um nome forte às suas bibliotecas do .NET de software livre. A nomeação forte de um assembly garante que a maioria das pessoas possa usá-lo, e o carregamento estrito do assembly só afeta .NET Framework.

> [!NOTE]
> Essas diretrizes são específicas para bibliotecas .NET distribuídas publicamente, como bibliotecas .NET publicadas em NuGet.org. A nomeação forte não é exigida pela maioria dos aplicativos .NET e não deve ser feita por padrão.

✔️ CONSIDERE dar um nome forte aos assemblies da sua biblioteca.

✔️ CONSIDERE adicionar a chave de nome forte ao seu sistema de controle do código-fonte.

> Uma chave disponível publicamente permite aos desenvolvedores modificar e recompilar o código-fonte da biblioteca com a mesma chave.
>
> Você não deverá tornar pública a chave de nome forte se ela tiver sido usada anteriormente para conceder permissões especiais em [cenários de confiança parcial](../../framework/misc/using-libraries-from-partially-trusted-code.md). Caso contrário, você poderá comprometer ambientes existentes.

> [!IMPORTANT]
> Quando a identidade do editor do código for desejada, [Authenticode](/windows-hardware/drivers/install/authenticode) e [Assinatura de Pacote do NuGet](/nuget/create-packages/sign-a-package) são recomendados. CAS (Segurança de Acesso do Código) não deve ser usada como uma mitigação de segurança.

✔️ CONSIDERE incrementar a versão do assembly nas alterações de versão principal somente para ajudar os usuários a reduzir os redirecionamentos de associação e a frequência com que eles sejam atualizados.

> Leia mais sobre [controle de versão e versão do assembly](./versioning.md#assembly-version).

❌ Não adicione, remova ou altere a chave de nomenclatura forte.

> Modificar a chave de nome forte do assembly muda a identidade do assembly e interrompe o código compilado que a utiliza. Para obter mais informações, veja [alterações interruptivas binárias](./breaking-changes.md#binary-breaking-change).

❌ Não publique versões de nome forte e não forte da sua biblioteca. Por exemplo, `Contoso.Api` e `Contoso.Api.StrongNamed`.

> Publicar dois pacotes bifurca o ecossistema do desenvolvedor. Além disso, se um aplicativo acabar dependendo de ambos os pacotes, o desenvolvedor poderá encontrar conflitos de nome de tipo. No que diz respeito ao .NET, há diferentes tipos em diferentes assemblies.

>[!div class="step-by-step"]
>[Anterior](cross-platform-targeting.md) 
> [Avançar](nuget.md)
