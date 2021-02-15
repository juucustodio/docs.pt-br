---
title: Carregar dados de arquivos e outras fontes
description: Saiba como carregar dados para processamento e treinamento no ML.NET usando a API. São armazenados em arquivos, bancos de dados, JSON, XML ou coleções na memória.
ms.date: 11/07/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc,how-to, title-hack-0625
ms.openlocfilehash: edcb1c4d00a09ba8404b08ddc3ca3447a52a81b6
ms.sourcegitcommit: aa6d8a90a4f5d8fe0f6e967980b8c98433f05a44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90679580"
---
# <a name="load-data-from-files-and-other-sources"></a>Carregar dados de arquivos e outras fontes

Saiba como carregar dados para processamento e treinamento no ML.NET usando a API. Originalmente, os dados são armazenados em arquivos ou outras fontes de dados, como bancos de dados, JSON, XML ou coleções na memória.

Se você estiver usando o construtor de modelos, consulte [carregar dados de treinamento no construtor de modelos](load-data-model-builder.md).

## <a name="create-the-data-model"></a>Criar o modelo de dados

O ML.NET permite que você defina modelos de dados por meio de classes. Por exemplo, considerando os seguintes dados de entrada:

```text
Size (Sq. ft.), HistoricalPrice1 ($), HistoricalPrice2 ($), HistoricalPrice3 ($), Current Price ($)
700, 100000, 3000000, 250000, 500000
1000, 600000, 400000, 650000, 700000
```

Crie um modelo de dados que represente o snippet a seguir:

```csharp
public class HousingData
{
    [LoadColumn(0)]
    public float Size { get; set; }

    [LoadColumn(1, 3)]
    [VectorType(3)]
    public float[] HistoricalPrices { get; set; }

    [LoadColumn(4)]
    [ColumnName("Label")]
    public float CurrentPrice { get; set; }
}
```

### <a name="annotating-the-data-model-with-column-attributes"></a>Anotando o modelo de dados com atributos de coluna

Atributos dão ao ML.NET mais informações sobre o modelo de dados e a fonte de dados.

O [`LoadColumn`](xref:Microsoft.ML.Data.LoadColumnAttribute) atributo especifica os índices de coluna de suas propriedades.

> [!IMPORTANT]
> [`LoadColumn`](xref:Microsoft.ML.Data.LoadColumnAttribute) Só é necessário ao carregar dados de um arquivo.

Carregar colunas como:

- Colunas individuais como `Size` e `CurrentPrices` na classe `HousingData`.
- Como várias colunas por vez na forma de um vetor `HistoricalPrices` na classe `HousingData`.

Se você tiver uma propriedade Vector, aplique o [`VectorType`](xref:Microsoft.ML.Data.VectorTypeAttribute) atributo à propriedade em seu modelo de dados. É importante observar que todos os elementos no vetor precisam ser do mesmo tipo. Manter as colunas separadas permite a facilidade e a flexibilidade da engenharia de recursos, mas, para um número muito grande de colunas, a operação nas colunas individuais causa um impacto na velocidade de treinamento.

O ML.NET opera por meio de nomes de coluna. Se você quiser alterar o nome de uma coluna para algo diferente do nome da propriedade, use o [`ColumnName`](xref:Microsoft.ML.Data.ColumnNameAttribute) atributo. Ao criar objetos na memória, você ainda cria objetos usando o nome da propriedade. No entanto, para o processamento de dados e a criação de modelos de aprendizado de máquina, o ML.NET substitui e faz referência à propriedade com o valor fornecido no [`ColumnName`](xref:Microsoft.ML.Data.ColumnNameAttribute) atributo.

## <a name="load-data-from-a-single-file"></a>Carregar dados de um único arquivo

Para carregar dados de um arquivo, use o [`LoadFromTextFile`](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%2A) método junto com o modelo de dados para os dados a serem carregados. Uma vez que o parâmetro `separatorChar` é delimitado por tabulação por padrão, altere-o para seu arquivo de dados conforme necessário. Se o arquivo tiver um cabeçalho, defina o parâmetro `hasHeader` como `true` para ignorar a primeira linha no arquivo e começar a carregar dados da segunda linha.

```csharp
//Create MLContext
MLContext mlContext = new MLContext();

//Load Data
IDataView data = mlContext.Data.LoadFromTextFile<HousingData>("my-data-file.csv", separatorChar: ',', hasHeader: true);
```

## <a name="load-data-from-multiple-files"></a>Carregar dados de vários arquivos

Caso seus dados sejam armazenados em vários arquivos, desde que o esquema de dados seja o mesmo, o ML.NET permitirá que você carregue dados de vários arquivos que estejam no mesmo diretório ou em vários diretórios.

### <a name="load-from-files-in-a-single-directory"></a>Carregar de arquivos em um único diretório

Quando todos os arquivos de dados estiverem no mesmo diretório, use curingas no [`LoadFromTextFile`](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%2A) método.

```csharp
//Create MLContext
MLContext mlContext = new MLContext();

//Load Data File
IDataView data = mlContext.Data.LoadFromTextFile<HousingData>("Data/*", separatorChar: ',', hasHeader: true);
```

### <a name="load-from-files-in-multiple-directories"></a>Carregar de arquivos em vários diretórios

Para carregar dados de vários diretórios, use o [`CreateTextLoader`](xref:Microsoft.ML.TextLoaderSaverCatalog.CreateTextLoader%2A) método para criar um [`TextLoader`](xref:Microsoft.ML.Data.TextLoader) . Em seguida, use o [`TextLoader.Load`](xref:Microsoft.ML.DataLoaderExtensions.Load%2A) método e especifique os caminhos de arquivo individuais (curingas não podem ser usados).

