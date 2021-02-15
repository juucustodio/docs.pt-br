---
ms.openlocfilehash: 53840ddd59ae3463bae2930fd0151ab2cd2d65cb
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593313"
---
### <a name="design-time-builds-only-return-top-level-package-references"></a>As compilações de tempo de design retornam apenas referências de pacote de nível superior

A partir do SDK do .NET Core 3.1.400, somente referências de pacote de nível superior são retornadas pelo `RunResolvePackageDependencies` destino.

#### <a name="version-introduced"></a>Versão introduzida

SDK do .NET Core 3.1.400

#### <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do SDK do .NET Core, o `RunResolvePackageDependencies` destino criou os seguintes itens do MSBuild que continham informações do arquivo de ativos do NuGet:

- `PackageDefinitions`
- `PackageDependencies`
- `TargetDefinitions`
- `FileDefinitions`
- `FileDependencies`

Esses dados são usados pelo Visual Studio para preencher o nó de dependências no Gerenciador de Soluções. No entanto, ele pode ser uma grande quantidade de dados, e os dados não são necessários, a menos que o nó de dependências seja expandido.

A partir do SDK do .NET Core versão 3.1.400, a maioria desses itens não é gerada por padrão. Somente os itens do tipo `Package` são retornados. Se o Visual Studio precisar que os itens preencham o nó de dependências, ele lerá as informações diretamente do arquivo de ativos.

#### <a name="reason-for-change"></a>Motivo da alteração

Essa mudança foi introduzida para melhorar o desempenho da carga de solução dentro do Visual Studio. Anteriormente, todas as referências de pacote seriam carregadas, o que envolveva o carregamento de muitas referências que a maioria dos usuários nunca exibiria.

#### <a name="recommended-action"></a>Ação recomendada

Se você tiver a lógica do MSBuild que depende desses itens sendo criados, defina a `EmitLegacyAssetsFileItems` propriedade como `true` em seu arquivo de projeto. Essa configuração habilita o comportamento anterior em que todos os itens são criados.

#### <a name="category"></a>Categoria

MSBuild

#### <a name="affected-apis"></a>APIs afetadas

N/D
