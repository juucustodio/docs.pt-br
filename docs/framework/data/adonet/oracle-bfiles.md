---
description: 'Saiba mais sobre: Oracle BARQUIVOs'
title: Oracle BFILEs
ms.date: 03/30/2017
ms.assetid: 341bbf84-4734-4d44-8723-ccedee954e21
ms.openlocfilehash: e1fda4ad4acb225dc9a70c92b2c4f2b1d61ab1d7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99672485"
---
# <a name="oracle-bfiles"></a>Oracle BFILEs

O provedor de dados .NET Framework para Oracle inclui a classe <xref:System.Data.OracleClient.OracleBFile>, que é usada para trabalhar com os tipos de dados Oracle <xref:System.Data.OracleClient.OracleType.BFile>.  
  
 O tipo de dados Oracle **bArquivo** é um tipo de dados **LOB** Oracle que contém uma referência a dados binários com um tamanho máximo de 4 gigabytes. Um Oracle **bArquivo** é diferente de outros tipos de dados **LOB** da Oracle, pois seus dados são armazenados em um arquivo físico no sistema operacional, e não no servidor. Observe que o tipo de dados **bArquivo** fornece acesso somente leitura aos dados.  
  
 Outras características de um tipo de dados **bArquivo** que o distinguem de um tipo de dados **LOB** são:  
  
- Contém dados não estruturados.  
  
- Dá suporte a agrupamento do lado do servidor.  
  
- Usa semântica de cópia de referência. Por exemplo, se você executar uma operação de cópia em um **bArquivo**, somente o localizador **bArquivo** (que é uma referência ao arquivo) será copiado. Os dados no arquivo não são copiados.  
  
 O tipo de dados **bArquivo** deve ser usado para referenciar LOBs que são grandes em tamanho e, portanto, não é prático armazenar no banco de dados. Mais sobrecarga de cliente, servidor e comunicação é envolvida ao usar um tipo de dados **bArquivo** em comparação com o tipo de dados **LOB** . É mais eficiente acessar um **bArquivo** se você só precisa obter uma pequena quantidade de dados. Será mais eficiente acessar LOBs residentes em banco de dados se você precisar obter o objeto inteiro.  
  
 Cada objeto **OracleBFile** não nulo é associado a duas entidades que definem o local do arquivo físico subjacente:  
  
1. Um objeto DIRECTORY da Oracle, que é um alias de banco de dados para um diretório no sistema de arquivos, e  
  
2. O nome de arquivo do arquivo físico subjacente, que está localizado no diretório associado ao objeto DIRECTORY.  
  
## <a name="example"></a>Exemplo  

 O exemplo de C# a seguir demonstra como você pode criar um **bArquivo** em uma tabela do Oracle e, em seguida, recuperá-lo na forma de um objeto **OracleBFile** . O exemplo demonstra como usar o <xref:System.Data.OracleClient.OracleDataReader> objeto e os métodos **OracleBFile** **Seek** e **Read** . Observe que, para usar este exemplo, você deve primeiro criar um diretório chamado "c: \\ \bfiles" e o arquivo chamado "MyFile.jpg" no servidor Oracle.  
  
```csharp  
using System;  
using System.IO;  
using System.Data;  
using System.Data.OracleClient;  
  
public class Sample  
{  
   public static void Main(string[] args)  
   {  
      OracleConnection connection = new OracleConnection(  
        "Data Source=Oracle8i;Integrated Security=yes");  
      connection.Open();  
  
      OracleCommand command = connection.CreateCommand();  
      command.CommandText =
        "CREATE or REPLACE DIRECTORY MyDir as 'c:\\bfiles'";  
      command.ExecuteNonQuery();  
      command.CommandText =
        "DROP TABLE MyBFileTable";  
      try {  
        command.ExecuteNonQuery();  
      }  
      catch {  
      }  
      command.CommandText =
        "CREATE TABLE MyBFileTable(col1 number, col2 BFILE)";  
      command.ExecuteNonQuery();  
      command.CommandText =
        "INSERT INTO MyBFileTable values ('2', BFILENAME('MyDir', " +  
        "'MyFile.jpg'))";  
      command.ExecuteNonQuery();  
      command.CommandText = "SELECT * FROM MyBFileTable";  
  
        byte[] buffer = new byte[100];  
  
      OracleDataReader reader = command.ExecuteReader();  
      using (reader) {  
          if (reader.Read()) {  
                OracleBFile bFile = reader.GetOracleBFile(1);  
                using (bFile) {  
                  bFile.Seek(0, SeekOrigin.Begin);  
                  bFile.Read(buffer, 0, 100);  
              }  
          }  
      }  
  
      connection.Close();  
   }  
  
}  
```  
  
## <a name="see-also"></a>Consulte também

- [Oracle e ADO.NET](oracle-and-adonet.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