```csharp
//Create MLContext
MLContext mlContext = new MLContext();

// Create TextLoader
TextLoader textLoader = mlContext.Data.CreateTextLoader<HousingData>(separatorChar: ',', hasHeader: true);

// Load Data
IDataView data = textLoader.Load("DataFolder/SubFolder1/1.txt", "DataFolder/SubFolder2/1.txt");
```

## <a name="load-data-from-a-relational-database"></a>Carregar dados de um banco de dado relacional

O ML.NET dá suporte ao carregamento de dados de uma variedade de bancos de dado relacionais com suporte pelo [`System.Data`](xref:System.Data) que incluem SQL Server, banco de dados SQL do Azure, Oracle, SQLite, PostgreSQL, progresso, IBM DB2 e muito mais.

> [!NOTE]
> Para usar `DatabaseLoader` o, referencie o pacote NuGet [System. Data. SqlClient](https://www.nuget.org/packages/System.Data.SqlClient) .

Dado um banco de dados com uma tabela chamada `House` e o esquema a seguir:

```sql
CREATE TABLE [House] (
    [HouseId] INT NOT NULL IDENTITY,
    [Size] INT NOT NULL,
    [NumBed] INT NOT NULL,
    [Price] REAL NOT NULL
    CONSTRAINT [PK_House] PRIMARY KEY ([HouseId])
);
```

Os dados podem ser modelados por uma classe como `HouseData`.

```csharp
public class HouseData
{
    public float Size { get; set; }

    public float NumBed { get; set; }

    public float Price { get; set; }
}
```

Em seguida, dentro do seu aplicativo, crie um `DatabaseLoader` .

```csharp
MLContext mlContext = new MLContext();

DatabaseLoader loader = mlContext.Data.CreateDatabaseLoader<HouseData>();
```

Defina a cadeia de conexão, bem como o comando SQL a ser executado no banco de dados e crie uma `DatabaseSource` instância. Este exemplo usa um banco de dados SQL Server LocalDB com um caminho de arquivo. No entanto, o DatabaseLoader dá suporte a qualquer outra cadeia de conexão válida para bancos de dados locais e na nuvem.

```csharp
string connectionString = @"Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=<YOUR-DB-FILEPATH>;Database=<YOUR-DB-NAME>;Integrated Security=True;Connect Timeout=30";

string sqlCommand = "SELECT Size, CAST(NumBed as REAL) as NumBed, Price FROM House";

DatabaseSource dbSource = new DatabaseSource(SqlClientFactory.Instance, connectionString, sqlCommand);
```

Dados numéricos que não são do tipo [`Real`](xref:System.Data.SqlDbType) têm que ser convertidos em [`Real`](xref:System.Data.SqlDbType) . O [`Real`](xref:System.Data.SqlDbType) tipo é representado como um valor de ponto flutuante de precisão simples ou [`Single`](xref:System.Single) , o tipo de entrada esperado por algoritmos ml.net. Neste exemplo, a `NumBed` coluna é um número inteiro no banco de dados. Usando a `CAST` função interna, ela é convertida em [`Real`](xref:System.Data.SqlDbType) . Como a `Price` Propriedade já é do tipo [`Real`](xref:System.Data.SqlDbType) , ela é carregada como está.

Use o `Load` método para carregar os dados em um [`IDataView`](xref:Microsoft.ML.IDataView) .

```csharp
IDataView data = loader.Load(dbSource);
```

## <a name="load-data-from-other-sources"></a>Carregar dados de outras fontes

Além de carregar os dados armazenados em arquivos, o ML.NET dá suporte ao carregamento de dados de várias fontes que incluem, mas não se limitam a:

- Coleções na memória
- JSON/XML

Observe que, ao trabalhar com fontes de streaming, o ML.NET espera que a entrada esteja na forma de uma coleção em memória. Portanto, ao trabalhar com fontes, como JSON/XML, formate os dados em uma coleção em memória.

Dada a coleção em memória a seguir:

```csharp
HousingData[] inMemoryCollection = new HousingData[]
{
    new HousingData
    {
        Size =700f,
        HistoricalPrices = new float[]
        {
            100000f, 3000000f, 250000f
        },
        CurrentPrice = 500000f
    },
    new HousingData
    {
        Size =1000f,
        HistoricalPrices = new float[]
        {
            600000f, 400000f, 650000f
        },
        CurrentPrice=700000f
    }
};
```

Carregue a coleção na memória em um [`IDataView`](xref:Microsoft.ML.IDataView) com o [`LoadFromEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.LoadFromEnumerable%2A) método:

> [!IMPORTANT]
> [`LoadFromEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.LoadFromEnumerable%2A) pressupõe que o [`IEnumerable`](xref:System.Collections.IEnumerable) seu carregamento é seguro para threads.

```csharp
// Create MLContext
MLContext mlContext = new MLContext();

//Load Data
IDataView data = mlContext.Data.LoadFromEnumerable<HousingData>(inMemoryCollection);
```

## <a name="next-steps"></a>Próximas etapas

- Para limpar ou, de outra forma, processar dados, consulte [preparar dados para criar um modelo](prepare-data-ml-net.md).
- Quando estiver pronto para criar um modelo, consulte [treinar e avaliar um modelo](train-machine-learning-model-ml-net.md).
