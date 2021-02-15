---
description: 'Saiba mais sobre: conjuntos de valores tipados'
title: DataSets tipados
ms.date: 03/30/2017
ms.assetid: 033d2548-cf24-4c05-8179-67d8b009c048
ms.openlocfilehash: 698efbe52e960afe00ca337445df919545d8437e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651490"
---
# <a name="typed-datasets"></a>DataSets tipados

Juntamente com acesso de associação tardia por meio de valores com variáveis fracamente tipadas, o <xref:System.Data.DataSet> fornece acesso a dados por meio de uma metáfora fortemente tipada. Tabelas e colunas que fazem parte do **conjunto** de um podem ser acessadas usando nomes amigáveis de usuário e variáveis com rigidez de tipos.  
  
 Um **DataSet** tipado é uma classe derivada de um **DataSet**. Como tal, ele herda todos os métodos, eventos e propriedades de um **conjunto** de uma. Além disso, um **DataSet** tipado fornece métodos, eventos e propriedades com rigidez de tipos. Isso significa que você pode acessar tabelas e colunas pelo nome, em vez de usar métodos baseados em coleção. Além da melhor legibilidade do código, um **DataSet** tipado também permite que o editor de código do Visual Studio .net preencha automaticamente as linhas conforme você digita.  
  
 Além disso, o **conjunto** de texto com rigidez de tipos fornece acesso a valores como o tipo correto no momento da compilação. Com um **conjunto** de texto com rigidez de tipos, erros de tipo incompatíveis são capturados quando o código é compilado em vez de em tempo de execução.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Gerando DataSets fortemente tipados](generating-strongly-typed-datasets.md)  
 Descreve como criar e usar um conjunto de um **DataSet** com rigidez de tipos.  
  
 [Anotando DataSets tipados](annotating-typed-datasets.md)  
 Descreve como anotar o esquema XSD (linguagem de definição de esquema XML) usado para gerar um **conjunto** de dado com rigidez de tipos, para dar aos elementos do **conjunto** de dado nomes amigáveis sem alterar o esquema subjacente.  
  
## <a name="see-also"></a>Consulte também

- [DataSets, DataTables e DataViews](index.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
