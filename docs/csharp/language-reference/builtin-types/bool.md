---
title: referência de C# tipo bool
ms.date: 11/26/2019
f1_keywords:
- bool
- bool_CSharpKeyword
helpviewer_keywords:
- bool data type [C#]
- Boolean [C#]
ms.assetid: 551cfe35-2632-4343-af49-33ad12da08e2
ms.openlocfilehash: 1e79de6d9e5cf973ce394bfb06871777c562c8ac
ms.sourcegitcommit: 93762e1a0dae1b5f64d82eebb7b705a6d566d839
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2019
ms.locfileid: "74553033"
---
# <a name="bool-c-reference"></a><span data-ttu-id="eb8ac-102">bool (C# referência)</span><span class="sxs-lookup"><span data-stu-id="eb8ac-102">bool (C# reference)</span></span>

<span data-ttu-id="eb8ac-103">A palavra-chave Type de `bool` é um alias para o tipo de estrutura .NET <xref:System.Boolean?displayProperty=nameWithType> que representa um valor booliano, que pode ser `true` ou `false`.</span><span class="sxs-lookup"><span data-stu-id="eb8ac-103">The `bool` type keyword is an alias for the .NET <xref:System.Boolean?displayProperty=nameWithType> structure type that represents a Boolean value, which can be either `true` or `false`.</span></span>

<span data-ttu-id="eb8ac-104">Para executar operações lógicas com valores do tipo `bool`, use operadores [lógicos boolianos](../operators/boolean-logical-operators.md) .</span><span class="sxs-lookup"><span data-stu-id="eb8ac-104">To perform logical operations with values of the `bool` type, use [Boolean logical](../operators/boolean-logical-operators.md) operators.</span></span> <span data-ttu-id="eb8ac-105">O tipo de `bool` é o tipo de resultado de operadores de [comparação](../operators/comparison-operators.md) e de [igualdade](../operators/equality-operators.md) .</span><span class="sxs-lookup"><span data-stu-id="eb8ac-105">The `bool` type is the result type of [comparison](../operators/comparison-operators.md) and [equality](../operators/equality-operators.md) operators.</span></span> <span data-ttu-id="eb8ac-106">Uma expressão de `bool` pode ser uma expressão condicional de controle nas instruções [If](../keywords/if-else.md) [, do,](../keywords/do.md) [while](../keywords/while.md)e [for](../keywords/for.md) e no [operador condicional `?:`](../operators/conditional-operator.md).</span><span class="sxs-lookup"><span data-stu-id="eb8ac-106">A `bool` expression can be a controlling conditional expression in the [if](../keywords/if-else.md), [do](../keywords/do.md), [while](../keywords/while.md), and [for](../keywords/for.md) statements and in the [conditional operator `?:`](../operators/conditional-operator.md).</span></span>

<span data-ttu-id="eb8ac-107">O valor padrão do tipo de `bool` é `false`.</span><span class="sxs-lookup"><span data-stu-id="eb8ac-107">The default value of the `bool` type is `false`.</span></span>

## <a name="literals"></a><span data-ttu-id="eb8ac-108">{1&gt;Literais&lt;1}</span><span class="sxs-lookup"><span data-stu-id="eb8ac-108">Literals</span></span>

<span data-ttu-id="eb8ac-109">Você pode usar os literais `true` e `false` para inicializar uma variável `bool` ou para passar um valor de `bool`:</span><span class="sxs-lookup"><span data-stu-id="eb8ac-109">You can use the `true` and `false` literals to initialize a `bool` variable or to pass a `bool` value:</span></span>

[!code-csharp-interactive[bool literals](~/samples/csharp/language-reference/builtin-types/BoolType.cs#Literals)]

## <a name="conversions"></a><span data-ttu-id="eb8ac-110">Conversões</span><span class="sxs-lookup"><span data-stu-id="eb8ac-110">Conversions</span></span>

<span data-ttu-id="eb8ac-111">C#fornece apenas duas conversões que envolvem o tipo de `bool`.</span><span class="sxs-lookup"><span data-stu-id="eb8ac-111">C# provides only two conversions that involve the `bool` type.</span></span> <span data-ttu-id="eb8ac-112">Essas são uma conversão implícita para o tipo de `bool?` anulável correspondente e uma conversão explícita do tipo `bool?`.</span><span class="sxs-lookup"><span data-stu-id="eb8ac-112">Those are an implicit conversion to the corresponding nullable `bool?` type and an explicit conversion from the `bool?` type.</span></span> <span data-ttu-id="eb8ac-113">No entanto, o .NET fornece métodos adicionais que você pode usar para converter de ou para o tipo de `bool`.</span><span class="sxs-lookup"><span data-stu-id="eb8ac-113">However, .NET provides additional methods that you can use to convert to or from the `bool` type.</span></span> <span data-ttu-id="eb8ac-114">Para obter mais informações, consulte a seção [convertendo de valores booleanos](/dotnet/api/system.boolean#converting-to-and-from-boolean-values) na página de referência da API <xref:System.Boolean?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="eb8ac-114">For more information, see the [Converting to and from Boolean values](/dotnet/api/system.boolean#converting-to-and-from-boolean-values) section of the <xref:System.Boolean?displayProperty=nameWithType> API reference page.</span></span>

## <a name="three-valued-boolean-logic"></a><span data-ttu-id="eb8ac-115">Lógica booleana de três valores</span><span class="sxs-lookup"><span data-stu-id="eb8ac-115">Three-valued Boolean logic</span></span>

<span data-ttu-id="eb8ac-116">Use o tipo de `bool?` anulável, se você precisar dar suporte à lógica de três valores, por exemplo, ao trabalhar com bancos de dados que dão suporte a um tipo booliano de três valores.</span><span class="sxs-lookup"><span data-stu-id="eb8ac-116">Use the nullable `bool?` type, if you need to support the three-valued logic, for example, when you work with databases that support a three-valued Boolean type.</span></span> <span data-ttu-id="eb8ac-117">Para os operandos `bool?`, os operadores `&` e `|` predefinidos oferecem suporte à lógica de três valores.</span><span class="sxs-lookup"><span data-stu-id="eb8ac-117">For the `bool?` operands, the predefined `&` and `|` operators support the three-valued logic.</span></span> <span data-ttu-id="eb8ac-118">Para obter mais informações, confira a seção [Operadores lógicos booleanos anuláveis](../operators/boolean-logical-operators.md#nullable-boolean-logical-operators) do artigo [Operadores lógicos boolianos](../operators/boolean-logical-operators.md).</span><span class="sxs-lookup"><span data-stu-id="eb8ac-118">For more information, see the [Nullable Boolean logical operators](../operators/boolean-logical-operators.md#nullable-boolean-logical-operators) section of the [Boolean logical operators](../operators/boolean-logical-operators.md) article.</span></span>

<span data-ttu-id="eb8ac-119">Para obter mais informações sobre tipos de valor anulável, consulte [tipos de valor anulável](nullable-value-types.md).</span><span class="sxs-lookup"><span data-stu-id="eb8ac-119">For more information about nullable value types, see [Nullable value types](nullable-value-types.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="eb8ac-120">Especificação da linguagem C#</span><span class="sxs-lookup"><span data-stu-id="eb8ac-120">C# language specification</span></span>

<span data-ttu-id="eb8ac-121">Para obter mais informações, consulte [a seção tipo bool](~/_csharplang/spec/types.md#the-bool-type) da [ C# especificação da linguagem](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eb8ac-121">For more information, see [The bool type](~/_csharplang/spec/types.md#the-bool-type) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="eb8ac-122">Consulte também</span><span class="sxs-lookup"><span data-stu-id="eb8ac-122">See also</span></span>

- [<span data-ttu-id="eb8ac-123">Referência de C#</span><span class="sxs-lookup"><span data-stu-id="eb8ac-123">C# reference</span></span>](../index.md)
- [<span data-ttu-id="eb8ac-124">Tabela de tipos internos</span><span class="sxs-lookup"><span data-stu-id="eb8ac-124">Built-in types table</span></span>](../keywords/built-in-types-table.md)
- [<span data-ttu-id="eb8ac-125">operadores true e false</span><span class="sxs-lookup"><span data-stu-id="eb8ac-125">true and false operators</span></span>](../operators/true-false-operators.md)