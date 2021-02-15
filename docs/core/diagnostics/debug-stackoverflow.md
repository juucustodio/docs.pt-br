---
title: Depuração de erros do StackOverflow
description: Saiba como diagnosticar exceções StackOverflow
ms.topic: tutorial
ms.date: 12/22/2020
ms.openlocfilehash: 92edf854ddcc2e778949d74eff1370cf27db25b4
ms.sourcegitcommit: c0b803bffaf101e12f071faf94ca21b46d04ff30
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/24/2020
ms.locfileid: "97764923"
---
# <a name="debugging-stackoverflow-errors"></a>Depuração de erros do StackOverflow

Um <xref:System.StackOverflowException> é gerado quando a pilha de execução estoura porque contém muitas chamadas de método aninhadas.  

Por exemplo, suponha que você tenha um aplicativo da seguinte maneira:

````
using System;

namespace temp
{
    class Program
    {
        static void Main(string[] args)
        {
            Main(args); // oops this recursion won't stop
        }
    }
}
````

O método Main se chamará continuamente até que não haja mais espaço de pilha.  Quando não houver mais espaço de pilha, a execução não poderá continuar e, portanto, gerará um <xref:System.StackOverflowException> .  

````
> dotnet run
Stack overflow.
````

> [!NOTE]
> No .NET 5 e posterior, a pilha de chamadas é saída para o console.

> [!NOTE]
> Este artigo descreve como depurar um estouro de pilha com o lldb. Se você estiver executando o no Windows, sugerimos a depuração do aplicativo com o [Visual Studio](/visualstudio/debugger/what-is-debugging) ou [Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging).  

## <a name="example"></a>Exemplo

1. Execute o aplicativo com ele configurado para coletar um despejo na falha

    ````
    > export COMPlus_DbgEnableMiniDump=1
    > dotnet run
    Stack overflow.
    Writing minidump with heap to file /tmp/coredump.6412
    Written 58191872 bytes (14207 pages) to core file
    ````

2. Instalar a extensão SOS usando [dotnet-SOS](dotnet-sos.md)

    ````
    dotnet-sos install
    ````

3. Depurar o despejo no lldb para ver a pilha com falha

    ````
    lldb --core /temp/coredump.6412
    (lldb) bt
    ...
        frame #261930: 0x00007f59b40900cc
        frame #261931: 0x00007f59b40900cc
        frame #261932: 0x00007f59b40900cc
        frame #261933: 0x00007f59b40900cc
        frame #261934: 0x00007f59b40900cc
        frame #261935: 0x00007f5a2d4a080f libcoreclr.so`CallDescrWorkerInternal at unixasmmacrosamd64.inc:867
        frame #261936: 0x00007f5a2d3cc4c3 libcoreclr.so`MethodDescCallSite::CallTargetWorker(unsigned long const*, unsigned long*, int) at callhelpers.cpp:70
        frame #261937: 0x00007f5a2d3cc468 libcoreclr.so`MethodDescCallSite::CallTargetWorker(this=<unavailable>, pArguments=0x00007ffe8222e7b0, pReturnValue=0x0000000000000000, cbReturnValue=0) at callhelpers.cpp:604
        frame #261938: 0x00007f5a2d4b6182 libcoreclr.so`RunMain(MethodDesc*, short, int*, PtrArray**) [inlined] MethodDescCallSite::Call(this=<unavailable>, pArguments=<unavailable>) at callhelpers.h:468
    ...
    ````

4. O quadro superior `0x00007f59b40900cc` é repetido várias vezes. Use o comando [SOS](sos-debugging-extension.md) `ip2md` para descobrir qual método está localizado no `0x00007f59b40900cc` Endereço

    ````
    (lldb) ip2md 0x00007f59b40900cc
    MethodDesc:   00007f59b413ffa8
    Method Name:          temp.Program.Main(System.String[])
    Class:                00007f59b4181d40
    MethodTable:          00007f59b4190020
    mdToken:              0000000006000001
    Module:               00007f59b413dbf8
    IsJitted:             yes
    Current CodeAddr:     00007f59b40900a0
    Version History:
      ILCodeVersion:      0000000000000000
      ReJIT ID:           0
      IL Addr:            0000000000000000
         CodeAddr:           00007f59b40900a0  (MinOptJitted)
         NativeCodeVersion:  0000000000000000
    Source file:  /temp/Program.cs @ 9
    ````

5. Veja o método indicado Temp. Program. principal (System. String []) e Source "/temp/Program.cs @ 9" para ver se você pode descobrir o que você fez errado. Se ainda não estava claro, você poderia adicionar o registro em log nessa área do código.

## <a name="see-also"></a>Consulte Também

* [Uma introdução aos despejos no .NET](dumps.md)
* [Depurar despejos do Linux](debug-linux-dumps.md)
* [Extensão de depuração SOS para .NET](sos-debugging-extension.md)
