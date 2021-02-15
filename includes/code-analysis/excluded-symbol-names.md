---
ms.openlocfilehash: 83644b9205d650da68c910095dd1d22a14940c44
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97366854"
---
### <a name="exclude-specific-symbols"></a>Excluir símbolos específicos

Você pode excluir símbolos específicos, como tipos e métodos, da análise. Por exemplo, para especificar que a regra não deve ser executada em nenhum código dentro de tipos nomeados `MyType` , adicione o seguinte par chave-valor a um arquivo *. editorconfig* em seu projeto:

```ini
dotnet_code_quality.CAXXXX.excluded_symbol_names = MyType
```

Formatos de nome de símbolo permitidos no valor de opção (separados por `|` ):

- Somente nome do símbolo (inclui todos os símbolos com o nome, independentemente do tipo ou namespace que o contém).
- Nomes totalmente qualificados no [formato de ID de documentação](../../docs/csharp/programming-guide/xmldoc/processing-the-xml-file.md#id-strings)do símbolo. Cada nome de símbolo requer um prefixo de tipo de símbolo, como `M:` para métodos, `T:` para tipos e `N:` para namespaces.
- `.ctor` para construtores e `.cctor` para construtores estáticos.

Exemplos:

| Valor de Opção | Resumo |
| --- | --- |
|`dotnet_code_quality.CAXXXX.excluded_symbol_names = MyType` | Corresponde a todos os símbolos chamados `MyType` . |
|`dotnet_code_quality.CAXXXX.excluded_symbol_names = MyType1|MyType2` | Corresponde a todos os símbolos nomeados `MyType1` ou `MyType2` . |
|`dotnet_code_quality.CAXXXX.excluded_symbol_names = M:NS.MyType.MyMethod(ParamType)` | Corresponde ao método específico `MyMethod` com a assinatura totalmente qualificada especificada. |
|`dotnet_code_quality.CAXXXX.excluded_symbol_names = M:NS1.MyType1.MyMethod1(ParamType)|M:NS2.MyType2.MyMethod2(ParamType)` | O corresponde a métodos específicos `MyMethod1` e `MyMethod2` com as respectivas assinaturas totalmente qualificadas. |
