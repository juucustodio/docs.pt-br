---
description: 'Saiba mais sobre: procedimentos de solução de problemas (Visual Basic)'
title: Procedimentos de solução de problemas
ms.date: 07/20/2015
helpviewer_keywords:
- troubleshooting Visual Basic, procedures
- procedures [Visual Basic], troubleshooting
- Visual Basic code, procedures
- troubleshooting procedures
- procedures [Visual Basic], about procedures
ms.assetid: 525721e8-2e02-4f75-b5d8-6b893462cf2b
ms.openlocfilehash: a36e2ef9442fc0e76c9a98e83007976393e7957b
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100471143"
---
# <a name="troubleshooting-procedures-visual-basic"></a>Procedimentos de solução de problemas (Visual Basic)

Esta página lista alguns problemas comuns que podem ocorrer ao trabalhar com procedimentos.  
  
## <a name="returning-an-array-type-from-a-function-procedure"></a>Retornando um tipo de matriz de um procedimento de função

Se um `Function` procedimento retornar um tipo de dados de matriz, você não poderá usar o `Function` nome para armazenar valores nos elementos da matriz. Se você tentar fazer isso, o compilador o interpretará como uma chamada para o `Function` . O exemplo a seguir gera erros de compilador:
  
```vb
Function AllOnes(n As Integer) As Integer()
   For i As Integer = 1 To n - 1  
      ' The following statement generates a COMPILER ERROR.  
      AllOnes(i) = 1  
   Next  

   ' The following statement generates a COMPILER ERROR.  
   Return AllOnes()  
End Function
```

