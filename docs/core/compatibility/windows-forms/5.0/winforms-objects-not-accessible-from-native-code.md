---
title: 'Alteração significativa: objetos WinForms não acessíveis a partir de código nativo'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que os objetos de Windows Forms não são mais acessíveis a partir de código nativo.
ms.date: 01/29/2021
ms.openlocfilehash: 53343f3f07817f735fa3b0ee77a352dcc80d4b6c
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506541"
---
# <a name="native-code-cant-access-windows-forms-objects"></a>O código nativo não pode acessar objetos Windows Forms

A partir do .NET 5,0, você não pode mais acessar Windows Forms objetos do código nativo.

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, alguns tipos de Windows Forms foram decorados como visíveis para a interoperabilidade COM e, portanto, eram acessíveis para código nativo. A partir do .NET 5,0, nenhuma API Windows Forms é visível para a interoperabilidade COM ou acessível para código nativo. O tempo de execução do .NET não dá mais suporte à criação de bibliotecas de tipos personalizadas prontas. Além disso, o tempo de execução do .NET não pode depender da biblioteca de tipos para .NET Framework (o que exigiria manter a forma das classes como estavam em .NET Framework).

## <a name="reason-for-change"></a>Motivo da alteração

- Remoção de `ComVisible(true)` enumerações que foram usadas para geração e pesquisa de biblioteca de tipos (arquivo tlb): como não há um TLB do WinForms fornecido pelo .NET Core, não há nenhum valor para manter esse atributo.
- Remoção de `ComVisible(true)` `AccessibleObject` classes de: as classes não podem ser cocriadas (não têm nenhum construtor sem parâmetros) e a exposição de uma instância já existente ao com não requer esse atributo.
- Remoção de `ComVisible(true)` `Control` classes from `Component` : isso foi usado para permitir a hospedagem de controles WinForms via OLE/ActiveX, por exemplo, no VB6 ou no MFC. No entanto, isso requer um TLB para WinForms, que não é mais fornecido, bem como ativação baseada no registro, que também não funcionaria prontamente. Em geral, não havia nenhuma manutenção da hospedagem baseada em COM de controles WinForms, portanto, o suporte foi removido, em vez de deixá-lo em um estado sem suporte.
- Remoção de `ClassInterface` atributos de controles: se não houver suporte para a hospedagem via OLE/ActiveX, esses atributos não serão mais necessários. Eles são mantidos em outros locais em que os objetos ainda são expostos ao COM e o atributo pode ser relevante.
- Remoção de `ComVisible(true)` de `EventArgs` : eles provavelmente eram usados com hospedagem OLE/ActiveX, que não tem mais suporte. Eles também não podem ser cocriados, portanto, o atributo não tem nenhuma finalidade. Além disso, a exposição de instâncias existentes sem fornecer um TLB não faz sentido.
- Remoção de `ComVisible(true)` delegados: a finalidade é desconhecida, mas como a hospedagem do ActiveX de controles WinForms não é mais suportada, é improvável que haja alguma utilidade.
- Remoção de `ComVisible(true)` um código não público: o único consumidor potencial seria o novo Visual Studio Designer, mas sem um GUID especificado, é improvável que ainda seja necessário.
- Remoção de `ComVisible(true)` algumas classes de designer público arbitrárias: o Visual Studio Designer antigo pode ter usado a interoperabilidade com para se comunicar com essas classes. No entanto, o designer antigo não dá suporte ao .NET Core, portanto, poucas pessoas precisariam delas `ComVisible` .
- `IWin32Window` definido o mesmo GUID que foi definido em .NET Framework, que tem consequências perigosas. Se você precisar de interoperabilidade com .NET Framework, use `ComImport` .
- O WinForms gerenciados `IDataObject` foi feito `ComVisible` . Isso não é necessário, há uma `ComImport` declaração de interface separada para `IDataObject` interoperabilidade com. É muito importante ter o gerenciado `IDataObject` `ComVisible` , uma vez que nenhum tlb é fornecido e o marshaling sempre falhará. Além disso, o GUID não foi especificado e difere de .NET Framework, portanto, seu improvável que remover um IID não documentado afetará os clientes de forma negativa.
- Remoção de `ComVisible(false)` : elas são colocadas em locais aparentemente arbitrários e são redundantes quando o padrão é não expor classes para interoperabilidade com.

## <a name="version-introduced"></a>Versão introduzida

.NET 5.0

## <a name="recommended-action"></a>Ação recomendada

O exemplo a seguir funciona em .NET Framework e no .NET Core 3,1. Este exemplo se baseia na biblioteca de tipos de .NET Framework, que permite que o JavaScript chame de volta na subclasse do formulário via reflexão.

```cs
[PermissionSet(SecurityAction.Demand, Name="FullTrust")]
[System.Runtime.InteropServices.ComVisibleAttribute(true)]
public class Form1 : Form
{
    private WebBrowser webBrowser1 = new WebBrowser();

    protected override void OnLoad(EventArgs e)
    {
        webBrowser1.AllowWebBrowserDrop = false;
        webBrowser1.IsWebBrowserContextMenuEnabled = false;
        webBrowser1.WebBrowserShortcutsEnabled = false;
        webBrowser1.ObjectForScripting = this;

        webBrowser1.DocumentText =
            "<html><body><button " +
            "onclick=\"window.external.Test('called from script code')\">" +
            "call client code from script code</button>" +
            "</body></html>";
    }

    public void Test(String message)
    {
        MessageBox.Show(message, "client code");
    }
}
```

Há duas maneiras possíveis de fazer o exemplo funcionar no .NET 5,0 e versões posteriores:

- Introduza um `ObjectForScripting` objeto declarado pelo usuário que dá suporte a `IDispatch` (que é aplicado por padrão, a menos que seja alterado explicitamente no nível do projeto).

  ```cs
  public class MyScriptObject
  {
      private Form1 _form;

      public MyScriptObject(Form1 form)
      {
          _form = form;
      }

      public void Test(string message)
      {
          MessageBox.Show(message, "client code");
      }
  }

  public partial class Form1 : Form
  {
      protected override void OnLoad(EventArgs e)
      {
          ...

          // Works correctly.
          webBrowser1.ObjectForScripting = new MyScriptObject(this);

          ...
      }
  }
  ```

- Declare uma interface com os métodos a serem expostos.

  ```cs
  public interface IForm1
  {
      void Test(string message);
  }

  [ComDefaultInterface(typeof(IForm1))]
  public partial class Form1 : Form, IForm1
  {
      protected override void OnLoad(EventArgs e)
      {
          ...

          // Works correctly.
          webBrowser1.ObjectForScripting = this;

          ...
      }
  }
  ```

## <a name="affected-apis"></a>APIs afetadas

Todas as APIs de Windows Forms.

<!--

### Category

- Windows Forms

-->
