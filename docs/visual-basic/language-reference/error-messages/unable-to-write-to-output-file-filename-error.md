---
description: "Saiba mais sobre: BC31019: não é possível gravar no arquivo de saída ' <filename> ': <error>"
title: "Não é possível gravar no arquivo de saída '<filename>': <error>"
ms.date: 07/20/2015
f1_keywords:
- vbc31019
- bc31019
helpviewer_keywords:
- BC31019
ms.assetid: 0845b245-11bb-46fd-95ca-f6cef3c318ef
ms.openlocfilehash: 4a1feff6429a5b82968d3a87e4c9c9ef80e6612a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99640895"
---
# <a name="bc31019-unable-to-write-to-output-file-filename-error"></a>BC31019: não é possível gravar no arquivo de saída ' \<filename> ': \<error>

Ocorreu um problema na criação do arquivo.

 Não foi possível abrir um arquivo de saída para gravação. O arquivo (ou a pasta que contém o arquivo) pode estar aberto para uso exclusivo por outro processo ou pode ter seu atributo definido como somente leitura.

 Algumas situações comuns em que um arquivo fica aberto exclusivamente são quando:

- O aplicativo está em execução e usando os arquivos dele. Para resolver esse problema, verifique se o aplicativo não está em execução.

- Outro aplicativo abriu o arquivo. Para resolver esse problema, verifique se nenhum outro aplicativo está acessando os arquivos. Nem sempre é óbvio qual aplicativo está acessando seus arquivos. Nesse caso, reiniciar o computador pode ser o caminho mais fácil para encerrar o aplicativo.

 Se apenas um dos arquivos de saída do projeto estiver marcado como somente leitura, esta exceção será acionada.

 **ID do erro:** BC31019

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Compile o programa novamente para verificar se o erro persiste.

2. Se o erro continuar, salve seu trabalho e reinicie o Visual Studio.

3. Se o erro persistir, reinicie o computador.

4. Se o erro se repetir, reinstale Visual Basic.

5. Se o erro persistir após a reinstalação, notifique o Microsoft Product Support Services.

### <a name="to-check-file-attributes-in-file-explorer"></a>Para verificar atributos de arquivo no Explorador de Arquivos

1. Abra a pasta que lhe interessa.

2. Clique no ícone **exibições** e escolha **detalhes**.

3. Clique com o botão direito do mouse no cabeçalho da coluna e escolha **atributos** na lista suspensa.

### <a name="to-change-the-attributes-of-a-file-or-folder"></a>Para alterar os atributos de um arquivo ou pasta

1. No **Explorador de arquivos**, clique com o botão direito do mouse no arquivo ou pasta e escolha **Propriedades**.

2. Na seção **atributos** da guia **geral** , desmarque a caixa **somente leitura** .

3. Pressione **OK**.

## <a name="see-also"></a>Consulte também

- [Fale conosco](/visualstudio/ide/feedback-options)
