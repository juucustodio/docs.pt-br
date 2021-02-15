---
title: Usar manipuladores de exceção filtrados pelo usuário
description: Saiba como usar manipuladores de exceção filtrados pelo usuário em C# e Visual Basic.
ms.date: 12/14/2020
helpviewer_keywords:
- user-filtered exceptions
- exceptions, user-filtered
dev_langs:
- csharp
- vb
ms.openlocfilehash: 2dba43ad2fc685a6555ab43fc973814fd7f359a3
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512665"
---
# <a name="use-user-filtered-exception-handlers"></a>Usar manipuladores de exceção filtrados pelo usuário

Os manipuladores de exceção filtrados por usuário capturam e tratam exceções com base nos requisitos que você define para a exceção. Esses manipuladores usam a `catch` instrução com a `when` palavra-chave ( `Catch` e `When` em Visual Basic).  
  
 Essa técnica é útil quando um objeto de exceção em particular corresponde a vários erros. Nesse caso, o objeto normalmente tem uma propriedade que contém o código de erro específico associado ao erro. Você pode usar a propriedade código de erro na expressão para selecionar apenas o erro específico que você deseja tratar nessa `catch` cláusula.  
  
 O exemplo a seguir ilustra a `catch` / `when` instrução.

```csharp
try
{
    //Try statements.  
}
catch (Exception ex) when (ex.Message.Contains("404"))
{
    //Catch statements.
}
```  
  
```vb
Try  
    'Try statements.  
    Catch When Err = VBErr_ClassLoadException
    'Catch statements.
End Try  
```  
  
 A expressão da cláusula filtrada pelo usuário não é restrita de nenhuma forma. Se ocorrer uma exceção durante a execução da expressão filtrada pelo usuário, essa exceção será descartada e será considerado que a expressão do filtro foi avaliada como falsa. Nesse caso, o Common Language Runtime continua a pesquisar um manipulador para a exceção atual.  
  
## <a name="combine-the-specific-exception-and-the-user-filtered-clauses"></a>Combinar a exceção específica e as cláusulas filtradas pelo usuário  

 Uma `catch` instrução pode conter a exceção específica e as cláusulas filtradas pelo usuário. O runtime testa primeiro a exceção específica. Se a exceção específica for bem-sucedida, o runtime executará o filtro do usuário. O filtro genérico pode conter uma referência à variável declarada no filtro da classe. Observe que a ordem das duas cláusulas do filtro não pode ser invertida.  
  
 O exemplo a seguir mostra uma exceção específica na instrução **Catch** , bem como a cláusula filtrada pelo usuário usando a palavra-chave **When** .  
  
```csharp
try
{
    //Try statements.  
}
catch (System.Net.Http.HttpRequestException ex) when (ex.Message.Contains("404"))
{
    //Catch statements.
}
```  
  
```vb
Try  
    'Try statements.
    Catch cle As ClassLoadException When cle.IsRecoverable()  
    'Catch statements.
End Try  
```  

## <a name="see-also"></a>Consulte também

- [Exceções](index.md)
