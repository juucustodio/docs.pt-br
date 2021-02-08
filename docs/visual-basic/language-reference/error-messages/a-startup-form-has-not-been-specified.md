---
description: 'Saiba mais sobre: um formulário de inicialização não foi especificado'
title: Não foi especificado um formulário de inicialização
ms.date: 07/20/2015
f1_keywords:
- vbrAppModel_NoStartupForm
ms.assetid: 8e04af49-4bef-49de-a7ec-e407e9873da7
ms.openlocfilehash: 4b00890f07121ef55ce49978842010cc54aba29b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99797179"
---
# <a name="a-startup-form-has-not-been-specified"></a>Não foi especificado um formulário de inicialização

O aplicativo usa a <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> classe, mas não especifica o formulário de inicialização.  
  
 Isso pode ocorrer se a caixa de seleção **habilitar estrutura de aplicativo** estiver marcada no designer de projeto, mas o **formulário de inicialização** não for especificado. Para obter mais informações, consulte [Página de aplicativo, Designer de Projeto (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic).  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1. Especifique um objeto de inicialização para o aplicativo.  
  
     Para obter mais informações, consulte [Página de aplicativo, Designer de Projeto (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic).  
  
2. Substitua o <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A> método para definir a <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A> propriedade para o formulário de inicialização.  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A>
- [Visão geral do modelo de aplicativo do Visual Basic](../../developing-apps/development-with-my/overview-of-the-visual-basic-application-model.md)
