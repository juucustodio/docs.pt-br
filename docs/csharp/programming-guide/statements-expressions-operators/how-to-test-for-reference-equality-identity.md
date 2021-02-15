---
title: Como testar a igualdade de referência (identidade)-guia de programação C#
description: Saiba como testar a igualdade de referência (identidade). Consulte um exemplo de código e exiba recursos adicionais disponíveis.
ms.date: 07/20/2015
helpviewer_keywords:
- object identity [C#]
- reference equality [C#]
ms.assetid: 91307fda-267b-4fd2-a338-2aada39ee791
ms.openlocfilehash: 148f37b37639061e84cefafc5f057e6e7b54563f
ms.sourcegitcommit: 8299abfbd5c49b596d61f1e4d09bc6b8ba055b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/27/2021
ms.locfileid: "98899146"
---
# <a name="how-to-test-for-reference-equality-identity-c-programming-guide"></a>Como testar a igualdade de referência (identidade) (guia de programação C#)

Não é necessário implementar qualquer lógica personalizada para dar suporte a comparações de igualdade de referência em seus tipos. Essa funcionalidade é fornecida para todos os tipos pelo método estático <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType>.  
  
 O exemplo a seguir mostra como determinar se duas variáveis têm *igualdade de referência*, que significa que elas se referem ao mesmo objeto na memória.  
  
 O exemplo também mostra por que <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType> sempre retorna `false` para tipos de valor e por que você não deve usar <xref:System.Object.ReferenceEquals%2A> para determinar igualdade de cadeia de caracteres.  
  
## <a name="example"></a>Exemplo  

 [!code-csharp[TestingReferenceEquality](snippets/how-to-test-for-reference-equality-identity/Program.cs)]  
  
 A implementação de `Equals` na classe base universal <xref:System.Object?displayProperty=nameWithType> também realiza uma verificação de igualdade de referência, mas é melhor não usar isso, porque, se uma classe substituir o método, os resultados poderão não ser o que você espera. O mesmo é verdadeiro para os operadores `==` e `!=`. Quando eles estiverem operando em tipos de referência, o comportamento padrão de `==` e `!=` é realizar uma verificação de igualdade de referência. No entanto, as classes derivadas podem sobrecarregar o operador para executar uma verificação de igualdade de valor. Para minimizar o potencial de erro, será melhor usar sempre <xref:System.Object.ReferenceEquals%2A> quando for necessário determinar se os dois objetos têm igualdade de referência.  
  
 Cadeias de caracteres constantes dentro do mesmo assembly sempre são internalizadas pelo runtime. Ou seja, apenas uma instância de cada cadeia de caracteres literal única é mantida. No entanto, o runtime não garante que cadeias de caracteres criadas em runtime sejam internalizadas nem garante que duas de cadeias de caracteres constantes iguais em diferentes assemblies sejam internalizadas.  
  
## <a name="see-also"></a>Confira também

- [Comparações de igualdade](./equality-comparisons.md)
