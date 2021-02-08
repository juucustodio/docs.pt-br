---
description: 'Saiba mais sobre: Configurando a validação da atividade'
title: Configurando a validação de atividades
ms.date: 03/30/2017
ms.assetid: 25a4eccb-b8fc-4857-a01d-2683b6341219
ms.openlocfilehash: 9e40842a18dd2afd9a5ec0104d66e8971d691b5f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792746"
---
# <a name="configuring-activity-validation"></a>Configurando a validação de atividades

Validação de atividade autores e permite que usuários da atividade para identificar e relatar erros na configuração de uma atividade antes da execução. Windows Workflow Foundation (WF) fornece os três tipos de validação de atividade a seguir:  
  
- `RequiredArgument` e atributos de `OverloadGroup` .  
  
- Validação classe base imperativa.  
  
- Restrições declarativas.  
  
 `RequiredArgument` e atributos de `OverloadGroup` indicam que determinados argumentos em uma atividade são necessários. A validação classe base imperativa fornece uma maneira simples para uma atividade fornece validação sobre se, e restrições declarativas permitem a validação sobre a atividade e sua relação com o fluxo de trabalho contém. Se uma atividade não é configurado corretamente de acordo com os requisitos de validação, erros e avisos de validação são retornados. Se um trabalho de que são criados usando o designer de trabalho, todos os erros e avisos de validação são exibidos no designer. Se o trabalho são criados fora do designer de trabalho todos os erros de validação são retornados quando o fluxo de trabalho é chamado. Independentemente de como funciona foram criados, um trabalho com erros de validação são permitidos nunca executar. Esta seção fornece uma visão geral desses tipos de validação de atividade e como validação de atividade é chamada.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Argumentos necessários e grupos de sobrecarga](required-arguments-and-overload-groups.md)  
 Descreve como usar atributos de `RequiredArgument` e de `OverloadGroup` para fornecer validação.  
  
 [Validação classe base imperativa](imperative-code-based-validation.md)  
 Descreve como usar a validação classe base para <xref:System.Activities.CodeActivity> e atividades com base <xref:System.Activities.NativeActivity> .  
  
 [Restrições declarativas](declarative-constraints.md)  
 Descreve como usar restrições declarativas para fornecer validação complexa de atividade.  
  
 [Invocando a validação de atividades](invoking-activity-validation.md)  
 Discute quando a validação de atividade é chamado automaticamente e como chamar explicitamente validação.  
  
## <a name="reference"></a>Referência  
  
## <a name="related-sections"></a>Seções relacionadas
