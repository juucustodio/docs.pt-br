---
description: 'Saiba mais sobre: Localizando os fusos horários definidos em um sistema local'
title: Encontrando os fusos horários definidos em um sistema local
ms.date: 04/10/2017
helpviewer_keywords:
- time zones [.NET], local
- time zones [.NET], finding local system time zones
- time zone identifiers [.NET]
- local time zone access
- time zones [.NET], retrieving
- UTC times, finding local system time zones
- time zones [.NET], UTC
ms.assetid: 3f63b1bc-9a4b-4bde-84ea-ab028a80d3e1
ms.openlocfilehash: 1b7a4d1962adac42b47cda42d4d1223c4b79852a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99702633"
---
# <a name="finding-the-time-zones-defined-on-a-local-system"></a>Encontrando os fusos horários definidos em um sistema local

A <xref:System.TimeZoneInfo> classe não expõe um construtor público. Como resultado, a `new` palavra-chave não pode ser usada para criar um novo <xref:System.TimeZoneInfo> objeto. Em vez disso, <xref:System.TimeZoneInfo> os objetos são instanciados recuperando informações em fusos horários predefinidos do registro ou criando um fuso horário personalizado. Este tópico discute a instanciação de um fuso horário a partir dos dados armazenados no registro. Além disso, `static` `shared` as propriedades (em Visual Basic) da <xref:System.TimeZoneInfo> classe fornecem acesso ao UTC (tempo Universal Coordenado) e ao fuso horário local.

> [!NOTE]
> Para os fusos horários que não estão definidos no registro, você pode criar fusos horários personalizados chamando as sobrecargas do <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> método. A criação de um fuso horário personalizado é discutida nas tópicos [como: criar zonas de tempo sem regras de ajuste](create-time-zones-without-adjustment-rules.md) e [como criar fusos horários com regras de ajuste](create-time-zones-with-adjustment-rules.md) . Além disso, você pode criar uma instância de um <xref:System.TimeZoneInfo> objeto restaurando-o de uma cadeia de caracteres serializada com o <xref:System.TimeZoneInfo.FromSerializedString%2A> método. A serialização e desserialização de um <xref:System.TimeZoneInfo> objeto é discutida no tópico [como: salvar fusos horários em um recurso incorporado](save-time-zones-to-an-embedded-resource.md) e [como: restaurar fusos horários de um recurso inserido](restore-time-zones-from-an-embedded-resource.md) .

## <a name="accessing-individual-time-zones"></a>Acessando fusos horários individuais

A <xref:System.TimeZoneInfo> classe fornece dois objetos de fuso horário predefinidos que representam a hora UTC e o fuso horário local. Elas estão disponíveis nas <xref:System.TimeZoneInfo.Utc%2A> Propriedades e <xref:System.TimeZoneInfo.Local%2A> , respectivamente. Para obter instruções sobre como acessar os fusos horários UTC ou local, consulte [como acessar o UTC predefinido e os objetos de fuso horário local](access-utc-and-local.md).

Você também pode criar uma instância de um <xref:System.TimeZoneInfo> objeto que representa qualquer fuso horário definido no registro. Para obter instruções sobre como criar uma instância de um objeto de fuso horário específico, consulte [como criar uma instância de um objeto TimeZoneInfo](instantiate-time-zone-info.md).

## <a name="time-zone-identifiers"></a>Identificadores de fuso horário

O identificador do fuso horário é um campo de chave que identifica exclusivamente o fuso horário. Enquanto a maioria das chaves são relativamente curtas, o identificador de fuso horário é comparativamente longo. Na maioria dos casos, seu valor corresponde à <xref:System.TimeZoneInfo.StandardName%2A?displayProperty=nameWithType> propriedade, que é usada para fornecer o nome do horário padrão do fuso horário. No entanto, há exceções. A melhor maneira de certificar-se de que você forneça um identificador válido é enumerar os fusos horários disponíveis no sistema e observar os identificadores associados.

## <a name="see-also"></a>Consulte também

- [Datas, horas e fusos horários](index.md)
- [Como: acessar os objetos de fuso horário predefinidos UTC e local](access-utc-and-local.md)
- [Como: criar uma instância de um objeto TimeZoneInfo](instantiate-time-zone-info.md)
- [Convertendo horários entre fusos horários](converting-between-time-zones.md)
