---
title: Aplicativos Azure Functions-sem servidor
description: O Azure Functions fornece recursos sem servidor em vários idiomas (C#, JavaScript, Java) e plataformas para fornecer código de escala instantânea controlado por eventos.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 04/06/2020
ms.openlocfilehash: 08e1aaecdee753dc25cca0d6356caaafae1ad510
ms.sourcegitcommit: f99115e12a5eb75638abe45072e023a3ce3351ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2020
ms.locfileid: "94557110"
---
# <a name="azure-functions"></a>Azure Functions

Azure Functions fornecer uma experiência de computação sem servidor. Uma função é invocada por um *gatilho* (como o acesso a um ponto de extremidade http ou um temporizador) e executa um bloco de código ou lógica de negócios. As funções também dão suporte a *associações* especializadas que se conectam a recursos como armazenamento e filas.

![Logotipo do Azure Functions](./media/azure-functions-logo.png)

A versão de tempo de execução atual 3,0 dá suporte a aplicativos .NET Core 3,1 de plataforma cruzada. Há suporte para idiomas adicionais além do C#, como JavaScript, F # e Java. As funções criadas no portal fornecem uma sintaxe de script avançada. As funções criadas como projetos autônomos podem ser implantadas com recursos e suporte completos à plataforma.

Para obter mais informações, consulte a [documentação do Azure Functions](/azure/azure-functions).

## <a name="programming-language-support"></a>Suporte à linguagem de programação

Todos os idiomas a seguir têm suporte na disponibilidade geral (GA).

|Idioma      |Tempos de execução com suporte|
|--------------|------------------|
|**C#**        |.NET Core 3.1     |
|**JavaScript**|Nó 10 & 12      |
|**F#**        |.NET Core 3.1     |
|**Java**      |Java 8            |
|**Python**    |Python 3,6, 3,7, & 3,8|
|**TypeScript**|Nó 10 & 12 (via JavaScript)|
|**PowerShell**|PowerShell Core 6|

Para obter mais informações, consulte [Linguagens com suporte](/azure/azure-functions/supported-languages).

## <a name="app-service-plans"></a>Planos do serviço de aplicativo

As funções são apoiadas por um *plano do serviço de aplicativo*. O plano define os recursos usados pelo aplicativo de funções. Você pode atribuir planos a uma região, determinar o tamanho e o número de máquinas virtuais que serão usadas e escolher um tipo de preço. Para uma abordagem verdadeira sem servidor, os aplicativos de função podem usar o plano de **consumo** . O plano de consumo dimensionará o back-end automaticamente com base na carga.

Outra opção de hospedagem para aplicativos de funções é o [plano Premium](/azure/azure-functions/functions-premium-plan). Esse plano fornece uma instância "Always on" para evitar o início frio, dá suporte a recursos avançados como conectividade VNet e é executado em hardware Premium.

Para obter mais informações, consulte [planos do serviço de aplicativo](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).

## <a name="create-your-first-function"></a>Criar sua primeira função

Há três maneiras comuns de criar aplicativos de funções.

- Funções de script no Portal.
- Crie os recursos necessários usando o CLI do Azure.
- Crie funções localmente usando seu IDE favorito e publique-as no Azure.

Para obter mais informações sobre como criar uma função com script no portal, consulte [criar sua primeira função no portal do Azure](/azure/azure-functions/functions-create-first-azure-function).

Para criar a partir do CLI do Azure, consulte [criar sua primeira função usando o CLI do Azure](/azure/azure-functions/functions-create-first-azure-function-azure-cli).

Para criar uma função do Visual Studio, consulte [criar sua primeira função usando o Visual Studio](/azure/azure-functions/functions-create-your-first-function-visual-studio).

## <a name="understand-triggers-and-bindings"></a>Entender gatilhos e associações

As funções são invocadas por um *gatilho* e podem ter exatamente uma. Além de invocar a função, determinados gatilhos também servem como associações. Você também pode definir várias associações além do gatilho. As *associações* fornecem uma maneira declarativa de conectar dados ao seu código. Eles podem ser passados (entrada) ou receber dados (saída). Os gatilhos e as associações facilitam o trabalho com as funções. As associações removem a sobrecarga de criar manualmente as conexões do banco de dados ou do sistema de arquivos. Todas as informações necessárias para as associações estão contidas em umfunctions.jsespecial *no* arquivo para scripts ou declaradas com atributos no código.

Alguns gatilhos comuns incluem:

- Armazenamento de BLOBs: invoque sua função quando um arquivo ou pasta for carregado ou alterado no armazenamento.
- HTTP: invoque sua função como uma API REST.
- Fila: invoque sua função quando houver itens em uma fila.
- Temporizador: invocar sua função em uma cadência regular.

Exemplos de associações incluem:

- CosmosDB: Conecte-se facilmente ao banco de dados para carregar ou salvar arquivos.
- Armazenamento de tabelas: trabalhe com o armazenamento de chave/valor do seu aplicativo de funções.
- Armazenamento de filas: recuperar facilmente itens de uma fila ou colocar novos itens na fila.

O exemplo a seguir *functions.jsno* arquivo define um gatilho e uma associação:

```json
{
  "bindings": [
    {
      "name": "myBlob",
      "type": "blobTrigger",
      "direction": "in",
      "path": "images/{name}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "$return",
      "type": "queue",
      "direction": "out",
      "queueName": "images",
      "connection": "AzureWebJobsStorage"
    }
  ],
  "disabled": false
}
```

Neste exemplo, a função é disparada por uma alteração no armazenamento de BLOBs no `images` contêiner. As informações para o arquivo são passadas para que o gatilho também atue como uma associação. Existe outra associação para colocar informações em uma fila chamada `images` .

Este é o script C# para a função:

```csharp
public static string Run(Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
    return name;
}
```

O exemplo é uma função simples que usa o nome do arquivo que foi modificado ou carregado no armazenamento de BLOBs e o coloca em uma fila para processamento posterior.

Para obter uma lista completa de gatilhos e associações, consulte [Azure Functions os conceitos de gatilhos e associações](/azure/azure-functions/functions-triggers-bindings).

>[!div class="step-by-step"]
>[Anterior](azure-serverless-platform.md) 
> [Avançar](application-insights.md)
