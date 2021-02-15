---
description: 'Saiba mais sobre: acesso a dados seguros'
title: Acesso seguro a dados
ms.date: 03/30/2017
ms.assetid: 473ebd69-21a3-4627-b95e-4e04d035c56f
ms.openlocfilehash: 0f14f271dda9d07ba1efdea2328a5b3e30d14849
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99718883"
---
# <a name="secure-data-access"></a>Acesso seguro a dados

Para escrever um código de ADO.NET seguro, você precisa entender os mecanismos de segurança disponíveis no armazenamento de dados subjacente ou no Database. Você também precisa considerar as implicações de segurança de outros recursos ou componentes que seu aplicativo pode conter.  
  
## <a name="authentication-authorization-and-permissions"></a>Autenticação, autorização e permissões  

 Ao se conectar ao Microsoft SQL Server, você pode usar a autenticação do Windows, também conhecida como segurança integrada, que usa a identidade do usuário ativo do Windows atual em vez de passar uma ID de usuário e senha. Usar a autenticação do Windows é altamente recomendável porque as credenciais do usuário não são expostas na cadeia de conexão. Se você não puder usar a autenticação do Windows para se conectar ao SQL Server, considere criar cadeias de conexão em tempo de execução usando o <xref:System.Data.SqlClient.SqlConnectionStringBuilder> .  
  
 As credenciais usadas para autenticação precisam ser tratadas de forma diferente com base no tipo de aplicativo. Por exemplo, em um aplicativo Windows Forms, o usuário pode ser solicitado a fornecer informações de autenticação ou as credenciais do Windows do usuário podem ser usadas. No entanto, um aplicativo Web geralmente acessa dados usando as credenciais fornecidas pelo próprio aplicativo em vez de pelo usuário.  
  
 Depois que os usuários tiverem sido autenticados, o escopo de suas ações dependerá das permissões que foram concedidas a eles. Sempre siga o princípio de privilégios mínimos e conceda apenas permissões que são absolutamente necessárias.  
  
 Para obter mais informações, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Protegendo informações de conexão](protecting-connection-information.md)|Descreve as práticas recomendadas de segurança e as técnicas para proteger as informações de conexão, como usar a configuração protegida para criptografar cadeias de conexão.|  
|[Recomendações para estratégias de acesso a dados](/previous-versions/visualstudio/visual-studio-2008/8fxztkff(v=vs.90))|Fornece recomendações para o acesso a dados e a execução de operações de Database.|  
|[Construtores de cadeia de conexão](connection-string-builders.md)|Descreve como criar cadeias de conexão da entrada do usuário em tempo de execução.|  
|[Visão geral de segurança do SQL Server](./sql/overview-of-sql-server-security.md)|Descreve a arquitetura de segurança do SQL Server.|  
  
## <a name="parameterized-commands-and-sql-injection"></a>Comandos com parâmetros e injeção de SQL  

 O uso de comandos com parâmetros ajuda a proteger contra ataques de injeção de SQL, em que um invasor "injeta" um comando em uma instrução SQL que compromete a segurança no servidor. Os comandos com parâmetros são protegidos contra um ataque de injeção de SQL, garantindo que os valores recebidos de uma fonte externa sejam passados apenas como valores e não façam parte da instrução Transact-SQL. Como resultado, comandos Transact-SQL inseridos em um valor não são executados na fonte de dados. Em vez disso, eles são avaliados exclusivamente como um valor de parâmetro. Além dos benefícios de segurança, os comandos com parâmetros fornecem um método conveniente para organizar valores passados com uma instrução Transact-SQL ou para um procedimento armazenado.  
  
 Para obter mais informações sobre como usar comandos com parâmetros, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Parâmetros DataAdapter](dataadapter-parameters.md)|Descreve como usar parâmetros com um `DataAdapter` .|  
|[Modificando dados com procedimentos armazenados](modifying-data-with-stored-procedures.md)|Descreve como especificar parâmetros e obter um valor de retorno.|  
|[Gerenciando permissões com procedimentos armazenados no SQL Server](./sql/managing-permissions-with-stored-procedures-in-sql-server.md)|Descreve como usar SQL Server procedimentos armazenados para encapsular o acesso a dados.|  
  
## <a name="script-exploits"></a>Scripts maliciosos  

 Uma exploração de script é outra forma de injeção que usa caracteres mal-intencionados inseridos em uma página da Web. O navegador não valida os caracteres inseridos e os processará como parte da página.  
  
 Para obter mais informações, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Visão geral de scripts maliciosos](/previous-versions/aspnet/w1sw53ds(v=vs.100))|Descreve como proteger contra scripts e explorações de instrução SQL.|  
  
