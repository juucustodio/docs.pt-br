---
title: Selecione a versão do idioma do Visual Basic
description: Configure o compilador para executar a validação de sintaxe usando uma versão específica do compilador.
ms.date: 05/24/2018
ms.openlocfilehash: 09503db726f9d993bc986860c57aa98652b696d1
ms.sourcegitcommit: 65af0f0ad316858882845391d60ef7e303b756e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/05/2021
ms.locfileid: "99585449"
---
# <a name="select-the-visual-basic-language-version"></a>Selecione a versão do idioma do Visual Basic

O compilador de Visual Basic usa como padrão a versão principal mais recente do idioma que foi lançado. Você pode optar por compilar qualquer projeto usando uma nova versão de ponto da linguagem. A escolha de uma versão mais recente da linguagem permite que o projeto use as últimas funcionalidades da linguagem. Em outros cenários, talvez você precise validar se um projeto é compilado por completo ao usar uma versão mais antiga da linguagem.

Essa funcionalidade separa a decisão de instalar novas versões do SDK e das ferramentas no ambiente de desenvolvimento da decisão de incorporar novas funcionalidades da linguagem em um projeto. Instale o último SDK e as últimas ferramentas no computador de build. Cada projeto pode ser configurado para usar uma versão específica da linguagem de seu build.

Há três maneiras de definir a versão do idioma:

- Editar manualmente seu [arquivo **. vbproj**](#edit-the-vbproj-file)
- Definir a versão [de idioma para vários projetos em um subdiretório](#configure-multiple-projects)
- Configurar a [ `-langversion` opção do compilador](#set-the-langversion-compiler-option)

## <a name="edit-the-vbproj-file"></a>Editar o arquivo vbproj

Você pode definir a versão de idioma no arquivo **. vbproj** . Adicione o seguinte elemento:

```xml
<PropertyGroup>
   <LangVersion>latest</LangVersion>
</PropertyGroup>
```

O valor `latest` usa a versão secundária mais recente do idioma de Visual Basic. Os valores válidos são:

|Valor|Significado|
|------------|-------------|
|padrão|O compilador aceita toda a sintaxe de linguagem válida da versão principal mais recente à qual dá suporte.|
|9|O compilador aceita apenas a sintaxe incluída no Visual Basic 9,0 ou inferior.|
|10|O compilador aceita apenas a sintaxe incluída no Visual Basic 10,0 ou inferior.|
|11|O compilador aceita apenas a sintaxe incluída no Visual Basic 11,0 ou inferior.|
|12|O compilador aceita apenas a sintaxe incluída no Visual Basic 12,0 ou inferior.|
|14|O compilador aceita apenas a sintaxe incluída no Visual Basic 14,0 ou inferior.|
|15|O compilador aceita apenas a sintaxe incluída no Visual Basic 15,0 ou inferior.|
|15.3|O compilador aceita apenas a sintaxe incluída no Visual Basic 15,3 ou inferior.|
|15.5|O compilador aceita apenas a sintaxe incluída no Visual Basic 15,5 ou inferior.|
|16|O compilador aceita apenas a sintaxe incluída no Visual Basic 16 ou inferior.|
|16,9|O compilador aceita apenas a sintaxe incluída no Visual Basic 16,9 ou inferior.|
|mais recente|O compilador aceita toda a sintaxe de linguagem à qual dá suporte.|

As cadeias de caracteres especiais `default` e `latest` são resolvidas nas últimas versões da linguagem principal e secundária instaladas no computador de build, respectivamente.

## <a name="configure-multiple-projects"></a>Configurar vários projetos

Crie um arquivo **Directory.build.props** que contém o elemento `<LangVersion>` para configurar vários diretórios. Normalmente, você faz isso no diretório da solução. Adicione o seguinte a um arquivo **Directory.build.props** no diretório de solução:

```xml
<Project>
 <PropertyGroup>
   <LangVersion>15.5</LangVersion>
 </PropertyGroup>
</Project>
```

Agora, as compilações em cada subdiretório do diretório que contém esse arquivo usarão Visual Basic sintaxe da versão 15,5. Para obter mais informações, confira o artigo sobre como [personalizar o build](/visualstudio/msbuild/customize-your-build).

## <a name="set-the-langversion-compiler-option"></a>Definir a opção langversion do compilador

Você pode usar a opção `-langversion` da linha de comando. Para obter mais informações, confira o artigo sobre a opção [-langversion](../reference/command-line-compiler/langversion.md) do compilador. Você pode ver uma lista dos valores válidos digitando  `vbc -langversion:?` .
