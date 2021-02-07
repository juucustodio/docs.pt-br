---
description: 'Saiba mais sobre: como criar uma instância de um objeto TimeZoneInfo'
title: 'Como: criar uma instância de um objeto TimeZoneInfo'
ms.date: 04/10/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- instantiating time zone objects
- time zone objects [.NET], instantiation
ms.assetid: 8cb620e5-c6a6-4267-a52e-beeb73cd1a34
ms.openlocfilehash: d063833aa60142bf6f942a836c7f89777d9073a5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99702607"
---
# <a name="how-to-instantiate-a-timezoneinfo-object"></a>Como: criar uma instância de um objeto TimeZoneInfo

A maneira mais comum de instanciar um <xref:System.TimeZoneInfo> objeto é recuperar informações sobre ele do registro. Este tópico discute como criar uma instância de um <xref:System.TimeZoneInfo> objeto do registro do sistema local.

### <a name="to-instantiate-a-timezoneinfo-object"></a>Para criar uma instância de um objeto TimeZoneInfo

1. Declare um <xref:System.TimeZoneInfo> objeto.

2. Chame o `static` `Shared` método (no Visual Basic) <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A?displayProperty=nameWithType> .

3. Manipule quaisquer exceções geradas pelo método, especialmente as <xref:System.TimeZoneNotFoundException> que são geradas se o fuso horário não estiver definido no registro.

## <a name="example"></a>Exemplo

O código a seguir recupera um <xref:System.TimeZoneInfo> objeto que representa o fuso horário padrão do leste e exibe a hora padrão do leste que corresponde à hora local.

[!code-csharp[System.TimeZone2.Concepts#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#5)]
[!code-vb[System.TimeZone2.Concepts#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#5)]

O <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A?displayProperty=nameWithType> parâmetro único do método é o identificador do fuso horário que você deseja recuperar, que corresponde à propriedade do objeto <xref:System.TimeZoneInfo.Id%2A?displayProperty=nameWithType> . O identificador do fuso horário é um campo de chave que identifica exclusivamente o fuso horário. Enquanto a maioria das chaves são relativamente curtas, o identificador de fuso horário é comparativamente longo. Na maioria dos casos, seu valor corresponde à <xref:System.TimeZoneInfo.StandardName%2A> propriedade de um <xref:System.TimeZoneInfo> objeto, que é usado para fornecer o nome do horário padrão do fuso horário. No entanto, há exceções. A melhor maneira de certificar-se de que você forneça um identificador válido é enumerar os fusos horários disponíveis no sistema e observar os identificadores dos fusos horários presentes nele. Para obter uma ilustração, consulte [como: enumerar fusos horários presentes em um computador](enumerate-time-zones.md). O tópico [Encontrando os fusos horários definidos em um sistema local](finding-the-time-zones-on-local-system.md) também contém uma lista de identificadores de fuso horário selecionados.

Se o fuso horário for encontrado, o método retornará seu <xref:System.TimeZoneInfo> objeto. Se o fuso horário não for encontrado, o método lançará um <xref:System.TimeZoneNotFoundException> . Se o fuso horário for encontrado, mas seus dados estiverem corrompidos ou incompletos, o método lançará um <xref:System.InvalidTimeZoneException> .

Se seu aplicativo depende de um fuso horário que deve estar presente, você deve primeiro chamar o <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> método para recuperar as informações de fuso horário do registro. Se a chamada do método falhar, o manipulador de exceção deverá criar uma nova instância do fuso horário ou recriá-la desserializando um <xref:System.TimeZoneInfo> objeto serializado. Consulte [como: restaurar fusos horários de um recurso inserido](restore-time-zones-from-an-embedded-resource.md) para obter um exemplo.

## <a name="see-also"></a>Consulte também

- [Datas, horas e fusos horários](index.md)
- [Encontrando os fusos horários definidos em um sistema local](finding-the-time-zones-on-local-system.md)
- [Como acessar o UTC predefinido e os objetos de fuso horário local](access-utc-and-local.md)
