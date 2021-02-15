---
description: 'Saiba mais sobre: kit de ferramentas de conjunto de regras externo'
title: Kit de ferramentas de Ruleset externo
ms.date: 03/30/2017
ms.assetid: a306d283-a031-475e-aa01-9ae86e7adcb0
ms.openlocfilehash: 41ee739ee90ba6dc1583369930919816e9afd53b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755376"
---
# <a name="external-ruleset-toolkit"></a>Kit de ferramentas de Ruleset externo

Normalmente quando as regras são usadas em um aplicativo de fluxo de trabalho, as regras são parte do assembly. Em algumas situações, convém manter o RuleSets separada do assembly de modo que eles possam ser atualizados sem recriar e implantar o assembly de fluxo de trabalho. Este exemplo permite que você gerencie e edite RuleSets em uma base de dados e acesse o RuleSets de um fluxo de trabalho em runtime. Isso permite que instâncias em execução de fluxo de trabalho para inserir automaticamente alterações de RuleSet.

O exemplo externo do kit de ferramentas de RuleSet contém uma ferramenta baseada em Windows que você pode usar para gerenciar e editar versões de RuleSet em uma base de dados. Ele também inclui uma atividade e um serviço de hospedagem para executar essas regras.

> [!NOTE]
> Este exemplo requer [Microsoft SQL Server](/sql).

O Visual Studio fornece um editor de RuleSet como parte do Windows Workflow Foundation (WF). Você pode iniciar o editor clicando duas vezes na atividade de `Policy` em um fluxo de trabalho; serializa o objeto definido de RuleSet para o arquivo de .rules associado com o fluxo de trabalho (uma atividade de `Policy` executa uma instância de RuleSet contra o fluxo de trabalho). O arquivo de .rules é compilado no assembly como um recurso quando você compila o projeto de fluxo de trabalho.

Componentes deste exemplo incluem:

- Uma ferramenta de interface gráfica do usuário de RuleSet que você pode usar para editar e gerenciar versões de RuleSet na base de dados.

- Um serviço de RuleSet que é configurado no aplicativo host e acesse RuleSets de base de dados.

- Uma atividade de `ExternalPolicy` que é um RuleSet de serviço de RuleSet e executa o RuleSet contra o fluxo de trabalho.

A interação dos componentes é mostrada na imagem a seguir. As seções a seguir descrevem cada componente.

