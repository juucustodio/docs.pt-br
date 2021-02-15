---
title: 'Alteração significativa: Cryptography. OID é funcionalmente somente init'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que os setters de propriedade na classe Cryptography. Oid agora lançam uma exceção se você tentar alterar um valor.
ms.date: 08/16/2020
ms.openlocfilehash: a3b5a393e2a84f7c9a60c2a821ecfda9c6acd2e3
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760336"
---
# <a name="systemsecuritycryptographyoid-is-functionally-init-only"></a>System. Security. Cryptography. OID é funcionalmente somente init

A <xref:System.Security.Cryptography.Oid?displayProperty=fullName> classe, que é usada para representar valores de identificador de objeto ASN. 1 e seus nomes "amigáveis", anteriormente era totalmente mutável. Essa imutabilidade costuma ser despercebida ou surgiu como uma surpresa. Os setters de propriedade agora lançam um <xref:System.PlatformNotSupportedException> quando você tenta alterar o valor depois que ele já foi atribuído.

## <a name="change-description"></a>Descrição das alterações

Em versões anteriores, os setters de propriedade em <xref:System.Security.Cryptography.Oid> podem ser usados para alterar o valor das <xref:System.Security.Cryptography.Oid.FriendlyName> <xref:System.Security.Cryptography.Oid.Value> Propriedades e.

No .NET 5,0 e versões posteriores, os setters de propriedade só podem ser usados para inicializar o valor. Depois que a propriedade tiver um valor, de um construtor ou de uma chamada anterior para o setter de propriedade, o setter da propriedade sempre lançará um <xref:System.PlatformNotSupportedException> .

## <a name="reason-for-change"></a>Motivo da alteração

Essa alteração permite a reutilização de <xref:System.Security.Cryptography.Oid> objetos como parte dos valores de retorno em APIs públicas para reduzir os perfis de alocação de objetos. Ele evita a necessidade de criar cópias "defensivas" temporárias quando <xref:System.Security.Cryptography.Oid> os valores são usados como entradas.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Evite usar os <xref:System.Security.Cryptography.Oid> setters de propriedade diferentes de para a inicialização do objeto. Para representar um novo valor, use uma nova instância em vez de alterar o valor em um objeto existente.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Security.Cryptography.Oid.FriendlyName?displayProperty=fullName>
- <xref:System.Security.Cryptography.Oid.Value?displayProperty=fullName>

<!--

### Affected APIs

- `P:System.Security.Cryptography.Oid.FriendlyName`
- `P:System.Security.Cryptography.Oid.Value`

### Category

Cryptography

-->
