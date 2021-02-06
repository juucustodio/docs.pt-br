---
description: 'Saiba mais sobre: Depurando consultas LINQ to DataSet'
title: Consultas LINQ to DataSet de depuração
ms.date: 03/30/2017
ms.assetid: f4c54015-8ce2-4c5c-8d18-7038144cc66d
ms.openlocfilehash: f1293ba195c96d6868fdd5bfee50e8734f9cecc4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651217"
---
# <a name="debugging-linq-to-dataset-queries"></a>Consultas LINQ to DataSet de depuração

O Visual Studio dá suporte à depuração de código de LINQ to DataSet. No entanto, há algumas diferenças entre depuração LINQ to DataSet código e código não LINQ to DataSet gerenciado. A maioria dos recursos de depuração funciona com LINQ to DataSet instruções, incluindo a depuração, a definição de pontos de interrupção e a exibição de resultados que são mostrados nas janelas do depurador. No entanto, a execução de consulta adiada no tem alguns efeitos colaterais que você deve considerar ao depurar LINQ to DataSet código e há algumas limitações no uso de editar e continuar. Este tópico discute aspectos de depuração que são exclusivos para LINQ to DataSet em comparação com código não LINQ to DataSet gerenciado.  
  
## <a name="viewing-results"></a>Resultados de exibição  

 Você pode exibir o resultado de uma instrução de LINQ to DataSet usando DataTips, o janela Inspeção e a caixa de diálogo QuickWatch. Usando uma janela de origem, você pode pausar o ponteiro em uma consulta na janela de origem e um DataTip aparecerá. Você pode copiar uma variável LINQ to DataSet e colá-la no janela Inspeção ou na caixa de diálogo QuickWatch. No LINQ to DataSet, uma consulta não é avaliada quando é criada ou declarada, mas somente quando a consulta é executada. Isso é chamado de *execução adiada*. Portanto, a variável de consulta não tem um valor até que seja avaliada. Para obter mais informações, consulte [consultas no LINQ to DataSet](queries-in-linq-to-dataset.md).  
  
 O depurador deve avaliar uma consulta para exibir os resultados da consulta. Essa avaliação implícita ocorre quando você exibe um LINQ to DataSet resultado da consulta no depurador e tem alguns efeitos que você deve considerar. Cada avaliação de consulta leva tempo. Expandir o nó de resultados leva tempo. Para algumas consultas, a avaliação repetida pode causar uma caneta visível de desempenho. Avaliar uma consulta também pode causar efeitos colaterais, que são alterações ao valor de dados ou de estado do seu programa. Nem todas as consultas têm efeitos colaterais. Para determinar se uma consulta com segurança pode ser avaliada sem efeitos colaterais, você deve compreender o código que implementa a consulta. Para obter mais informações, consulte [efeitos colaterais e expressões](/previous-versions/visualstudio/visual-studio-2013/a7a250bs(v=vs.120)).  
  
## <a name="edit-and-continue"></a>Editar e continuar  

 Editar e continuar não oferece suporte a alterações em LINQ to DataSet consultas. Se você adicionar, remover ou alterar uma instrução de LINQ to DataSet durante uma sessão de depuração, será exibida uma caixa de diálogo informando que a alteração não é suportada por editar e continuar. Nesse ponto, você pode desfazer as alterações ou parar a sessão de depuração e reiniciar uma nova sessão com o código editado.  
  
 Além disso, editar e continuar não dá suporte à alteração do tipo ou do valor de uma variável usada em uma instrução LINQ to DataSet. Além disso, você pode desfazer as alterações ou parar e reiniciar a sessão de depuração.  
  
 No Visual C# no Visual Studio, você não pode usar Edit and Continue em nenhum código em um método que contenha uma consulta LINQ to DataSet.  
  
 Em Visual Basic no Visual Studio, você pode usar editar e continuar em código não LINQ to DataSet, mesmo em um método que contém uma consulta LINQ to DataSet. Você pode adicionar ou remover o código antes da instrução LINQ to DataSet, mesmo que as alterações afetem o número de linha da consulta LINQ to DataSet. Sua experiência de depuração de Visual Basic para código que não é de LINQ to DataSet permanece a mesma que antes LINQ to DataSet foi introduzida. Você não pode alterar, adicionar ou remover uma consulta LINQ to DataSet, no entanto, a menos que você interrompa a depuração para aplicar as alterações.  
  
## <a name="see-also"></a>Consulte também

- [Depurando código gerenciado](/visualstudio/debugger/debugging-managed-code)
- [Guia de programação](programming-guide-linq-to-dataset.md)
