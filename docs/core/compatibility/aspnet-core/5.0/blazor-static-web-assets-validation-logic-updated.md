---
title: 'Alteração significativa: mais incrivelmente: lógica de validação atualizada para ativos da Web estáticos'
description: 'Saiba mais sobre as alterações significativas no ASP.NET Core 5,0 intitulados mais recentes: lógica de validação atualizada para ativos da Web estáticos'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: f201818c0130739e8da4f42e7b1f3a1987f70d1c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760376"
---
# <a name="blazor-updated-validation-logic-for-static-web-assets"></a>Mais incrivelmente: lógica de validação atualizada para ativos da Web estáticos

Houve um problema na validação de conflito para ativos da Web estáticos no ASP.NET Core 3,1 e no Webassembly 3,2 de mais. O problema:

* Impedia a detecção adequada de conflitos entre os ativos do host e os ativos das bibliotecas de classe Razor (RCLs) e dos aplicativos Webassembly mais valiosos.
* Afeta principalmente os aplicativos Webassembly mais valiosos, já que, por padrão, os ativos da Web estáticos no RCLs são servidos sob o `_content/$(PackageId)` prefixo.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="old-behavior"></a>Comportamento antigo

Durante o desenvolvimento, os ativos da Web estáticos de um RCL podem ser silenciosamente substituídos por ativos de projeto de host na mesma caminho do host. Considere um RCL que definiu um ativo estático da Web para ser servido em */folder/file.txt*. Se o host colocou um arquivo em *wwwroot/pasta/file.txt*, o arquivo no servidor substituiu silenciosamente o arquivo no aplicativo Webassembly RCL ou mais novo.

## <a name="new-behavior"></a>Novo comportamento

ASP.NET Core detecta corretamente quando esse problema ocorre. Ele informa a você, o usuário, do conflito para que você possa executar a ação apropriada.

## <a name="reason-for-change"></a>Motivo da alteração

Os ativos da Web estáticos não devem ser substituíveis por arquivos no host *wwwroot* do projeto. Permitir a substituição desses arquivos pode levar a erros que são difíceis de diagnosticar. O resultado pode ser alterações de comportamento indefinido em aplicativos publicados.

## <a name="recommended-action"></a>Ação recomendada

Por padrão, não há motivo para um arquivo RCL entrar em conflito com um arquivo no host. Os arquivos RCL são prefixados com `_content/${PackageId}` . Os arquivos Webassembly mais claros são colocados na raiz do espaço de URL do host, o que torna os conflitos mais fáceis. Por exemplo, os aplicativos Webassembly mais poseriais contêm um arquivo *favicon. ico* que o host também pode incluir em sua pasta *wwwroot* .

Se a origem do conflito for um arquivo RCL, isso geralmente significa que o código está copiando os ativos da biblioteca para a pasta *wwwroot* do projeto. Escrever código para copiar arquivos anula um objetivo principal de ativos da Web estáticos. Essa meta é fundamental para obter atualizações no navegador quando o conteúdo é atualizado sem a necessidade de disparar uma nova compilação.

Você pode optar por preservar esse comportamento e manter o arquivo no host. Para fazer isso, remova o arquivo da lista de ativos da Web estáticos com um destino MSBuild personalizado.

Para usar o arquivo do RCL ou o arquivo do aplicativo Webassembly mais novo, em vez do arquivo do projeto host, remova o arquivo do projeto host.

## <a name="affected-apis"></a>APIs afetadas

Nenhum

<!--

### Category

ASP.NET Core

### Affected APIs

Not detectable via API analysis

-->
