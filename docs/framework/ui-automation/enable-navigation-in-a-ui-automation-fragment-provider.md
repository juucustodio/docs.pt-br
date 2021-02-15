---
title: Permitir navegação em um fragmento por um provedor de automação de interface do usuário
description: Leia um exemplo que mostra como habilitar a navegação em um provedor de automação de interface do usuário para um elemento que está dentro de um fragmento.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- UI Automation, enabling navigation in provider
- navigation, enabling in UI Automation provider
ms.assetid: 3cb6092a-58c9-4ca0-84a5-0e54d5d00a0d
ms.openlocfilehash: d8fb67a84b7cba84fe65cd2f87baa6549122d2a2
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96276497"
---
# <a name="enable-navigation-in-a-ui-automation-fragment-provider"></a>Permitir navegação em um fragmento por um provedor de automação de interface do usuário

> [!NOTE]
> Esta documentação destina-se a desenvolvedores do .NET Framework que querem usar as classes da [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gerenciadas definidas no namespace <xref:System.Windows.Automation>. Para obter as informações mais recentes sobre a [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: UI Automation](/windows/win32/winauto/entry-uiauto-win32) (API de Automação do Windows: Automação da Interface do Usuário).  
  
 Este tópico contém um código de exemplo que mostra como habilitar a navegação em um provedor de automação de interface do usuário para um elemento que está dentro de um fragmento.  
  
## <a name="example"></a>Exemplo  

 O código de exemplo a seguir implementa <xref:System.Windows.Automation.Provider.IRawElementProviderFragment.Navigate%2A> para um item de lista em uma lista. O elemento pai é o elemento da caixa de listagem e os elementos irmãos são outros itens na coleção de listas. O método retorna `null` ( `Nothing` em Visual Basic) para direções que não são válidas; nesse caso, <xref:System.Windows.Automation.Provider.NavigateDirection.FirstChild> e <xref:System.Windows.Automation.Provider.NavigateDirection.LastChild> , porque o elemento não tem filhos.  
  
 [!code-csharp[UIAFragmentProvider_snip#103](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListItemFragment.cs#103)]
 [!code-vb[UIAFragmentProvider_snip#103](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListItemFragment.vb#103)]  
  
## <a name="see-also"></a>Veja também

- [Visão Geral dos Provedores de Automação de Interface do Usuário](ui-automation-providers-overview.md)
- [Implementação do provedor de automação de interface do usuário no lado do servidor](server-side-ui-automation-provider-implementation.md)