![Diagrama mostrando a visão geral de exemplo do conjunto de ferramentas do RuleSet externo.](./media/external-ruleset-toolkit/ruleset-toolkit-overview.gif)

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ExternalRuleSetToolKit`

## <a name="ruleset-tool"></a>Ferramenta de RuleSet

A imagem a seguir é uma captura de tela da ferramenta RuleSet. No menu **repositório de regras** , você pode carregar os RuleSets disponíveis do banco de dados e salvar os RuleSets modificados de volta no repositório. Um arquivo de configuração do aplicativo fornece uma cadeia de caracteres de conexão de base de dados para o base de dados de RuleSet. Quando você inicia a ferramenta, carrega automaticamente o RuleSets de base de dados configurado.

![Captura de tela mostrando o navegador RuleSet.](./media/external-ruleset-toolkit/ruleset-browser-dialog.gif)

A ferramenta de RuleSet aplica o versão e números de versão secundária ao RuleSets, permitindo que você mantém simultaneamente e versões de armazenamento várias (a ferramenta não fornecer nenhum bloqueio ou outros recursos de gerenciamento de configuração além do recurso de controle de versão). Usando a ferramenta, você pode criar novas versões de RuleSet ou excluir versões existentes. Quando você clica em **novo**, a ferramenta cria um novo nome de conjunto de regras e aplica a versão 1,0. Quando você copiar uma versão, a ferramenta cria uma cópia da versão de RuleSet selecionada, incluindo as regras contidas, e atribuir novos, números de versão exclusivos. Esses números de versão são baseados em números de versão de RuleSets existente. Você pode alterar o nome e números de versão de RuleSet usando os campos associados no formulário.

Quando você clica em **Editar regras**, o editor de conjunto de regras é iniciado, conforme mostrado na imagem a seguir:

![Captura de tela mostrando o editor de conjunto de regras.](./media/external-ruleset-toolkit/ruleset-editor-dialog.gif)

Essa é uma nova hospedagem da caixa de diálogo do editor que faz parte do suplemento Windows Workflow Foundation Visual Studio. Fornece a mesma funcionalidade, incluindo suporte Intellisense. As regras são criadas em relação a um tipo de destino (como um fluxo de trabalho) associado ao conjunto de regras na ferramenta; Quando você clica em **procurar** na caixa de diálogo da ferramenta principal, a caixa de diálogo **seletor de fluxo de trabalho/tipo** é exibida, como mostra a Figura 4.

![Seleção de tipo de &#47;de fluxo de trabalho](./media/71f08d57-e8f2-499e-8151-ece2cbdcabfd.gif "71f08d57-e8f2-499e-8151-ece2cbdcabfd")

Figure 4: Seletor de fluxo de trabalho/tipo

Você pode usar a caixa de diálogo **seletor de fluxo de trabalho/tipo** para especificar um assembly e um tipo específico dentro desse assembly. Esse tipo é o tipo de destino com que as regras são criadas (e execução). Em muitos casos, o tipo de destino é um fluxo de trabalho ou qualquer outro tipo de atividade. No entanto, você pode executar um RuleSet contra qualquer tipo .NET.

O caminho para o arquivo de assembly e o conjunto de regras de tipo `name are stored with the` no banco de dados, de modo que, quando o RuleSet é recuperado do banco de dados, a ferramenta tenta carregar automaticamente o tipo de destino.

Quando você clica em **OK** na caixa de diálogo **seletor de fluxo de trabalho/tipo** , ele valida o tipo selecionado em relação ao conjunto de regras para garantir que o tipo de destino tenha todos os membros referenciados pelas regras. Os erros são mostrados em uma caixa de diálogo **erros de validação** . Você pode optar por continuar com a alteração, independentemente dos erros, ou clicar em **Cancelar**. No menu **ferramentas** na caixa de diálogo principal da ferramenta, você pode clicar em **validar** para validar novamente a versão do RuleSet em relação à atividade de destino.

![Captura de tela mostrando a caixa de diálogo erros de validação.](./media/external-ruleset-toolkit/validation-errors-dialog.png)

No menu **dados** da ferramenta, você pode importar e exportar conjuntos de regras. Quando você clica em **importar**, uma caixa de diálogo de escolha de arquivo é exibida, na qual você pode selecionar um arquivo. Rules. Ele pode ou não ser um arquivo inicialmente criado no Visual Studio. O arquivo de .rules deve conter uma instância serializada de `RuleDefinitions` que contém uma coleção de condições e uma coleção de RuleSets. A ferramenta não usa a coleção de condições, mas usa o `RuleDefinitions` formato. Rules para permitir a interação com o ambiente do Visual Studio.

Depois de selecionar um arquivo. Rules, uma caixa de diálogo **seletor de RuleSet** é exibida. Você pode usar a caixa de diálogo para selecionar o RuleSets do arquivo que você deseja importar (a opção especificar qualquer RuleSets). RuleSets no arquivo de .rules não tem números de versão, porque o controle de versão em um projeto de WF é o mesmo que a versão do assembly. Durante o processo de importação, a ferramenta atribui automaticamente o próximo número de versão principal disponível (que pode ser alterado após a importação); Você pode ver os números de versão atribuídos na lista **seletor de RuleSet** .

Para cada RuleSet importa, tentativas da ferramenta de localizar o tipo associado bin \ debug no local do arquivo de .rules (se existir), com base nos membros usados no RuleSet. Se a ferramenta encontrar vários tipos de correspondência, tentar escolha um tipo com base em uma correspondência entre o nome de arquivo .rules e o nome do tipo (por exemplo, o tipo de `Workflow1` corresponde a Workflow1.rules). Se as correspondências múltiplas existirem, você será solicitado para selecionar o tipo. Se esse mecanismo de identificação automática não conseguir localizar um tipo ou assembly correspondente, depois de importar, você poderá clicar em **procurar** na caixa de diálogo da ferramenta principal para navegar até o tipo associado. A imagem a seguir mostra o seletor de conjunto de regras:

![Captura de tela mostrando a caixa de diálogo Seletor de RuleSet.](./media/external-ruleset-toolkit/ruleset-selector-dialog.gif)

Quando você clica em **dados-exportar** no menu principal da ferramenta, a caixa de diálogo **seletor** do conjunto de regras é exibida novamente, na qual você pode determinar os conjuntos de regras do banco de dados que devem ser exportados. Quando você clica em **OK**, uma caixa de diálogo **salvar arquivo** é exibida, na qual você pode especificar o nome e o local do arquivo. Rules resultante. Porque o arquivo de .rules não contém informações de versão, você pode selecionar apenas uma versão de RuleSet com um determinado nome de RuleSet.

## <a name="policyfromservice-activity"></a>Atividade de PolicyFromService

O código para atividades de `PolicyFromService` é simples. Funciona bem como a atividade de `Policy` fornecida com o WF, mas em vez de recuperar o destino RuleSet do arquivo de .rules, chama um serviço de hospedagem para obter a instância de RuleSet. Execute o RuleSet contra a instância de atividade de fluxo de trabalho de raiz.

Para usar a atividade em um fluxo de trabalho, adicione uma referência a `PolicyActivities` e assemblies de `RuleSetService` do fluxo de trabalho projeto. Consulte o procedimento no final deste tópico para uma discussão sobre como adicionar a atividade a caixa de ferramentas.

Após a atividade colocado no fluxo de trabalho, você deve fornecer o nome de RuleSet a ser executado. Você pode inserir o nome como um valor literal, ou o associar a uma variável de fluxo de trabalho ou propriedade de outra atividade. Opcionalmente, você pode digitar números de versão para o RuleSet específico que deve ser executado. Se você deixar o valor padrão de 0 para os números de versão principal e secundário, o número de versão do último na base de dados é fornecida automaticamente para atividades.

## <a name="ruleset-service"></a>Serviço de RuleSet

O serviço é responsável por recuperar a versão especificada de RuleSet de base de dados dados e a atividade de chamada. Como discutido anteriormente, se os valores de versão principal e versão secundária passados na chamada de `GetRuleSet` são ambos 0, o serviço recupera a versão mais recente. Neste ponto, não há cachê de definições ou de instâncias de RuleSet; da mesma forma, não há nenhum recurso para marcar versões de RuleSet como “implantado para” diferenciá-las de RuleSets em andamento.

O base de dados a ser acessado pelo serviço deve ser configurado no host que usa um arquivo de configuração do aplicativo.

#### <a name="to-run-the-tool"></a>Para executar a ferramenta

1. A pasta que configura a tabela de RuleSet usado pela ferramenta e o serviço contém um arquivo de Setup.sql. Você pode executar o arquivo em lotes de Setup.cmd para criar o base de dados de regras em SQL express e configurar a tabela de RuleSet.

2. Se você editar o arquivo em lotes ou o Setup.sql e os especifica para não usar o SQL express ou não coloque a tabela em uma base de dados chamado algo diferente `Rules`, os arquivos de configuração do aplicativo na ferramenta de RuleSet e projetos de `UsageSample` devem ser editados com a mesma informações.

3. Depois que você execute o script de Setup.sql, você pode criar a solução de `ExternalRuleSetToolkit` e em iniciar a ferramenta de RuleSet de projeto de ExternalRuleSetTool.

4. A solução sequencial do aplicativo de console do fluxo de trabalho `RuleSetToolkitUsageSample` inclui um fluxo de trabalho de exemplo. O fluxo de trabalho consiste em uma atividade de `PolicyFromService` e duas variáveis, `orderValue` e `discount`, com que o destino RuleSet executa.

5. Para usar o exemplo, crie a solução de `RuleSetToolkitUsageSample` . Em seguida, no menu principal da ferramenta RuleSet, clique em **dados-importar** e aponte para o arquivo DiscountRuleSet. Rules na pasta RuleSetToolkitUsageSample Clique na opção de menu **repositório de regras-salvar** para salvar o conjunto de regras importado no banco de dados.

6. Porque o assembly de `PolicyActivities` é referenciado de projeto de fluxo de trabalho de exemplo, a atividade de `PolicyFromService` aparece no fluxo de trabalho. , No entanto, não aparece na caixa de ferramentas por padrão. Para adicioná-lo à caixa de ferramentas, faça o seguinte:

    - Clique com o botão direito do mouse na caixa de ferramentas e selecione **escolher itens** (isso pode levar algum tempo).

    - Quando a caixa de diálogo **escolher itens da caixa de ferramentas** for exibida, clique na guia **atividades** .

    - Navegue até o `PolicyActivities` assembly na `ExternalRuleSetToolkit` solução e clique em **abrir**.

    - Verifique se a `PolicyFromService` atividade está selecionada na caixa de diálogo **escolher itens da caixa de ferramentas** e clique em **OK**.

    - A atividade agora deve aparecer na caixa de ferramentas na categoria **componentes RuleSetToolkitUsageSample** .

7. O serviço de RuleSet já está configurado no host do aplicativo de console usando a seguinte declaração em Module.vb.

    ```csharp
    workflowRuntime.AddService(new RuleSetService());
    ```

8. Você também pode configurar o serviço no host que usa um arquivo de configuração; consulte a documentação SDK para obter detalhes.

9. Um arquivo de configuração do aplicativo é adicionado ao projeto de fluxo de trabalho especificar a cadeia de conexão para o base de dados é usado pelo serviço. Isso deve ser a mesma cadeia de conexão usada pela ferramenta de RuleSet, apontando para a base de dados que contém a tabela de RuleSet.

10. Agora você pode executar o projeto de `RuleSetToolkitUsageSample` como você faria qualquer outro aplicativo de console do fluxo de trabalho. Pressione F5 ou CTRL + F5 no Visual Studio ou execute o arquivo de RuleSetToolkitUsageSample.exe diretamente.

    > [!NOTE]
    > Você deve fechar a ferramenta de RuleSet para recompilar o exemplo de uso, porque a ferramenta carrega o assembly de exemplo de uso.