A instrução `AllOnes(i) = 1` gera um erro de compilador porque ele parece chamar `AllOnes` com um argumento do tipo de dados errado (um escalar `Integer` em vez de uma `Integer` matriz). A instrução `Return AllOnes()` gera um erro de compilador porque ele parece chamar `AllOnes` sem argumento.  
  
 **Abordagem correta:** Para poder modificar os elementos de uma matriz que deve ser retornada, defina uma matriz interna como uma variável local. O exemplo a seguir é compilado sem erro:

 [!code-vb[VbVbcnProcedures#66](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#66)]

## <a name="argument-not-modified-by-procedure-call"></a>Argumento não modificado pela chamada de procedimento

Se você pretende permitir que um procedimento altere um elemento de programação subjacente a um argumento no código de chamada, você deve passá-lo por referência. Mas um procedimento pode acessar os elementos de um argumento de tipo de referência mesmo se você passá-lo por valor.

- **Variável subjacente**. Para permitir que o procedimento substitua o valor do elemento variável subjacente, o procedimento deve declarar o parâmetro [ByRef](../../../language-reference/modifiers/byref.md). Além disso, o código de chamada não deve colocar o argumento entre parênteses, porque isso substituiria o `ByRef` mecanismo de passagem.

- **Elementos de tipo de referência**. Se você declarar um parâmetro [ByVal](../../../language-reference/modifiers/byval.md), o procedimento não poderá modificar o elemento Variable subjacente. No entanto, se o argumento for um tipo de referência, o procedimento poderá modificar os membros do objeto para o qual ele aponta, mesmo que não possa substituir o valor da variável. Por exemplo, se o argumento for uma variável de matriz, o procedimento não poderá atribuir uma nova matriz a ele, mas poderá alterar um ou mais de seus elementos. Os elementos alterados são refletidos na variável de matriz subjacente no código de chamada.

O exemplo a seguir define dois procedimentos que usam uma variável de matriz por valor e operam em seus elementos. O procedimento `increase` simplesmente adiciona um a cada elemento. `replace`O procedimento atribui uma nova matriz ao parâmetro `a()` e, em seguida, adiciona um a cada elemento. No entanto, a reatribuição não afeta a variável de matriz subjacente no código de chamada porque `a()` é declarada `ByVal` .

[!code-vb[VbVbcnProcedures#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#35)]

[!code-vb[VbVbcnProcedures#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#38)]

O exemplo a seguir faz chamadas para `increase` e `replace` :

[!code-vb[VbVbcnProcedures#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#37)]
  
A primeira `MsgBox` chamada exibe "After aumente (n): 11, 21, 31, 41". Como `n` é um tipo de referência, `increase` o pode alterar seus membros, mesmo que seja passado `ByVal` .

A segunda `MsgBox` chamada exibe "após Replace (n): 11, 21, 31, 41". Como `n` é passado `ByVal` , `replace` não é possível modificar a variável `n` atribuindo uma nova matriz a ela. Quando `replace` o cria a nova instância de matriz `k` e a atribui à variável local `a` , ela perde a referência a `n` passada pelo código de chamada. Quando ele incrementa os membros de `a` , apenas a matriz local `k` é afetada.

**Abordagem correta:** Para poder modificar um elemento variável subjacente, passe-o por referência. O exemplo a seguir mostra a alteração na declaração de `replace` que permite substituir uma matriz por outra no código de chamada:

[!code-vb[VbVbcnProcedures#64](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#64)]

## <a name="unable-to-define-an-overload"></a>Não é possível definir uma sobrecarga

Se você quiser definir uma versão sobrecarregada de um procedimento, deverá usar o mesmo nome, mas uma assinatura diferente. Se o compilador não puder diferenciar a declaração de uma sobrecarga com a mesma assinatura, ele gerará um erro.

A *assinatura* de um procedimento é determinada pelo nome do procedimento e pela lista de parâmetros. Cada sobrecarga deve ter o mesmo nome de todas as outras sobrecargas, mas deve ser diferente de todas elas em pelo menos um dos outros componentes da assinatura. Para obter mais informações, consulte [sobrecarga de procedimento](./procedure-overloading.md).

Os itens a seguir, embora eles pertençam à lista de parâmetros, não são componentes da assinatura de um procedimento:

- Palavras-chave do modificador de procedimento, como `Public` , `Shared` e `Static` .
- Nomes de parâmetro.
- Palavras-chave do modificador de parâmetro, como `ByRef` e `Optional` .
- O tipo de dados do valor de retorno (exceto para um operador de conversão).

Não é possível sobrecarregar um procedimento, variando apenas um ou mais dos itens anteriores.

**Abordagem correta:** Para poder definir uma sobrecarga de procedimento, você deve variar a assinatura. Como você deve usar o mesmo nome, você deve variar o número, a ordem ou os tipos de dados dos parâmetros. Em um procedimento genérico, você pode variar o número de parâmetros de tipo. Em um operador de conversão ([função CType](../../../language-reference/functions/ctype-function.md)), você pode variar o tipo de retorno.

### <a name="overload-resolution-with-optional-and-paramarray-arguments"></a>Resolução de sobrecarga com argumentos opcional e ParamArray

Se você estiver sobrecarregando um procedimento com um ou mais parâmetros [opcionais](../../../language-reference/modifiers/optional.md) ou um parâmetro [ParamArray](../../../language-reference/modifiers/paramarray.md) , você deve evitar duplicar qualquer uma das *sobrecargas implícitas*. Para obter informações, consulte [Considerações sobre sobrecarga de procedimentos](./considerations-in-overloading-procedures.md).

## <a name="calling-the-wrong-version-of-an-overloaded-procedure"></a>Chamando a versão errada de um procedimento sobrecarregado

Se um procedimento tiver várias versões sobrecarregadas, você deve estar familiarizado com todas as suas listas de parâmetros e entender como Visual Basic resolve chamadas entre as sobrecargas. Caso contrário, você poderia chamar uma sobrecarga diferente da pretendida.

Quando você tiver determinado qual sobrecarga você deseja chamar, tenha cuidado para observar as seguintes regras:

- Forneça o número correto de argumentos e na ordem correta.  
- O ideal é que os argumentos tenham exatamente os mesmos tipos de dados que os parâmetros correspondentes. Em qualquer caso, o tipo de dados de cada argumento deve ampliar para o parâmetro correspondente. Isso é verdadeiro mesmo com a [instrução Option Strict](../../../language-reference/statements/option-strict-statement.md) definida como `Off` . Se uma sobrecarga exigir qualquer conversão de restrição da sua lista de argumentos, essa sobrecarga não será qualificada para ser chamada.
- Se você fornecer argumentos que exigem alargamento, torne seus tipos de dados o mais próximo possível dos tipos de dados de parâmetro correspondentes. Se duas ou mais sobrecargas aceitarem os tipos de dados de argumento, o compilador resolverá sua chamada para a sobrecarga que chama para a menor quantidade de alargamento.

Você pode reduzir a chance de incompatibilidades de tipo de dados usando a palavra-chave de conversão de [função CType](../../../language-reference/functions/ctype-function.md) ao preparar seus argumentos.

### <a name="overload-resolution-failure"></a>Falha na resolução de sobrecarga

Quando você chama um procedimento sobrecarregado, o compilador tenta eliminar tudo, exceto uma das sobrecargas. Se tiver sucesso, ele resolverá a chamada para essa sobrecarga. Se ele eliminar todas as sobrecargas ou se não puder reduzir as sobrecargas qualificadas para um único candidato, ele gerará um erro.

O exemplo a seguir ilustra o processo de resolução de sobrecarga:

[!code-vb[VbVbcnProcedures#62](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#62)]

[!code-vb[VbVbcnProcedures#63](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#63)]
  
Na primeira chamada, o compilador elimina a primeira sobrecarga porque o tipo do primeiro argumento () é `Short` limitado ao tipo do parâmetro correspondente ( `Byte` ). Em seguida, ele elimina a terceira sobrecarga porque cada tipo de argumento na segunda sobrecarga ( `Short` e `Single` ) se amplia ao tipo correspondente na terceira sobrecarga ( `Integer` e `Single` ). A segunda sobrecarga requer menos alargamento, portanto o compilador a utiliza para a chamada.

Na segunda chamada, o compilador não pode eliminar nenhuma das sobrecargas com base na restrição. Ele elimina a terceira sobrecarga pelo mesmo motivo que na primeira chamada, porque ela pode chamar a segunda sobrecarga com menos alargamento dos tipos de argumento. No entanto, o compilador não pode resolver entre a primeira e a segunda sobrecargas. Cada um tem um tipo de parâmetro definido que amplia o tipo correspondente no outro ( `Byte` para `Short` , mas `Single` para `Double` ). O compilador, portanto, gera um erro de resolução de sobrecarga.

**Abordagem correta:** Para poder chamar um procedimento sobrecarregado sem ambigüidade, use a [função CType](../../../language-reference/functions/ctype-function.md) para corresponder os tipos de dados de argumento aos tipos de parâmetro. O exemplo a seguir mostra uma chamada para `z` que força a resolução para a segunda sobrecarga.

[!code-vb[VbVbcnProcedures#65](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#65)]

### <a name="overload-resolution-with-optional-and-paramarray-arguments"></a>Resolução de sobrecarga com argumentos opcional e ParamArray

Se duas sobrecargas de um procedimento tiverem assinaturas idênticas, exceto que o último parâmetro é declarado [opcional](../../../language-reference/modifiers/optional.md) em um e [ParamArray](../../../language-reference/modifiers/paramarray.md) no outro, o compilador resolverá uma chamada para esse procedimento de acordo com a correspondência mais próxima. Para obter mais informações, consulte [sobrecarga de resolução](./overload-resolution.md).

## <a name="see-also"></a>Consulte também

- [Procedimentos](index.md)
- [Subprocedimentos](sub-procedures.md)
- [Procedimentos de função](function-procedures.md)
- [Procedimentos de propriedade](property-procedures.md)
- [Procedimentos do operador](operator-procedures.md)
- [Parâmetros e Argumentos de Procedimento](procedure-parameters-and-arguments.md)
- [Sobrecarga de procedimento](procedure-overloading.md)
- [Considerações sobre procedimentos de sobrecarga](considerations-in-overloading-procedures.md)
- [Resolução de sobrecarga](overload-resolution.md)
