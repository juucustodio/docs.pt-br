---
title: 'Como: obter informações sobre tipo e membro usando reflexo'
description: Saiba como obter informações de tipo e membro com reflexão, usando o namespace System. Reflection.
ms.date: 09/03/2019
helpviewer_keywords:
- reflection, obtaining member information
- types [.NET Framework], obtaining member information from
ms.assetid: 348ae651-ccda-4f13-8eda-19e8337e9438
dev_langs:
- cpp
- csharp
- vb
ms.openlocfilehash: 771917bb2ae5cae56c775ae23119d5eda9701df1
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266318"
---
# <a name="how-to-get-type-and-member-information-by-using-reflection"></a>Como: obter informações sobre tipo e membro usando reflexo

O <xref:System.Reflection> namespace contém muitos métodos para obter informações sobre tipos e seus membros. Este artigo demonstra um desses métodos, <xref:System.Type.GetMembers%2A?displayProperty=nameWithType> . Para obter informações adicionais, consulte [visão geral de reflexão](reflection.md).
  
## <a name="example"></a>Exemplo

O exemplo a seguir obtém informações de tipo e membro usando reflexão:

[!code-cpp[Get type members](../../../samples/snippets/standard/reflection/memberinfo/gettypemembers.cpp)]
[!code-csharp[Get type members](../../../samples/snippets/standard/reflection/memberinfo/gettypemembers.cs)]
[!code-vb[Get type members](../../../samples/snippets/standard/reflection/memberinfo/gettypemembers.vb)]

## <a name="see-also"></a>Veja também

- [Programa com domínios de aplicativo](../app-domains/application-domains.md#programming-with-application-domains)
- [Reflexão](reflection.md)
- [Usar domínios de aplicativo](../app-domains/use.md)
