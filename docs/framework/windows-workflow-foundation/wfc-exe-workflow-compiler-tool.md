---
title: Wfc.exe (ferramenta de compilador de linha de comando do fluxo de trabalho)
description: Entenda wfc.exe, a ferramenta de compilador de linha de comando do fluxo de trabalho.
ms.date: 10/10/2020
helpviewer_keywords:
- wfc [Workflow]
- compiler tool
- wfc.exe
- Workflow, compilation
- Workflow, XOML files
- Workflow, wcf
ms.openlocfilehash: 01cbfeb72e19f727a3a470059047a2192228c394
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293852"
---
# <a name="wfcexe-workflow-command-line-compiler-tool"></a>wfc.exe (ferramenta de compilador de linha de comando do fluxo de trabalho)

> [!NOTE]
> Este material discute tipos e namespaces obsoletos.

A ferramenta de compilador de linha de comando de wfc.exe fluxo de trabalho funciona com arquivos de marcação de fluxo de trabalho antigos que têm a extensão de arquivo *. xoml* (obsoleto).

## <a name="compilation-process"></a>Processo de compilação

Quando os fluxos de trabalho são compilados, os procedimentos a seguir são executados como parte do processo de compilação:

- A validação é executada para garantir que as atividades de fluxo de trabalho sejam validadas com base nas regras que as atividades definiram para si mesmas. Se houver erros de validação, o compilador retornará uma lista dos erros.  
- Uma classe parcial é gerada a partir da definição de marcação que é inserida no compilador.  

- O código é gerado para ajudar com a execução das atividades em tempo de execução. As assinaturas de evento são geradas, o que ajuda as atividades a saber quando as atividades que eles contêm têm concluído a execução.  
- As classes parciais geradas a partir do arquivo de marcação e as classes parciais do arquivo de código são inseridas no compilador .NET Framework C# ou Visual Basic. A saída desse processo é o assembly .NET, WorkflowSample.dll. Isso pode ser implantado para executar o fluxo de trabalho.

### <a name="compiler-options"></a>Opções do compilador

Esta seção mostra as opções para o compilador de linha de comando wfc.exe fluxo de trabalho.

```output
    Microsoft (R) Windows Workflow Compiler version 3.0.0.0
    Copyright (C) Microsoft Corporation 2005. All rights reserved.

                      Windows Workflow Compiler Options

    wfc.exe <Xoml file list> /target:assembly [<vb/cs file list>] [/language:...]
            [/out:...] [/reference:...] [/library:...] [/debug...] [/nocode...]
             [/checktypes...] [/resource:<resource info>]

                            - OUTPUT FILE -
    /out:<file>             Output file name
    /target:assembly        Build a Windows Workflow assembly (default).
                            Short form: /t:assembly
    /target:exe             Build a Windows Workflow application.
                            Short form: /t:exe
    /delaysign[+|-]         Delay-sign the assembly using only the public portion
                            of the strong name key.
    /keyfile:<file>         Specifies a strong name key file.
    /keycontainer:<string>  Specifies a strong name key container.

                            - INPUT FILES -
    <Xoml file list>        Xoml source file name(s).
    <vb/cs file list>       Code-beside file name(s).
    /reference:<file list>  Reference metadata from the specified assembly file(s).
                            Short form is '/r:'.
    /library:<path list>    Set of directories where to lookup for the references.
                            Short form is '/lib:'.
    /resource:<resinfo>     Embed the specified resource. Short form is '/res:'.
                            resinfo format is <file>[,<name>[,public|private]].

    Rules and freeform layout files must be embedded as assembly resources.
    The resource name is constructed by using the namespace and type name
    of the activity. For example, an activity named "MyActivity" in namespace
    "WFProject" would require resource names "WFProject.MyActivity.rules"
    and/or "WFProject.MyActivity.layout".

                            - CODE GENERATION -
    /debug[+|-]             Emit full debugging information. The default is '+'.
    /nocode[+|-]            Disallow code-beside model.
                            The default is '-'. Short form is '/nc:'.
    /checktypes[+|-]        Check for permitted types in wfc.exe.config file.
                            The default is '-'. Short form is '/ct:'.

                            - LANGUAGE -
    /language:[cs|vb]       The language to use for the generated class.
                            The default is 'CS' (C#). Short form is '/l:'.
    /rootnamespace:<string> Specifies the root Namespace for all type declarations.
                            Valid only for 'VB' (Visual Basic) language.
                            Short form is '/rns:'.

                            - MISCELLANEOUS -
    /help                   Display this usage message. Short form is '/?'.
    /nologo                 Suppress compiler copyright message. Short form is '/n'.

    /nowarn                 Ignore compiler warnings. Short form is '/w'.
```

## <a name="remarks"></a>Comentários

> [!NOTE]
> Este material discute tipos e namespaces obsoletos.

Uma lista de tipos autorizados geralmente é definida no arquivo *wfc.exe.config* . Durante a fase de validação da compilação do fluxo de trabalho, um documento de origem do fluxo de trabalho é rejeitado se ele ou o arquivo de regras complementares referencia diretamente qualquer tipo de .NET Framework não presente em uma lista de tipos autorizados. A lista de tipos autorizados é um documento XML em que cada entrada indica um `Assembly` indicador, um, `Namespace` um `TypeName` e um { `True`&#124;`False` } autorizado. `AuthorizedType` corresponde a uma entrada na lista. As designações de caractere curinga, que podem ser usadas para incluir ou excluir namespaces completos, são permitidas. Por exemplo, `Type="System.*"` inclui todos os tipos no <xref:System> , incluindo tipos contidos em namespaces filho.
  
O uso de uma lista de tipos autorizados é controlado pela <xref:System.Workflow.ComponentModel.Compiler.WorkflowCompiler> opção `'/checktypes'` .

```xml  
<configuration>  
  <System.Workflow.ComponentModel.WorkflowCompiler>
    <authorizedTypes>
      <targetFx version="v4.0">
        ...
        <authorizedType Assembly="System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" Namespace="System*" TypeName="*" Authorized="True"/>
        ...
      </targetFx>
    </authorizedTypes>
  </System.Workflow.ComponentModel.WorkflowCompiler>  
</configuration>  
```

> [!WARNING]
> Quando o `Type="System.*"` tipo está presente, é possível incluir outros tipos não pretendidos, como `Type="System.Configuration"` , para compilação. Você deve ter cuidado e examinar cada um deles. Para qualquer tipo que deva ser restringido, certifique-se de definir `Authorized` como `False` .

## <a name="see-also"></a>Veja também

- [Classe AuthorizedType](xref:System.Workflow.ComponentModel.Compiler.AuthorizedType)
