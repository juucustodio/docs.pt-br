---
ms.openlocfilehash: dfa8235fcfd868b80d3a610bddb492899519e289
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009041"
---
### <a name="xml-parsing-changes"></a>Alterações de análise de XML

| Nome    | Valor   |
|:--------|:--------|
| Escopo   | Secundária   |
| Versão | 4.5.2   |
| Type    | Runtime |

#### <a name="details"></a>Detalhes

Por motivos de segurança, as seguintes alterações foram introduzidas em APIS de análise de XML:

- <xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities?displayProperty=nameWithType> é definido como 10 milhões quando <xref:System.Xml.XmlReaderSettings> é inicializado.
- <xref:System.Xml.XmlReaderSettings.XmlResolver?displayProperty=nameWithType> é definido como `null` por padrão.

> [!NOTE]
> <xref:System.Xml.XmlReaderSettings> é usado por todos os analisadores XML, portanto, embora essa alteração ajude o <xref:System.Xml.XmlReader> caso, ela também afeta outros cenários.

#### <a name="suggestion"></a>Sugestão

Para reverter para o comportamento anterior, você pode definir um valor no registro. Adicione um valor DWORD chamado `EnableLegacyXmlSettings` à `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\XML` chave do registro e defina seu valor como `1` . Você também pode adicionar o valor do registro no hive do HKEY_CURRENT_USER em vez disso.

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities?displayProperty=fullName>
- <xref:System.Xml.XmlReaderSettings.XmlResolver?displayProperty=fullName>

Além disso, qualquer API XML que depende <xref:System.Xml.XmlResolver> , direta ou indiretamente, é afetada.

<!--

#### Affected APIs

- `P:System.Xml.XmlReaderSettings.MaxCharactersFromEntities`
- `P:System.Xml.XmlReaderSettings.XmlResolver`

-->
