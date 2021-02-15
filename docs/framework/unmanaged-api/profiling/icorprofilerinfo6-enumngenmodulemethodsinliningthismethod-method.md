---
description: 'Saiba mais sobre o método: ICorProfilerInfo6:: EnumNgenModuleMethodsInliningThisMethod'
title: Método ICorProfilerInfo6::EnumNgenModuleMethodsInliningThisMethod
ms.date: 03/30/2017
ms.assetid: b933dfe6-7833-40cb-aad8-40842dc3034f
ms.openlocfilehash: bd43dcecabe9a75f7ce3a94996727b192574e321
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99737162"
---
# <a name="icorprofilerinfo6enumngenmodulemethodsinliningthismethod-method"></a>Método ICorProfilerInfo6::EnumNgenModuleMethodsInliningThisMethod

Retorna um enumerador para todos os métodos que são definidos em um determinado módulo NGen e embutidos em um determinado método.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumNgenModuleMethodsInliningThisMethod(
        [in] ModuleID inlinersModuleId,
        [in] ModuleID inlineeModuleId,
        [in] mdMethodDef inlineeMethodId,
        [out] BOOL *incompleteData,
        [out] ICorProfilerMethodEnum** ppEnum
);
```

## <a name="parameters"></a>Parâmetros

`inlinersModuleId`\
no O identificador de um módulo NGen.

`inlineeModuleId`\
no O identificador de um módulo que define `inlineeMethodId` . Consulte a seção Comentários para obter mais informações.

`inlineeMethodId`\
no O identificador de um método embutido. Consulte a seção Comentários para obter mais informações.

`incompleteData`\
fora Um sinalizador que indica se `ppEnum` o contém todos os métodos que indefinem um determinado método.  Consulte a seção Comentários para obter mais informações.

`ppEnum`\
fora Um ponteiro para o endereço de um enumerador

## <a name="remarks"></a>Comentários

`inlineeModuleId` e, `inlineeMethodId` juntos, formam o identificador completo do método que pode ser embutido. Por exemplo, suponha que `A` o módulo defina um método `Simple.Add` :

```csharp
Simple.Add(int a, int b)
{ return a + b; }
```

e o módulo B define `Fancy.AddTwice` :

```csharp
Fancy.AddTwice(int a, int b)
{ return Simple.Add(a,b) + Simple.Add(a,b); }
```

Vamos supor também que `Fancy.AddTwice` o embutirá a chamada para `SimpleAdd` . Um criador de perfil pode usar esse enumerador para localizar todos os métodos definidos no módulo B que está embutido `Simple.Add` e o resultado seria enumerado `AddTwice` .  `inlineeModuleId` é o identificador do módulo `A` e `inlineeMethodId` é o identificador de `Simple.Add(int a, int b)` .

Se `incompleteData` for true Depois que a função retornar, o enumerador não conterá todos os métodos inalinhando um determinado método. Isso pode acontecer quando uma ou mais dependências diretas ou indiretas do módulo inlineers ainda não foram carregadas. Se um criador de perfil precisar de dados precisos, ele deverá tentar novamente mais tarde quando mais módulos forem carregados, preferencialmente em cada carregamento de módulo.

O `EnumNgenModuleMethodsInliningThisMethod` método pode ser usado para solucionar limitações de inalinhamento para ReJIT. O ReJIT permite que um criador de perfil altere a implementação de um método e, em seguida, crie um novo código para ele em tempo real. Por exemplo, poderíamos mudar da `Simple.Add` seguinte maneira:

```csharp
Simple.Add(int a, int b)
{ return 42; }
```

No entanto `Fancy.AddTwice` , como já foi embutido `Simple.Add` , ele continua tendo o mesmo comportamento que antes. Para contornar essa limitação, o chamador precisa pesquisar todos os métodos em todos os módulos que embutidos `Simple.Add` e usar `ICorProfilerInfo5::RequestRejit` em cada um desses métodos. Quando os métodos forem compilados novamente, eles terão o novo comportamento do `Simple.Add` em vez do comportamento antigo.

## <a name="requirements"></a>Requisitos

**Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).

**Cabeçalho:** CorProf. idl, CorProf. h

**Biblioteca:** CorGuids.lib

**.NET Framework versões:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]

## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo6](icorprofilerinfo6-interface.md)
