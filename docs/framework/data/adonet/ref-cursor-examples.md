---
description: 'Saiba mais sobre: exemplos de CURSOR de referência'
title: Exemplos de REF CURSOR
ms.date: 03/30/2017
ms.assetid: c257da03-c6c9-4cf8-b591-b7740a962c40
ms.openlocfilehash: e7cb411778b325400d37511b082032e590b339c0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99773219"
---
# <a name="ref-cursor-examples"></a>Exemplos de REF CURSOR

Os exemplos de REF CURSOR são compostos dos seguintes três exemplos do Microsoft Visual Basic que demonstram como usar REF CURSORs.  
  
|Amostra|Descrição|  
|------------|-----------------|  
|[Parâmetros de REF CURSOR em um OracleDataReader](ref-cursor-parameters-in-an-oracledatareader.md)|Este exemplo executa um procedimento armazenado PL/SQL, que retorna um parâmetro de REF CURSOR e lê o valor como um <xref:System.Data.OracleClient.OracleDataReader>.|  
|[Recuperar dados de vários REF CURSORs usando um OracleDataReader](retrieving-data-from-multiple-ref-cursors.md)|Este exemplo executa um procedimento armazenado PL/SQL que retorna dois parâmetros de CURSOR de referência e lê os valores usando um **OracleDataReader**.|  
|[Preenchendo um DataSet usando um ou mais REF CURSORs](filling-a-dataset-using-one-or-more-ref-cursors.md)|Este exemplo executa um procedimento armazenado PL/SQL, que retorna dois parâmetros de REF CURSOR e preenche um <xref:System.Data.DataSet> com as linhas retornadas.|  
  
 Para usar esses exemplos, você pode precisar criar as tabelas Oracle e deve criar um pacote PL/SQL e o corpo do pacote.  
  
## <a name="creating-the-oracle-tables"></a>Criando as tabelas do Oracle  

 Estes exemplos usam as tabelas que são definidas no esquema Scott/Tiger do Oracle. O esquema Scott/Tiger do Oracle é incluído na maioria das instalações do Oracle. Se esse esquema não existir, você poderá usar o arquivo de comandos SQL em {OracleHome}\rdbms\admin\scott.sql para criar as tabelas e os índices usados por esses exemplos.  
  
## <a name="creating-the-oracle-package-and-package-body"></a>Criando o pacote Oracle e o corpo do pacote  

 Esses exemplos requerem o seguinte pacote PL/SQL e o corpo do pacote no seu servidor. Crie o seguinte pacote Oracle no servidor Oracle.  
  
```sql
CREATE OR REPLACE PACKAGE CURSPKG AS
    TYPE T_CURSOR IS REF CURSOR;
    PROCEDURE OPEN_ONE_CURSOR (N_EMPNO IN NUMBER,
                               IO_CURSOR IN OUT T_CURSOR);
    PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,
                                DEPTCURSOR OUT T_CURSOR);  
END CURSPKG;  
/
```  
  
 Crie o seguinte corpo do pacote Oracle no servidor Oracle.  
  
```sql
CREATE OR REPLACE PACKAGE BODY CURSPKG AS  
    PROCEDURE OPEN_ONE_CURSOR (N_EMPNO IN NUMBER,  
                               IO_CURSOR IN OUT T_CURSOR)  
    IS
        V_CURSOR T_CURSOR;
    BEGIN
        IF N_EMPNO <> 0
        THEN  
             OPEN V_CURSOR FOR
             SELECT EMP.EMPNO, EMP.ENAME, DEPT.DEPTNO, DEPT.DNAME
                  FROM EMP, DEPT
                  WHERE EMP.DEPTNO = DEPT.DEPTNO
                  AND EMP.EMPNO = N_EMPNO;  
  
        ELSE
             OPEN V_CURSOR FOR
             SELECT EMP.EMPNO, EMP.ENAME, DEPT.DEPTNO, DEPT.DNAME
                  FROM EMP, DEPT
                  WHERE EMP.DEPTNO = DEPT.DEPTNO;  
  
        END IF;  
        IO_CURSOR := V_CURSOR;
    END OPEN_ONE_CURSOR;
  
    PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,  
                                DEPTCURSOR OUT T_CURSOR)  
    IS
        V_CURSOR1 T_CURSOR;
        V_CURSOR2 T_CURSOR;
    BEGIN
        OPEN V_CURSOR1 FOR SELECT * FROM EMP;  
        OPEN V_CURSOR2 FOR SELECT * FROM DEPT;  
        EMPCURSOR  := V_CURSOR1;
        DEPTCURSOR := V_CURSOR2;
    END OPEN_TWO_CURSORS;
END CURSPKG;  
/  
```  
  
## <a name="see-also"></a>Consulte também

- [REF CURSORs do Oracle](oracle-ref-cursors.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
