---
description: 'Saiba mais sobre: parâmetros de CURSOR de referência em um OracleDataReader'
title: Parâmetros de REF CURSOR em um OracleDataReader
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: 801dff0f-2508-45aa-9416-f45d6887740c
ms.openlocfilehash: 94c4e1fe6eb6c065b8551e09c49b322b4728abeb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739151"
---
# <a name="ref-cursor-parameters-in-an-oracledatareader"></a>Parâmetros de REF CURSOR em um OracleDataReader

Este exemplo de Visual Basic da Microsoft executa um procedimento armazenado PL/SQL que retorna um parâmetro de CURSOR REF e lê o valor como um <xref:System.Data.OracleClient.OracleDataReader> .

```vb
Private Sub Button1_Click(ByVal sender As Object, _
  ByVal e As System.EventArgs) Handles Button1.Click

  Dim connString As New String(_
      "Data Source=Oracle9i;User ID=scott;Password=[PLACEHOLDER];")
  Using conn As New OracleConnection(connString)
    Dim cmd As New OracleCommand()
    Dim rdr As OracleDataReader

    conn.Open()
    cmd.Connection = conn
    cmd.CommandText = "CURSPKG.OPEN_ONE_CURSOR"
    cmd.CommandType = CommandType.StoredProcedure
    cmd.Parameters.Add(New OracleParameter(
      "N_EMPNO", OracleType.Number)).Value = 7369
    cmd.Parameters.Add(New OracleParameter(
      "IO_CURSOR", OracleType.Cursor)).Direction = ParameterDirection.Output

    rdr = cmd.ExecuteReader()
    While (rdr.Read())
        REM do something with the values
    End While

    rdr.Close()
  End Using
End Sub
```

## <a name="see-also"></a>Consulte também

- [REF CURSORs do Oracle](oracle-ref-cursors.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
