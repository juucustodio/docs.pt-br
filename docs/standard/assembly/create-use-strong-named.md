---
title: Criar e usar assemblies com nome forte
description: Este artigo mostra o processo de assinatura de um assembly no .NET com um nome forte e mais tarde referenciando-o por esse nome.
ms.date: 08/19/2019
helpviewer_keywords:
- strong-name bypass feature
- strong-named assemblies, about strong-named assemblies
- strong-named assemblies
- signing assemblies
- assemblies [.NET], signing
- strong-named assemblies, scenarios
- assemblies [.NET], strong-named
- strong-named assemblies, loading into trusted application domains
- assembly binding, strong-named
ms.assetid: ffbf6d9e-4a88-4a8a-9645-4ce0ee1ee5f9
ms.openlocfilehash: 1d87edde97e77011b678662f61500c7acd8293b0
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162707"
---
# <a name="create-and-use-strong-named-assemblies"></a>Criar e usar assemblies com nome forte

Um nome forte consiste na identidade do assembly — seu nome de texto simples, número de versão e informações de cultura (se fornecidas) — mais uma chave pública e uma assinatura digital. Ela é gerada de um arquivo do assembly usando a chave privada correspondente. (O arquivo do assembly inclui o manifesto do assembly, que contém os nomes e os hashes de todos os arquivos que compõem o assembly.)

> [!WARNING]
> Por segurança, não confie em nomes fortes. Eles apenas fornecem uma identidade exclusiva.

Assembly de nome forte só pode usar tipos de outros assemblies de nome forte. Caso contrário, a integridade do assembly de nome forte estaria comprometida.

> [!NOTE]
> Embora o .NET Core dê suporte a assemblies de nome forte e todos os assemblies na biblioteca do .NET Core sejam assinados, a maioria dos assemblies de terceiros não precisa de nomes fortes. Para obter mais informações, consulte [assinatura de nome forte](https://github.com/dotnet/runtime/blob/master/docs/project/strong-name-signing.md) no github.

## <a name="strong-name-scenario"></a>Cenário de nome forte

O cenário a seguir descreve o processo de assinar um assembly com um nome forte e posteriormente referencia-lo por esse nome.

1. O Assembly A é criado com um nome forte usando um dos seguintes métodos:

    - Usando um ambiente de desenvolvimento que dá suporte à criação de nomes fortes, tal como o Visual Studio.

    - Criando um par de chaves de criptografia usando a [ferramenta Nome Forte (Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md) e atribuindo esse par de chaves ao assembly usando um compilador de linha de comando ou o [Assembly Linker (Al.exe)](../../framework/tools/al-exe-assembly-linker.md). O SDK do Windows fornece o Sn.exe e o Al.exe.

2. O ambiente de desenvolvimento ou a ferramenta assina o hash do arquivo que contém o manifesto do assembly com a chave privada do desenvolvedor. Esta assinatura digital é armazenada no arquivo PE que contém o manifesto do Assembly A.

3. O Assembly B é um consumidor do Assembly A. A seção de referência do manifesto do Assembly B inclui um token que representa a chave pública do Assembly A. Um token é uma parte da chave pública completa e é usado em vez da chave em si para economizar espaço.

4. O Common Language Runtime verifica a assinatura do nome forte quando o assembly é colocado no cache de assembly global. Ao associar por um nome forte no tempo de execução, o Common Language Runtime compara a chave armazenada no manifesto do assembly B com a chave usada para gerar o nome forte para o assembly A. Se as verificações de segurança do .NET forem aprovadas e a ligação tiver êxito, o assembly B terá uma garantia de que os bits do assembly A não foram adulterados e que esses bits realmente são provenientes dos desenvolvedores do assembly A.

> [!NOTE]
> Este cenário não aborda problemas de confiança. Os assemblies podem carregar assinaturas Microsoft Authenticode completas além de um nome forte. As assinaturas Authenticode incluem um certificado que estabelece a relação de confiança. É importante observar que os nomes fortes não exigem que o código esteja assinado dessa maneira. Os nomes fortes apenas fornecem uma identidade exclusiva.

## <a name="bypass-signature-verification-of-trusted-assemblies"></a>Ignorar a verificação de assinatura de assemblies confiáveis

A partir do .NET Framework 3.5 Service Pack 1, as assinaturas de nome forte não são validadas quando um assembly é carregado em um domínio do aplicativo de confiança total, como o domínio do aplicativo padrão para a zona `MyComputer`. Isso é conhecido como o recurso de desvio de nome forte. Em um ambiente de confiança total, as exigências de <xref:System.Security.Permissions.StrongNameIdentityPermission> sempre têm êxito para assemblies assinados de confiança total, independentemente de sua assinatura. O recurso de desvio de nome forte evita a sobrecarga desnecessária de verificação de assinatura de nome forte dos assemblies de confiança total nessa situação, permitindo que os assemblies carreguem mais rapidamente.

O recurso de desvio se aplica a qualquer assembly que está assinado com um nome forte e que tem as seguintes características:

- Totalmente confiável sem a evidência <xref:System.Security.Policy.StrongName> (por exemplo, tem a evidência de zona `MyComputer`).

- Carregado em um <xref:System.AppDomain> totalmente confiável.

- Carregado de um local sob a propriedade <xref:System.AppDomainSetup.ApplicationBase%2A> desse <xref:System.AppDomain>.

- Não assinado com atraso.

Esse recurso pode ser desabilitado para aplicativos individuais ou para um computador. Consulte [como desabilitar o recurso de bypass de nome forte](disable-strong-name-bypass-feature.md).

## <a name="related-topics"></a>Tópicos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Como criar um par de chaves pública-privada](create-public-private-key-pair.md)|Descreve como criar um par de chaves de criptografia para assinar um assembly.|
|[Como assinar um assembly com um nome forte](sign-strong-name.md)|Descreve como criar um assembly de nome forte.|
|[Nomenclatura forte aprimorada](enhanced-strong-naming.md)|Descreve aprimoramentos para nomes fortes no .NET Framework 4.5.|
|[Como referenciar um assembly de nome forte](reference-strong-named.md)|Descreve como referenciar tipos ou recursos em um assembly de nome forte no tempo de compilação ou no tempo de execução.|
|[Como desabilitar o recurso de bypass de nome forte](disable-strong-name-bypass-feature.md)|Descreve como desabilitar o recurso que ignora a validação de assinaturas de nome forte. Esse recurso pode ser desabilitado para todos ou para aplicativos específicos.|
|[Criar assemblies](create.md)|Fornece uma visão geral dos assemblies de arquivo único e vários arquivos.|
|[Como atrasar a assinatura de um assembly no Visual Studio](/visualstudio/ide/managing-assembly-and-manifest-signing#how-to-sign-an-assembly-in-visual-studio)|Explica como assinar um assembly com um nome forte, depois que o assembly foi criado.|
|[Sn.exe (ferramenta de nome forte)](../../framework/tools/sn-exe-strong-name-tool.md)|Descreve a ferramenta incluída no .NET Framework que ajuda a criar assemblies com nomes fortes. Esta ferramenta oferece opções para o gerenciamento de chaves, geração de assinaturas e verificação de assinaturas.|
|[Al.exe (Assembly linker)](../../framework/tools/al-exe-assembly-linker.md)|Descreve a ferramenta incluída no .NET Framework que gera um arquivo que tem um manifesto do assembly de módulos ou arquivos de recurso.|
