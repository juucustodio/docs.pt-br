---
description: 'Saiba mais sobre: funções estáticas globais do Fusion'
title: Funções estáticas globais de fusão
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged global static functions [.NET Framework], fusion
- fusion global static functions [.NET Framework]
- global static functions [.NET Framework fusion]
ms.assetid: 229b2188-9168-4b44-a987-e1f515494688
ms.openlocfilehash: c696908f72d67ecff5e7383e7a2754dd5436b819
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99761077"
---
# <a name="fusion-global-static-functions"></a>Funções estáticas globais de fusão

Esta seção descreve as funções estáticas globais não gerenciadas que a API do Fusion usa.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Função ClearDownloadCache](cleardownloadcache-function.md)  
 Limpa o cache de assembly global de assemblies baixados.  
  
 [Função CompareAssemblyIdentity](compareassemblyidentity-function.md)  
 Compara duas identidades de assembly para determinar se elas são equivalentes.  
  
 [Função CreateApplicationContext](createapplicationcontext-function.md)  
 Somente interno. (Essa função dá suporte à infraestrutura de .NET Framework e não se destina a ser usada diretamente do seu código.)  
  
 [Função CreateAssemblyCache](createassemblycache-function.md)  
 Obtém um ponteiro para uma nova instância [IAssemblyCache](iassemblycache-interface.md) que representa o cache de assembly global.  
  
 [Função CreateAssemblyEnum](createassemblyenum-function.md)  
 Obtém um ponteiro para uma instância de [IAssemblyEnum](iassemblyenum-interface.md) que representa uma lista de objetos que existem no assembly especificado.  
  
 [Função CreateAssemblyNameObject](createassemblynameobject-function.md)  
 Obtém um ponteiro para uma instância de [IAssemblyName](iassemblyname-interface.md) que representa a identidade exclusiva do assembly com o nome especificado.  
  
 [Função CreateHistoryReader](createhistoryreader-function.md)  
 Cria um leitor de histórico para o arquivo especificado.  
  
 [Função CreateInstallReferenceEnum](createinstallreferenceenum-function.md)  
 Obtém um ponteiro para uma instância de [IInstallReferenceEnum](iinstallreferenceenum-interface.md) que representa uma lista de referências de um aplicativo para o assembly especificado.  
  
 [Função GetAppIdAuthority](getappidauthority-function.md)  
 Obtém um ponteiro para uma instância de [IAppIdAuthority](iappidauthority-interface.md) que gerencia chaves para identidades e referências de aplicativo.  
  
 [Função GetAssemblyIdentityFromFile](getassemblyidentityfromfile-function.md)  
 Obtém um ponteiro para um `IUnknown` objeto com o especificado `IID` no assembly no caminho do arquivo especificado.  
  
 [Função GetCachePath](getcachepath-function.md)  
 Obtém o caminho para o assembly armazenado em cache, usando os sinalizadores especificados.  
  
 [Função GetHistoryFileDirectory](gethistoryfiledirectory-function.md)  
 Recupera o caminho do diretório de histórico do aplicativo.  
  
 [Função GetIdentityAuthority](getidentityauthority-function.md)  
 Obtém um ponteiro para uma instância de [IIdentityAuthority](iidentityauthority-interface.md) que gerencia chaves para objetos de código.  
  
 [Função IsFrameworkAssembly](isframeworkassembly-function.md)  
 Obtém um valor que indica se o assembly especificado é gerenciado.  
  
 [Função NukeDownloadedCache](nukedownloadedcache-function.md)  
 Exclui o cache de download do Common Language Runtime.  
  
 [Função PreBindAssemblyEx](prebindassemblyex-function.md)  
 Obtém o nome de exibição de pós-política para um assembly.  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Interfaces de fusão](fusion-interfaces.md)  
  
 [Enumerações Fusion](fusion-enumerations.md)  
  
 [Estruturas de fusão](fusion-structures.md)  
  
 [Cache de assemblies global](../../app-domains/gac.md)
