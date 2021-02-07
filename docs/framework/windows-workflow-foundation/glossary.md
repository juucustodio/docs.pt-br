---
description: 'Saiba mais sobre: Windows Workflow Foundation glossário para .NET Framework 4,5'
title: Windows Workflow Foundation Glossary for .NET Framework 4.5 (Glossário do Windows Workflow Foundation para .NET Framework 4.5)
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Workflow Foundation [WF], glossary
- WF [WF], glossary
ms.assetid: ab682b2f-3779-45ca-b831-b7c03d7dbb3a
ms.openlocfilehash: 5339b3236a901e51a196aae7597aa2764bbd1c61
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99742258"
---
# <a name="windows-workflow-foundation-glossary-for-net-framework-45"></a>Windows Workflow Foundation Glossary for .NET Framework 4.5 (Glossário do Windows Workflow Foundation para .NET Framework 4.5)

Os termos a seguir são usados na documentação do Windows Workflow Foundation.

## <a name="terms"></a>Termos

|Termo|Definição|
|----------|----------------|
|activity|Uma unidade de comportamento do programa no Windows Workflow Foundation. Atividades únicas podem ser compostas em atividades mais complexas.|
|ação de atividade|Uma estrutura de dados usada para expor retornos de chamada para execução de fluxo de trabalho e atividade.|
|argumento|Define o fluxo de dados para dentro e fora de uma atividade. Cada argumento tem uma direção especificada: in, out ou in/out/out. Eles representam os parâmetros de entrada, saída e entrada/saída da atividade.|
|indicador|O ponto no qual uma atividade pode pausar e aguardar para ser retomada.|
|anos|Um grupo de ações projetadas para desfazer ou atenuar o efeito do trabalho concluído anteriormente.|
|exata|O mecanismo para rotear mensagens para um fluxo de trabalho ou instância de serviço.|
|expressão|Uma construção que usa um ou mais argumentos, executa uma operação nos argumentos e retorna um único valor. As expressões podem ser usadas em qualquer lugar em que uma atividade possa ser usada.|
|fazem|Um paradigma de modelagem conhecido que representa componentes de programa como símbolos vinculados com setas direcionais.  No .NET Framework 4, os fluxos de trabalho podem ser modelados como fluxogramas usando a atividade FlowChart.|
|processo de execução longa|Uma unidade de execução do programa que não retorna imediatamente e pode abranger as reinicializações do sistema.|
|persistência|Salvar o estado de um fluxo de trabalho ou serviço em um meio durável, para que ele possa ser descarregado da memória ou recuperado após uma falha do sistema.|
|computador de estado|Um paradigma de modelagem conhecido que representa componentes de programa como Estados individuais vinculados com transições de estado orientadas a eventos.  Os fluxos de trabalho podem ser modelados como máquinas de estado usando a atividade StateMachine.|
|substância|Representa um grupo de indicadores relacionados em um identificador comum e permite que o tempo de execução tome decisões sobre se uma continuação específica do indicador é válida ou se pode se tornar válida.|
|conversor de tipo|Um tipo de CLR pode ser associado com um ou mais tipos derivados System.ComponentModel.TypeConverter que permitem converter instâncias do tipo da CLR e instâncias de outros tipos. Um conversor de tipo é associado a um tipo CLR usando o atributo System. ComponentModel. TypeConverterAttribute.  Um TypeConverterAttribute pode ser especificado diretamente no tipo de CLR ou propriedade. Um conversor de tipo especificado em uma propriedade sempre tem precedência sobre um conversor de tipo especificado no tipo de CLR de propriedade.|
|variável|Representa o armazenamento de alguns dados que devem ser salvos e acessados posteriormente.|
|fluxo de trabalho|Uma única atividade ou árvore de atividades invocada por um processo de host.|
|XAML|extensible application marcação idioma|
