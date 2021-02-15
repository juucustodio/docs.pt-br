---
description: 'Saiba mais sobre: Visual Basic convenções de codificação'
title: Convenções de codificação
ms.date: 07/20/2015
helpviewer_keywords:
- coding conventions [Visual Basic], Visual Basic
- examples [Visual Basic], coding conventions
- Visual Basic code, conventions
ms.assetid: c1df130b-fec6-49a5-becf-0a7e494a1d0f
ms.openlocfilehash: 424871ab0e77629ded977bd0be768ed8736d1761
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100460027"
---
# <a name="visual-basic-coding-conventions"></a>Convenções de codificação do Visual Basic

A Microsoft desenvolve exemplos e documentação que seguem as diretrizes neste tópico. Se você seguir as mesmas convenções de codificação, poderá obter os seguintes benefícios:  
  
- Seu código terá uma aparência consistente, para que os leitores possam se concentrar melhor no conteúdo, não no layout.  
  
- Os leitores entendem seu código mais rapidamente, pois eles podem fazer suposições com base na experiência anterior.  
  
- Você pode copiar, alterar e manter o código mais facilmente.  
  
- Você ajuda a garantir que seu código demonstre "práticas recomendadas" para Visual Basic.  
  
## <a name="naming-conventions"></a>Convenções de nomenclatura  
  
- Para obter informações sobre as diretrizes de nomenclatura, consulte o tópico [diretrizes de nomenclatura](../../../standard/design-guidelines/naming-guidelines.md) .  
  
- Não use "My" ou "My" como parte de um nome de variável. Essa prática cria confusão com os `My` objetos.  
  
- Você não precisa alterar os nomes dos objetos no código gerado automaticamente para que eles se adaptem às diretrizes.  
  
## <a name="layout-conventions"></a>Convenções de Layout  
  
- Inserir tabulações como espaços e usar recuo inteligente com recuos de quatro espaços.  
  
- Use a forma **bonita (reformatação) de código** para reformatar seu código no editor de códigos. Para obter mais informações, consulte [Opções, editor de texto, básico (Visual Basic)](/visualstudio/ide/reference/options-text-editor-basic-visual-basic).  
  
- Use apenas uma instrução por linha. Não use o caractere separador de linha Visual Basic (:).  
  
- Evite usar o caractere de continuação de linha explícito "_" em favor da continuação de linha implícita onde quer que o idioma o permita.  
  
- Use apenas uma declaração por linha.  
  
- Se a **listagem completa (reformatação) do código** não Formatar linhas de continuação automaticamente, recue manualmente as linhas de continuação uma parada de tabulação. No entanto, sempre os itens são alinhados à esquerda em uma lista.  
  
    ```vb  
    a As Integer,  
    b As Integer  
    ```  
  
- Adicione pelo menos uma linha em branco entre as definições de método e propriedade.  
  
## <a name="commenting-conventions"></a>Comentando Convenções  
  
- Coloque comentários em uma linha separada, em vez de no final de uma linha de código.  
  
- Inicie o texto de comentário com uma letra maiúscula e o texto de comentário final com um ponto.  
  
