---
title: 'Alteração significativa: MVC: ObjectModelValidator chama uma nova sobrecarga de ValidationVisitor. Validate'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core 5,0 intitulado MVC: ObjectModelValidator chama uma nova sobrecarga de ValidationVisitor. Validate'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: b28c357f51291a4f73889d5d413a983f79e09daf
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760526"
---
# <a name="mvc-objectmodelvalidator-calls-a-new-overload-of-validationvisitorvalidate"></a>MVC: ObjectModelValidator chama uma nova sobrecarga de ValidationVisitor. Validate

No ASP.NET Core 5,0, uma sobrecarga do <xref:Microsoft.AspNetCore.Mvc.ModelBinding.Validation.ValidationVisitor.Validate%2A?displayProperty=nameWithType> foi adicionada. A nova sobrecarga aceita a instância de modelo de nível superior que contém propriedades:

```diff
  bool Validate(ModelMetadata metadata, string key, object model, bool alwaysValidateAtTopLevel);
+ bool Validate(ModelMetadata metadata, string key, object model, bool alwaysValidateAtTopLevel, object container);
```

<xref:Microsoft.AspNetCore.Mvc.ModelBinding.ObjectModelValidator> invoca essa nova sobrecarga de `ValidationVisitor` para executar a validação. Essa nova sobrecarga será pertinente se a sua biblioteca de validação se integrar com o sistema de validação de modelo do MVC ASP.NET Core.

Para obter uma discussão, consulte o problema do GitHub [dotnet/aspnetcore # 26020](https://github.com/dotnet/aspnetcore/issues/26020).

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="old-behavior"></a>Comportamento antigo

`ObjectModelValidator` Invoca a seguinte sobrecarga durante a validação do modelo:

```csharp
ValidationVisitor.Validate(ModelMetadata metadata, string key, object model, bool alwaysValidateAtTopLevel)
```

## <a name="new-behavior"></a>Novo comportamento

`ObjectModelValidator` Invoca a seguinte sobrecarga durante a validação do modelo:

```csharp
ValidationVisitor.Validate(ModelMetadata metadata, string key, object model, bool alwaysValidateAtTopLevel, object container)
```

## <a name="reason-for-change"></a>Motivo da alteração

Essa alteração foi introduzida para dar suporte a validadores, como <xref:System.ComponentModel.DataAnnotations.CompareAttribute> , que dependem da inspeção de outras propriedades.

## <a name="recommended-action"></a>Ação recomendada

As estruturas de validação que dependem de `ObjectModelValidator` para invocar a sobrecarga existente do `ValidationVisitor` devem substituir o novo método ao direcionar o .NET 5,0 ou posterior:

```csharp
public class MyCustomValidationVisitor : ValidationVisitor
{
+  public override bool Validate(ModelMetadata metadata, string key, object model, bool alwaysValidateAtTopLevel, object container)
+  {
+    ...
}
```

## <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.Mvc.ModelBinding.Validation.ValidationVisitor.Validate%2A?displayProperty=nameWithType>

<!--

### Category

ASP.NET Core

### Affected APIs

`Overload:Microsoft.AspNetCore.Mvc.ModelBinding.Validation.ValidationVisitor.Validate`

-->
