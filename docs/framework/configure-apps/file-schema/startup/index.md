---
description: 'Saiba mais sobre: esquema de configurações de inicialização'
title: Esquema de configurações de inicialização
ms.date: 03/30/2017
helpviewer_keywords:
- startup settings schema
- schema startup settings
- configuration schema [.NET Framework], startup settings
ms.assetid: 03de6972-442a-4648-9f3e-efa654e3b949
ms.openlocfilehash: 268b8d8dc2598add61435dd6b07031aa06831737
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99726085"
---
# <a name="startup-settings-schema"></a>Esquema de configurações de inicialização

As configurações de inicialização especificam a versão do Common Language Runtime que deve executar o aplicativo.  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<requiredRuntime>](requiredruntime-element.md)|Especifica que o aplicativo dá suporte apenas à versão 1.0 do Common Language Runtime. Os aplicativos criados com a versão de tempo de execução 1,1 devem usar o **\<supportedRuntime>** elemento.|  
|[\<supportedRuntime>](supportedruntime-element.md)|Especifica a quais versões do Common Language Runtime o aplicativo oferece suporte.|  
|[\<startup>](startup-element.md)|Contém os **\<requiredRuntime>** **\<supportedRuntime>** elementos e.|  
  
## <a name="see-also"></a>Consulte também

- [Esquema do arquivo de configuração](../index.md)
- [Como configurar um aplicativo para dar suporte a .NET Framework 4 ou versões posteriores](../../../migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)
