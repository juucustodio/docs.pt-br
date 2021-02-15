---
title: 'Alteração significativa: algumas propriedades TableLayoutSettings lançam InvalidEnumArgumentException'
description: Saiba mais sobre a alteração significativa no .NET 6,0 em que algumas APIs TableLayoutSettings agora lançam um InvalidEnumArgumentException para argumentos inválidos.
ms.date: 01/18/2021
ms.openlocfilehash: 8397952e4647347718f11597a100c5d764e7186b
ms.sourcegitcommit: f8cd3ef517ee177c99feed944824c27d208cc0d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2021
ms.locfileid: "98570261"
---
# <a name="selected-tablelayoutsettings-properties-throw-invalidenumargumentexception"></a>As propriedades TableLayoutSettings selecionadas lançam InvalidEnumArgumentException

<xref:System.Windows.Forms.TableLayoutSettings>As propriedades selecionadas agora lançam um <xref:System.ComponentModel.InvalidEnumArgumentException> se você tentar atribuir um valor incorreto.

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, essas propriedades lançam um <xref:System.ArgumentOutOfRangeException> se você tentar atribuir um valor incorreto. A partir do .NET 6,0, essas propriedades lançam um <xref:System.ComponentModel.InvalidEnumArgumentException> nesses casos.

## <a name="reason-for-change"></a>Motivo da alteração

<xref:System.ComponentModel.InvalidEnumArgumentException>O lançamento está em linha com a API de Windows Forms existente em situações semelhantes. Lançar essa exceção também fornece aos desenvolvedores uma melhor experiência de depuração.

## <a name="version-introduced"></a>Versão introduzida

.NET 6,0

## <a name="recommended-action"></a>Ação recomendada

- Atualize o código para impedir a atribuição de valores incorretos.
- Se necessário, manipule um <xref:System.ComponentModel.InvalidEnumArgumentException> ao acessar essas APIs.

## <a name="affected-apis"></a>APIs afetadas

A tabela a seguir lista as propriedades afetadas:

| Propriedade | Versão alterada |
|-|-|-|-|
| <xref:System.Windows.Forms.TableLayoutPanel.CellBorderStyle?displayProperty=fullName> | Preview 1 |
| <xref:System.Windows.Forms.TableLayoutPanel.GrowStyle?displayProperty=fullName> | Preview 1 |

<!--

### Affected APIs

- `P:System.Windows.Forms.TableLayoutPanel.CellBorderStyle`
- `P:System.Windows.Forms.TableLayoutPanel.GrowStyle`

### Category

Windows Forms

-->
