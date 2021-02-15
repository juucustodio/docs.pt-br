---
title: Eventos de tempo de execução do carregador e do fichário
description: Consulte eventos de tempo de execução do .NET que coletam informações de diagnóstico específicas para eventos ETW Loader e Binder, que coletam informações sobre o carregador e o associador de assembly.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- Assembly Loader events (CoreCLR)
- Assembly Binder events (CoreCLR)
- ETW, EventPipe, LTTng assembly loader and binder events (CoreCLR)
ms.openlocfilehash: 2284c580482f6b93a77f44649225ff7e5485666a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96585633"
---
# <a name="net-runtime-loader-and-binder-events"></a>Carregador de tempo de execução .NET e eventos do fichário

Esses eventos coletam informações relacionadas ao carregamento e ao descarregamento de assemblies e módulos. Para obter mais informações sobre como usar esses eventos para fins de diagnóstico, consulte [log e rastreamento de aplicativos .net](../../core/diagnostics/logging-tracing.md)

|Palavra-chave para acionar o evento|Evento|Level|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` (0x8)|`DomainModuleLoad_V1`|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`DomainModuleLoad_V1`|151|Gerado quando um módulo é carregado para um domínio do aplicativo.|

## <a name="moduleload_v2-event"></a>ModuleLoad_V2 evento

|Palavra-chave para acionar o evento|Evento|Level|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` (0x8)|`DomainModuleLoad_V1`|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ModuleLoad_V2`|152|Gerado quando um módulo é carregado durante o tempo de vida de um processo.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ModuleID`|`win:UInt64`|ID exclusiva para o módulo.|
|`AssemblyID`|`win:UInt64`|ID do assembly em que esse módulo reside.|
|`ModuleFlags`|`win:UInt32`|0x1: módulo de domínio neutro.<br /><br /> 0x2: o módulo tem uma imagem nativa.<br /><br /> 0x4: módulo dinâmico.<br /><br /> 0x8: módulo de manifesto.|
|`Reserved1`|`win:UInt32`|Campo reservado.|
|`ModuleILPath`|`win:UnicodeString`|Caminho da imagem de Common Intermediate Language (CIL) para o módulo ou nome de módulo dinâmico se for um assembly dinâmico (terminação nula).|
|`ModuleNativePath`|`win:UnicodeString`|Caminho da imagem nativa do módulo, se presente (terminado em nulo).|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|
|`ManagedPdbSignature`|`win:GUID`|Assinatura GUID do banco de dados de programa (PDB) gerenciado que corresponde a esse módulo.|
|`ManagedPdbAge`|`win:UInt32`|Número de idade escrito para o PDB gerenciado que corresponde a esse módulo.|
|`ManagedPdbBuildPath`|`win:UnicodeString`|Caminho para o local em que o PDB gerenciado que corresponde a esse módulo foi criado. Em alguns casos, isso pode ser apenas um nome de arquivo.|
|`NativePdbSignature`|`win:GUID`|Assinatura GUID do gerador de imagem nativa (NGen) PDB que corresponde a esse módulo, se aplicável.|
|`NativePdbAge`|`win:UInt32`|Número de idade escrito para o PDB do NGen que corresponde a esse módulo, se aplicável.|
|`NativePdbBuildPath`|`win:UnicodeString`|Caminho para o local em que o PDB do NGen que corresponde a esse módulo foi criado, se aplicável. Em alguns casos, isso pode ser apenas um nome de arquivo.|

## <a name="moduleunload_v2-event"></a>ModuleUnload_V2 evento

