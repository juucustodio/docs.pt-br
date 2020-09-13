---
title: Como criar exemplos de LINQ to XML
description: O código C# e Visual Basic nesta documentação usa classes e tipos de vários namespaces. Para compilar e executar o código, você deve fornecer as diretivas e instruções apropriadas para acessar os namespaces.
ms.date: 07/20/2015
ms.assetid: e5d18fa1-2704-48fe-a44b-1564f97c9e9c
ms.openlocfilehash: 94b2368e2c861f84d7db08fbbba57ef0f0da4d40
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551890"
---
# <a name="how-to-build-linq-to-xml-examples"></a>Como criar exemplos de LINQ to XML

Os trechos de código e os exemplos nesta documentação usam classes e tipos de vários namespaces. Ao compilar o código C#, você precisa fornecer as `using` diretivas apropriadas e, ao compilar Visual Basic código, precisa fornecer `Imports` instruções apropriadas.

## <a name="example"></a>Exemplo

O código a seguir contém diretivas de `using` que os exemplos de C# exigem para compilar e executar. Nem todas as diretivas de `using` são necessárias para todos os exemplos.

```csharp
using System;
using System.Diagnostics;
using System.Collections;
using System.Collections.Generic;
using System.Collections.Specialized;
using System.Text;
using System.Linq;
using System.Xml;
using System.Xml.Linq;
using System.Xml.Schema;
using System.Xml.XPath;
using System.Xml.Xsl;
using System.IO;
using System.Threading;
using System.Reflection;
using System.IO.Packaging;
```

O código a seguir contém instruções de `Imports` que os exemplos de Visual Basic exigem para compilar e executar. Nem todas as instruções de `Imports` são necessárias para todos os exemplos.

```vb
Imports System.Diagnostics
Imports System.Collections
Imports System.Collections.Generic
Imports System.Collections.Specialized
Imports System.Text
Imports System.Linq
Imports System.Xml
Imports System.Xml.Linq
Imports System.Xml.Schema
Imports System.Xml.XPath
Imports System.Xml.Xsl
Imports System.IO
Imports System.Threading
Imports System.Reflection
Imports System.IO.Packaging
```

## <a name="see-also"></a>Confira também

- [Visão geral de LINQ to XML](linq-xml-overview.md)
