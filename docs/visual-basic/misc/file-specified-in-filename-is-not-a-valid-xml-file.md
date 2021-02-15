---
description: 'Saiba mais sobre: o arquivo especificado em FileName não é um arquivo XML válido'
title: O arquivo especificado em FileName não é um arquivo XML válido
ms.date: 07/20/2015
ms.assetid: c4c30bf3-e0ad-4bc8-89e0-2c3e49e9793b
ms.openlocfilehash: c7d521986f3489345117a3947ed1e9b459af897e
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100472976"
---
# <a name="file-specified-in-filename-is-not-a-valid-xml-file"></a>O arquivo especificado em FileName não é um arquivo XML válido

O nome de arquivo que você forneceu não é um arquivo XML válido. Para especificar a estrutura permitida e o conteúdo de um documento XML, você pode usar um DTD (definição de tipo de documento), um esquema XDR (Microsoft XML-Data Reduced) ou um esquema XSD (linguagem de definição de esquema XML). Os esquemas XSD são a maneira preferida de especificar gramáticas XML no .NET Framework.

> [!NOTE]
> Em algumas versões anteriores do Visual Studio, o **XML Designer** é o designer para datasets tipados e esquema XML. O **Designer de XML** ainda pode ser usado para criar e editar arquivos de esquema XML. No entanto, no Visual Studio 2012, o designer para criar e editar DataSets tipados é a **Designer de conjunto de dados**. Para obter mais informações, consulte [criando e editando conjuntos de dados tipados](/previous-versions/visualstudio/visual-studio-2013/314t4see(v=vs.120)).

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Verifique se você está fornecendo o nome de arquivo correto.

- Verifique se o arquivo especificado contém um XML válido carregando o arquivo XML que você deseja verificar no **XML Designer**. No menu **XML** , clique em **validar XML**. Os erros são exibidos no **lista de tarefas**.

- Se o arquivo XML tiver um esquema XML associado, verifique se os elementos aparecem na estrutura definida e se o conteúdo dos elementos individuais está em conformidade com os tipos de dados declarados especificados no esquema.

## <a name="see-also"></a>Consulte também

- <xref:System.Xml>
- [Como: analisar caminhos de arquivo](../developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
