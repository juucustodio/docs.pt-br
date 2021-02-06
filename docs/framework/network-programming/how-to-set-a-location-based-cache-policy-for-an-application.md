---
description: 'Saiba mais sobre: como definir uma política de cache de Location-Based para um aplicativo'
title: 'Como: Definir uma política de cache baseada na localização para um aplicativo'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- explicitly defining cache behavior
- location-based cache policies
- local cache
- request cache policies
- cache [.NET Framework], location-based policies
ms.assetid: 683bb88e-3411-4f46-9686-3411b6ba511c
ms.openlocfilehash: d86e40e24eacb6ce3107e50213941c1169191943
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99662774"
---
# <a name="how-to-set-a-location-based-cache-policy-for-an-application"></a>Como: Definir uma política de cache baseada na localização para um aplicativo

Políticas de cache com base no local permitem que um aplicativo defina explicitamente o comportamento do cache com base na localização do recurso solicitado. Este tópico demonstra como definir a política de cache programaticamente. Para obter informações sobre como definir a política para um aplicativo usando os arquivos de configuração, consulte [ \<requestCaching> elemento (configurações de rede)](../configure-apps/file-schema/network/requestcaching-element-network-settings.md).  
  
### <a name="to-set-a-location-based-cache-policy-for-an-application"></a>Para definir uma política de cache baseada na localização para um aplicativo  
  
1. Crie um objeto <xref:System.Net.Cache.RequestCachePolicy> ou <xref:System.Net.Cache.HttpRequestCachePolicy>.  
  
2. Defina o objeto de política como o padrão para o domínio do aplicativo.  
  
### <a name="to-set-a-policy-that-takes-requested-resources-from-a-cache"></a>Para definir uma política que toma recursos solicitados de um cache  
  
- Crie uma política que toma recursos solicitados de um cache se disponíveis e, caso contrário, envia solicitações ao servidor, definindo o nível de cache para <xref:System.Net.Cache.HttpRequestCacheLevel.CacheIfAvailable>. Uma solicitação pode ser atendida por qualquer cache entre o cliente e servidor, incluindo caches remotos.  
  
    ```csharp  
    public static void UseCacheIfAvailable()  
    {  
        HttpRequestCachePolicy policy = new HttpRequestCachePolicy  
            (HttpRequestCacheLevel.CacheIfAvailable);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub UseCacheIfAvailable()  
        Dim policy As New HttpRequestCachePolicy _  
             (HttpRequestCacheLevel.CacheIfAvailable)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### <a name="to-set-a-policy-that-prevents-any-cache-from-supplying-resources"></a>Para definir uma política que impede qualquer cache de fornecer recursos  
  
- Crie uma política que impede que qualquer cache forneça recursos solicitados, definindo o nível de cache para <xref:System.Net.Cache.HttpRequestCacheLevel.NoCacheNoStore>. Esse nível de política remove o recurso do cache local se ele está presente e indica para caches remotos que eles também devem remover o recurso.  
  
    ```csharp  
    public static void DoNotUseCache()  
    {  
    HttpRequestCachePolicy policy = new HttpRequestCachePolicy
            (HttpRequestCacheLevel.NoCacheNoStore);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub DoNotUseCache()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.NoCacheNoStore)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### <a name="to-set-a-policy-that-returns-requested-resources-only-if-they-are-in-the-local-cache"></a>Para definir uma política que retorna os recursos solicitados apenas se eles estiverem no cache local  
  
- Criar uma política que retorna os recursos solicitados apenas se estiverem no cache local, definindo o nível de cache para <xref:System.Net.Cache.HttpRequestCacheLevel.CacheOnly>. Se o recurso solicitado não estiver no cache, uma exceção <xref:System.Net.WebException> será lançada.  
  
    ```csharp  
    public static void OnlyUseCache()  
    {  
        HttpRequestCachePolicy policy = new HttpRequestCachePolicy
            (HttpRequestCacheLevel.CacheOnly);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub OnlyUseCache()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.CacheOnly)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### <a name="to-set-a-policy-that-prevents-the-local-cache-from-supplying-resources"></a>Para definir uma política que impede o cache local de fornecer recursos  
  
- Crie uma política que impede que o cache local forneça os recursos solicitados, definindo o nível de cache para <xref:System.Net.Cache.HttpRequestCacheLevel.Refresh>. Se o recurso solicitado está em um cache intermediário e é revalidado com êxito, o cache intermediário pode fornecer o recurso solicitado.  
  
    ```csharp  
    public static void DoNotUseLocalCache()  
    {  
     HttpRequestCachePolicy policy = new HttpRequestCachePolicy
            (HttpRequestCacheLevel.Refresh);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub DoNotUseLocalCache()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.Refresh)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### <a name="to-set-a-policy-that-prevents-any-cache-from-supplying-requested-resources"></a>Para definir uma política que impede qualquer cache de fornecer recursos solicitados  
  
- Crie uma política que impede que qualquer cache forneça recursos solicitados, definindo o nível de cache para <xref:System.Net.Cache.HttpRequestCacheLevel.Reload>. O recurso retornado pelo servidor pode ser armazenado no cache.  
  
    ```csharp  
    public static void SendToServer()  
    {  
    HttpRequestCachePolicy policy = new HttpRequestCachePolicy
            (HttpRequestCacheLevel.Reload);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub SendToServer()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.Reload)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### <a name="to-set-a-policy-that-allows-any-cache-to-supply-requested-resources-if-the-resource-on-the-server-is-not-newer-than-the-cached-copy"></a>Para definir uma política que permite que qualquer cache forneça recursos solicitados se o recurso no servidor não é mais recente do que a cópia armazenada em cache  
  
- Crie uma política que permite que qualquer cache forneça recursos solicitados se o recurso no servidor não é mais recente do que a cópia armazenada em cache definindo o nível de cache para <xref:System.Net.Cache.HttpRequestCacheLevel.Revalidate>.  
  
    ```csharp  
    public static void CheckServer()  
    {  
    HttpRequestCachePolicy policy = new HttpRequestCachePolicy  
             (HttpRequestCacheLevel.Revalidate);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub CheckServer()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.Revalidate)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
## <a name="see-also"></a>Consulte também

- [Gerenciamento de cache para aplicativos de rede](cache-management-for-network-applications.md)
- [Política de cache](cache-policy.md)
- [Políticas de cache baseadas na localização](location-based-cache-policies.md)
- [Políticas de cache baseadas em tempo](time-based-cache-policies.md)
- [\<requestCaching> Elemento (configurações de rede)](../configure-apps/file-schema/network/requestcaching-element-network-settings.md)
