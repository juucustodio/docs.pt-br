---
description: 'Saiba mais sobre: Criando e usando componentes no Visual Basic'
title: Como criar e usar componentes
ms.date: 07/20/2015
helpviewer_keywords:
- components [Visual Basic]
ms.assetid: ee6a4156-73f7-4e9b-8e01-c74c4798b65c
ms.openlocfilehash: f59b4774556d95dcbc1befb16409d68a51c50535
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99666583"
---
# <a name="creating-and-using-components-in-visual-basic"></a>Criando e usando componentes no Visual Basic

Um *componente* é uma classe que implementa a interface <xref:System.ComponentModel.IComponent?displayProperty=nameWithType> ou que deriva direta ou indiretamente de uma classe que implementa <xref:System.ComponentModel.IComponent>. Um componente do .NET é um objeto que é reutilizável, pode interagir com outros objetos e fornece controle sobre os recursos externos e o suporte a tempo de design.  
  
 Um recurso importante dos componentes é que eles são projetáveis, o que significa que uma classe que é um componente pode ser usada no ambiente de desenvolvimento integrado do Visual Studio. Um componente pode ser adicionado à Caixa de Ferramentas, arrastado e solto em um formulário e manipulado em uma superfície de design. O suporte de tempo de design base para componentes é incorporado ao .NET. Um desenvolvedor de componentes não precisa fazer nenhum trabalho adicional para aproveitar a funcionalidade de tempo de design base.  
  
 Um *controle* é semelhante a um componente, pois ambos são projetáveis. No entanto, um controle fornece uma interface do usuário, enquanto que um componente não. Um controle deve derivar de uma das classes de controle base: <xref:System.Windows.Forms.Control> ou <xref:System.Web.UI.Control>.  
  
## <a name="when-to-create-a-component"></a>Quando criar um componente  

 Se sua classe for ser usada em uma superfície de design (como o Designer do Windows Forms ou do Web Forms), mas não tiver uma interface do usuário, ela deverá ser um componente e implementar <xref:System.ComponentModel.IComponent> ou derivar de uma classe que implementa, direta ou indiretamente, <xref:System.ComponentModel.IComponent>.  
  
 As classes <xref:System.ComponentModel.Component> e <xref:System.ComponentModel.MarshalByValueComponent> são implementações base da interface <xref:System.ComponentModel.IComponent>. A principal diferença entre essas classes é que o marshaling da classe <xref:System.ComponentModel.Component> é realizado por referência, enquanto o marshaling de <xref:System.ComponentModel.IComponent> é realizado por valor. A lista a seguir fornece diretrizes amplas para os implementadores.  
  
- Se o seu componente precisar ter o marshaling realizado por referência, derive de <xref:System.ComponentModel.Component>.  
  
- Se o seu componente precisar ter o marshaling realizado por valor, derive de <xref:System.ComponentModel.MarshalByValueComponent>.  
  
- Se o seu componente não puder derivar de uma das implementações de base devido a herança única, implemente <xref:System.ComponentModel.IComponent>.  
  
## <a name="component-classes"></a>Classes de componentes  

 O namespace <xref:System.ComponentModel> fornece classes que são usadas para implementar o comportamento de tempo de design e tempo de execução de componentes e controles. Este namespace inclui as classes e interfaces base para implementar atributos e conversores de tipo, associar a fontes de dados e licenciar componentes.  
  
 As classes de componente principais são:  
  
- <xref:System.ComponentModel.Component>. Uma implementação base para a interface <xref:System.ComponentModel.IComponent>. Essa classe habilita o compartilhamento de objeto entre aplicativos.  
  
- <xref:System.ComponentModel.MarshalByValueComponent>. Uma implementação base para a interface <xref:System.ComponentModel.IComponent>.  
  
- <xref:System.ComponentModel.Container>. A implementação base para a interface <xref:System.ComponentModel.IContainer>. Essa classe encapsula zero ou mais componentes.  
  
 Algumas das classes usadas para licenciamento de componentes são:  
  
- <xref:System.ComponentModel.License>. A classe base abstrata para todas as licenças. Uma licença é concedida a uma instância específica de um componente.  
  
- <xref:System.ComponentModel.LicenseManager>. Fornece propriedades e métodos para adicionar uma licença a um componente e gerenciar um <xref:System.ComponentModel.LicenseProvider>.  
  
- <xref:System.ComponentModel.LicenseProvider>. A classe base abstrata para implementar um provedor de licença.  
  
- <xref:System.ComponentModel.LicenseProviderAttribute>. Especifica a classe <xref:System.ComponentModel.LicenseProvider> a ser usada com uma classe.  
  
 Classes normalmente usadas para descrever e persistir componentes.  
  
- <xref:System.ComponentModel.TypeDescriptor>. Fornece informações sobre as características de um componente, como atributos, propriedades e eventos.  
  
- <xref:System.ComponentModel.EventDescriptor>. Fornece informações sobre um evento.  
  
- <xref:System.ComponentModel.PropertyDescriptor>. Fornece informações sobre uma propriedade.  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Solução de problemas de criação de controle e de componente](/dotnet/desktop/winforms/controls/troubleshooting-control-and-component-authoring)  
 Explica como corrigir problemas comuns.  
  
## <a name="see-also"></a>Consulte também

- [Como acessar o suporte a tempo de design no Windows Forms](/dotnet/desktop/winforms/controls/developing-windows-forms-controls-at-design-time)