|Palavra-chave para acionar o evento|Evento|Level|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` (0x8)|`DomainModuleLoad_V1`|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ModuleUnload_V2`|153|Gerado quando um módulo é descarregado durante o tempo de vida de um processo.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ModuleID`|`win:UInt64`|ID exclusiva para o módulo.|
|`AssemblyID`|`win:UInt64`|ID do assembly em que esse módulo reside.|
|`ModuleFlags`|`win:UInt32`|0x1: módulo de domínio neutro.<br /><br /> 0x2: o módulo tem uma imagem nativa.<br /><br /> 0x4: módulo dinâmico.<br /><br /> 0x8: módulo de manifesto.|
|`Reserved1`|`win:UInt32`|Campo reservado.|
|`ModuleILPath`|`win:UnicodeString`|Caminho da imagem de Common Intermediate Language (CIL) para o módulo ou nome de módulo dinâmico se for um assembly dinâmico (terminação nula).|
|`ModuleNativePath`|`win:UnicodeString`|Caminho da imagem nativa do módulo, se presente (terminado em nulo).|
|`ClrInstanceID`|``win:UInt16``|ID exclusiva da instância do CLR ou do CoreCLR.|
|`ManagedPdbSignature`|`win:GUID`|Assinatura GUID do banco de dados de programa (PDB) gerenciado que corresponde a esse módulo.|
|`ManagedPdbAge`|`win:UInt32`|Número de idade escrito para o PDB gerenciado que corresponde a esse módulo.|
|`ManagedPdbBuildPath`|`win:UnicodeString`|Caminho para o local em que o PDB gerenciado que corresponde a esse módulo foi criado. Em alguns casos, isso pode ser apenas um nome de arquivo.|
|`NativePdbSignature`|`win:GUID`|Assinatura GUID do gerador de imagem nativa (NGen) PDB que corresponde a esse módulo, se aplicável.|
|`NativePdbAge`|`win:UInt32`|Número de idade escrito para o PDB do NGen que corresponde a esse módulo, se aplicável.|
|`NativePdbBuildPath`|`win:UnicodeString`|Caminho para o local em que o PDB do NGen que corresponde a esse módulo foi criado, se aplicável. Em alguns casos, isso pode ser apenas um nome de arquivo.|

## <a name="moduledcstart_v2-event"></a>ModuleDCStart_V2 evento

|Palavra-chave para acionar o evento|Evento|Level|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` (0x8)|`DomainModuleLoad_V1`|Informativo (4)

