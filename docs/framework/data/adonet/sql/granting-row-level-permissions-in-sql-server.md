---
description: 'Saiba mais sobre: concedendo permissões de Row-Level no SQL Server'
title: Conceder permissões de nível de linha no SQL Server
ms.date: 03/30/2017
ms.assetid: a55aaa12-34ab-41cd-9dec-fd255b29258c
ms.openlocfilehash: fe69a023b5befbdb53473881647fff8bdf0e9795
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99663294"
---
# <a name="granting-row-level-permissions-in-sql-server"></a>Conceder permissões de nível de linha no SQL Server

Em alguns cenários, há um requisito para controlar o acesso aos dados em um nível mais granular do que o que simplesmente conceder, revogar ou negar permissões fornece. Por exemplo, um aplicativo de banco de dados do hospital pode exigir que os médicos individuais estejam restritos a acessar informações relacionadas apenas a seus pacientes. Existem requisitos semelhantes em muitos ambientes, incluindo aplicativos financeiros, de lei, governamentais e militares. Para ajudar a resolver esses cenários, o SQL Server 2016 fornece um recurso de [segurança em nível de linha](/sql/relational-databases/security/row-level-security) que simplifica e centraliza a lógica de acesso em nível de linha em uma política de segurança. Para versões anteriores do SQL Server, uma funcionalidade semelhante pode ser obtida usando exibições para aplicar a filtragem em nível de linha.

## <a name="implementing-row-level-filtering"></a>Implementando a filtragem em nível de linha

A filtragem em nível de linha é usada para aplicativos que armazenam informações em uma única tabela, como no exemplo de hospital acima. Para implementar a filtragem em nível de linha, cada linha tem uma coluna que define um parâmetro de diferenciação, como um nome de usuário, rótulo ou outro identificador. Você cria uma política de segurança ou uma exibição na tabela, que filtra as linhas que o usuário pode acessar. Em seguida, você cria procedimentos armazenados parametrizados, que controlam os tipos de consultas que o usuário pode executar.

O exemplo a seguir descreve como configurar a filtragem em nível de linha com base em um usuário ou nome de logon:

- Crie a tabela, adicionando uma coluna para armazenar o nome.

- Habilitar Filtragem em nível de linha:

  - Se você estiver usando o SQL Server 2016 ou superior, ou o [banco de dados SQL do Azure](/azure/sql-database/), crie uma política de segurança que adiciona um predicado na tabela que restringe as linhas retornadas àquelas que correspondem ao usuário do banco de dados atual (usando a função interna CURRENT_USER ()) ou o nome de logon atual (usando a função interna SUSER_SNAME ()):

      ```sql
      CREATE SCHEMA Security
      GO

      CREATE FUNCTION Security.userAccessPredicate(@UserName sysname)
          RETURNS TABLE
          WITH SCHEMABINDING
      AS
          RETURN SELECT 1 AS accessResult
          WHERE @UserName = SUSER_SNAME()
      GO

      CREATE SECURITY POLICY Security.userAccessPolicy
          ADD FILTER PREDICATE Security.userAccessPredicate(UserName) ON dbo.MyTable,
          ADD BLOCK PREDICATE Security.userAccessPredicate(UserName) ON dbo.MyTable
      GO
      ```

  - Se você estiver usando uma versão do SQL Server anterior a 2016, poderá obter uma funcionalidade semelhante usando uma exibição:

      ```sql
      CREATE VIEW vw_MyTable
      AS
          RETURN SELECT * FROM MyTable
          WHERE UserName = SUSER_SNAME()
      GO
      ```

- Crie procedimentos armazenados para selecionar, inserir, atualizar e excluir dados. Se a filtragem for aplicada por uma política de segurança, os procedimentos armazenados devem executar essas operações na tabela base diretamente; caso contrário, se a filtragem for aplicada por um modo de exibição, os procedimentos armazenados deverão operar em relação à exibição. A política de segurança ou a exibição filtrará automaticamente as linhas retornadas ou modificadas por consultas de usuário, e o procedimento armazenado fornecerá um limite de segurança mais difícil para impedir que os usuários com acesso direto a consultas executem com êxito consultas que podem inferir a existência de dados filtrados.

- Para procedimentos armazenados que inserem dados, Capture o nome de usuário usando a mesma função especificada na política de segurança ou exibição e insira esse valor na coluna nome de usuário.

- Negue todas as permissões nas tabelas (e exibições, se aplicável) à `public` função. Os usuários não poderão herdar permissões de outras funções de banco de dados, pois o predicado de filtro é baseado em nomes de usuário ou de logon, não em funções.

- Conceda EXECUTE nos procedimentos armazenados para funções de banco de dados. Os usuários só podem acessar dados por meio dos procedimentos armazenados fornecidos.

## <a name="see-also"></a>Consulte também

- [Segurança em nível de linha](/sql/relational-databases/security/row-level-security)
- [Protegendo aplicativos ADO.NET](../securing-ado-net-applications.md)
- [Visão geral de segurança do SQL Server](overview-of-sql-server-security.md)
- [Cenários de Segurança de Aplicativo no SQL Server](application-security-scenarios-in-sql-server.md)
- [Gerenciando permissões com procedimentos armazenados no SQL Server](managing-permissions-with-stored-procedures-in-sql-server.md)
- [Gravação de SQL Dinâmico Seguro no SQL Server](writing-secure-dynamic-sql-in-sql-server.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
