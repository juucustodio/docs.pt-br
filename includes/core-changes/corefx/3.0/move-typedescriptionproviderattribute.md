---
ms.openlocfilehash: 7a2617f27dfd6bb527ff6d408fae6382075f24ae
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96031964"
---
### <a name="typedescriptionproviderattribute-moved-to-another-assembly"></a>TypeDescriptionProviderAttribute movido para outro assembly

A <xref:System.ComponentModel.TypeDescriptionProviderAttribute> classe foi movida.

#### <a name="change-description"></a>Descrição das alterações

No .NET Core 2,2 e versões anteriores, a <xref:System.ComponentModel.TypeDescriptionProviderAttribute> classe é encontrada no assembly *System. ComponentModel. TypeConverter* .

A partir do .NET Core 3,0, ele é encontrado no assembly *System. ObjectModel* .

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="recommended-action"></a>Ação recomendada

Essa alteração afeta apenas os aplicativos que usam a reflexão para carregar o <xref:System.ComponentModel.TypeDescriptionProviderAttribute> tipo chamando um método como <xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType> ou uma sobrecarga de <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType> que assume que o tipo está em um assembly específico. Se esse for o caso, o assembly referenciado na chamada do método deverá ser atualizado para refletir o novo local do assembly do tipo.

#### <a name="category"></a>Categoria

Windows Forms

#### <a name="affected-apis"></a>APIs afetadas

Nenhum.

<!--

#### Affected APIs

- Not detectable via API analysis

-->
