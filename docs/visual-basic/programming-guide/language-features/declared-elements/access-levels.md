---
description: 'Saiba mais sobre: níveis de acesso no Visual Basic'
title: Níveis de acesso
ms.date: 05/10/2018
helpviewer_keywords:
- members [Visual Basic], accessing in Visual Basic
- Friend access modifier
- access levels, declared elements
- access levels
- access modifiers
- Public access modifier
- Protected access modifier
- Protected Friend access modifier
- Private Protected access modifier
- Private access modifier
- declared elements [Visual Basic], access level
ms.assetid: 6e06c1ab-fd78-47f0-83a8-1152780b5e1a
ms.openlocfilehash: bd26dce5490fde915aeef0a1293ee504a9d4984c
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100464736"
---
# <a name="access-levels-in-visual-basic"></a>Níveis de acesso no Visual Basic

O *nível de acesso* de um elemento declarado é a extensão da capacidade de acessá-lo, ou seja, qual código tem permissão para lê-lo ou gravar nele. Isso é determinado não apenas pelo modo como você declara o próprio elemento, mas também pelo nível de acesso do contêiner do elemento. O código que não pode acessar um elemento recipiente não pode acessar nenhum de seus elementos contidos, mesmo aqueles declarados como `Public` . Por exemplo, uma `Public` variável em uma `Private` estrutura pode ser acessada de dentro da classe que contém a estrutura, mas não de fora dessa classe.

## <a name="public"></a>Público

A palavra-chave [Public](../../../language-reference/modifiers/public.md) na instrução de declaração especifica que o elemento pode ser acessado do código em qualquer lugar no mesmo projeto, de outros projetos que fazem referência ao projeto e de qualquer assembly criado a partir do projeto. O código a seguir mostra uma `Public` declaração de exemplo:

```vb
Public Class ClassForEverybody
```

Você pode usar `Public` somente no nível do módulo, da interface ou do namespace. Isso significa que você pode declarar um elemento público no nível de um arquivo ou namespace de origem, ou dentro de uma interface, módulo, classe ou estrutura, mas não em um procedimento.
  
## <a name="protected"></a>Protegido

A palavra-chave [Protected](../../../language-reference/modifiers/protected.md) na instrução de declaração especifica que o elemento pode ser acessado somente de dentro da mesma classe ou de uma classe derivada dessa classe. O código a seguir mostra uma `Protected` declaração de exemplo:

```vb
Protected Class ClassForMyHeirs
```

Você pode usar `Protected` somente no nível de classe e somente quando declarar um membro de uma classe. Isso significa que você pode declarar um elemento protegido em uma classe, mas não no nível de um arquivo ou namespace de origem, ou dentro de uma interface, módulo, estrutura ou procedimento.

## <a name="friend"></a>Friend

A palavra-chave [Friend](../../../language-reference/modifiers/friend.md) na instrução de declaração especifica que o elemento pode ser acessado de dentro do mesmo assembly, mas não de fora do assembly. O código a seguir mostra uma `Friend` declaração de exemplo:

```vb
Friend stringForThisProject As String
```

Você pode usar `Friend` somente no nível do módulo, da interface ou do namespace. Isso significa que você pode declarar um elemento Friend no nível de um arquivo ou namespace de origem, ou dentro de uma interface, módulo, classe ou estrutura, mas não em um procedimento.

## <a name="protected-friend"></a>Amigo Protegido

A combinação de palavra-chave [Friend protegida](../../../language-reference/modifiers/protected-friend.md) na instrução de declaração especifica que o elemento pode ser acessado de classes derivadas ou de dentro do mesmo assembly, ou ambos. O código a seguir mostra uma `Protected Friend` declaração de exemplo:

```vb
Protected Friend stringForProjectAndHeirs As String
```

Você pode usar `Protected Friend` somente no nível de classe e somente quando declarar um membro de uma classe. Isso significa que você pode declarar um elemento Friend protegido em uma classe, mas não no nível de um arquivo ou namespace de origem, ou dentro de uma interface, módulo, estrutura ou procedimento.

## <a name="private"></a>Privados

A palavra-chave [Private](../../../language-reference/modifiers/private.md) na instrução de declaração especifica que o elemento pode ser acessado somente de dentro do mesmo módulo, classe ou estrutura. O código a seguir mostra uma `Private` declaração de exemplo:

```vb
Private _numberForMeOnly As Integer
```

Você pode usar `Private` somente no nível do módulo. Isso significa que você pode declarar um elemento privado dentro de um módulo, classe ou estrutura, mas não no nível de um arquivo ou namespace de origem, dentro de uma interface ou em um procedimento.

No nível do módulo, a `Dim` instrução sem nenhuma palavra-chave de nível de acesso é equivalente a uma `Private` declaração. No entanto, talvez você queira usar a `Private` palavra-chave para tornar seu código mais fácil de ler e interpretar.

## <a name="private-protected"></a>Protegido de forma particular

A combinação de palavra-chave [protegida privada](../../../language-reference/modifiers/private-protected.md) na instrução de declaração especifica que o elemento pode ser acessado somente de dentro da mesma classe, bem como de classes derivadas encontradas no mesmo assembly que a classe que a contém. O `Private Protected` modificador de acesso tem suporte a partir do Visual Basic 15,5.

O exemplo a seguir mostra uma `Private Protected` declaração:

```vb
Private Protected internalValue As Integer
```

Você pode declarar um `Private Protected` elemento somente dentro de uma classe. Você não pode declará-lo em uma interface ou estrutura, nem pode declará-lo no nível de um arquivo ou namespace de origem, dentro de uma interface ou estrutura, ou em um procedimento.

