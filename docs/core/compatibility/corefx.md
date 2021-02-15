---
title: Alterações interruptivas na biblioteca do .NET
description: Lista as alterações interruptivas nas bibliotecas principais do .NET para as versões 1.0 a 3.0 do .NET Core.
ms.date: 07/27/2020
ms.openlocfilehash: 092ff36a5e07c9e226fe2a67d5e7cfd391e9d16b
ms.sourcegitcommit: fcbe432482464b1639decad78cc4dc8387c6269e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/12/2020
ms.locfileid: "97366873"
---
# <a name="core-net-libraries-breaking-changes-in-net-core-10-30"></a>Alterações interruptivas nas bibliotecas principais do .NET Core 1.0 a 3.0

As principais bibliotecas do .NET fornecem os primitivos e outros tipos gerais usados pelo .NET Core.

As seguintes alterações interruptivas estão documentadas nesta página:

| Alteração interruptiva | Versão introduzida |
| - | :-: |
| [Passar GroupCollection para métodos de extensão assumindo IEnumerable \<T> requer ambiguidade](#passing-groupcollection-to-extension-methods-taking-ienumerablet-requires-disambiguation) | 3.0 |
| [As APIs que relatam versão agora relatam produto e não versão de arquivo](#apis-that-report-version-now-report-product-and-not-file-version) | 3.0 |
| [Instâncias EncoderFallbackBuffer personalizadas não podem retornar recursivamente](#custom-encoderfallbackbuffer-instances-cannot-fall-back-recursively) | 3.0 |
| [Alterações de comportamento de análise e formatação de ponto flutuante](#floating-point-formatting-and-parsing-behavior-changed) | 3.0 |
| [Operações de análise de ponto flutuante não falham mais ou geram uma estourexception](#floating-point-parsing-operations-no-longer-fail-or-throw-an-overflowexception) | 3.0 |
| [InvalidAsynchronousStateException movido para outro assembly](#invalidasynchronousstateexception-moved-to-another-assembly) | 3.0 |
| [A substituição de sequências de bytes UTF-8 mal formados segue as diretrizes de Unicode](#replacing-ill-formed-utf-8-byte-sequences-follows-unicode-guidelines) | 3.0 |
| [TypeDescriptionProviderAttribute movido para outro assembly](#typedescriptionproviderattribute-moved-to-another-assembly) | 3.0 |
| [O ZipArchiveEntry não lida mais com os arquivos mortos com tamanhos de entrada inconsistentes](#ziparchiveentry-no-longer-handles-archives-with-inconsistent-entry-sizes) | 3.0 |
| [FieldInfo. SetValue gera uma exceção para campos estáticos somente de inicialização](#fieldinfosetvalue-throws-exception-for-static-init-only-fields) | 3.0 |
| [Campos privados adicionados aos tipos de struct internos](#private-fields-added-to-built-in-struct-types) | 2.1 |
| [Alteração no valor padrão de UseShellExecute](#change-in-default-value-of-useshellexecute) | 2.1 |
| [Versões do OpenSSL no macOS](#openssl-versions-on-macos) | 2.1 |
| [UnauthorizedAccessException gerado por FileSystemInfo. Attributes](#unauthorizedaccessexception-thrown-by-filesysteminfoattributes) | 1.0 |
| [Tratamento de exceções de estado de processo corrompido não é suportado](#handling-corrupted-state-exceptions-is-not-supported) | 1.0 |
| [As propriedades UriBuilder não precedem mais os caracteres à esquerda](#uribuilder-properties-no-longer-prepend-leading-characters) | 1.0 |
| [Process. StartInfo gera InvalidOperationException para processos que você não iniciou](#processstartinfo-throws-invalidoperationexception-for-processes-you-didnt-start) | 1.0 |

## <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE [disambiguate-generic-type-for-groupcollection](../../../includes/core-changes/corefx/3.0/disambiguate-generic-type-for-groupcollection.md)]

***

[!INCLUDE[APIs that report version now report product and not file version](~/includes/core-changes/corefx/3.0/version-information-changes.md)]

**_

[!INCLUDE[Custom EncoderFallbackBuffer instances cannot fall back recursively](~/includes/core-changes/corefx/3.0/custom-encoderfallbackbuffer-cannot-be-recursive.md)]

_*_

[!INCLUDE[Floating point formatting and parsing behavior changes](~/includes/core-changes/corefx/3.0/floating-point-changes.md)]

_*_

[!INCLUDE[Floating-point parsing operations no longer fail or throw an OverflowException](~/includes/core-changes/corefx/3.0/floating-point-parsing-does-not-overflow.md)]

_*_

[!INCLUDE[InvalidAsynchronousStateException moved to another assembly](~/includes/core-changes/corefx/3.0/move-invalidasynchronousstateexception.md)]

_*_

[!INCLUDE[NET Core 3.0 follows Unicode best practices when replacing ill-formed UTF-8 byte sequences](~/includes/core-changes/corefx/3.0/net-core-3-0-follows-unicode-utf8-best-practices.md)]

_*_

[!INCLUDE[TypeDescriptionProviderAttribute moved to another assembly](~/includes/core-changes/corefx/3.0/move-typedescriptionproviderattribute.md)]

_*_

[!INCLUDE[ZipArchiveEntry no longer handles archives with inconsistent entry sizes](~/includes/core-changes/corefx/3.0/ziparchiveentry-and-inconsistent-entry-sizes.md)]

_*_

[!INCLUDE [FieldInfo.SetValue throws exception for static, init-only fields](~/includes/core-changes/corefx/3.0/fieldinfo-setvalue-exception.md)]

_*_

## <a name="net-core-21"></a>.NET Core 2.1

[!INCLUDE[Private fields added to built-in struct types](~/includes/core-changes/corefx/2.1/instantiate-struct.md)]

_*_

[!INCLUDE[Change in default value of UseShellExecute](~/includes/core-changes/corefx/2.1/process-start-changes.md)]

_*_

[!INCLUDE [OpenSSL versions on macOS](../../../includes/core-changes/corefx/openssl-dependencies-macos.md)]

_*_

## <a name="net-core-10"></a>.NET Core 1.0

[!INCLUDE [UnauthorizedAccessException thrown by FileSystemInfo.Attributes](~/includes/core-changes/corefx/1.0/filesysteminfo-attributes-exceptions.md)]

_*_

[!INCLUDE [corrupted-state-exceptions](~/includes/core-changes/corefx/1.0/corrupted-state-exceptions.md)]

_*_

[!INCLUDE [uribuilder-behavior-changes](../../../includes/core-changes/corefx/1.0/uribuilder-behavior-changes.md)]

_*_

[!INCLUDE [startinfo-throws-exception](../../../includes/core-changes/corefx/1.0/startinfo-throws-exception.md)]

_**
