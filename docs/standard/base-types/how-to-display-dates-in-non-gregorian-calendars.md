---
description: 'Saiba mais sobre: como exibir datas em calendários não gregorianos'
title: 'Como: exibir datas em calendários não gregorianos'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- formatting [.NET], dates
- dates [.NET], formatting
- calendars [.NET], displaying dates
- displaying date and time data
ms.assetid: ed324eff-4aff-4a76-b6c0-04e6c0d8f5a9
ms.openlocfilehash: 246878bb22adc722d69b1196c480e2989c24beee
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99629793"
---
# <a name="how-to-display-dates-in-non-gregorian-calendars"></a>Como: exibir datas em calendários não gregorianos

Os tipos <xref:System.DateTime> e <xref:System.DateTimeOffset> usam o calendário gregoriano como seu calendário padrão. Isso significa que chamar o método `ToString` de um valor de data e hora exibe a representação de cadeia de caracteres da data e hora no calendário gregoriano, mesmo que a data e hora tenha sido criada usando outro calendário. Isso é ilustrado no exemplo a seguir, que usa duas maneiras diferentes para criar um valor de data e hora com o calendário persa, mas ainda exibe esses valores de data e hora no calendário gregoriano quando chama o método <xref:System.DateTime.ToString%2A>. Este exemplo reflete duas técnicas comumente usadas, mas incorretas, para exibir a data em um calendário específico.  
  
 [!code-csharp[Formatting.HowTo.Calendar#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Calendar/cs/Calendar1.cs#1)]
 [!code-vb[Formatting.HowTo.Calendar#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Calendar/vb/Calendar1.vb#1)]  
  
 Duas técnicas diferentes podem ser usadas para exibir a data em um calendário específico. A primeira requer que o calendário seja o calendário padrão de uma determinada cultura. O segundo pode ser usado com qualquer calendário.  
  
### <a name="to-display-the-date-for-a-cultures-default-calendar"></a>Para exibir a data do calendário padrão de uma cultura  
  
1. Crie uma instância de um objeto de calendário derivado da classe <xref:System.Globalization.Calendar> que representa o calendário a ser usado.  
  
2. Crie uma instância de um objeto <xref:System.Globalization.CultureInfo> que representa a cultura cuja formatação será usada para exibir a data.  
  
3. Chame o método <xref:System.Array.Exists%2A?displayProperty=nameWithType> para determinar se o objeto de calendário é um membro da matriz retornada pela propriedade <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType>. Isso indica que o calendário pode servir como calendário padrão para o objeto <xref:System.Globalization.CultureInfo>. Se ele não for membro da matriz, siga as instruções na seção "Para exibir a data em qualquer calendário".  
  
4. Atribua o objeto de calendário à propriedade <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A> do objeto <xref:System.Globalization.DateTimeFormatInfo> retornado pela propriedade <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=nameWithType>.  
  
    > [!NOTE]
    > A classe <xref:System.Globalization.CultureInfo> também tem uma propriedade <xref:System.Globalization.CultureInfo.Calendar%2A>. No entanto, ela é somente leitura e constante; não é alterada para refletir o novo calendário padrão atribuído à propriedade <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=nameWithType>.  
  
5. Chame o método <xref:System.DateTime.ToString%2A> ou <xref:System.DateTime.ToString%2A> e passe-o para o objeto <xref:System.Globalization.CultureInfo> cujo calendário padrão foi modificado na etapa anterior.  
  
### <a name="to-display-the-date-in-any-calendar"></a>Para exibir a data em qualquer calendário  
  
1. Crie uma instância de um objeto de calendário derivado da classe <xref:System.Globalization.Calendar> que representa o calendário a ser usado.  
  
2. Determine quais elementos de data e hora devem aparecer na representação de cadeia de caracteres do valor de data e hora.  
  
3. Para cada elemento de data e hora que você deseja exibir, chame o método `Get` do objeto de calendário... método. Os métodos a seguir estão disponíveis:  
  
    - <xref:System.Globalization.Calendar.GetYear%2A>, para exibir o ano no calendário apropriado.  
  
    - <xref:System.Globalization.Calendar.GetMonth%2A>, para exibir o mês no calendário apropriado.  
  
    - <xref:System.Globalization.Calendar.GetDayOfMonth%2A>, para exibir o número do dia do mês no calendário apropriado.  
  
    - <xref:System.Globalization.Calendar.GetHour%2A>, para exibir a hora do dia no calendário apropriado.  
  
    - <xref:System.Globalization.Calendar.GetMinute%2A>, para exibir os minutos da hora no calendário apropriado.  
  
    - <xref:System.Globalization.Calendar.GetSecond%2A>, para exibir os segundos do minuto no calendário apropriado.  
  
    - <xref:System.Globalization.Calendar.GetMilliseconds%2A>, para exibir os milissegundos do segundo no calendário apropriado.  
  
## <a name="example"></a>Exemplo  

 O exemplo exibe uma data usando dois calendários diferentes. Ele exibe a data após definir o calendário islâmico como calendário padrão para a cultura ar-JO e exibe a data usando o calendário persa, que não tem suporte como calendário opcional pela cultura fa-IR.  
  
 [!code-csharp[Formatting.HowTo.Calendar#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Calendar/cs/Calendar1.cs#2)]
 [!code-vb[Formatting.HowTo.Calendar#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Calendar/vb/Calendar1.vb#2)]  
  
 Cada objeto <xref:System.Globalization.CultureInfo> pode dar suporte a um ou mais calendários, que são indicados pela propriedade <xref:System.Globalization.CultureInfo.OptionalCalendars%2A>. Um deles é designado como o calendário padrão da cultura e é retornado pela propriedade somente leitura <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType>. Outro dos calendários opcionais pode ser designado como o padrão, atribuindo um objeto <xref:System.Globalization.Calendar> que representa o calendário para a propriedade <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=nameWithType> retornada pela propriedade <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=nameWithType>. No entanto, alguns calendários, como o calendário persa representado pela classe <xref:System.Globalization.PersianCalendar>, não servem como calendários opcionais para nenhuma cultura.  
  
 O exemplo define uma classe de utilitário de calendário reutilizável, `CalendarUtility`, para manipular muitos dos detalhes de gerar a representação de cadeia de caracteres de uma data usando um calendário específico. A classe `CalendarUtility` tem os seguintes membros:  
  
- Um construtor parametrizado cujo único parâmetro é um objeto <xref:System.Globalization.Calendar> em que uma data deve ser representada. Ele é atribuído a um campo particular da classe.  
  
- `CalendarExists`, um método particular que retorna um valor booliano que indica se o calendário representado pelo `CalendarUtility` objeto tem suporte do objeto <xref:System.Globalization.CultureInfo> passado para o método como um parâmetro. O método ajusta uma chamada para o método <xref:System.Array.Exists%2A?displayProperty=nameWithType> ao qual ele passa a matriz <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType>.  
  
- `HasSameName`, um método particular atribuído ao representante <xref:System.Predicate%601> que é transmitido como um parâmetro para o método <xref:System.Array.Exists%2A?displayProperty=nameWithType>. Cada membro da matriz é passado ao método até que o método retorne `true`. O método determina se o nome de um calendário opcional é o mesmo que o calendário representado pelo objeto `CalendarUtility`.  
  
- `DisplayDate`, um método público sobrecarregado a que são passados dois parâmetros: um valor de <xref:System.DateTime> ou <xref:System.DateTimeOffset> para expressar no calendário representado pelo objeto `CalendarUtility`; e a cultura cujas regras de formatação devem ser usadas. Seu comportamento ao retornar a representação de cadeia de caracteres de uma data depende de o calendário de destino ter suporte da cultura cujas regras de formatação devem ser usadas.  
  
 Independentemente do calendário usado para criar um valor <xref:System.DateTime> ou <xref:System.DateTimeOffset> neste exemplo, o valor normalmente é expresso como uma data no calendário gregoriano. Isso ocorre porque os tipos <xref:System.DateTime> e <xref:System.DateTimeOffset> não preservam nenhuma informação de calendário. Internamente, eles são representados como o número de marcadores decorridos desde a meia-noite de 1º de janeiro de 0001. A interpretação desse número depende do calendário. Na maioria das culturas, o calendário padrão é o calendário gregoriano.
