---
title: Visão geral da biblioteca de classes do .NET
description: Saiba mais sobre a biblioteca de classes .NET. As APIs do .NET incluem classes, interfaces, delegados e tipos de valor para fornecer acesso à funcionalidade do sistema.
ms.date: 02/08/2018
helpviewer_keywords:
- classes [.NET], library overview
- .NET, library overview
- class objects value type
- naming conventions [.NET]
- types, .NET
- user-defined types
- Visual Basic, data types
- data types [.NET], C++
- Visual C#, data types
- libraries, .NET
- data types [.NET], F#
- System namespace
- F#, data types
- .NET, class library
- type system [.NET]
- data types [.NET]
- value types
- data types [.NET], Visual Basic
- Common Language Specification
- namespaces [.NET]
- floating point value type
- class library [.NET]
- CLS
- logical value type
- built-in types
- namespaces [.NET], about namespaces
- Visual C++, data types
- members [.NET], type
- data types [.NET], C#
- integer value type
- base types, class library
ms.assetid: 7e4c5921-955d-4b06-8709-101873acf157
ms.openlocfilehash: 44a46db4fa7ebf6dd5802cc07e7d18744c72ad68
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94831254"
---
# <a name="net-class-library-overview"></a>Visão geral da biblioteca de classes do .NET

As APIs do .NET incluem classes, interfaces, delegados e tipos de valor que agilizam e otimizam o processo de desenvolvimento e fornecem acesso à funcionalidade do sistema. Para facilitar a interoperabilidade entre linguagens, os tipos do .NET têm conformidade com CLS e, assim, podem ser usados por qualquer linguagem de programação cujo compilador esteja de acordo com a CLS (Common Language Specification).  
  
Os tipos do .NET são a base na qual os aplicativos, os componentes e os controles do .NET são criados. O .NET inclui tipos que executam as seguintes funções:  
  
- Representam tipos de dados base e exceções.  
  
- Encapsulam estruturas de dados.  
  
- Executam E/S.  
  
- Acessam informações sobre tipos carregados.  
  
- Invocar verificações de segurança do .NET.  
  
- Fornecem acesso a dados, uma GUI detalhada do lado do cliente e uma GUI do lado do cliente controlada pelo servidor.  
  
O .NET fornece um conjunto avançado de interfaces, bem como classes abstratas e concretas (não abstratas). Você pode usar as classes concretas como estão ou, em muitos casos, derivar suas próprias classes. Para usar a funcionalidade de uma interface, você pode criar uma classe que implementa a interface ou derivar uma classe de uma das classes do .NET que implementa a interface.  
  
## <a name="naming-conventions"></a>Convenções de nomenclatura

 Os tipos do .NET usam um esquema de nomenclatura de sintaxe por ponto que denota uma hierarquia. Essa técnica agrupa tipos relacionados em namespaces para que eles possam ser pesquisados e referenciados com mais facilidade. A primeira parte do nome completo — até o ponto mais à direita — é o nome do namespace. A última parte do nome é o nome do tipo. Por exemplo, `System.Collections.Generic.List<T>` representa o tipo `List<T>`, que pertence ao namespace `System.Collections.Generic`. Os tipos em <xref:System.Collections.Generic> podem ser usados para trabalhar com coleções genéricas.  
  
 Esse esquema de nomenclatura torna mais fácil para os desenvolvedores de biblioteca que estendem o .NET criar grupos hierárquicos de tipos e nomeá-los de maneira consistente e informativa. Ele também permite que tipos sejam identificados sem ambiguidades por seu nome completo (ou seja, pelo namespace e pelo nome de tipo), o que impede conflitos de nomes de tipo. Os desenvolvedores de bibliotecas devem usar a seguinte convenção para criar nomes para seus namespaces:  
  
 *CompanyName*.*TechnologyName*  
  
 Por exemplo, o namespace `Microsoft.Word` segue esta diretriz.  
  
 O uso de padrões de nomenclatura para agrupar tipos relacionados em namespaces é uma maneira útil de criar e documentar bibliotecas de classes. No entanto, esse esquema de nomenclatura não afeta visibilidade, acesso a membro, herança, segurança ou associação. Um namespace pode ser particionado em vários assemblies e um único assembly pode conter tipos de vários namespaces. O assembly fornece a estrutura formal para criação de versão, implantação, segurança, carregamento e visibilidade no Common Language Runtime.  
  
 Para obter mais informações sobre namespaces e nomes de tipos, consulte [Common Type System](base-types/common-type-system.md).  
  
## <a name="system-namespace"></a>namespace System

 O <xref:System> é o namespace raiz para tipos fundamentais no.NET. Esse namespace contém classes que representam os tipos de dados base usados por todos os aplicativos: <xref:System.Object> (a raiz da hierarquia de herança), <xref:System.Byte>, <xref:System.Char>, <xref:System.Array>, <xref:System.Int32>, <xref:System.String> etc. Muitos desses tipos correspondem aos tipos de dados primitivos que sua linguagem de programação usa. Ao escrever código usando tipos .NET, você pode usar a palavra-chave correspondente da sua linguagem quando um tipo de dados base .NET é esperado.  
  
 A tabela a seguir lista os tipos base que o .NET fornece, descreve resumidamente cada tipo e indica o tipo correspondente em Visual Basic, C#, C++ e F#.  
  
