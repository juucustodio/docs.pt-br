---
title: Arquivos de configuração predefinidos (análise de código)
description: Saiba como usar editorconfig predefinidos e arquivos de conjunto de regras para direcionar tipos específicos de análise de código.
ms.date: 09/24/2020
ms.topic: conceptual
ms.openlocfilehash: 4937dcab1183fa3f63be4afc71627a7c7c08c6bd
ms.sourcegitcommit: 665f8fc55258356f4d2f4a6585b750c974b26675
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/30/2020
ms.locfileid: "96585036"
---
# <a name="predefined-configuration-files"></a>Arquivos de configuração predefinidos

Os arquivos de [conjunto de regras](/visualstudio/code-quality/using-rule-sets-to-group-code-analysis-rules) e EditorConfig predefinidos estão disponíveis para facilitar e facilitar a habilitação de uma categoria de regras de qualidade de código, como segurança ou regras de design. Ao habilitar uma categoria específica de regras, você pode identificar problemas direcionados e condições específicas. Para acessar esses arquivos predefinidos, instale o pacote analisador NuGet do [Microsoft. CodeAnalysis. Netanalyzers](https://github.com/dotnet/roslyn-analyzers#microsoftcodeanalysisnetanalyzers) .

[Microsoft. CodeAnalysis. Netanalyzers](https://github.com/dotnet/roslyn-analyzers#microsoftcodeanalysisnetanalyzers) inclui arquivos EditorConfig predefinidos e conjuntos de regras para as seguintes categorias de regra:

- Todas as regras
- Fluxo de dados
- Design
- Documentação
- Globalização
- Interoperabilidade
- Facilidade de manutenção
- Nomenclatura
- Desempenho
- Portado do FxCop
- Confiabilidade
- Segurança
- Uso

Cada uma dessas categorias de regras tem um EditorConfig ou um arquivo de conjunto de regras para:

- Habilitar todas as regras na categoria (e desabilitar todas as outras regras)
- Usar a severidade padrão de cada regra e habilitada por configuração padrão (e desabilitar todas as outras regras)

> [!TIP]
> A categoria "todas as regras" tem um EditorConfig adicional ou um arquivo de conjunto de regras para desabilitar todas as regras. Use esse arquivo para eliminar rapidamente qualquer erro ou aviso do analisador em um projeto.

## <a name="predefined-editorconfig-files"></a>Arquivos EditorConfig predefinidos

Os arquivos EditorConfig predefinidos para o pacote do analisador Microsoft. CodeAnalysis. netanalyzers estão localizados no subdiretório *EditorConfig* do qual o pacote NuGet foi instalado. Por exemplo, o arquivo EditorConfig para habilitar todas as regras de segurança está localizado em *EditorConfig/SecurityRulesEnabled/. EditorConfig*.

Copie o arquivo *. editorconfig* escolhido para o diretório raiz do projeto.

## <a name="predefined-rule-sets"></a>Conjuntos de regras predefinidas

Os arquivos de conjunto de regras predefinidos para o pacote do analisador Microsoft. CodeAnalysis. netanalyzers estão localizados no subdiretório *RuleSets* de onde o pacote NuGet foi instalado. Por exemplo, o arquivo de conjunto de regras para habilitar todas as regras de segurança está localizado em *RuleSets/SecurityRulesEnabled. RuleSet*. Copie um ou mais conjuntos de regras e cole-os no diretório que contém o projeto.

## <a name="see-also"></a>Confira também

- [Configuração do analisador](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md)
- [Opções de regra de estilo de código .NET para EditorConfig](code-style-rule-options.md)
