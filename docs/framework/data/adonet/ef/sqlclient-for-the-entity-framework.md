---
description: 'Saiba mais sobre: SqlClient para o Entity Framework'
title: SqlClient para Entity Framework
ms.date: 03/30/2017
ms.assetid: 9a5d6d39-d955-43a5-a5c2-931c239398f1
ms.openlocfilehash: eba5602c13f66d1ee4404bbc27035304e34c1cd0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99673122"
---
# <a name="sqlclient-for-the-entity-framework"></a>SqlClient para Entity Framework

Esta seção descreve o provedor de dados. NET Framework para SQL Server (SqlClient), que permite Entity Framework para trabalhar sobre o Microsoft SQL Server.  
  
## <a name="provider-schema-attribute"></a>Atributo do provedor  

 `Provider` é um atributo do elemento de `Schema` na linguagem de definição de esquema de armazenamento (SSDL).  
  
 Para usar SqlClient, atribua a cadeia de caracteres “System.Data.SqlClient” ao atributo de `Provider` do elemento de `Schema` .  
  
## <a name="providermanifesttoken-schema-attribute"></a>Atributo do esquema de ProviderManifestToken  

 `ProviderManifestToken` é necessário um atributo do elemento de `Schema` em SSDL. Este token é usado para carregar o manifesto do provedor para cenários off-line. Para obter mais informações sobre o `ProviderManifestToken` atributo, consulte [elemento de esquema (SSDL)](/ef/ef6/modeling/designer/advanced/edmx/ssdl-spec#schema-element-ssdl).  
  
 O SqlClient pode ser usado como um provedor de dados para diferentes versões do SQL Server. Essas versões têm recursos diferentes. Por exemplo, SQL Server 2000 não oferece suporte `varchar(max)` `nvarchar(max)` a tipos e que foram introduzidos com SQL Server 2005.  
  
 SqlClient gerencia e aceita os seguintes tokens de manifesto de provedor para versões diferentes do SQL Server.  
  
|SQL Server 2000|SQL Server 2005|SQL Server 2008|  
|-|-|-|  
|2000|2005|2008|  
  
> [!NOTE]
> A partir do Visual Studio 2010, as [ferramentas de Modelo de Dados de Entidade ADO.net](/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100)) não dão suporte a SQL Server 2000.  
  
## <a name="provider-namespace-name"></a>Nome do namespace do provedor  

 Todos os provedores devem especificar um namespace. Essa propriedade informa a Entity Framework que prefixo é usado pelo provedor para compilações específicas, como tipos e funções. O namespace para manifestos de provedor SqlClient é `SqlServer`. Para obter mais informações sobre namespaces, consulte [namespaces](./language-reference/namespaces-entity-sql.md).  
  
## <a name="types"></a>Tipos  

 O provedor SqlClient para Entity Framework fornece informações de mapeamento entre tipos de modelo conceitual e tipos SQL Server. Para obter mais informações, consulte [SqlClient para Entity FrameworkTypes](sqlclient-for-ef-types.md).  
  
## <a name="functions"></a>Funções  

 O provedor SqlClient para Entity Framework define a lista de funções suportadas pelo provedor. Para obter uma lista das funções com suporte, consulte [SqlClient para funções de Entity Framework](sqlclient-for-ef-functions.md).  
  
## <a name="in-this-section"></a>Nesta seção  

 [SqlClient para funções de Entity Framework](sqlclient-for-ef-functions.md)  
  
 [SqlClient para a entidade FrameworkTypes](sqlclient-for-ef-types.md)  
  
 [Problemas conhecidos em SqlClient para Entity Framework](known-issues-in-sqlclient-for-entity-framework.md)  
  
## <a name="see-also"></a>Consulte também

- [Linguagem Entity SQL](./language-reference/entity-sql-language.md)
- [Referência de linguagem](./language-reference/index.md)
- [Problemas conhecidos no provedor SqlClient para Entity Framework](sqlclient-for-the-entity-framework.md)