|Categoria|Nome da classe|Descrição|Tipo de dados do Visual Basic|Tipo de dados em C#|Tipo de dados de C++/CLI|Tipo de dados de F#|  
|--------------|----------------|-----------------|----------------------------|-------------------|---------------------|-----------------------|  
|Integer|<xref:System.Byte>|Um inteiro de 8 bits sem sinal.|**Byte**|**byte**|**unsigned char**|**byte**|  
||<xref:System.SByte>|Um inteiro com sinal de 8 bits.<br /><br /> Não compatível com CLS.|**SByte**|**sbyte**|**char**<br /> - ou -<br /> **signed** **char**|**sbyte**|  
||<xref:System.Int16>|Um inteiro de 16 bits com sinal.|**Baixo**|**short**|**short**|**int16**|  
||<xref:System.Int32>|Um inteiro com sinal de 32 bits.|**Inteiro**|**int**|**int**<br /><br /> - ou -<br /><br /> **longo**|**int**|  
||<xref:System.Int64>|Um inteiro com sinal de 64 bits.|**Long**|**longo**|**__int64**|**int64**|  
||<xref:System.UInt16>|Um inteiro sem sinal de 16 bits.<br /><br /> Não compatível com CLS.|**Num**|**ushort**|**unsigned short**|**UInt16**|  
||<xref:System.UInt32>|Um inteiro sem sinal de 32 bits.<br /><br /> Não compatível com CLS.|**UInteger**|**uint**|**unsigned int**<br /> - ou -<br /> **unsigned long**|**uint32**|  
||<xref:System.UInt64>|Um inteiro sem sinal de 64 bits.<br /><br /> Não compatível com CLS.|**ULong**|**ULONG**|**unsigned __int64**|**uint64**|  
|Ponto flutuante|<xref:System.Single>|Um número de ponto flutuante de precisão simples (32 bits).|**Single**|**float**|**float**|**float32**<br> ou<br>**single**|  
||<xref:System.Double>|Um número de ponto flutuante de precisão dupla (64 bits).|**Double**|**double**|**double**|**float**<br> ou <br> **double**|  
|Lógico|<xref:System.Boolean>|Um valor booliano (verdadeiro ou falso).|**Booliano**|**bool**|**bool**|**bool**|  
|Outro|<xref:System.Char>|Um caractere Unicode (16 bits).|**º**|**char**|**wchar_t**|**char**|  
||<xref:System.Decimal>|Um valor decimal (128 bits).|**Decimal**|**decimal**|**Decimal**|**decimal**|  
||<xref:System.IntPtr>|Um inteiro com sinal cujo tamanho dependa da plataforma subjacente (um valor de 32 bits em uma plataforma de 32 bits e um valor de 64 bits em uma plataforma de 64 bits).|**IntPtr**<br /><br /> Nenhum tipo interno.|**IntPtr**<br /><br /> Nenhum tipo interno.|**IntPtr**<br /><br /> Nenhum tipo interno.|**unativeint**|  
||<xref:System.UIntPtr>|Um inteiro sem sinal cujo tamanho dependa da plataforma subjacente (um valor de 32 bits em uma plataforma de 32 bits e um valor de 64 bits em uma plataforma de 64 bits).<br /><br /> Não compatível com CLS.|**UIntPtr**<br /><br /> Nenhum tipo interno.|**UIntPtr**<br /><br /> Nenhum tipo interno.|**UIntPtr**<br /><br /> Nenhum tipo interno.|**unativeint**|  
||<xref:System.Object>|A raiz da hierarquia do objeto.|**Objeto**|**object**|**Objeto ^**|**obj**|  
||<xref:System.String>|Uma cadeia de caracteres Unicode imutável e de comprimento fixo.|**Cadeia de caracteres**|**cadeia de caracteres**|**Cadeia de caracteres ^**|**cadeia de caracteres**|  
  
 Além dos tipos de dados base, o namespace <xref:System> contém mais de 100 classes, que vão desde classes que identificam exceções até classes que lidam com os conceitos de runtime, como domínios de aplicativo e o coletor de lixo. O namespace <xref:System> também contém vários namespaces de segundo nível.  
  
 Para obter mais informações sobre namespaces, use o [Navegador de API do .NET](../../api/index.md) para procurar a Biblioteca de classes do .NET. A documentação de referência de API fornece informações sobre cada namespace, seus tipos e cada um dos seus membros.  
  
## <a name="see-also"></a>Confira também

- [Common Type System](base-types/common-type-system.md)
- [Navegador de API .NET](../../api/index.md)
- [Visão geral](../framework/get-started/overview.md)
