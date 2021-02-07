---
description: 'Saiba mais sobre: etapas típicas para usar LINQ to SQL'
title: Etapas comuns de uso do LINQ to SQL
ms.date: 03/30/2017
ms.assetid: 9a88bd51-bd74-48f7-a9b1-f650e8d55a3e
ms.openlocfilehash: eb35b983471db8926646418352b01e1186e235e6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99680961"
---
# <a name="typical-steps-for-using-linq-to-sql"></a>Etapas comuns de uso do LINQ to SQL

Para implementar um aplicativo [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], siga as etapas descritas mais adiante neste tópico. Observe que várias etapas são opcionais. É muito provável que você possa usar o modelo de objeto em seu estado padrão.  
  
 Para um início realmente rápido, use o Object Relational Designer para criar o modelo de objeto e começar a codificar suas consultas.  
  
## <a name="creating-the-object-model"></a>Criando o modelo de objeto  

 A primeira etapa é criar um modelo de objeto a partir dos metadados de um banco de dados relacional existente. O modelo de objeto representa o banco de dados de acordo com a linguagem de programação do desenvolvedor. Para obter mais informações, consulte [o modelo de objeto LINQ to SQL](the-linq-to-sql-object-model.md).  
  
### <a name="1-select-a-tool-to-create-the-model"></a>1. Selecione uma ferramenta para criar o modelo.  

 Três ferramentas estão disponíveis para criar o modelo.  
  
- O Object Relational Designer  
  
     Esse designer fornece uma interface de usuário perfeita para criar um modelo de objeto a partir de um banco de dados existente. Essa ferramenta faz parte do IDE do Visual Studio e é mais adequada para bancos de dados pequenos ou médios.  
  
- A ferramenta de geração de código SQLMetal  
  
     Esse utilitário de linha de comando fornece um conjunto ligeiramente diferente de opções do o/R Designer. A modelagem de grandes bancos de dados é mais bem efetuada com essa ferramenta. Para obter mais informações, consulte [SqlMetal.exe (ferramenta de geração de código)](../../../../tools/sqlmetal-exe-code-generation-tool.md).  
  
- Um editor de código  
  
     Você pode escrever seu próprio código usando o editor de código do Visual Studio ou outro editor. Não recomendamos essa abordagem, que pode ser propenso a erros, quando você tem um banco de dados existente e pode usar o o/R Designer ou a ferramenta SqlMetal. Entretanto, o editor de códigos pode ser útil para refinar ou modificar o código que você já gerou usando outras ferramentas. Para obter mais informações, consulte [como: Personalizar classes de entidade usando o editor de código](how-to-customize-entity-classes-by-using-the-code-editor.md).  
  
### <a name="2-select-the-kind-of-code-you-want-to-generate"></a>2. Selecione o tipo de código que você deseja gerar.  
  
- Um arquivo de código-fonte do C# ou Visual Basic para mapeamento baseado em atributo.  
  
     Em seguida, você inclui esse arquivo de código em seu projeto do Visual Studio. Para obter mais informações, consulte [mapeamento baseado em atributo](attribute-based-mapping.md).  
  
- Um arquivo XML para mapeamento externo.  
  
     Usando essa abordagem, você pode manter os metadados de mapeamento fora de seu código de aplicativo. Para obter mais informações, consulte [mapeamento externo](external-mapping.md).  
  
    > [!NOTE]
    > O o/R Designer não oferece suporte à geração de arquivos de mapeamento externos. Você deve usar a ferramenta SQLMetal para implementar esse recurso.  
  
- Um arquivo DBML, que você pode modificar antes de gerar um arquivo de código final.  
  
     Esse é um recurso avançado.  
  
### <a name="3-refine-the-code-file-to-reflect-the-needs-of-your-application"></a>3. Refine o arquivo de código para refletir as necessidades do seu aplicativo.  

 Para essa finalidade, você pode usar o o/R Designer ou o editor de código.  
  
## <a name="using-the-object-model"></a>Usando o modelo de objeto  

 A ilustração a seguir mostra a relação entre o desenvolvedor e os dados em um cenário de duas camadas. Para outros cenários, consulte [N-tier e aplicativos remotos com LINQ to SQL](n-tier-and-remote-applications-with-linq-to-sql.md).  
  
 ![Captura de tela que mostra o modelo de objeto LINQ.](./media/the-linq-to-sql-object-model/linq-object-model-two-tier.png)  
  
 Agora que você tem o modelo de objeto, você descreve as solicitações de informações e manipula dados dentro desse modelo. Você pensa em termos de objetos e propriedades no seu modelo de objeto e não em termos de linhas e colunas do banco de dados. Você não lida diretamente com o banco de dados.  
  
 Quando você instruir [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] a executar uma consulta que você descreveu ou chamar `SubmitChanges()` em dados que você manipulou, o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] se comunicará com o Database no idioma do banco de dados.  
  
 A seguir estão etapas comuns de uso do modelo de objeto que você criou.  
  
### <a name="1-create-queries-to-retrieve-information-from-the-database"></a>1. crie consultas para recuperar informações do banco de dados.  

 Para obter mais informações, consulte [conceitos de consulta](query-concepts.md) e exemplos de [consulta](query-examples.md).  
  
### <a name="2-override-default-behaviors-for-insert-update-and-delete"></a>2. substituir os comportamentos padrão para inserir, atualizar e excluir.  

 Essa etapa é opcional. Para obter mais informações, consulte [Personalizando as operações de inserção, atualização e exclusão](customizing-insert-update-and-delete-operations.md).  
  
### <a name="3-set-appropriate-options-to-detect-and-report-concurrency-conflicts"></a>3. Defina as opções apropriadas para detectar e relatar conflitos de simultaneidade.  

 Você pode deixar o modelo com seus valores padrão para manipular conflitos de simultaneidade, ou pode alterá-lo para atender aos seus propósitos. Para obter mais informações, consulte [como especificar quais membros são testados para conflitos de simultaneidade](how-to-specify-which-members-are-tested-for-concurrency-conflicts.md) e [como especificar quando exceções de simultaneidade são geradas](how-to-specify-when-concurrency-exceptions-are-thrown.md).  
  
### <a name="4-establish-an-inheritance-hierarchy"></a>4. estabeleça uma hierarquia de herança.  

 Essa etapa é opcional. Para obter mais informações, consulte [suporte à herança](inheritance-support.md).  
  
### <a name="5-provide-an-appropriate-user-interface"></a>5. forneça uma interface do usuário apropriada.  

 Esta etapa é opcional, e depende de como o aplicativo será usado.  
  
### <a name="6-debug-and-test-your-application"></a>6. depure e teste seu aplicativo.  

 Para obter mais informações, consulte [depuração de suporte](debugging-support.md).  
  
## <a name="see-also"></a>Consulte também

- [Introdução](getting-started.md)
- [Criando o modelo de objeto](creating-the-object-model.md)
- [Procedimentos armazenados](stored-procedures.md)
