---
title: Usando variância para delegados genéricos Func e Action (C#)
description: Saiba mais sobre como usar Covariance e contravariância nos delegados de Func e Action Generic para proporcionar mais flexibilidade em seu código.
ms.date: 07/20/2015
ms.assetid: 1826774f-2b7a-470f-b110-17cfdd6abdae
ms.openlocfilehash: 613470d7870aa6a917d19904a92e56f0e61f1ed9
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91176338"
---
# <a name="using-variance-for-func-and-action-generic-delegates-c"></a>Usando variância para delegados genéricos Func e Action (C#)

Esses exemplos demonstram como usar covariância e contravariância nos delegados genéricos `Func` e `Action` para permitir a reutilização dos métodos e fornecer mais flexibilidade em seu código.  
  
 Para obter mais informações sobre covariância e contravariância, consulte [Variação em delegações (C#)](./variance-in-delegates.md).  
  
## <a name="using-delegates-with-covariant-type-parameters"></a>Usando delegados com parâmetros de tipo covariantes  

 O exemplo a seguir ilustra os benefícios do suporte à covariância nos delegados genéricos `Func`. O método `FindByTitle` assume um parâmetro do tipo `String` e retorna um objeto do tipo `Employee`. No entanto, você pode atribuir esse método ao delegado `Func<String, Person>` porque `Employee` herda `Person`.  
  
```csharp  
// Simple hierarchy of classes.  
public class Person { }  
public class Employee : Person { }  
class Program  
{  
    static Employee FindByTitle(String title)  
    {  
        // This is a stub for a method that returns  
        // an employee that has the specified title.  
        return new Employee();  
    }  
  
    static void Test()  
    {  
        // Create an instance of the delegate without using variance.  
        Func<String, Employee> findEmployee = FindByTitle;  
  
        // The delegate expects a method to return Person,  
        // but you can assign it a method that returns Employee.  
        Func<String, Person> findPerson = FindByTitle;  
  
        // You can also assign a delegate
        // that returns a more derived type
        // to a delegate that returns a less derived type.  
        findPerson = findEmployee;  
  
    }  
}  
```  
  
## <a name="using-delegates-with-contravariant-type-parameters"></a>Usando delegados com parâmetros de tipo contravariantes  

 O exemplo a seguir ilustra os benefícios do suporte à contravariância nos delegados genéricos `Action`. O método `AddToContacts` assume um parâmetro do tipo `Person`. No entanto, você pode atribuir esse método ao delegado `Action<Employee>` porque `Employee` herda `Person`.  
  
```csharp  
public class Person { }  
public class Employee : Person { }  
class Program  
{  
    static void AddToContacts(Person person)  
    {  
        // This method adds a Person object  
        // to a contact list.  
    }  
  
    static void Test()  
    {  
        // Create an instance of the delegate without using variance.  
        Action<Person> addPersonToContacts = AddToContacts;  
  
        // The Action delegate expects
        // a method that has an Employee parameter,  
        // but you can assign it a method that has a Person parameter  
        // because Employee derives from Person.  
        Action<Employee> addEmployeeToContacts = AddToContacts;  
  
        // You can also assign a delegate
        // that accepts a less derived parameter to a delegate
        // that accepts a more derived parameter.  
        addEmployeeToContacts = addPersonToContacts;  
    }  
}  
```  
  
## <a name="see-also"></a>Confira também

- [Covariância e contravariância (C#)](./index.md)
- [Genéricos](../../../../standard/generics/index.md)