|Evento|ID do evento|Descrição
|-----------|--------------|-----------------|
|`ModuleDCStart_V2`|153|Enumera módulos durante um encerramento inicial.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ModuleID`|`win:UInt64`|ID exclusiva para o módulo.|
|`AssemblyID`|`win:UInt64`|ID do assembly em que esse módulo reside.|
|`ModuleFlags`|`win:UInt32`|0x1: módulo de domínio neutro.<br /><br /> 0x2: o módulo tem uma imagem nativa.<br /><br /> 0x4: módulo dinâmico.<br /><br /> 0x8: módulo de manifesto.|
|`Reserved1`|`win:UInt32`|Campo reservado.|
|`ModuleILPath`|`win:UnicodeString`|Caminho da imagem de Common Intermediate Language (CIL) para o módulo ou nome de módulo dinâmico se for um assembly dinâmico (terminação nula).|
|`ModuleNativePath`|`win:UnicodeString`|Caminho da imagem nativa do módulo, se presente (terminado em nulo).|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|
|`ManagedPdbSignature`|`win:GUID`|Assinatura GUID do banco de dados de programa (PDB) gerenciado que corresponde a esse módulo.|
|`ManagedPdbAge`|`win:UInt32`|Número de idade escrito para o PDB gerenciado que corresponde a esse módulo.|
|`ManagedPdbBuildPath`|`win:UnicodeString`|Caminho para o local em que o PDB gerenciado que corresponde a esse módulo foi criado. Em alguns casos, isso pode ser apenas um nome de arquivo.|
|`NativePdbSignature`|`win:GUID`|Assinatura GUID do gerador de imagem nativa (NGen) PDB que corresponde a esse módulo, se aplicável.|
|`NativePdbAge`|`win:UInt32`|Número de idade escrito para o PDB do NGen que corresponde a esse módulo, se aplicável.|
|`NativePdbBuildPath`|`win:UnicodeString`|Caminho para o local em que o PDB do NGen que corresponde a esse módulo foi criado, se aplicável. Em alguns casos, isso pode ser apenas um nome de arquivo.|

## <a name="moduledcend_v2-event"></a>ModuleDCEnd_V2 evento

|Palavra-chave para acionar o evento|Evento|Level|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` (0x8)|`DomainModuleLoad_V1`|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ModuleDCEnd_V2`|154|Enumera módulos durante um encerramento final.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`ModuleID`|`win:UInt64`|ID exclusiva para o módulo.|
|`AssemblyID`|`win:UInt64`|ID do assembly em que esse módulo reside.|
|`ModuleFlags`|`win:UInt32`|0x1: módulo de domínio neutro.<br /><br /> 0x2: o módulo tem uma imagem nativa.<br /><br /> 0x4: módulo dinâmico.<br /><br /> 0x8: módulo de manifesto.|
|`Reserved1`|`win:UInt32`|Campo reservado.|
|`ModuleILPath`|`win:UnicodeString`|Caminho da imagem de Common Intermediate Language (CIL) para o módulo ou nome de módulo dinâmico se for um assembly dinâmico (terminação nula).|
|`ModuleNativePath`|`win:UnicodeString`|Caminho da imagem nativa do módulo, se presente (terminado em nulo).|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva da instância do CLR ou do CoreCLR.|
|`ManagedPdbSignature`|`win:GUID`|Assinatura GUID do banco de dados de programa (PDB) gerenciado que corresponde a esse módulo.|
|`ManagedPdbAge`|`win:UInt32`|Número de idade escrito para o PDB gerenciado que corresponde a esse módulo.|
|`ManagedPdbBuildPath`|`win:UnicodeString`|Caminho para o local em que o PDB gerenciado que corresponde a esse módulo foi criado. Em alguns casos, isso pode ser apenas um nome de arquivo.|
|`NativePdbSignature`|`win:GUID`|Assinatura GUID do gerador de imagem nativa (NGen) PDB que corresponde a esse módulo, se aplicável.|
|`NativePdbAge`|`win:UInt32`|Número de idade escrito para o PDB do NGen que corresponde a esse módulo, se aplicável.|
|`NativePdbBuildPath`|`win:UnicodeString`|Caminho para o local em que o PDB do NGen que corresponde a esse módulo foi criado, se aplicável. Em alguns casos, isso pode ser apenas um nome de arquivo.|

## <a name="assemblyload_v1-event"></a>AssemblyLoad_V1 evento

|Palavra-chave para acionar o evento|Evento|Level|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` (0x8)|`DomainModuleLoad_V1`|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`AssemblyLoad_V1`|154|Gerado quando um assembly é carregado.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`AssemblyID`|`win:UInt64`|ID exclusiva para o assembly.|
|`AppDomainID`|`win:UInt64`|ID do domínio desse assembly.|
|`BindingID`|`win:UInt64`|ID que identifica exclusivamente a associação do assembly.|
|`AssemblyFlags`|`win:UInt32`|0x1: assembly de domínio neutro.<br /><br /> 0x2: assembly dinâmico.<br /><br /> 0x4: o assembly tem uma imagem nativa.<br /><br /> 0x8: assembly de coleção.|
|`AssemblyName`|`win:UnicodeString`|O nome totalmente qualificado do assembly.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.

## <a name="assemblyunload_v1-event"></a>AssemblyUnload_V1 evento

