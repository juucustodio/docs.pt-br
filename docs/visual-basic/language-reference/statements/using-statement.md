---
description: 'Saiba mais sobre a instrução: using (Visual Basic)'
title: Instrução Using
ms.date: 07/20/2015
f1_keywords:
- vb.using
helpviewer_keywords:
- resource disposal
- Try...Catch...Finally statements, equivalent to Using statement
- resources [Visual Basic], disposing
- Using statement [Visual Basic]
ms.assetid: 665d1580-dd54-4e96-a9a9-6be2a68948f1
ms.openlocfilehash: fea77a441182b7c3ecac58d4fe7f1297a87f086c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99740880"
---
# <a name="using-statement-visual-basic"></a>Instrução Using (Visual Basic)

Declara o início de um `Using` bloco e, opcionalmente, adquire os recursos do sistema que o bloco controla.

## <a name="syntax"></a>Syntax

```vb
Using { resourcelist | resourceexpression }
    [ statements ]
End Using
```

## <a name="parts"></a>Partes

|Termo|Definição|  
|---|---|  
|`resourcelist`|Necessário se você não fornecer `resourceexpression` . Lista de um ou mais recursos do sistema que esse `Using` bloco controla, separados por vírgulas.|  
|`resourceexpression`|Necessário se você não fornecer `resourcelist` . Variável ou expressão de referência que se refere a um recurso do sistema a ser controlado por este `Using` bloco.|  
|`statements`|Opcional. Bloco de instruções que o `Using` bloco executa.|  
|`End Using`|Obrigatório. Encerra a definição do `Using` bloco e descarta todos os recursos que ele controla.|  

 Cada recurso na `resourcelist` parte tem a seguinte sintaxe e partes:

 `resourcename As New resourcetype [ ( [ arglist ] ) ]`

 -ou-

 `resourcename As resourcetype = resourceexpression`

## <a name="resourcelist-parts"></a>Partes da resourceList

|Termo|Definição|  
|---|---|  
|`resourcename`|Obrigatório. Variável de referência que se refere a um recurso do sistema que o `Using` bloco controla.|  
|`New`|Obrigatório se a `Using` instrução adquire o recurso. Se você já tiver adquirido o recurso, use a segunda sintaxe alternativa.|  
|`resourcetype`|Obrigatório. A classe do recurso. A classe deve implementar a <xref:System.IDisposable> interface.|  
|`arglist`|Opcional. Lista de argumentos que você está passando para o construtor para criar uma instância do `resourcetype` . Consulte a [lista de parâmetros](parameter-list.md).|  
|`resourceexpression`|Obrigatório. Variável ou expressão referente a um recurso do sistema que atende aos requisitos do `resourcetype` . Se você usar a segunda alternativa de sintaxe, deverá adquirir o recurso antes de passar o controle para a `Using` instrução.|  
  
## <a name="remarks"></a>Comentários

 Às vezes, seu código requer um recurso não gerenciado, como um identificador de arquivo, um wrapper COM ou uma conexão SQL. Um `Using` bloco garante a eliminação de um ou mais desses recursos quando seu código é concluído com eles. Isso os torna disponíveis para uso de outro código.

 Os recursos gerenciados são descartados pelo GC (coletor de lixo .NET Framework) sem qualquer codificação extra de sua parte. Você não precisa de um `Using` bloco para recursos gerenciados. No entanto, você ainda pode usar um `Using` bloco para forçar a eliminação de um recurso gerenciado em vez de aguardar o coletor de lixo.

 Um `Using` bloco tem três partes: aquisição, uso e alienação.

- A *aquisição* significa criar uma variável e inicializá-la para se referir ao recurso do sistema. A `Using` instrução pode adquirir um ou mais recursos ou você pode adquirir exatamente um recurso antes de inserir o bloco e fornecê-lo à `Using` instrução. Se você fornecer `resourceexpression` , deverá adquirir o recurso antes de passar o controle para a `Using` instrução.

- O *uso* significa acessar os recursos e executar ações com eles. As instruções entre `Using` e `End Using` representam o uso dos recursos.

- *Alienação* significa chamar o <xref:System.IDisposable.Dispose%2A> método no objeto em `resourcename` . Isso permite que o objeto termine corretamente seus recursos. A `End Using` instrução descarta os recursos sob o `Using` controle do bloco.

## <a name="behavior"></a>Comportamento

 Um `Using` bloco se comporta como uma `Try` construção... `Finally` na qual o `Try` bloco usa os recursos e o `Finally` bloco os descarta. Por isso, o `Using` bloqueio garante a alienação dos recursos, independentemente de como você sai do bloco. Isso é verdadeiro mesmo no caso de uma exceção sem tratamento, exceto para um <xref:System.StackOverflowException> .

 O escopo de cada variável de recurso adquirido pela `Using` instrução é limitado ao `Using` bloco.

 Se você especificar mais de um recurso do sistema na `Using` instrução, o efeito será o mesmo que se você tiver aninhado `Using` blocos um dentro de outro.

 Se `resourcename` for `Nothing` , nenhuma chamada para <xref:System.IDisposable.Dispose%2A> será feita e nenhuma exceção será lançada.

## <a name="structured-exception-handling-within-a-using-block"></a>Manipulação de exceção estruturada dentro de um bloco Using

 Se você precisar manipular uma exceção que pode ocorrer dentro do `Using` bloco, você pode adicionar uma `Try` construção... completa `Finally` . Se você precisar lidar com o caso em que a `Using` instrução não é bem-sucedida ao adquirir um recurso, você pode testar para ver se `resourcename` é `Nothing` .

## <a name="structured-exception-handling-instead-of-a-using-block"></a>Manipulação de exceção estruturada em vez de um bloco Using

 Se precisar de um controle mais preciso sobre a aquisição dos recursos ou se precisar de código adicional no `Finally` bloco, você poderá reescrever o `Using` bloco como uma `Try` construção.... `Finally` O exemplo a seguir mostra o esqueleto `Try` e as `Using` construções que são equivalentes na aquisição e na alienação de `resource` .

```vb
Using resource As New resourceType
    ' Insert code to work with resource.
End Using

' For the acquisition and disposal of resource, the following  
' Try construction is equivalent to the Using block.
Dim resource As New resourceType
Try
    ' Insert code to work with resource.
Finally
    If resource IsNot Nothing Then
        resource.Dispose()
    End If
End Try
```

> [!NOTE]
> O código dentro do `Using` bloco não deve atribuir o objeto em `resourcename` outra variável. Quando você sai do `Using` bloco, o recurso é Descartado e a outra variável não pode acessar o recurso ao qual ele aponta.

## <a name="example"></a>Exemplo

 O exemplo a seguir cria um arquivo chamado log.txt e grava duas linhas de texto no arquivo. O exemplo também lê o mesmo arquivo e exibe as linhas de texto:

 Como as <xref:System.IO.TextWriter> <xref:System.IO.TextReader> classes e implementam a <xref:System.IDisposable> interface, o código pode usar `Using` instruções para garantir que o arquivo seja fechado corretamente após as operações de gravação e leitura.

 [!code-vb[VbVbalrStatements#50](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#50)]

## <a name="see-also"></a>Consulte também

- <xref:System.IDisposable>
- [Instrução Try...Catch...Finally](try-catch-finally-statement.md)
- [Como descartar um recurso do sistema](../../programming-guide/language-features/control-flow/how-to-dispose-of-a-system-resource.md)
