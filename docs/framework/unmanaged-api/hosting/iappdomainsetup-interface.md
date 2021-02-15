---
description: 'Saiba mais sobre: interface IAppDomainSetup'
title: Interface IAppDomainSetup
ms.date: 03/30/2017
api_name:
- IAppDomainSetup
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IAppDomainSetup
helpviewer_keywords:
- IAppDomainSetup interface [.NET Framework hosting]
ms.assetid: 1844da85-c031-40bf-bea4-1a3d12a36c8c
topic_type:
- apiref
ms.openlocfilehash: 8fd224308ea68f7b56ae174c7f71fc4f89630101
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99760578"
---
# <a name="iappdomainsetup-interface"></a>Interface IAppDomainSetup

Fornece propriedades que permitem ao host configurar um <xref:System.AppDomain?displayProperty=nameWithType> tipo antes de chamar o método [ICorRuntimeHost:: CreateDomainEx](icorruntimehost-createdomainex-method.md) para criá-lo.  
  
## <a name="properties"></a>Propriedades  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|<xref:System.AppDomainSetup.ApplicationBase%2A>|Obtém ou define o nome do diretório que contém o aplicativo.|  
|<xref:System.AppDomainSetup.ApplicationName%2A>|Obtém ou define o nome do aplicativo.|  
|<xref:System.AppDomainSetup.CachePath%2A>|Obtém ou define o nome de uma área específica para o aplicativo em que os arquivos são copiados por sombra.|  
|<xref:System.AppDomainSetup.ConfigurationFile%2A>|Obtém ou define o nome do arquivo de configuração para um aplicativo.|  
|<xref:System.AppDomainSetup.DynamicBase%2A>|Obtém ou define o nome do diretório onde os arquivos gerados dinamicamente são armazenados e acessados.|  
|<xref:System.AppDomainSetup.LicenseFile%2A>|Obtém ou define o caminho para o arquivo de licença que está associado a esse domínio.|  
|<xref:System.AppDomainSetup.PrivateBinPath%2A>|Obtém ou define a lista de diretórios combinados com o <xref:System.AppDomainSetup.ApplicationBase%2A> diretório para investigação de assemblies privados.|  
|<xref:System.AppDomainSetup.PrivateBinPathProbe%2A>|Obtém ou define um valor de cadeia de caracteres que inclui ou exclui <xref:System.AppDomainSetup.ApplicationBase%2A> do caminho de pesquisa para o aplicativo.|  
|<xref:System.AppDomainSetup.ShadowCopyDirectories%2A>|Obtém ou define os nomes dos diretórios que contêm assemblies a serem copiados por sombra.|  
|<xref:System.AppDomainSetup.ShadowCopyFiles%2A>|Obtém ou define uma cadeia de caracteres que indica se a cópia de sombra está ativada ou desativada. Os valores válidos são "true" ou "false".|  
  
## <a name="remarks"></a>Comentários  

 A `IAppDomainSetup` interface corresponde à interface gerenciada <xref:System.IAppDomainSetup> , que o <xref:System.AppDomainSetup> tipo implementa. Consulte <xref:System.IAppDomainSetup?displayProperty=nameWithType> para obter descrições detalhadas de suas propriedades.  
  
 `IAppDomainSetup` representa informações de associação de assembly que podem ser adicionadas a uma <xref:System.AppDomain> instância antes da sua criação. Por exemplo, um host pode definir a <xref:System.AppDomainSetup.ApplicationBase%2A> propriedade para estabelecer um diretório raiz, que o Common Language Runtime (CLR) testa para assemblies gerenciados.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.AppDomain>
- <xref:System.AppDomainSetup>
- <xref:System.IAppDomainSetup>
- [Interfaces de hospedagem](hosting-interfaces.md)