|Palavra-chave para acionar o evento|Evento|Level|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` (0x8)|`DomainModuleLoad_V1`|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`FireAssemblyUnload_V1`|155|Gerado quando um assembly é carregado.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`AssemblyID`|`win:UInt64`|ID exclusiva para o assembly.|
|`AppDomainID`|`win:UInt64`|ID do domínio desse assembly.|
|`BindingID`|`win:UInt64`|ID que identifica exclusivamente a associação do assembly.|
|`AssemblyFlags`|`win:UInt32`|0x1: assembly de domínio neutro.<br /><br /> 0x2: assembly dinâmico.<br /><br /> 0x4: o assembly tem uma imagem nativa.<br /><br /> 0x8: assembly de coleção.|
|`AssemblyName`|`win:UnicodeString`|O nome totalmente qualificado do assembly.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="assemblydcstart_v1-event"></a>AssemblyDCStart_V1 evento

|Palavra-chave para acionar o evento|Evento|Level|
|-----------------------------------|-----------|-----------|
|`LoaderKeyword` (0x8)|`DomainModuleLoad_V1`|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`AssemblyDCStart_V1`|155|Enumera assemblies durante um encerramento inicial.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`AssemblyID`|`win:UInt64`|ID exclusiva para o assembly.|
|`AppDomainID`|`win:UInt64`|ID do domínio desse assembly.|
|`BindingID`|`win:UInt64`|ID que identifica exclusivamente a associação do assembly.|
|`AssemblyFlags`|`win:UInt32`|0x1: assembly de domínio neutro.<br /><br /> 0x2: assembly dinâmico.<br /><br /> 0x4: o assembly tem uma imagem nativa.<br /><br /> 0x8: assembly de coleção.|
|`AssemblyName`|`win:UnicodeString`|O nome totalmente qualificado do assembly.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="assemblyloadstart-event"></a>Evento AssemblyLoadStart

|Palavra-chave para acionar o evento|Evento|Level|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|`AssemblyLoadStart`|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`AssemblyLoadStart`|290|Um carregamento de assembly foi solicitado.

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`AssemblyName`|`win:UnicodeString`|Nome do nome do assembly.|
|`AssemblyPath`|`win:UnicodeString`|Caminho do nome do assembly.|
|`RequestingAssembly`|`win:UnicodeString`|Nome do assembly de solicitação ("pai").|
|`AssemblyLoadContext`|`win:UnicodeString`|Contexto de carregamento do assembly.|
|`RequestingAssemblyLoadContext`|`win:UnicodeString`|O contexto de carregamento do assembly de solicitação ("pai").|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="assemblyloadstop-event"></a>Evento AssemblyLoadStop

|Palavra-chave para acionar o evento|Evento|Level|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|`AssemblyLoadStart`|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`AssemblyLoadStart`|291|Um carregamento de assembly foi solicitado.

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`AssemblyName`|`win:UnicodeString`|Nome do nome do assembly.|
|`AssemblyPath`|`win:UnicodeString`|Caminho do nome do assembly.|
|`RequestingAssembly`|`win:UnicodeString`|Nome do assembly de solicitação ("pai").|
|`AssemblyLoadContext`|`win:UnicodeString`|Contexto de carregamento do assembly.|
|`RequestingAssemblyLoadContext`|`win:UnicodeString`|O contexto de carregamento do assembly de solicitação ("pai").|
|`Success`|`win:Boolean`|Se o assembly foi carregado com êxito.|
|`ResultAssemblyName`|`win:UnicodeString`|O nome do assembly que foi carregado.|
|`ResultAssemblyPath`|`win:UnicodeString`|O caminho do assembly do qual foi carregado.|
|`Cached`|`win:UnicodeString`|Se a carga foi armazenada em cache.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="resolutionattempted-event"></a>Evento ResolutionAttempted

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`ResolutionAttempted`|292|Um carregamento de assembly foi solicitado.

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`AssemblyName`|`win:UnicodeString`|Nome do nome do assembly.|
|`Stage`|`win:UInt16`|O estágio de resolução.<br/><br/>0: localizar no carregamento.<br/><br/>1: contexto de carregamento do assembly</br><br/>2: assemblies de aplicativo.<br/><br/>3: fallback de contexto de carregamento de assembly padrão. <br/><br/>4: resolver assembly satélite. <br/><br/>5: resolução de contexto de carregamento de assembly.<br/><br/>6: resolução de assembly AppDomain.
|`AssemblyLoadContext`|`win:UnicodeString`|Contexto de carregamento do assembly.|
|`Result`|`win:UInt16`|O resultado da tentativa de resolução.<br/><br/>0: êxito<br/><br/>1: assembly não encontrado<br/><br/>2: versão incompatível<br/><br/>3: nome do assembly incompatível<br/><br/>4: falha<br/><br/>5: exceção|
|`ResultAssemblyName`|`win:UnicodeString`|O nome do assembly que foi resolvido.|
|`ResultAssemblyPath`|`win:UnicodeString`|O caminho do assembly que foi resolvido a partir de.|
|`ErrorMessage`|`win:UnicodeString`|Mensagem de erro se houver uma exceção.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="assemblyloadcontextresolvinghandlerinvoked-event"></a>Evento AssemblyLoadContextResolvingHandlerInvoked

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`AssemblyLoadContextResolvingHandlerInvoked`|293|Um manipulador [AssemblyLoadContext. resolvendo](xref:System.Runtime.Loader.AssemblyLoadContext.Resolving) foi invocado.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`AssemblyName`|`win:UnicodeString`|Nome do nome do assembly.|
|`HandlerName`|`win:UnicodeString`|Nome do manipulador invocado.|
|`AssemblyLoadContext`|`win:UnicodeString`|Contexto de carregamento do assembly.|
|`ResultAssemblyName`|`win:UnicodeString`|O nome do assembly que foi resolvido.|
|`ResultAssemblyPath`|`win:UnicodeString`|O caminho do assembly que foi resolvido a partir de.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="appdomainassemblyresolvehandlerinvoked-event"></a>Evento AppDomainAssemblyResolveHandlerInvoked

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`AppDomainAssemblyResolveHandlerInvoked`|294|Um <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> manipulador foi invocado.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`AssemblyName`|`win:UnicodeString`|Nome do nome do assembly.|
|`HandlerName`|`win:UnicodeString`|Nome do manipulador invocado.|
|`ResultAssemblyName`|`win:UnicodeString`|O nome do assembly que foi resolvido.|
|`ResultAssemblyPath`|`win:UnicodeString`|O caminho do assembly que foi resolvido a partir de.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="assemblyloadfromresolvehandlerinvoked-event"></a>Evento AssemblyLoadFromResolveHandlerInvoked

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`AssemblyLoadFromResolveHandlerInvoked`|295|Um <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> manipulador foi invocado.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`AssemblyName`|`win:UnicodeString`|Nome do nome do assembly.|
|`IsTrackedLoad`|`win:Boolean`|Se o carregamento do assembly é acompanhado.|
|`RequestingAssemblyPath`|`win:UnicodeString`|O caminho do assembly solicitante.|
|`ComputedRequestedAssemblyPath`|`win:UnicodeString`|O caminho do assembly que foi solicitado.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|

## <a name="knownpathprobed-event"></a>Evento KnownPathProbed

|Palavra-chave para acionar o evento|Level|
|-----------------------------------|-----------|-----------|
|`Binder` 0x4|Informativo (4)|

|Evento|ID do evento|Descrição|
|-----------|--------------|-----------------|
|`KnownPathProbed`|296|Um caminho conhecido foi investigado para um assembly.|

|Nome do campo|Tipo de dados|Descrição|
|----------------|---------------|-----------------|
|`FilePath`|`win:UnicodeString`|Caminho investigado.|
|`Source`|`win:UInt16`|Origem do caminho investigado.<br/><br/>0x0: assemblies de aplicativo.<br/><br/>0x1: caminho de imagem nativa do aplicativo.<br/><br/>0x2: caminho do aplicativo.</br><br/>0x3: raízes de recurso de plataforma.<br/><br/>0x4: subdiretório satélite.</br>|
|`Result`|`win:UInt32`|HRESULT para a investigação.|
|`ClrInstanceID`|`win:UInt16`|ID exclusiva para a instância do CoreCLR.|
