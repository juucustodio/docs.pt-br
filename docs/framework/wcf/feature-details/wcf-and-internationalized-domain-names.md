---
title: WCF e nomes de domínio internacionalizados
ms.date: 03/30/2017
ms.assetid: c8a3e10a-8bc2-4a78-8d86-a562ba6e65fa
ms.openlocfilehash: 1db62f3e7d073fd1bf9bf9d4d0e17703310f2e69
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988589"
---
# <a name="wcf-and-internationalized-domain-names"></a>WCF e nomes de domínio internacionalizados
Foi adicionado suporte para permitir serviços WCF com IDNs (nomes de domínio internacionalizados). Um nome de domínio internacionalizado é um nome de domínio que contém caracteres não ASCII. Esse suporte inclui a capacidade de hospedar um serviço WCF com um nome IDN e um cliente WCF para se comunicar com um serviço Web com um nome IDN.  
  
## <a name="systemuri-and-idn"></a>System. URI e IDN  
 <xref:System.Uri>tem duas propriedades <xref:System.Uri.Host%2A> e <xref:System.Uri.DnsSafeHost%2A>. Essas propriedades contêm valores Unicode ou Punycode dependendo das definições de configuração de IDN.  
  
 O IDN está habilitado no arquivo de configuração de um aplicativo usando o seguinte XML  
  
```xml  
<configuration>  
  <uri>  
    <idn enabled="All/AllExceptIntranet/None" />  
  </uri>  
</configuration>  
```  
  
 O \<elemento > IDN contém o atributo enabled que pode ser definido como um dos seguintes valores:  
  
1. "None"  
  
2. "AllExceptIntranet"  
  
3. Os  
  
 Quando a configuração de IDN é definida como "None", nenhuma conversões é executada por URI. host ou URI. DnsSafeHost. Quando a configuração de IDN é definida como "All", Uri. O host permanece Unicode e URI. DnsSafeHost é convertido em Punycode. Quando a configuração de IDN é definida como "AllExceptIntranet", Uri. DnsSafeHost é convertido em Punycode para endereços da Internet e permanece Unicode para endereços de intranet. Essa configuração é importante para a resolução correta de nomes DNS. Observe que essa configuração não precisa ser configurada para o Windows 8 e versões mais recentes.  
  
> [!WARNING]
> Você nunca deve embutir em código um endereço usando Punycode. O WCF irá convertê-lo para você com base nas definições de configuração aplicadas.  
  
> [!WARNING]
> Ao adicionar caracteres Unicode a applicationHost. exe. config, salve o arquivo usando a codificação UTF-8.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Uri?displayProperty=nameWithType>
