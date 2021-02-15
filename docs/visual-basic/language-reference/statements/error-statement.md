---
description: 'Saiba mais sobre: instrução de erro'
title: Instrução Error
ms.date: 07/20/2015
f1_keywords:
- vb.error
helpviewer_keywords:
- Error statement [Visual Basic], syntax
- Error statement [Visual Basic]
- Error keyword [Visual Basic]
- run-time errors [Visual Basic], codes
- errors [Visual Basic], simulating
ms.assetid: 85cd5c59-5224-4f02-aaf5-fcfefab17a29
ms.openlocfilehash: 6c152e9e4fb4fa3a937042761c7d776b337f4fef
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99769137"
---
# <a name="error-statement"></a>Instrução Error

Simula a ocorrência de um erro.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Error errornumber  
```  
  
## <a name="parts"></a>Partes  

 `errornumber`  
 Obrigatório. Pode ser qualquer número de erro válido.  
  
## <a name="remarks"></a>Comentários  

 A `Error` instrução tem suporte para compatibilidade com versões anteriores. No novo código, especialmente ao criar objetos, use o `Err` método do objeto `Raise` para gerar erros em tempo de execução.  
  
 Se `errornumber` for definido, a `Error` instrução chamará o manipulador de erro depois que as propriedades do `Err` objeto forem atribuídas aos seguintes valores padrão:  
  
|Propriedade|Valor|  
|--------------|-----------|  
|`Number`|Valor especificado como argumento para `Error` instrução. Pode ser qualquer número de erro válido.|  
|`Source`|Nome do projeto de Visual Basic atual.|  
|`Description`|Expressão de cadeia de caracteres correspondente ao valor de retorno da `Error` função para o especificado `Number` , se essa cadeia de caracteres existir. Se a cadeia de caracteres não existir, `Description` conterá uma cadeia de caracteres de comprimento zero ("").|  
|`HelpFile`|A unidade, o caminho e o nome de arquivo totalmente qualificados do arquivo de ajuda Visual Basic apropriado.|  
|`HelpContext`|A ID de contexto do arquivo de ajuda Visual Basic apropriada para o erro correspondente à `Number` propriedade.|  
|`LastDLLError`|Zero.|  
  
 Se nenhum manipulador de erro existir, ou se nenhum estiver habilitado, uma mensagem de erro será criada e exibida nas `Err` Propriedades do objeto.  
  
> [!NOTE]
> Alguns aplicativos host Visual Basic não podem criar objetos. Consulte a documentação do aplicativo host para determinar se ele pode criar classes e objetos.  
  
## <a name="example"></a>Exemplo  

 Este exemplo usa a `Error` instrução para gerar o número de erro 11.  
  
```vb  
On Error Resume Next   ' Defer error handling.  
Error 11   ' Simulate the "Division by zero" error.  
```  
  
## <a name="requirements"></a>Requisitos  

 **Namespace:** [Microsoft. VisualBasic](../runtime-library-members.md)  
  
 **Assembly:** Visual Basic a biblioteca de tempo de execução (em Microsoft.VisualBasic.dll)  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.ErrObject.Clear%2A>
- <xref:Microsoft.VisualBasic.Information.Err%2A>
- <xref:Microsoft.VisualBasic.ErrObject.Raise%2A>
- [Instrução On Error](on-error-statement.md)
- [Instrução Resume](resume-statement.md)
- [Mensagens de erro](../error-messages/index.md)
