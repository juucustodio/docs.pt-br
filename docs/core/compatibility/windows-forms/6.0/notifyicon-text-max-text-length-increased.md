---
title: 'Alteração significativa: NotifyIcon. texto tamanho máximo do texto aumentado'
description: Saiba mais sobre a alteração significativa no .NET 6,0 em que o tamanho máximo de texto para a Propriedade NotifyIcon. Text aumentou.
ms.date: 01/19/2021
ms.openlocfilehash: 0029556f3ec2795fb079575b329e7fbd187d486f
ms.sourcegitcommit: 632818f4b527e5bf3c48fc04e0c7f3b4bdb8a248
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98617986"
---
# <a name="notifyicontext-maximum-text-length-increased"></a>NotifyIcon. texto tamanho máximo do texto aumentado

O comprimento de texto máximo permitido para a <xref:System.Windows.Forms.NotifyIcon.Text?displayProperty=nameWithType> Propriedade aumentou de 63 para 127.

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, o tamanho máximo de texto permitido para a <xref:System.Windows.Forms.NotifyIcon.Text?displayProperty=nameWithType> propriedade é de 63 caracteres. A partir do .NET 6,0, o comprimento máximo de texto permitido é de 127 caracteres. Em qualquer versão, um <xref:System.ArgumentException> é gerado quando você tenta definir um valor que seja maior que o limite.

## <a name="reason-for-change"></a>Motivo da alteração

O tamanho máximo de texto permitido foi aumentado para estar em linha com a [API subjacente do Windows](/windows/win32/api/shellapi/ns-shellapi-notifyicondataw#nif_showtip-0x00000080). A API do Windows foi atualizada no Windows 2000, mas devido a motivos de compatibilidade, o limite de tamanho para essa propriedade não foi atualizado no .NET Framework.

## <a name="version-introduced"></a>Versão introduzida

.NET 6,0 Preview 1

## <a name="recommended-action"></a>Ação recomendada

Examine seu código e relaxe quaisquer condições de proteção existentes, se necessário.

## <a name="affected-apis"></a>APIs afetadas

<xref:System.Windows.Forms.NotifyIcon.Text?displayProperty=fullName>

<!--

### Affected APIs

- `P:System.Windows.Forms.NotifyIcon.Text`

### Category

Windows Forms

-->
