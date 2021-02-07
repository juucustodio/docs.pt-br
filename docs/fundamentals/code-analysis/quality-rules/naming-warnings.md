---
title: Regras de nomenclatura (análise de código)
description: Saiba mais sobre as regras de nomenclatura da análise de código.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.namingrules
helpviewer_keywords:
- managed code analysis rules, naming rules
- naming rules
- rules, naming
author: gewarren
ms.author: gewarren
ms.openlocfilehash: 57524fbff364fd03a90b90a0900bd17e9c8a9248
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99732313"
---
# <a name="naming-rules"></a>Regras de nomenclatura

As regras de nomenclatura dão suporte à adesão às [convenções de nomenclatura das diretrizes de design do .net](../../../standard/design-guidelines/naming-guidelines.md).

## <a name="in-this-section"></a>Nesta seção

|Regra|Descrição|
|----------|-----------------|
|[CA1700: Não nomear valores de enumeração 'Reserved'](ca1700.md)|Esta regra pressupõe que um membro da enumeração que tenha um nome que contém "reserved" não é usado atualmente, mas é um espaço reservado a ser renomeado ou removido em uma versão futura. Renomear ou remover um membro é uma alteração drástica.|
|[CA1707: Identificadores não devem conter sublinhados](ca1707.md)|Por convenção, os nomes de identificador não contêm o caractere de sublinhado (_). Esta regra verifica namespaces, tipos, membros e parâmetros.|
|[CA1708: Identificadores devem ser diferentes em algo além das maiúsculas e minúsculas](ca1708.md)|Os identificadores de namespaces, tipos, membros e parâmetros não podem se diferenciar apenas por maiúsculas porque linguagens com o Common Language Runtime como destino não precisam diferenciar maiúsculas e minúsculas.|
|[CA1710: Identificadores devem ter um sufixo correto](ca1710.md)|Por convenção, os nomes de tipos que estendem determinados tipos de base ou que implementam determinadas interfaces, ou tipos derivados desses tipos, têm um sufixo associado ao tipo ou interface base.|
|[CA1711: Identificadores não devem ter um sufixo incorreto](ca1711.md)|Por convenção, apenas os nomes de tipos que estendem determinados tipos de base ou que implementam determinadas interfaces, ou tipos derivados desses tipos, devem terminar com sufixos reservados específicos. Outros nomes de tipo não devem usar esses sufixos reservados.|
|[CA1712: Não prefixar valores de enumeração com um nome de tipo](ca1712.md)|Os nomes dos membros de enumeração não são prefixados com o nome do tipo porque as informações de tipo devem ser fornecidas pelas ferramentas de desenvolvimento.|
|[CA1713: Eventos não devem ter o prefixo anterior ou posterior](ca1713.md)|O nome de um evento começa com "Before" ou "After". Para nomear eventos relacionados acionados em uma sequência específica, use o presente ou o pretérito para indicar a posição relativa na sequência de ações.|
|[CA1714: Enumerações de sinalizador devem ter nomes no plural](ca1714.md)|Uma enumeração pública tem o atributo System. FlagsAttribute e seu nome não termina em "s". Os tipos marcados com FlagsAttribute têm nomes que são plural porque o atributo indica que mais de um valor pode ser especificado.|
|[CA1715: Identificadores devem ter um prefixo correto](ca1715.md)|O nome de uma interface visível externamente não começa com um "I" maiúsculo.  O nome de um parâmetro de tipo genérico em um tipo ou método visível externamente não começa com um "T" maiúsculo.|
|[CA1716: Identificadores não devem corresponder a palavras-chave](ca1716.md)|Um nome de namespace ou um nome de tipo corresponde a uma palavra-chave reservada em uma linguagem de programação. Os identificadores de namespaces e tipos não devem corresponder a palavras-chave definidas por com o Common Language Runtime como destino.|
|[CA1717: Apenas enumerações FlagsAttribute devem ter nomes no plural](ca1717.md)|As convenções de nomenclatura determinam que um nome no plural para uma enumeração indica que mais de um valor de enumeração pode ser especificado ao mesmo tempo.|
|[CA1720: Identificadores não devem conter nomes de tipos](ca1720.md)|O nome de um parâmetro em um membro visível externamente contém um nome de tipo de dados, ou o nome de um membro visível externamente contém um nome de tipo de dados específico da linguagem.|
|[CA1721: Nomes de propriedades não devem corresponder a métodos get](ca1721.md)|O nome de um membro público ou protegido começa com "Get" e, de outra forma, corresponde ao nome de uma propriedade pública ou protegida. Métodos "Get" e propriedades devem ter nomes que diferenciem claramente a função.|
|[CA1724: Nomes de tipos não devem corresponder a namespaces](ca1724.md)|Os nomes de tipo não devem corresponder aos nomes dos namespaces do .NET. A violação dessa regra pode reduzir a usabilidade da biblioteca.|
|[CA1725: Nomes de parâmetros devem corresponder à declaração base](ca1725.md)|A nomenclatura consistente dos parâmetros em uma hierarquia de substituição aumenta a usabilidade das substituições de método. Um nome de parâmetro em um método derivado diferente do nome na declaração de base pode causar confusão em relação à possibilidade do método ser uma substituição do método de base ou de uma nova sobrecarga do método.|
