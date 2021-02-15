---
description: 'Saiba mais sobre: dados FILESTREAM'
title: Dados FILESTREAM
ms.date: 03/30/2017
ms.assetid: bd8b845c-0f09-4295-b466-97ef106eefa8
ms.openlocfilehash: 0110be6b867a07ec1cd204e2a3de371367bbfa36
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802041"
---
# <a name="filestream-data"></a>Dados FILESTREAM

O atributo de armazenamento FILESTREAM é para dados binários (BLOB) armazenados em uma coluna varbinary(max). Antes do FILESTREAM, o armazenamento de dados binários exigia tratamento especial. Dados não estruturados, como documentos de texto, imagens e vídeos, geralmente são armazenados fora do banco de dados, o que dificulta o gerenciamento.

> [!NOTE]
> Você deve instalar o .NET Framework 3.5 SP1 (ou posterior) para trabalhar com dados FILESTREAM usando o SqlClient.

A especificação do atributo FILESTREAM em uma coluna varbinary(max) faz com que o SQL Server armazene os dados no sistema de arquivos NTFS local em vez de no arquivo de banco de dados. Embora eles sejam armazenados separadamente, você pode usar as mesmas instruções Transact-SQL, que são compatíveis para trabalhar usando dados varbinary(max) que estão armazenados no banco de dados.

## <a name="sqlclient-support-for-filestream"></a>Suporte do SqlClient para FILESTREAM

O Provedor de Dados .NET Framework para SQL Server, <xref:System.Data.SqlClient> , oferece suporte à leitura e gravação de dados FILESTREAM usando a <xref:System.Data.SqlTypes.SqlFileStream> classe definida no <xref:System.Data.SqlTypes> namespace. O `SqlFileStream` herda da classe <xref:System.IO.Stream>, que fornece métodos para leitura e gravação em fluxos de dados. A leitura de um fluxo transfere dados do fluxo para uma estrutura de dados, como uma matriz de bytes. A gravação transfere os dados da estrutura de dados para um fluxo.

### <a name="creating-the-sql-server-table"></a>Criando a tabela SQL Server

As instruções Transact-SQL a seguir criam uma tabela denominada employees e insere uma linha de dados. Depois de habilitar o armazenamento de FILESTREAM, você pode usar essa tabela em conjunto com os exemplos de código a seguir. Os links para os recursos nos Manuais Online do SQL Server estão localizados no final deste tópico.

```sql
CREATE TABLE employees
(
  EmployeeId INT  NOT NULL  PRIMARY KEY,
  Photo VARBINARY(MAX) FILESTREAM  NULL,
  RowGuid UNIQUEIDENTIFIER  NOT NULL  ROWGUIDCOL
  UNIQUE DEFAULT NEWID()
)
GO
Insert into employees
Values(1, 0x00, default)
GO
```

### <a name="example-reading-overwriting-and-inserting-filestream-data"></a>Exemplo: ler, substituindo e inserir dados FILESTREAM

A amostra a seguir demonstra como ler dados de um FILESTREAM. O código obtém o caminho lógico para o arquivo, configurando o `FileAccess` como `Read` e o `FileOptions` como `SequentialScan`. Em seguida, o código lê os bytes de SqlFileStream no buffer. Então, os bytes são gravados na janela do console.

A amostra a seguir demonstra como gravar dados em um FILESTREAM em que todos os dados existentes são substituídos. O código obtém o caminho lógico para o arquivo e cria o `SqlFileStream`, configurando o `FileAccess` como `Write` e o `FileOptions` como `SequentialScan`. Um byte é gravado no `SqlFileStream`, substituindo todos os dados no arquivo.

O exemplo também demonstra como gravar dados em um FILESTREAM usando o método Seek para acrescentar dados ao final do arquivo. O código obtém o caminho lógico para o arquivo e cria o `SqlFileStream`, configurando o `FileAccess` como `ReadWrite` e o `FileOptions` como `SequentialScan`. O código usa o método Seek para buscar até o final do arquivo, acrescentando um byte ao arquivo existente.

```csharp
using System;
using System.Data.SqlClient;
using System.Data.SqlTypes;
using System.Data;
using System.IO;

namespace FileStreamTest
{
    class Program
    {
        static void Main(string[] args)
        {
            SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder("server=(local);integrated security=true;database=myDB");
            ReadFileStream(builder);
            OverwriteFileStream(builder);
            InsertFileStream(builder);

            Console.WriteLine("Done");
        }

        private static void ReadFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();
                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for the file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Read, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Read the contents as bytes and write them to the console
                            for (long index = 0; index < fileStream.Length; index++)
                            {
                                Console.WriteLine(fileStream.ReadByte());
                            }
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void OverwriteFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Write, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Write a single byte to the file. This will
                            // replace any data in the file.
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void InsertFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.ReadWrite, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Seek to the end of the file
                            fileStream.Seek(0, SeekOrigin.End);

                            // Append a single byte
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }

        }
    }
}
```

Para obter outro exemplo, confira [Como armazenar e buscar dados binários em uma coluna de fluxo de arquivos](https://www.codeproject.com/Articles/32216/How-to-store-and-fetch-binary-data-into-a-file-str).

## <a name="resources-in-sql-server-books-online"></a>Recursos nos Manuais Online do SQL Server

A documentação completa do FILESTREAM está localizada nas seguintes seções dos Manuais Online do SQL Server.

|Tópico|Descrição|
|-----------|-----------------|
|[FILESTREAM (SQL Server)](/sql/relational-databases/blob/filestream-sql-server)|Descreve quando usar o armazenamento FILESTREAM e como ele integra o Mecanismo de Banco de Dados do SQL Server com um sistema de arquivos NTFS.|
|[Criar aplicativos clientes para dados FILESTREAM](/sql/relational-databases/blob/create-client-applications-for-filestream-data)|Descreve as funções da API do Windows para trabalhar usando dados FILESTREAM.|
|[FILESTREAM e outros recursos do SQL Server](/sql/relational-databases/blob/filestream-compatibility-with-other-sql-server-features)|Fornece considerações, diretrizes e limitações para usar dados FILESTREAM com outros recursos do SQL Server.|

## <a name="see-also"></a>Confira também

- [Tipos de dados do SQL Server e ADO.NET](sql-server-data-types.md)
- [Recuperando e modificando dados no ADO.NET](../retrieving-and-modifying-data.md)
- [Segurança de acesso do código e o ADO.NET](../code-access-security.md)
- [Dados binários e de valor grande do SQL Server](sql-server-binary-and-large-value-data.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
