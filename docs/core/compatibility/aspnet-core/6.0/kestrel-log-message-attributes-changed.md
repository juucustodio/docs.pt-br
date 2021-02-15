---
title: 'Alteração significativa: Kestrel: atributos de mensagem de log alterados'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core 6,0 intitulado Kestrel: atributos de mensagem de log alterados'
author: scottaddie
ms.author: scaddie
ms.date: 02/01/2021
ms.openlocfilehash: 30b03c22a6c85623fec7db14b58b169f887395a0
ms.sourcegitcommit: 4df8e005c074ceb1f978f007b222fe253be2baf3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/04/2021
ms.locfileid: "99551552"
---
# <a name="kestrel-log-message-attributes-changed"></a>Kestrel: atributos de mensagem de log alterados

As mensagens de log do Kestrel têm IDs e nomes associados. Esses atributos identificam exclusivamente tipos diferentes de mensagens de log. Alguns desses identificadores e nomes foram duplicados incorretamente. Esse problema de duplicação é corrigido no ASP.NET Core 6,0.

## <a name="version-introduced"></a>Versão introduzida

6.0

## <a name="old-behavior"></a>Comportamento antigo

A tabela a seguir mostra o estado das mensagens de log afetadas antes de ASP.NET Core 6,0.

| Descrição da mensagem                   | Nome                    | ID |
|---------------------------------------|-------------------------|----|
| Mensagens de log fechadas de conexão HTTP/2 | `Http2ConnectionClosed` | 36 |
| Quadro HTTP/2 enviando mensagens de log     | `Http2FrameReceived`    | 37 |

## <a name="new-behavior"></a>Novo comportamento

A tabela a seguir mostra o estado das mensagens de log afetadas no ASP.NET Core 6,0.

| Descrição da mensagem                   | Nome                    | ID |
|---------------------------------------|-------------------------|----|
| Mensagens de log fechadas de conexão HTTP/2 | `Http2ConnectionClosed` | 48 |
| Quadro HTTP/2 enviando mensagens de log     | `Http2FrameSending`     | 49 |

## <a name="reason-for-change"></a>Motivo da alteração

Os nomes e IDs de log devem ser exclusivos para que tipos de mensagem diferentes possam ser identificados.

## <a name="recommended-action"></a>Ação recomendada

Se você tiver código ou configuração que faça referência a IDs e nomes antigos, atualize essas referências para usar os novos IDs e nomes.

<!--

## Category

ASP.NET Core

## Affected APIs

Not detectable via API analysis

-->