- Insira um espaço entre o delimitador de comentário (') e o texto do comentário.  
  
     [!code-vb[VbVbalrGuidelines#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#2)]  
  
- Não coloque comentários com blocos formatados de asteriscos.  
  
## <a name="program-structure"></a>Estrutura do programa  
  
- Ao usar o `Main` método, use a construção padrão para novos aplicativos de console e use `My` para argumentos de linha de comando.  
  
     [!code-vb[VbVbalrGuidelines#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#3)]  
  
## <a name="language-guidelines"></a>Diretrizes de Linguagem  
  
### <a name="string-data-type"></a>Tipo de dados da cadeia de caracteres  
  
- Use a [interpolação de cadeia de caracteres](../language-features/strings/interpolated-strings.md) para concatenar cadeias de caracteres curtas, como é mostrado no código a seguir.
  
     ```vb
     MsgBox($"hello{vbCrLf}goodbye")
     ```
  
- Para acrescentar cadeias de caracteres em loops, use o <xref:System.Text.StringBuilder> objeto.  
  
     [!code-vb[VbVbalrGuidelines#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#5)]  
  
### <a name="relaxed-delegates-in-event-handlers"></a>Delegados relaxados em manipuladores de eventos  

 Não qualifique explicitamente os argumentos (Object e EventArgs) para manipuladores de eventos. Se você não estiver usando os argumentos do evento que são passados para um evento (por exemplo, Sender As Object, e como EventArgs), use delegados relaxados e deixe os argumentos do evento em seu código:  
  
 [!code-vb[VbVbalrGuidelines#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#7)]  
  
### <a name="unsigned-data-type"></a>Tipo de Dados Sem Sinal  
  
- Use `Integer` tipos não assinados, exceto onde forem necessários.  
  
### <a name="arrays"></a>Matrizes  
  
- Use a sintaxe curta ao inicializar matrizes na linha da declaração. Por exemplo, use a sintaxe a seguir.  
  
     [!code-vb[VbVbalrGuidelines#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#8)]  
  
     Não use a sintaxe a seguir.  
  
     [!code-vb[VbVbalrGuidelines#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#9)]  
  
- Coloque o designador de matriz no tipo, não na variável. Por exemplo, use a seguinte sintaxe:  
  
     [!code-vb[VbVbalrGuidelines#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#11)]  
  
     Não use a seguinte sintaxe:  
  
     [!code-vb[VbVbalrGuidelines#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#10)]  
  
- Use a sintaxe {} ao declarar e inicializar matrizes de tipos de dados básicos. Por exemplo, use a seguinte sintaxe:  
  
     [!code-vb[VbVbalrGuidelines#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#12)]  
  
     Não use a seguinte sintaxe:  
  
     [!code-vb[VbVbalrGuidelines#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#13)]  
  
### <a name="use-the-with-keyword"></a>Usar a palavra-chave with  

 Quando você faz uma série de chamadas para um objeto, considere usar a `With` palavra-chave:  
  
 [!code-vb[VbVbalrGuidelines#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#15)]  
  
### <a name="use-the-trycatch-and-using-statements-when-you-use-exception-handling"></a>Use a tentativa... Capturar e usar instruções ao usar a manipulação de exceções  

 Não use `On Error Goto`.  
  
### <a name="use-the-isnot-keyword"></a>Usar a palavra-chave IsNot  

 Use a `IsNot` palavra-chave em vez de `Not...Is Nothing` .  
  
### <a name="new-keyword"></a>Nova palavra-chave  
  
- Use a instanciação curta. Por exemplo, use a seguinte sintaxe:  
  
     [!code-vb[VbVbalrGuidelines#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#21)]  
  
     A linha anterior é equivalente a esta:  
  
     [!code-vb[VbVbalrGuidelines#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#22)]  
  
- Use inicializadores de objeto para novos objetos em vez do construtor sem parâmetros:  
  
     [!code-vb[VbVbalrGuidelines#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#23)]  
  
### <a name="event-handling"></a>Tratamento de Evento  
  
- Use `Handles` em vez de `AddHandler` :  
  
     [!code-vb[VbVbalrGuidelines#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#24)]  
  
- Use `AddressOf` e não instancie explicitamente o delegado:  
  
     [!code-vb[VbVbalrGuidelines#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#25)]  
  
- Quando você define um evento, usa a sintaxe curta e permite que o compilador defina o delegado:  
  
     [!code-vb[VbVbalrGuidelines#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#26)]  
  
- Não verifique se um evento é `Nothing` (nulo) antes de chamar o `RaiseEvent` método. `RaiseEvent` verifica `Nothing` antes de gerar o evento.  
  
### <a name="using-shared-members"></a>Usando membros compartilhados  

 Chame `Shared` membros usando o nome da classe, não de uma variável de instância.  
  
### <a name="use-xml-literals"></a>Usar literais XML  

 Os literais XML simplificam as tarefas mais comuns que você encontrar ao trabalhar com XML (por exemplo, carregar, consultar e transformar). Ao desenvolver com XML, siga estas diretrizes:  
  
- Use literais XML para criar documentos e fragmentos XML em vez de chamar APIs XML diretamente.  
  
- Importe namespaces XML no nível de arquivo ou projeto para aproveitar as otimizações de desempenho para literais XML.  
  
- Use as propriedades do eixo XML para acessar elementos e atributos em um documento XML.  
  
- Use expressões inseridas para incluir valores e para criar XML a partir de valores existentes em vez de usar chamadas de API, como o `Add` método:  
  
     [!code-vb[VbVbalrGuidelines#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#27)]  
  
### <a name="linq-queries"></a>Consultas LINQ  
  
- Use nomes significativos para variáveis de consulta:  
  
     [!code-vb[VbVbalrGuidelines#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#28)]  
  
- Forneça nomes para elementos em uma consulta para garantir que os nomes de propriedade de tipos anônimos sejam colocados em maiúsculas corretamente usando a embalagem do Pascal:  
  
     [!code-vb[VbVbalrGuidelines#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#29)]  
  
- Renomeie propriedades quando os nomes de propriedades no resultado forem ambíguos. Por exemplo, se sua consulta retornar um nome de cliente e uma ID de pedido, renomeie-os em vez de deixá-los como `Name` e `ID` no resultado:  
  
     [!code-vb[VbVbalrGuidelines#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#30)]  
  
- Use a inferência de tipos na declaração de variáveis de consulta e variáveis de intervalo:  
  
     [!code-vb[VbVbalrGuidelines#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#31)]  
  
- Alinhar cláusulas de consulta na `From` instrução:  
  
     [!code-vb[VbVbalrGuidelines#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#32)]  
  
- Use `Where` cláusulas antes de outras cláusulas de consulta para que as cláusulas de consulta posteriores operem no conjunto de dados filtrado:  
  
     [!code-vb[VbVbalrGuidelines#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#33)]  
  
- Use a `Join` cláusula para definir explicitamente uma operação JOIN em vez de usar a `Where` cláusula para definir implicitamente uma operação JOIN:  
  
     [!code-vb[VbVbalrGuidelines#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#34)]  
  
## <a name="see-also"></a>Consulte também

- [Diretrizes de codificação segura](../../../standard/security/secure-coding-guidelines.md)
