---
title: APIs sem suporte no .NET Core
titleSuffix: ''
description: Saiba quais APIs do .NET Framework que sempre lançam uma exceção no .NET Core.
ms.date: 12/23/2019
ms.openlocfilehash: 94f334d7e4b7daf407f489ba274172ced9eefa81
ms.sourcegitcommit: b1f4756120deaecb8b554477bb040620f69a4209
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/03/2020
ms.locfileid: "89414429"
---
# <a name="apis-that-always-throw-exceptions-on-net-core"></a>APIs que sempre lançam exceções no .NET Core

As APIs a seguir sempre lançarão um <xref:System.PlatformNotSupportedException> no .NET Core em todos ou em um subconjunto de plataformas.

Este artigo organiza os membros de API afetados por namespace.

> [!NOTE]
>
> - Este artigo é um trabalho em andamento. Não é uma lista completa de APIs que lançam exceções no .NET Core.
> - Este artigo não inclui as implementações de interface explícitas para serialização binária que lançam no .NET Core. Para obter mais informações, consulte [serialização binária no .NET Core](../../standard/serialization/binary-serialization.md#net-core).

## <a name="system"></a>Sistema

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.AppDomain.CreateDomain%2A?displayProperty=nameWithType> | Todos |
| <xref:System.AppDomain.ExecuteAssembly(System.String,System.String[],System.Byte[],System.Configuration.Assemblies.AssemblyHashAlgorithm)?displayProperty=nameWithType> | Todos |
| <xref:System.Console.CapsLock?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Console.NumberLock?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Delegate.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |
| <xref:System.Exception.SerializeObjectState?displayProperty=nameWithType> | Todos |
| <xref:System.MarshalByRefObject.GetLifetimeService?displayProperty=nameWithType> | Todos |
| <xref:System.MarshalByRefObject.InitializeLifetimeService?displayProperty=nameWithType> | Todos |
| <xref:System.OperatingSystem.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |
| <xref:System.Type.ReflectionOnlyGetType(System.String,System.Boolean,System.Boolean)?displayProperty=nameWithType> | Todos |

## <a name="systemcodedomcompiler"></a>System.CodeDom.Compiler

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromDom%2A?displayProperty=nameWithType> | Todos |
| <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A?displayProperty=nameWithType> | Todos |
| <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromSource%2A?displayProperty=nameWithType> | Todos |

## <a name="systemcollectionsspecialized"></a>System.Collections.Specialized

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Collections.Specialized.NameObjectCollectionBase.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Todos |
| <xref:System.Collections.Specialized.NameObjectCollectionBase.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |
| <xref:System.Collections.Specialized.NameObjectCollectionBase.OnDeserialization(System.Object)?displayProperty=nameWithType> | Todos |

## <a name="systemconfiguration"></a>System.Configuration

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Configuration.RsaProtectedConfigurationProvider?displayProperty=nameWithType> (todos os membros) | Tudo |

## <a name="systemconsole"></a>System.Console

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Console.Beep?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Console.BufferHeight?displayProperty=nameWithType> (definir somente) | Linux e macOS |
| <xref:System.Console.BufferWidth?displayProperty=nameWithType> (definir somente) | Linux e macOS |
| <xref:System.Console.CursorSize?displayProperty=nameWithType> (definir somente) | Linux e macOS |
| <xref:System.Console.CursorVisible?displayProperty=nameWithType> (somente Get) | Linux e macOS |
| <xref:System.Console.MoveBufferArea%2A?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Console.SetWindowPosition%2A?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Console.SetWindowSize%2A?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Console.Title?displayProperty=nameWithType> (somente Get) | Linux e macOS |
| <xref:System.Console.WindowHeight?displayProperty=nameWithType> (definir somente) | Linux e macOS |
| <xref:System.Console.WindowLeft?displayProperty=nameWithType> (definir somente) | Linux e macOS |
| <xref:System.Console.WindowTop?displayProperty=nameWithType> (definir somente) | Linux e macOS |
| <xref:System.Console.WindowWidth?displayProperty=nameWithType> (definir somente) | Linux e macOS |

## <a name="systemdatacommon"></a>System.Data.Common

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Data.Common.DbDataReader.GetSchemaTable%2A?displayProperty=nameWithType> (gera <xref:System.NotSupportedException> ) | Tudo |

## <a name="systemdiagnosticsprocess"></a>System.Diagnostics.Process

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Diagnostics.Process.MaxWorkingSet?displayProperty=nameWithType> (definir somente) | Linux |
| <xref:System.Diagnostics.Process.MinWorkingSet?displayProperty=nameWithType> (definir somente) | Linux |
| <xref:System.Diagnostics.Process.ProcessorAffinity?displayProperty=nameWithType> | macOS |
| <xref:System.Diagnostics.Process.MainWindowHandle?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Diagnostics.ProcessStartInfo.UserName?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Diagnostics.ProcessStartInfo.PasswordInClearText?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Diagnostics.ProcessStartInfo.Domain?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Diagnostics.ProcessStartInfo.LoadUserProfile?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Diagnostics.ProcessThread.BasePriority?displayProperty=nameWithType> (definir somente) | Linux e macOS |
| <xref:System.Diagnostics.ProcessThread.BasePriority?displayProperty=nameWithType> (somente Get) | macOS |
| <xref:System.Diagnostics.ProcessThread.ProcessorAffinity?displayProperty=nameWithType> (definir somente) | Linux e macOS |

## <a name="systemio"></a>System.IO

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.IO.FileSystemInfo.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Todos |
| <xref:System.IO.FileSystemInfo.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |

## <a name="systemiopipes"></a>System.IO.Pipes

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.IO.Pipes.NamedPipeClientStream.NumberOfServerInstances?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.IO.Pipes.NamedPipeServerStream.GetImpersonationUserName?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.IO.Pipes.PipeStream.InBufferSize?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.IO.Pipes.PipeStream.OutBufferSize?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.IO.Pipes.PipeStream.ReadMode?displayProperty=nameWithType> (definir somente) | Linux e macOS |
| <xref:System.IO.Pipes.PipeStream.WaitForPipeDrain?displayProperty=nameWithType> | Linux e macOS |

## <a name="systemmedia"></a>System. Media

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Media.SoundPlayer.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Tudo |

## <a name="systemnet"></a>System.Net

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Net.AuthenticationManager.Authenticate(System.String,System.Net.WebRequest,System.Net.ICredentials)?displayProperty=nameWithType> | Todos |
| <xref:System.Net.AuthenticationManager.PreAuthenticate(System.Net.WebRequest,System.Net.ICredentials)?displayProperty=nameWithType> | Todos |
| <xref:System.Net.FileWebRequest.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Todos |
| <xref:System.Net.FileWebRequest.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |
| <xref:System.Net.FileWebResponse.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Todos |
| <xref:System.Net.FileWebResponse.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |
| <xref:System.Net.HttpWebRequest.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Todos |
| <xref:System.Net.HttpWebRequest.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |
| <xref:System.Net.HttpWebResponse.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Todos |
| <xref:System.Net.HttpWebResponse.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |
| <xref:System.Net.WebProxy.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Todos |
| <xref:System.Net.WebProxy.GetDefaultProxy?displayProperty=nameWithType> | Todos |
| <xref:System.Net.WebProxy.GetObjectData%2A?displayProperty=nameWithType> | Todos |
| <xref:System.Net.WebRequest.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Todos |
| <xref:System.Net.WebRequest.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |
| <xref:System.Net.WebResponse.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Todos |
| <xref:System.Net.WebResponse.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |

## <a name="systemnetnetworkinformation"></a>System.Net.NetworkInformation

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Net.NetworkInformation.Ping.Send%2A?displayProperty=nameWithType> | Windows (UWP) |

## <a name="systemnetsockets"></a>System.Net.Sockets

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Net.Sockets.Socket.%23ctor(System.Net.Sockets.SocketInformation)> | Todos |
| <xref:System.Net.Sockets.Socket.DuplicateAndClose(System.Int32)?displayProperty=nameWithType> | Todos |

## <a name="systemnetwebsockets"></a>System.Net.WebSockets

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Net.WebSockets.WebSocket.RegisterPrefixes?displayProperty=nameWithType> | Tudo |

## <a name="systemreflection"></a>System.Reflection

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> | Todos |
| <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom(System.String)?displayProperty=nameWithType> | Todos |
| <xref:System.Reflection.AssemblyName.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |
| <xref:System.Reflection.AssemblyName.OnDeserialization(System.Object)?displayProperty=nameWithType> | Todos |
| <xref:System.Reflection.StrongNameKeyPair.%23ctor(System.String)> | Todos |
| <xref:System.Reflection.StrongNameKeyPair.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Todos |
| <xref:System.Reflection.StrongNameKeyPair.PublicKey?displayProperty=nameWithType> | Todos |

## <a name="systemruntimecompilerservices"></a>System.Runtime.CompilerServices

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Runtime.CompilerServices.DebugInfoGenerator.CreatePdbGenerator?displayProperty=nameWithType> | Tudo |

## <a name="systemruntimeinteropservices"></a>System.Runtime.InteropServices

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Runtime.InteropServices.Marshal.GetIDispatchForObject(System.Object)?displayProperty=nameWithType> | Todos |
| <xref:System.Runtime.InteropServices.RuntimeEnvironment.SystemConfigurationFile?displayProperty=nameWithType> | Todos |
| <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetRuntimeInterfaceAsIntPtr(System.Guid,System.Guid)?displayProperty=nameWithType> | Todos |
| <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetRuntimeInterfaceAsObject(System.Guid,System.Guid)?displayProperty=nameWithType> | Todos |
| <xref:System.Runtime.InteropServices.WindowsRuntime.WindowsRuntimeMarshal.StringToHString(System.String)?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Runtime.InteropServices.WindowsRuntime.WindowsRuntimeMarshal.PtrToStringHString(System.IntPtr)?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Runtime.InteropServices.WindowsRuntime.WindowsRuntimeMarshal.FreeHString(System.IntPtr)?displayProperty=nameWithType> | Linux e macOS |

## <a name="systemruntimeserialization"></a>System.Runtime.Serialization

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Runtime.Serialization.XsdDataContractExporter.Schemas?displayProperty=nameWithType> | Tudo |

## <a name="systemsecurity"></a>System.Security

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Security.CodeAccessPermission.Deny?displayProperty=nameWithType> | Todos |
| <xref:System.Security.CodeAccessPermission.PermitOnly?displayProperty=nameWithType> | Todos |
| <xref:System.Security.PermissionSet.ConvertPermissionSet(System.String,System.Byte[],System.String)?displayProperty=nameWithType> | Todos |
| <xref:System.Security.PermissionSet.Deny?displayProperty=nameWithType> | Todos |
| <xref:System.Security.PermissionSet.PermitOnly?displayProperty=nameWithType> | Todos |
| <xref:System.Security.SecurityContext.Capture?displayProperty=nameWithType> | Todos |
| <xref:System.Security.SecurityContext.CreateCopy?displayProperty=nameWithType> | Todos |
| <xref:System.Security.SecurityContext.Dispose?displayProperty=nameWithType> | Todos |
| <xref:System.Security.SecurityContext.IsFlowSuppressed?displayProperty=nameWithType> | Todos |
| <xref:System.Security.SecurityContext.IsWindowsIdentityFlowSuppressed?displayProperty=nameWithType> | Todos |
| <xref:System.Security.SecurityContext.RestoreFlow?displayProperty=nameWithType> | Todos |
| <xref:System.Security.SecurityContext.Run(System.Security.SecurityContext,System.Threading.ContextCallback,System.Object)?displayProperty=nameWithType> | Todos |
| <xref:System.Security.SecurityContext.SuppressFlow?displayProperty=nameWithType> | Todos |
| <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity?displayProperty=nameWithType> | Todos |

## <a name="systemsecurityclaims"></a>System.Security.Claims

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Security.Claims.ClaimsPrincipal.%23ctor> | Todos |
| <xref:System.Security.Claims.ClaimsPrincipal.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |
| <xref:System.Security.Claims.ClaimsIdentity.%23ctor(System.Runtime.Serialization.SerializationInfo)> | Todos |
| <xref:System.Security.Claims.ClaimsIdentity.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Todos |
| <xref:System.Security.Claims.ClaimsIdentity.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |

## <a name="systemsecuritycryptography"></a>System.Security.Cryptography

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create(System.String)?displayProperty=nameWithType> | Tudo |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.%23ctor%2A> | Linux e macOS |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.Accessible?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.Exportable?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.HardwareDevice?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.KeyContainerName?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.KeyNumber?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.MachineKeyStore?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.Protected?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.ProviderName?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.ProviderType?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.RandomlyGenerated?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.Removable?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.CspKeyContainerInfo.UniqueKeyContainerName?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> | Todos |
| <xref:System.Security.Cryptography.HMAC.Create?displayProperty=nameWithType> | Todos |
| <xref:System.Security.Cryptography.HMAC.Create(System.String)?displayProperty=nameWithType> | Todos |
| <xref:System.Security.Cryptography.HMAC.HashCore%2A?displayProperty=nameWithType> | Todos |
| <xref:System.Security.Cryptography.HMAC.HashFinal%2A?displayProperty=nameWithType> | Todos |
| <xref:System.Security.Cryptography.HMAC.Initialize%2A?displayProperty=nameWithType> | Todos |
| <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=nameWithType> | Todos |
| <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create(System.String)?displayProperty=nameWithType> | Todos |
| <xref:System.Security.Cryptography.ProtectedData.Protect%2A?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.ProtectedData.Unprotect%2A?displayProperty=nameWithType> | Linux e macOS |
| <xref:System.Security.Cryptography.RSA.FromXmlString%2A?displayProperty=nameWithType> | Todos |
| <xref:System.Security.Cryptography.RSA.ToXmlString%2A?displayProperty=nameWithType> | Todos |
| <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=nameWithType> | Todos |
| <xref:System.Security.Cryptography.SymmetricAlgorithm.Create(System.String)?displayProperty=nameWithType> | Todos |

## <a name="systemsecuritycryptographypkcs"></a>System.Security.Cryptography.Pkcs

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Security.Cryptography.Pkcs.CmsSigner.%23ctor(System.Security.Cryptography.CspParameters)> | Todos |
| <xref:System.Security.Cryptography.Pkcs.SignerInfo.ComputeCounterSignature?displayProperty=nameWithType> | Todos |

## <a name="systemsecuritycryptographyx509certificates"></a>System.Security.Cryptography.X509Certificates

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Security.Cryptography.X509Certificates.X509Certificate.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Todos |
| <xref:System.Security.Cryptography.X509Certificates.X509Certificate.Import%2A?displayProperty=nameWithType> | Todos |
| <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Todos |
| <xref:System.Security.Cryptography.X509Certificates.X509Certificate2.PrivateKey?displayProperty=nameWithType> (definir somente) | Tudo |

## <a name="systemsecurityauthenticationextendedprotection"></a>System.Security.Authentication.ExtendedProtection

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Tudo |

## <a name="systemsecuritypolicy"></a>System. Security. Policy

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Security.Policy.Hash.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Tudo |

## <a name="systemserviceprocessservicecontroller"></a>System.ServiceProcess.ServiceController

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.ServiceProcess.TimeoutException.%23ctor(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)> | Tudo |

## <a name="systemtextregularexpressions"></a>System.Text.RegularExpressions

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A?displayProperty=nameWithType> | Tudo |

## <a name="systemthreading"></a>System.Threading

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Threading.CompressedStack.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |
| <xref:System.Threading.ExecutionContext.GetObjectData(System.Runtime.Serialization.SerializationInfo,System.Runtime.Serialization.StreamingContext)?displayProperty=nameWithType> | Todos |
| <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> | Todos |
| <xref:System.Threading.Thread.ResetAbort?displayProperty=nameWithType> | Todos |
| <xref:System.Threading.Thread.Resume?displayProperty=nameWithType> | Todos |
| <xref:System.Threading.Thread.Suspend?displayProperty=nameWithType> | Todos |

## <a name="systemxml"></a>System.Xml

| Membro | Plataformas que lançam |
| - | - |
| <xref:System.Xml.XmlDictionaryReader.CreateMtomReader(System.Byte[],System.Int32,System.Int32,System.Text.Encoding[],System.String,System.Xml.XmlDictionaryReaderQuotas,System.Int32,System.Xml.OnXmlDictionaryReaderClose)?displayProperty=nameWithType> | Todos |
| <xref:System.Xml.XmlDictionaryReader.CreateMtomReader(System.IO.Stream,System.Text.Encoding[],System.String,System.Xml.XmlDictionaryReaderQuotas,System.Int32,System.Xml.OnXmlDictionaryReaderClose)?displayProperty=nameWithType> | Todos |
| <xref:System.Xml.XmlDictionaryWriter.CreateMtomWriter(System.IO.Stream,System.Text.Encoding,System.Int32,System.String,System.String,System.String,System.Boolean,System.Boolean)?displayProperty=nameWithType> | Todos |

## <a name="see-also"></a>Confira também

- [Alterações recentes de migração do .NET Framework para o .NET Core](fx-core.md)
- [Serialização binária no .NET Core](../../standard/serialization/binary-serialization.md#net-core)
- [Analisador de portabilidade .NET](../../standard/analyzers/portability-analyzer.md)
