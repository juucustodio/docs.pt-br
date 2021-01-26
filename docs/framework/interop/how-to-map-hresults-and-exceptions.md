---
title: 'Como: Mapear HRESULTs e exceções'
description: Examine como mapear valores HRESULT retornados de métodos COM para exceções geradas por métodos .NET. O tempo de execução manipula a transição entre COM e .NET.
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- interoperation with unmanaged code, HRESULTs
- exceptions, HRESULTs
- interoperation with unmanaged code, exceptions
- HRESULTs
- COM interop, HRESULTs
- COM interop, exceptions
ms.assetid: 610b364b-2761-429d-9c4a-afbc3e66f1b9
ms.openlocfilehash: ff20dc50e1a5f1ce87a4a40691110d247b52e479
ms.sourcegitcommit: 4d5e25a46aa7cd0d29b4b9227b92987354d444c4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98794687"
---
# <a name="how-to-map-hresults-and-exceptions"></a>Como: Mapear HRESULTs e exceções

Métodos COM relatam erros retornando HRESULTs; métodos .NET os relatam gerando exceções. O runtime manipula a transição entre os dois. Cada classe de exceção do .NET Framework mapeia para um HRESULT.

 Classes de exceção definidas pelo usuário podem especificar qualquer HRESULT apropriado. Essas classes de exceção podem alterar dinamicamente o HRESULT a ser retornado quando a exceção é gerada definindo o `HResult` campo no objeto de exceção. Informações adicionais sobre a exceção são fornecidas ao cliente por meio da `IErrorInfo` interface, que é implementada no objeto .net no processo não gerenciado.

 Se você criar uma classe que estenda `System.Exception` , deverá definir o campo HRESULT durante a construção. Caso contrário, a classe base atribui o valor de HRESULT. Você pode mapear as novas classes de exceção para um HRESULT existente, fornecendo o valor no construtor da exceção.

 Observe que o runtime, às vezes, ignorará um `HRESULT` em casos nos quais um `IErrorInfo` estiver presente no thread.  Esse comportamento poderá ocorrer nos casos em que o `HRESULT` e o `IErrorInfo` não representarem o mesmo erro.

### <a name="to-create-a-new-exception-class-and-map-it-to-an-hresult"></a>Para criar uma nova classe de exceção e mapeá-la para um HRESULT

1. Use o código a seguir para criar uma nova classe de exceção chamada `NoAccessException` e mapeá-la para o HRESULT `E_ACCESSDENIED`.

    ```cpp
    Class NoAccessException : public ApplicationException
    {
        NoAccessException () {
        HResult = E_ACCESSDENIED;
    }
    }
    CMyClass::MethodThatThrows
    {
    throw new NoAccessException();
    }
    ```

 Você pode encontrar um programa (em qualquer linguagem de programação) que usa o código gerenciado e não gerenciado simultaneamente. Por exemplo, o marshaler personalizado no exemplo de código a seguir usa o `Marshal.ThrowExceptionForHR(int HResult)` método para lançar uma exceção com um valor HRESULT específico. O método pesquisa o HRESULT e gera o tipo de exceção apropriado. Por exemplo, o HRESULT no fragmento de código a seguir gera `ArgumentException` .

