---
description: abstract – Referência de C#
title: abstract – Referência de C#
ms.date: 07/20/2015
f1_keywords:
- abstract
- abstract_CSharpKeyword
helpviewer_keywords:
- abstract keyword [C#]
ms.assetid: b0797770-c1f3-4b4d-9441-b9122602a6bb
ms.openlocfilehash: 276e3f6ab50a069e3852c529c13eaad3c64e42ad
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91168875"
---
# <a name="abstract-c-reference"></a>abstract (Referência de C#)

O modificador `abstract` indica que o item que está sendo modificado tem uma implementação ausente ou incompleta. O modificador abstrato pode ser usado com classes, métodos, propriedades, indexadores e eventos. Use o modificador `abstract` em uma declaração de classe para indicar que uma classe se destina somente a ser uma classe base de outras classes, não instanciada por conta própria. Membros marcados como abstratos precisam ser implementados por classes não abstratas que derivam da classe abstrata.
  
## <a name="example"></a>Exemplo  

 Neste exemplo, a classe `Square` deve fornecer uma implementação de `GetArea` porque deriva de `Shape`:  
  
 [!code-csharp[csrefKeywordsModifiers#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#1)]
  
 As classes abstratas têm os seguintes recursos:  
  
- Uma classe abstrata não pode ser instanciada.  
  
- Uma classe abstrata pode conter acessadores e métodos abstratos.  
  
- Não é possível modificar uma classe abstrata com o modificador [sealed](./sealed.md) porque os dois modificadores têm significados opostos. O modificador `sealed` impede que uma classe seja herdada e o modificador `abstract` requer uma classe a ser herdada.  
  
- Uma classe não abstrata derivada de uma classe abstrata deve incluir implementações reais de todos os acessadores e métodos abstratos herdados.  
  
 Use o modificador `abstract` em uma declaração de método ou propriedade para indicar que o método ou propriedade não contem a implementação.  
  
 Os métodos abstratos têm os seguintes recursos:  
  
- Um método abstrato é implicitamente um método virtual.  
  
- Declarações de método abstrato são permitidas apenas em classes abstratas.  
  
- Como uma declaração de método abstrato não fornece nenhuma implementação real, não há nenhum corpo de método, a declaração do método simplesmente termina com um ponto e vírgula e não há chaves ({ }) após a assinatura. Por exemplo:  
  
    ```csharp  
    public abstract void MyMethod();  
    ```  
  
     A implementação é fornecida por uma [substituição](./override.md) de método, que é um membro de uma classe não abstrata.  
  
- É um erro usar os modificadores [static](./static.md) ou [virtual](./virtual.md) em uma declaração de método abstrato.  
  
 Propriedades abstratas se comportam como métodos abstratos, exceto pelas diferenças na sintaxe de declaração e chamada.  
  
- É um erro usar o modificador `abstract` em uma propriedade estática.  
  
- Uma propriedade herdada abstrata pode ser substituída em uma classe derivada incluindo uma declaração de propriedade que usa o modificador [override](./override.md).  
  
 Para obter mais informações sobre classes abstratas, consulte [Classes e membros de classes abstratos e lacrados](../../programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md).  
  
 Uma classe abstrata deve fornecer uma implementação para todos os membros de interface.  
  
 Uma classe abstrata que implementa uma interface pode mapear os métodos de interface em métodos abstratos. Por exemplo:  
  
[!code-csharp[csrefKeywordsModifiers#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#2)]
  
## <a name="example"></a>Exemplo  

 Nesse exemplo, a classe `DerivedClass` é derivada de uma classe abstrata `BaseClass`. A classe abstrata contém um método abstrato, `AbstractMethod` e duas propriedades abstratas, `X` e `Y`.  
  
[!code-csharp[csrefKeywordsModifiers#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#3)]
  
 No exemplo anterior, se você tentar instanciar a classe abstrata usando uma instrução como esta:  
  
```csharp
BaseClass bc = new BaseClass();   // Error  
```  
  
Você receberá uma mensagem de erro informando que o compilador não pode criar uma instância da classe abstrata "BaseClass".  
  
## <a name="c-language-specification"></a>Especificação da Linguagem C#  

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Confira também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Modificadores](index.md)
- [virtual](./virtual.md)
- [override](./override.md)
- [Palavras-chave do C#](./index.md)
