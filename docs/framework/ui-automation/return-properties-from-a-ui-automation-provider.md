---
title: Retornando Propriedades de um Provedor de Automação de IU
description: Veja como um provedor de automação de interface do usuário pode retornar propriedades de um elemento para aplicativos cliente no .NET.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- providers, UI Automation, returning properties
- properties, returned by UI Automation providers
- UI Automation, providers returning properties
ms.assetid: 5eba950e-b9e1-48eb-ab8e-b69db76bf589
ms.openlocfilehash: 8269d7d04a67c2a89a28160c0a8bc82bd627749f
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96250470"
---
# <a name="return-properties-from-a-ui-automation-provider"></a>Retornando Propriedades de um Provedor de Automação de IU

> [!NOTE]
> Esta documentação destina-se a desenvolvedores do .NET Framework que querem usar as classes da [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gerenciadas definidas no namespace <xref:System.Windows.Automation>. Para obter as informações mais recentes sobre a [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: UI Automation](/windows/win32/winauto/entry-uiauto-win32) (API de Automação do Windows: Automação da Interface do Usuário).  
  
 Este tópico contém um código de exemplo que mostra como um provedor de automação de interface do usuário pode retornar propriedades de um elemento para aplicativos cliente.  
  
 Para qualquer propriedade para a qual não há suporte explícito, o provedor deve retornar `null` ( `Nothing` em Visual Basic). Isso garante que [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] as tentativas de obter a propriedade de outra fonte, como o provedor de janela do host.  
  
## <a name="example"></a>Exemplo  

 [!code-csharp[UIAFragmentProvider_snip#117](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListFragment.cs#117)]
 [!code-vb[UIAFragmentProvider_snip#117](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListFragment.vb#117)]  
  
## <a name="see-also"></a>Consulte também

- [Visão Geral dos Provedores de Automação de Interface do Usuário](ui-automation-providers-overview.md)
- [Implementação do provedor de automação de interface do usuário no lado do servidor](server-side-ui-automation-provider-implementation.md)
