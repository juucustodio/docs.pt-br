---
description: 'Saiba mais sobre: como exibir erros de validação em um designer rehospedado'
title: 'Como: exibir erros de validação em um designer com hospedagem alterada'
ms.date: 03/30/2017
ms.assetid: 5aa8fb53-8f75-433b-bc06-7c7d33583d5d
ms.openlocfilehash: 75ff45e6e9a81df96a9940ce21d1b160cab1000e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99777730"
---
# <a name="how-to-display-validation-errors-in-a-rehosted-designer"></a>Como: exibir erros de validação em um designer com hospedagem alterada

Este tópico descreve como recuperar e publicar erros de validação em uma Designer de Fluxo de Trabalho do Windows rehospedada. Isso fornece-nos com um procedimento para confirmar que um fluxo de trabalho em um designer rehosted é válido.  
  
 Esta tarefa tem duas partes. O primeiro é fornecer uma implementação <xref:System.Activities.Presentation.Validation.IValidationErrorService>.  Há um método importante para implementar essa interface, o <xref:System.Activities.Presentation.Validation.IValidationErrorService.ShowValidationErrors%2A> que o transmitirão uma lista de objetos <xref:System.Activities.Presentation.Validation.ValidationErrorInfo> que contêm informações sobre os erros ao log de depuração.  Após implementado a interface, você recupera informações de erro publicar uma instância dessa implementação para o contexto de edição.  
  
### <a name="implement-the-ivalidationerrorservice-interface"></a>Implementar a interface de IValidationErrorService  
  
1. Aqui está um exemplo de código para uma implementação simples que grava para fora os erros de validação para o log de depuração.  
  
    ```csharp  
    using System.Activities.Presentation.Validation;  
    using System.Collections.Generic;  
    using System.Diagnostics;  
    using System.Linq;  
  
    namespace VariableFinderShell  
    {  
        class DebugValidationErrorService : IValidationErrorService  
        {  
            public void ShowValidationErrors(IList<ValidationErrorInfo> errors)  
            {  
                errors.ToList().ForEach(vei => Debug.WriteLine($"Error: {vei.Message}"));  
            }  
        }  
    }  
    ```  
  
### <a name="publishing-to-the-editing-context"></a>Publicação ao contexto de edição  
  
1. Aqui está o código que irá publicar esse ao contexto de edição.  
  
    ```csharp  
    wd.Context.Services.Publish<IValidationErrorService>(new DebugValidationErrorService());  
    ```
