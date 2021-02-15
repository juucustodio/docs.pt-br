---
title: 'Alteração significativa: algumas APIs lançam ArgumentNullException'
description: Saiba mais sobre a alteração significativa no .NET 6,0 em que algumas APIs validam argumentos e agora lançam um ArgumentNullException.
ms.date: 01/29/2021
ms.openlocfilehash: f9d7dc8bb57ed8dc5b4ff41bda9b3bde7db7b880
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99804159"
---
# <a name="some-apis-throw-argumentnullexception"></a>Algumas APIs geram ArgumentNullException

Algumas APIs agora validam os parâmetros de entrada e lançam um <xref:System.ArgumentNullException> onde anteriormente eles lançaram um <xref:System.NullReferenceException> , se invocados com `null` argumentos de entrada.

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, as APIs afetadas lançam um <xref:System.NullReferenceException> se invocado com um argumento que é `null` .

A partir do .NET 6,0, as APIs afetadas lançam um <xref:System.ArgumentNullException> se invocado com um argumento que é `null` .

## <a name="reason-for-change"></a>Motivo da alteração

O lançamento <xref:System.ArgumentNullException> está em conformidade com o comportamento do tempo de execução do .net. Ele fornece uma experiência de depuração melhor, comunicando claramente qual argumento causou a exceção.

## <a name="version-introduced"></a>Versão introduzida

.NET 6.0

## <a name="recommended-action"></a>Ação recomendada

- Examine e, se necessário, atualize seu código para evitar passar `null` argumentos de entrada para as APIs afetadas.
- Se seu código processar <xref:System.NullReferenceException> , substitua ou adicione um manipulador adicional para <xref:System.ArgumentNullException> .

## <a name="affected-apis"></a>APIs afetadas

A tabela a seguir lista as propriedades afetadas:

| Propriedade | Versão alterada |
|-|-|-|-|
| <xref:System.Windows.Forms.TreeNodeCollection.Item(System.Int32)?displayProperty=fullName> | Preview 1 |

<!--

### Affected APIs

- `P:System.Windows.Forms.TreeNodeCollection.Item(System.Int32)`

### Category

Windows Forms

-->
