---
description: 'Saiba mais sobre: executando operações de catálogo'
title: Executar operações de catálogo
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e60f542f-6271-495b-a9e4-48553481c2a3
ms.openlocfilehash: c484e3a56d846de66c6e13b374efe58430ab86b2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754336"
---
# <a name="performing-catalog-operations"></a>Executar operações de catálogo

Para executar um comando a fim de modificar um banco de dados ou catálogo, como a instrução CREATE TABLE ou CREATE PROCEDURE, crie um objeto **Command** usando as instruções SQL apropriadas e um objeto **Connection**. Execute o comando com o método **ExecuteNonQuery** do objeto **Command** .  
  
 O exemplo de código a seguir cria um procedimento armazenado em um banco de dados do Microsoft SQL Server.  
  
```vb  
' Assumes connection is a valid SqlConnection.  
Dim queryString As String = "CREATE PROCEDURE InsertCategory " & _  
    "@CategoryName nchar(15), " & _  
    "@Identity int OUT " & _  
    "AS " & _  
    "INSERT INTO Categories (CategoryName) VALUES(@CategoryName) " & _  
    "SET @Identity = @@Identity " & _  
    "RETURN @@ROWCOUNT"  
  
Dim command As SqlCommand = New SqlCommand(queryString, connection)  
command.ExecuteNonQuery()  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
string queryString = "CREATE PROCEDURE InsertCategory  " +
    "@CategoryName nchar(15), " +  
    "@Identity int OUT " +  
    "AS " +
    "INSERT INTO Categories (CategoryName) VALUES(@CategoryName) " +
    "SET @Identity = @@Identity " +  
    "RETURN @@ROWCOUNT";  
  
SqlCommand command = new SqlCommand(queryString, connection);  
command.ExecuteNonQuery();  
```  
  
## <a name="see-also"></a>Confira também

- [Usando comandos para modificar dados](using-commands-to-modify-data.md)
- [Comandos e parâmetros](commands-and-parameters.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
