---
description: '#Nullable-referência C#'
title: '#Nullable-referência C#'
ms.date: 11/18/2020
f1_keywords:
- '#nullable'
helpviewer_keywords:
- '#nullable directive [C#]'
ms.openlocfilehash: 4c114a09f29769fcc824bcdabdc1d523e33f199d
ms.sourcegitcommit: 30e9e11dfd90112b8eec6406186ba3533f21eba1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2020
ms.locfileid: "95099456"
---
# <a name="nullable-c-reference"></a>#nullable (referência C#)

A `#nullable` diretiva de pré-processador define o *contexto de anotação anulável* e o *contexto de aviso anulável*. Essa diretiva controla se as anotações anuláveis têm efeito e se são fornecidos avisos de nulidade. Cada contexto é *desabilitado* ou *habilitado*.

Ambos os contextos podem ser especificados no nível do projeto (fora do código-fonte do C#). A `#nullable` diretiva controla os contextos de anotação e de aviso e tem precedência sobre as configurações de nível de projeto. Uma diretiva define os contextos que ele controla até que outra diretiva o substitua, ou até o final do arquivo de origem.

O efeito das diretivas é o seguinte:

- `#nullable disable`: Define a anotação anulável e contextos de aviso como *desabilitado*.
- `#nullable enable`: Define a anotação anulável e contextos de aviso como *habilitado*.
- `#nullable restore`: Restaura os contextos de anotação e de aviso anuláveis para as configurações do projeto.
- `#nullable disable annotations`: Define o contexto de anotação anulável como *desabilitado*.
- `#nullable enable annotations`: Define o contexto de anotação anulável como *habilitado*.
- `#nullable restore annotations`: Restaura o contexto de anotação anulável para as configurações do projeto.
- `#nullable disable warnings`: Define o contexto de aviso anulável como *desabilitado*.
- `#nullable enable warnings`: Define o contexto de aviso anulável como *habilitado*.
- `#nullable restore warnings`: Restaura o contexto de aviso anulável para as configurações do projeto.

## <a name="see-also"></a>Confira também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Diretivas de pré-processador do C#](./index.md)
