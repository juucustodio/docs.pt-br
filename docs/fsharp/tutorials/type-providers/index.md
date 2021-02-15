---
title: Provedores de tipos
description: 'Saiba como um provedor de tipo F # é um componente que fornece tipos, propriedades e métodos para uso em seus programas.'
ms.date: 04/02/2018
ms.openlocfilehash: f01e207407b2282005d5722bed798df1d49d3ef6
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100468220"
---
# <a name="type-providers"></a>Provedores de tipos

Um provedor de tipos F# é um componente que fornece tipos, propriedades e métodos para uso em seu programa. Os provedores de tipos geram o que são conhecidos como **tipos fornecidos**, que são gerados pelo compilador F # e são baseados em uma fonte de dados externa.

Por exemplo, um provedor de tipo F # para SQL pode gerar tipos que representam tabelas e colunas em um banco de dados relacional. Na verdade, é isso que o provedor de tipo [Sqlfornecetor](https://fsprojects.github.io/SQLProvider/) faz.

Os tipos fornecidos dependem de parâmetros de entrada para um provedor de tipo. Essa entrada pode ser uma fonte de dados de exemplo (como um arquivo de esquema JSON), uma URL que aponta diretamente para um serviço externo ou uma cadeia de conexão para uma fonte de dados. Um provedor de tipos também pode garantir que os grupos de tipos sejam expandidos apenas sob demanda; ou seja, eles serão expandidos se os tipos forem realmente referenciados por seu programa. Isso permite a integração direta e sob demanda de espaços de informações em grande escala como mercados de dados online de uma forma fortemente tipada.

## <a name="generative-and-erased-type-providers"></a>Geração e provedores de tipo apagados

Os provedores de tipos são fornecidos em duas formas: geração e Erase.

Os provedores de tipo geração produzem tipos que podem ser gravados como tipos .NET no assembly no qual são produzidos. Isso permite que eles sejam consumidos do código em outros assemblies. Isso significa que a representação tipada da fonte de dados deve ser geralmente uma que seja viável para representar com tipos .NET.

Apagar provedores de tipo produz tipos que só podem ser consumidos no assembly ou projeto do qual são gerados. Os tipos são efêmeros; ou seja, eles não são gravados em um assembly e não podem ser consumidos pelo código em outros assemblies. Eles podem conter membros *atrasados* , permitindo que você use tipos fornecidos de um espaço de informações potencialmente infinito. Eles são úteis para usar um pequeno subconjunto de uma fonte de dados grande e interconectada.

## <a name="commonly-used-type-providers"></a>Provedores de tipo comumente usados

As seguintes bibliotecas amplamente usadas contêm provedores de tipos para usos diferentes:

- O FSharp. Data inclui provedores de tipos para formatos de documentos JSON, XML, CSV e HTML.
- O [Sqlfornecetor](https://fsprojects.github.io/SQLProvider/) fornece acesso com rigidez de tipos para bancos de dados de relação por meio de mapeamento de objeto e consultas de F # LINQ nessas fontes.
- O [FSharp. Data. SqlClient](https://fsprojects.github.io/FSharp.Data.SqlClient/) tem um conjunto de provedores de tipos para inserção verificada em tempo de compilação de T-SQL em F #.
- O [provedor de tipos de armazenamento do Azure](https://fsprojects.github.io/AzureStorageTypeProvider/) fornece tipos para BLOBs, tabelas e filas do Azure, permitindo que você acesse esses recursos sem a necessidade de especificar nomes de recursos como cadeias de caracteres em todo o programa.
- [FSharp. Data. GraphQL](https://fsprojects.github.io/FSharp.Data.GraphQL/index.html) contém o **GraphQLProvider**, que fornece tipos com base em um servidor GraphQL especificado pela URL.

Quando necessário, você pode [criar seus próprios provedores de tipo personalizados](creating-a-type-provider.md)ou provedores de tipo de referência que foram criados por outras pessoas. Por exemplo, suponha que sua organização tenha um serviço de dados que forneça um grande e crescente número de conjuntos de dados nomeados, cada um com seu próprio esquema de dados estáveis. Você pode optar por criar um provedor de tipos que leia os esquemas e apresente os conjuntos de dados mais recentes disponíveis para o programador de uma forma fortemente tipada.

## <a name="see-also"></a>Consulte também

- [Tutorial: criar um provedor de tipos](creating-a-type-provider.md)
- [Referência de linguagem F #](../../language-reference/index.md)