## <a name="probing-attacks"></a>Ataques de investigação  

 Os invasores geralmente usam informações de uma exceção, como o nome do seu servidor, banco de dados ou tabela, para montar um ataque em seu sistema. Como as exceções podem conter informações específicas sobre seu aplicativo ou fonte de dados, você pode ajudar a manter seu aplicativo e a fonte de dados mais protegidos, expondo apenas as informações essenciais ao cliente.  
  
 Para obter mais informações, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Tratando e gerando exceções no .NET](../../../standard/exceptions/index.md)|Descreve as formas básicas de manipulação de exceção estruturada try/catch/finally.|  
|[Práticas recomendadas para exceções](../../../standard/exceptions/best-practices-for-exceptions.md)|Descreve as práticas recomendadas para lidar com exceções.|  
  
## <a name="protecting-microsoft-access-and-excel-data-sources"></a>Protegendo fontes de dados do Microsoft Access e do Excel  

 O Microsoft Access e o Microsoft Excel podem atuar como um armazenamento de dados para um aplicativo ADO.NET quando os requisitos de segurança são mínimos ou inexistentes. Seus recursos de segurança são eficazes para Deterrence, mas não devem ser confiáveis para fazer mais do que desencorajar o meddling por usuários não informados. Os arquivos de dados físicos para acesso e Excel existem no sistema de arquivos e devem ser acessíveis a todos os usuários. Isso os torna vulneráveis a ataques que podem resultar em roubo ou perda de dados, já que os arquivos podem ser facilmente copiados ou alterados. Quando a segurança robusta é necessária, use SQL Server ou outro banco de dados baseado em servidor em que os arquivos físicos não possam ser lidos do sistema de arquivos.  
  
 Para obter mais informações sobre como proteger dados do Access e do Excel, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Considerações sobre segurança e diretrizes para o Access 2007](/previous-versions/office/developer/office-2007/bb421308(v=office.12))|Descreve as técnicas de segurança para o acesso 2007, como criptografar arquivos, administrar senhas, converter bancos de dados para os novos formatos de ACCDB e ACCDE e usar outras opções de segurança.|  
|[Introdução à segurança do Access 2010](https://support.office.com/article/Introduction-to-Access-2010-security-CAE6D764-0318-4622-955F-68D9F186D6CA)|Fornece uma visão geral dos recursos de segurança oferecidos pelo Access 2010.|  

## <a name="enterprise-services"></a>Serviços corporativos  

 O COM+ contém seu próprio modelo de segurança que se baseia em contas do Windows NT e na representação de processo/thread. O <xref:System.EnterpriseServices> namespace fornece wrappers que permitem que aplicativos .net integrem código gerenciado com os serviços de segurança do com+ por meio da <xref:System.EnterpriseServices.ServicedComponent> classe.  
  
 Para obter mais informações, consulte o recurso a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Segurança baseada em função](/previous-versions/dotnet/netframework-1.1/s6y8k15h(v=vs.71))|Discute como integrar código gerenciado com os serviços de segurança do COM+.|  
  
## <a name="interoperating-with-unmanaged-code"></a>Interoperação com código não gerenciado  

 O .NET Framework fornece a interação com código não gerenciado, incluindo componentes COM, serviços COM+, bibliotecas de tipo externo e muitos serviços de sistema operacional. Trabalhar com código não gerenciado envolve a saída fora do perímetro de segurança para código gerenciado. Seu código e qualquer código que chame ele deve ter permissão de código não gerenciado ( <xref:System.Security.Permissions.SecurityPermission> com o <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode> sinalizador especificado). O código não gerenciado pode introduzir vulnerabilidades de segurança não pretendidas em seu aplicativo. Portanto, você deve evitar a interoperação com código não gerenciado, a menos que seja absolutamente necessário.  
  
 Para obter mais informações, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Interoperação com código não gerenciado](../../interop/index.md)|Contém tópicos que descrevem como expor componentes COM ao .NET Framework e como expor .NET Framework componentes ao COM.|
|[Interoperabilidade COM avançada](/previous-versions/dotnet/netframework-4.0/bd9cdfyx(v=vs.100))|Contém tópicos avançados, como assemblies de interoperabilidade primária, threading e marshaling personalizado.|

## <a name="see-also"></a>Consulte também

- [Protegendo aplicativos ADO.NET](securing-ado-net-applications.md)
- [Segurança do SQL Server](./sql/sql-server-security.md)
- [Recomendações para estratégias de acesso a dados](/previous-versions/visualstudio/visual-studio-2008/8fxztkff(v=vs.90))
- [Protegendo informações de conexão](protecting-connection-information.md)
- [Construtores de cadeia de conexão](connection-string-builders.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