O `Private Protected` modificador de acesso é suportado pelo Visual Basic 15,5 e posterior. Para usá-lo, adicione o seguinte elemento ao seu arquivo de Visual Basic projeto (*\* . vbproj*). Desde que Visual Basic 15,5 ou posterior esteja instalado no seu sistema, ele permite que você aproveite todos os recursos de linguagem suportados pela versão mais recente do compilador de Visual Basic:

```xml
<PropertyGroup>
   <LangVersion>latest</LangVersion>
</PropertyGroup>
```

Para usar o `Private Protected` modificador de acesso, você deve adicionar o seguinte elemento ao seu arquivo de Visual Basic projeto (*\* . vbproj*):

```xml
<PropertyGroup>
   <LangVersion>15.5</LangVersion>
</PropertyGroup>
```

Para obter mais informações, consulte [definindo a versão do idioma do Visual Basic](../../../language-reference/configure-language-version.md).

## <a name="access-modifiers"></a>Modificadores de acesso

As palavras-chave que especificam o nível de acesso são chamadas de *modificadores de acesso*. A tabela a seguir compara os modificadores de acesso:

|Modificador de acesso|Nível de acesso concedido|Elementos que você pode declarar com este nível de acesso|Contexto de declaração no qual você pode usar este modificador|
|---------------------|--------------------------|-----------------------------------------------------|----------------------------------------------------------------|
|`Public`|Unrestricted:<br /><br /> Qualquer código que possa ver um elemento público pode acessá-lo|Interfaces<br /><br /> Módulos<br /><br /> Classes<br /><br /> Estruturas<br /><br /> Membros da estrutura<br /><br /> Procedimentos<br /><br /> Propriedades<br /><br /> Variáveis de membro<br /><br /> Constantes<br /><br /> Enumerações<br /><br /> Eventos<br /><br /> Declarações externas<br /><br /> Delegados|Arquivo de origem<br /><br /> Namespace<br /><br /> Interface<br /><br /> Módulo<br /><br /> Classe<br /><br /> Estrutura|
|`Protected`|Derivação:<br /><br /> O código na classe que declara um elemento protegido, ou uma classe derivada dele, pode acessar o elemento|Interfaces<br /><br /> Classes<br /><br /> Estruturas<br /><br /> Procedimentos<br /><br /> Propriedades<br /><br /> Variáveis de membro<br /><br /> Constantes<br /><br /> Enumerações<br /><br /> Eventos<br /><br /> Declarações externas<br /><br /> Delegados|Classe|
|`Friend`|Assembly:<br /><br /> O código no assembly que declara um elemento Friend pode acessá-lo|Interfaces<br /><br /> Módulos<br /><br /> Classes<br /><br /> Estruturas<br /><br /> Membros da estrutura<br /><br /> Procedimentos<br /><br /> Propriedades<br /><br /> Variáveis de membro<br /><br /> Constantes<br /><br /> Enumerações<br /><br /> Eventos<br /><br /> Declarações externas<br /><br /> Delegados|Arquivo de origem<br /><br /> Namespace<br /><br /> Interface<br /><br /> Módulo<br /><br /> Classe<br /><br /> Estrutura|
|`Protected` `Friend`|União de `Protected` e `Friend` :<br /><br /> O código na mesma classe ou no mesmo assembly como um elemento Friend protegido, ou dentro de qualquer classe derivada da classe do elemento, pode acessá-lo|Interfaces<br /><br /> Classes<br /><br /> Estruturas<br /><br /> Procedimentos<br /><br /> Propriedades<br /><br /> Variáveis de membro<br /><br /> Constantes<br /><br /> Enumerações<br /><br /> Eventos<br /><br /> Declarações externas<br /><br /> Delegados|Classe|
|`Private`|Contexto da declaração:<br /><br /> O código no tipo que declara um elemento privado, incluindo o código nos tipos contidos, pode acessar o elemento|Interfaces<br /><br /> Classes<br /><br /> Estruturas<br /><br /> Membros da estrutura<br /><br /> Procedimentos<br /><br /> Propriedades<br /><br /> Variáveis de membro<br /><br /> Constantes<br /><br /> Enumerações<br /><br /> Eventos<br /><br /> Declarações externas<br /><br /> Delegados|Módulo<br /><br /> Classe<br /><br /> Estrutura|
|`Private Protected`|Código na classe que declara um elemento protegido particular ou código em uma classe derivada encontrada no mesmo assembly que a classe Bas.|Interfaces<br /><br /> Classes<br /><br /> Estruturas<br /><br /> Procedimentos<br /><br /> Propriedades<br /><br /> Variáveis de membro<br /><br /> Constantes<br /><br /> Enumerações<br /><br /> Eventos<br /><br /> Declarações externas<br /><br /> Delegados|Classe|

## <a name="see-also"></a>Consulte também

- [Instrução Dim](../../../language-reference/statements/dim-statement.md)
- [Estático](../../../language-reference/modifiers/static.md)
- [Nomes de elementos declarados](declared-element-names.md)
- [Referências a elementos declarados](references-to-declared-elements.md)
- [Características do Elemento Declarado](declared-element-characteristics.md)
- [Tempo de vida no Visual Basic](lifetime.md)
- [Escopo no Visual Basic](scope.md)
- [Como controlar a disponibilidade de uma variável](how-to-control-the-availability-of-a-variable.md)
- [Variáveis](../variables/index.md)
- [Declaração de Variável](../variables/variable-declaration.md)
