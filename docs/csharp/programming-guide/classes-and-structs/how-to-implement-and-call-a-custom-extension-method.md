---
title: Практическое руководство. Реализация и вызов пользовательского метода расширения (руководство по программированию на C#)
description: Узнайте, как реализовать методы расширения для любого типа .NET. Клиентский код может использовать ваши методы путем добавления ссылки на содержащую их библиотеку DLL и добавления директивы using.
ms.date: 07/20/2015
helpviewer_keywords:
- extension methods [C#], implementing and calling
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 7dab2a56-cf8e-4a47-a444-fe610a02772a
ms.openlocfilehash: 4ae48a05d451a3276b3a0f2ee4d6c633ce7db306
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513018"
---
# <a name="how-to-implement-and-call-a-custom-extension-method-c-programming-guide"></a>Практическое руководство. Реализация и вызов пользовательского метода расширения (руководство по программированию на C#)

Этот раздел описывает, как реализовать свои методы расширения для любого типа .NET Framework. Клиентский код может использовать методы расширения путем добавления ссылки на содержащую их библиотеку DLL и добавления директивы [using](../../language-reference/keywords/using-directive.md), которая указывает пространство имен, в котором определены методы расширения.  
  
## <a name="to-define-and-call-the-extension-method"></a>Определение и вызов метода расширения  
  
1. Определите статический [класс](./static-classes-and-static-class-members.md), который будет содержать метод расширения.  
  
     Класс должен быть видимым для клиентского кода. Дополнительные сведения о правилах доступа см. в разделах [Модификаторы доступа](./access-modifiers.md).  
  
2. Реализуйте метод расширения как статический метод как минимум с тем же уровнем видимости, что и содержащий класс.  
  
3. Первый параметр метода указывает тип, с которым работает метод. Ему должен предшествовать модификатор [this](../../language-reference/keywords/this.md).  
  
4. В вызывающем коде добавьте директиву `using`, чтобы задать [пространство имен](../../language-reference/keywords/namespace.md), содержащее класс метода расширения.  
  
5. Вызовите методы, как если бы они являлись методами экземпляра для типа.  
  
     Обратите внимание, что первый параметр не указан вызывающим кодом, поскольку он представляет тип, к которому применяется оператор, и компилятору уже известен тип объекта. Вам необходимо предоставить аргументы только для параметров со 2 по `n`.  
  
## <a name="example"></a>Пример  

 В приведенном ниже примере реализуется метод расширения с именем `WordCount` в классе `CustomExtensions.StringExtension`. Метод работает с классом <xref:System.String> класса, который указан как первый параметр метода. Пространство имен `CustomExtensions` импортируется в пространство имен приложения, и метод вызывается внутри метода `Main`.  
  
 [!code-csharp[csProgGuideExtensionMethods#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#1)]  
  
## <a name="net-security"></a>Безопасность .NET  

 Методы расширения не предоставляют определенных уязвимостей безопасности. Они не могут использоваться для олицетворения существующих методов для типа, поскольку все конфликты имен разрешаются в пользу метода экземпляра или статического метода, определяемого самим типом. Методы расширения не могут получить доступ к любым конфиденциальным данным в расширенном классе.  
  
## <a name="see-also"></a>См. также

- [Руководство по программированию на C#](../index.md)
- [Методы расширения](./extension-methods.md)
- [Встроенный язык запросов LINQ](../../linq/linq-in-csharp.md)
- [Статические классы и члены статических классов](./static-classes-and-static-class-members.md)
- [protected](../../language-reference/keywords/protected.md)
- [internal](../../language-reference/keywords/internal.md)
- [public](../../language-reference/keywords/public.md)
- [this](../../language-reference/keywords/this.md)
- [namespace](../../language-reference/keywords/namespace.md)
