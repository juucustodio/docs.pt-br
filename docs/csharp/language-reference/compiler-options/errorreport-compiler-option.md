---
description: -errorreport (opções do compilador C#)
title: -errorreport (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /errorreport
helpviewer_keywords:
- -errorreport compiler option [C#]
- errorreport compiler option [C#]
- /errorreport compiler option [C#]
ms.assetid: bd0e7493-b79d-4369-9c3f-ba26ebdfbedf
ms.openlocfilehash: 6238ac392ff99d18d9cc7ea07e23b08ff235c14f
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91173224"
---
# <a name="-errorreport-c-compiler-options"></a>-errorreport (opções do compilador C#)

Esta opção fornece uma maneira conveniente de relatar um erro interno do compilador do C# à Microsoft.

> [!NOTE]
> No Windows Vista e Windows Server 2008, as configurações de relatório de erros que você faz para o Visual Studio não substituem as configurações feitas pelo WER (Relatório de Erros do Windows). As configurações do WER sempre têm precedência sobre as configurações de relatório de erros do Visual Studio.

## <a name="syntax"></a>Sintaxe

```console
-errorreport:{ none | prompt | queue | send }
```

## <a name="arguments"></a>Argumentos

 **nenhum**  
 Relatórios sobre erros internos do compilador não serão coletados ou enviados à Microsoft.

 **aviso** Solicita que você envie um relatório quando recebe um erro de compilador interno. **prompt** é o padrão quando você compila um aplicativo no ambiente de desenvolvimento.

 **fila** Enfileira o relatório de erros. Quando você faz logon com credenciais administrativas, pode relatar falhas desde a última vez que você fez logon. Não será solicitado que você envie relatórios de falhas mais de uma vez a cada três dias. **queue** é o padrão quando você compila um aplicativo na linha de comando.

 **Enviar** Envia automaticamente relatórios de erros de compilador interno à Microsoft. Para habilitar essa opção, primeiro você deve concordar com a política de coleta de dados da Microsoft. Na primeira vez que você especificar **-errorreport:send** em um computador, uma mensagem de compilador indicará um site que contém a política de coleta de dados da Microsoft.

## <a name="remarks"></a>Comentários

 Um ICE (erro interno do compilador) ocorre quando o compilador não pode processar um arquivo de código-fonte. Quando um ICE ocorre, o compilador não produz um arquivo de saída ou qualquer diagnóstico útil que você pode usar para corrigir o código.

 Em versões anteriores, quando você recebia um ICE, era incentivado a entrar em contato com o Microsoft Product Support Services para relatar o problema. Usando **-errorreport**, você pode fornecer informações do ICE à equipe do Visual C#. Os relatórios de erro podem ajudar a melhorar versões futuras do compilador.

 A capacidade do usuário de enviar relatórios depende das permissões de política de usuário e de computador.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio

1. Abra a página **Propriedades** do projeto. Para obter mais informações, consulte [Página Build, Designer de Projeto (C#)](/visualstudio/ide/reference/build-page-project-designer-csharp).

2. Clique na página de propriedades **Compilar**.

3. Clique no botão **Avançado** .

4. Modifique a propriedade **Relatório de Erros do Compilador Interno**.

 Para saber mais sobre como definir essa opção do compilador programaticamente, veja <xref:VSLangProj80.CSharpProjectConfigurationProperties3.ErrorReport%2A>.

## <a name="see-also"></a>Confira também

- [Opções do compilador de C#](./index.md)