```cpp
CMyClass::MethodThatThrows
{
    Marshal.ThrowExceptionForHR(COR_E_ARGUMENT);
}
```

 A tabela a seguir fornece os mapeamentos comuns do HRESULT para sua classe de exceção comparável no .NET. Valores HRESULT sem mapeamentos explícitos são mapeados para `COMException` . O mapeamento completo atualizado pode ser encontrado no [repositório dotnet/tempo de execução](https://github.com/dotnet/runtime/blob/master/src/coreclr/vm/rexcep.h).

|HRESULT|Exceção do .NET|
|-------------|--------------------|
|`COR_E_APPLICATION`|`ApplicationException`|
|`COR_E_ARGUMENT` ou `E_INVALIDARG`|`ArgumentException`|
|`COR_E_ARGUMENTOUTOFRANGE`|`ArgumentOutOfRangeException`|
|`COR_E_ARITHMETIC or ERROR_ARITHMETIC_OVERFLOW`|`ArithmeticException`|
|`COR_E_ARRAYTYPEMISMATCH`|`ArrayTypeMismatchException`|
|`COR_E_BADIMAGEFORMAT or ERROR_BAD_FORMAT`|`BadImageFormatException`|
|`COR_E_DIRECTORYNOTFOUND or ERROR_PATH_NOT_FOUND`|`DirectoryNotFoundException`|
|`COR_E_DIVIDEBYZERO`|`DivideByZeroException`|
|`COR_E_DUPLICATEWAITOBJECT`|`DuplicateWaitObjectException`|
|`COR_E_ENDOFSTREAM`|`EndOfStreamException`|
|`COR_E_ENTRYPOINTNOTFOUND`|`EntryPointNotFoundException`|
|`COR_E_EXCEPTION`|`Exception`|
|`COR_E_EXECUTIONENGINE`|`ExecutionEngineException`|
|`COR_E_FIELDACCESS`|`FieldAccessException`|
|`COR_E_FILENOTFOUND or ERROR_FILE_NOT_FOUND`|`FileNotFoundException`|
|`COR_E_FORMAT`|`FormatException`|
|`COR_E_INDEXOUTOFRANGE`|`IndexOutOfRangeException`|
|`COR_E_INVALIDCAST or E_NOINTERFACE`|`InvalidCastException`|
|`COR_E_INVALIDFILTERCRITERIA`|`InvalidFilterCriteriaException`|
|`COR_E_INVALIDOPERATION`|`InvalidOperationException`|
|`COR_E_IO`|`IOException`|
|`COR_E_MEMBERACCESS`|`AccessException`|
|`COR_E_METHODACCESS`|`MethodAccessException`|
|`COR_E_MISSINGFIELD`|`MissingFieldException`|
|`COR_E_MISSINGMANIFESTRESOURCE`|`MissingManifestResourceException`|
|`COR_E_MISSINGMEMBER`|`MissingMemberException`|
|`COR_E_MISSINGMETHOD`|`MissingMethodException`|
|`COR_E_NOTFINITENUMBER`|`NotFiniteNumberException`|
|`E_NOTIMPL`|`NotImplementedException`|
|`COR_E_NOTSUPPORTED`|`NotSupportedException`|
|`COR_E_NULLREFERENCE orE_POINTER`|`NullReferenceException`|
|`COR_E_OUTOFMEMORY or`<br /><br /> `E_OUTOFMEMORY`|`OutOfMemoryException`|
|`COR_E_OVERFLOW`|`OverflowException`|
|`COR_E_PATHTOOLONG or ERROR_FILENAME_EXCED_RANGE`|`PathTooLongException`|
|`COR_E_RANK`|`RankException`|
|`COR_E_REFLECTIONTYPELOAD`|`ReflectionTypeLoadException`|
|`COR_E_SECURITY`|`SecurityException`|
|`COR_E_SERIALIZATION`|`SerializationException`|
|`COR_E_STACKOVERFLOW orERROR_STACK_OVERFLOW`|`StackOverflowException`|
|`COR_E_SYNCHRONIZATIONLOCK`|`SynchronizationLockException`|
|`COR_E_SYSTEM`|`SystemException`|
|`COR_E_TARGET`|`TargetException`|
|`COR_E_TARGETINVOCATION`|`TargetInvocationException`|
|`COR_E_TARGETPARAMCOUNT`|`TargetParameterCountException`|
|`COR_E_THREADINTERRUPTED`|`ThreadInterruptedException`|
|`COR_E_THREADSTATE`|`ThreadStateException`|
|`COR_E_TYPELOAD`|`TypeLoadException`|
|`COR_E_TYPEINITIALIZATION`|`TypeInitializationException`|
|`COR_E_VERIFICATION`|`VerificationException`|

 Para recuperar informações sobre erros estendidos, o cliente gerenciado deve examinar os campos do objeto de exceção gerado. Para o objeto de exceção fornecer informações úteis sobre um erro, o objeto COM deve implementar a `IErrorInfo` interface. O tempo de execução usa as informações fornecidas pelo `IErrorInfo` para inicializar o objeto de exceção.

 Se o objeto COM não oferecer suporte `IErrorInfo` , o tempo de execução Inicializa um objeto de exceção com valores padrão. A tabela a seguir lista cada campo associado a um objeto de exceção e identifica a fonte de informações padrão quando o objeto COM dá suporte a `IErrorInfo` .

 Observe que o runtime, às vezes, ignorará um `HRESULT` em casos nos quais um `IErrorInfo` estiver presente no thread.  Esse comportamento poderá ocorrer nos casos em que o `HRESULT` e o `IErrorInfo` não representarem o mesmo erro.

|Campo de exceção|Origem das informações do COM|
|---------------------|------------------------------------|
|`ErrorCode`|HRESULT retornado da chamada.|
|`HelpLink`|Se `IErrorInfo->HelpContext` for diferente de zero, a cadeia de caracteres será formada por concatenação `IErrorInfo->GetHelpFile` e "#" e `IErrorInfo->GetHelpContext` . Caso contrário, a cadeia de caracteres será retornada de `IErrorInfo->GetHelpFile` .|
|`InnerException`|Sempre uma referência nula ( `Nothing` em Visual Basic).|
|`Message`|Cadeia de caracteres retornada de `IErrorInfo->GetDescription` .|
|`Source`|Cadeia de caracteres retornada de `IErrorInfo->GetSource` .|
|`StackTrace`|O rastreamento de pilha.|
|`TargetSite`|O nome do método que retornou o HRESULT com falha.|

 Os campos de exceção, como `Message` , `Source` e `StackTrace` não estão disponíveis para o `StackOverflowException` .

## <a name="see-also"></a>Confira também

- [Interoperabilidade COM avançada](/previous-versions/dotnet/netframework-4.0/bd9cdfyx(v=vs.100))
- [Exceções](../../standard/exceptions/index.md)
