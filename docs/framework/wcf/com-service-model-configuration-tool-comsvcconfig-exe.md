---
description: 'Saiba mais sobre: ferramenta de configuração do modelo de serviço COM+ (ComSvcConfig.exe)'
title: Ferramenta de configuração de modelo de serviço COM+ (ComSvcConfig.exe)
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation, COM+ integration
- WCF, COM+ integration
ms.assetid: 7717c6c2-85fc-418b-a8ed-bad8e61cec5c
ms.openlocfilehash: 81bfcbd468cb5401646a49967b6381b48e2f7cf0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99781058"
---
# <a name="com-service-model-configuration-tool-comsvcconfigexe"></a>Ferramenta de configuração de modelo de serviço COM+ (ComSvcConfig.exe)

A ferramenta de linha de comando de configuração do modelo de serviço COM+ (ComSvcConfig.exe) permite que você configure as interfaces COM+ para serem expostas como serviços Web.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
ComSvcConfig.exe /install | /uninstall | /list [/application:<ApplicationID | ApplicationName>] [/contract:<ClassID | ProgID | *,InterfaceID | InterfaceName | *>] [/hosting:<complus | was>] [/webSite:<WebsiteName>] [/webDirectory:<WebDirectoryName>] [/mex] [/id] [/nologo] [/verbose] [/help] [/partial]  
```  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> Você deve ser um administrador no computador local para usar ComSvcConfig.exe.  
  
 A ferramenta pode ser encontrada no seguinte local  
  
 %SystemRoot%\Microsoft.Net\Framework\v3.0\Windows Communication Foundation \  
  
 Para obter mais informações sobre ComSvcConfig.exe, consulte [como: usar a ferramenta de configuração do modelo de serviço com+](./feature-details/how-to-use-the-com-service-model-configuration-tool.md).  
  
 A tabela a seguir descreve os modos que podem ser usados com ComSvcConfig.exe.  
  
|Opção|Descrição|  
|------------|-----------------|  
|`install`|Instala uma configuração para uma interface COM+ para integração do modelo de serviço.<br /><br /> Forma abreviada `/i` .|  
|`uninstall`|Desinstala uma configuração de uma interface COM+ da integração do modelo de serviço.<br /><br /> Forma abreviada `/u` .|  
|`list`|Lista informações sobre aplicativos COM+ e componentes que têm interfaces configuradas para integração do modelo de serviço.<br /><br /> Forma abreviada `/l` .|  
  
 A tabela a seguir descreve os sinalizadores que podem ser usados com ComSvcConfig.exe.  
  
|Opção|Descrição|  
|------------|-----------------|  
|`/application:` \<*ApplicationID* &#124; *ApplicationName*\>|Especifica o aplicativo COM+ a ser configurado.<br /><br /> Forma abreviada `/a` .|  
|`/contract:` \<*ClassID*  &#124; *ProgID*  &#124; \*,*InterfaceID* &#124; *InterfaceName* &#124; \*\>|Especifica o componente e a interface COM+ que serão configurados como o contrato para o serviço.<br /><br /> Forma abreviada `/c` .<br /><br /> Embora o caractere curinga ( \* ) possa ser usado quando você especifica os nomes do componente e da interface, é recomendável não usá-lo, pois você pode expor interfaces que não pretendiam.|  
|`/hosting:` \<*complus*  &#124; *was*\>|Especifica se o modo de hospedagem COM+ ou o modo de hospedagem da Web deve ser usado.<br /><br /> Forma abreviada `/h` .<br /><br /> Usar o modo de hospedagem COM+ requer ativação explícita do aplicativo COM+. O uso do modo de hospedagem da Web permite que o aplicativo COM+ seja ativado automaticamente conforme necessário. Se o aplicativo COM+ for um aplicativo de biblioteca, ele será executado no processo de Serviços de Informações da Internet (IIS). Se o aplicativo COM+ for um aplicativo de servidor, ele será executado no processo de Dllhost.exe.|  
|`/webSite:` \<*WebsiteName*\>|Especifica o site para hospedagem quando o modo de hospedagem da Web é usado (consulte o `/hosting` sinalizador).<br /><br /> Forma abreviada `/w` .<br /><br /> Se nenhum site da Web for especificado, o site padrão será usado.|  
|`/webDirectory:` \<*WebDirectoryName*\>|Especifica o diretório virtual para hospedagem quando a hospedagem Web é usada (consulte o `/hosting` sinalizador).<br /><br /> Forma abreviada `/d` .|  
|`/mex`|Adiciona um ponto de extremidade de serviço de intercâmbio de metadados (MEX) à configuração de serviço padrão para dar suporte a clientes que desejam recuperar uma definição de contrato do serviço.<br /><br /> Forma abreviada `/x` .|  
|`/id`|Exibe as informações de aplicativo, componente e interface como IDs.<br /><br /> Forma abreviada `/k` .|  
|`/nologo`|Impede que ComSvcConfig.exe exibam seu logotipo.<br /><br /> Forma abreviada `/n` .|  
|`/verbose`|Gera todos os avisos ou texto informativo além dos erros encontrados.<br /><br /> Forma abreviada `/v` .|  
|`/help`|Exibe a mensagem de uso.<br /><br /> Forma abreviada `/?` .|  
|`/partial`|Gera uma configuração de serviço quando a interface especificada inclui uma ou mais assinaturas de método que podem ser expostas. No momento da inicialização do serviço, os métodos compatíveis aparecem como operações no contrato de serviço, e os métodos não compatíveis são ignorados e estão ausentes do contrato de serviço.<br /><br /> Se esse sinalizador estiver ausente, a ferramenta não gerará uma configuração de serviço quando a interface especificada incluir um ou mais métodos incompatíveis.|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="description"></a>Descrição  

 O exemplo a seguir adiciona a `IFinances` interface do `ItemOrders.IFinancial` componente (do aplicativo OnlineStore com+) ao conjunto de interfaces que são expostas como serviços Web, usando o modo de hospedagem com+. Todos os avisos serão exibidos além dos erros encontrados.  
  
### <a name="code"></a>Código  
  
```console  
ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus /verbose  
```  
  
### <a name="description"></a>Descrição  

 O exemplo a seguir adiciona a `IStockLevels` interface do `ItemInventory.Warehouse` componente (do aplicativo OnlineWarehouse com+) ao conjunto de interfaces que são expostas como serviços Web, usando o modo de hospedagem da Web. O serviço Web é hospedado na Web no diretório virtual OnlineWarehouse do IIS.  
  
### <a name="code"></a>Código  
  
```console  
ComSvcConfig.exe /install /application:OnlineWarehouse /contract:ItemInventory.Warehouse,IStockLevels /hosting:was /webDirectory:root/OnlineWarehouse  
```  
  
### <a name="description"></a>Descrição  

 O exemplo a seguir remove a `IFinances` interface do `ItemOrders.Financial` componente (do aplicativo OnlineStore com+) do conjunto de interfaces que são expostas como serviços Web.  
  
### <a name="code"></a>Código  
  
```console  
ComSvcConfig.exe /uninstall /application:OnlineStore /interface:ItemOrders.Financial,IFinances /hosting:complus  
```  
  
### <a name="description"></a>Descrição  

 O exemplo a seguir lista as interfaces hospedadas do COM+ atualmente expostas, juntamente com os detalhes de endereço e associação correspondentes, para o aplicativo OnlineStore COM+ no computador local.  
  
### <a name="code"></a>Código  
  
```console  
ComSvcConfig.exe /list /application:OnlineStore /hosting:complus  
```  
  
## <a name="see-also"></a>Consulte também

- [Como: usar a ferramenta de configuração do modelo de serviço COM+](./feature-details/how-to-use-the-com-service-model-configuration-tool.md)
