---
title: "Оператор ~ (справочник по C#)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- ~_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- tilde (~) one's complement operator [C#]
- ~ operator [C#]
- ~ [C#], bitwise complement operator
- bitwise complement operator [C#]
ms.assetid: 11bc078a-50e2-4d7e-9896-67ef669dc602
caps.latest.revision: 18
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: ffbfc379b7c021ccd8fbed9b796aa9fda6618b55
ms.contentlocale: ru-ru
ms.lasthandoff: 07/28/2017

---
# <a name="-operator-c-reference"></a><span data-ttu-id="defa2-102">Оператор ~ (справочник по C#)</span><span class="sxs-lookup"><span data-stu-id="defa2-102">~ Operator (C# Reference)</span></span>
<span data-ttu-id="defa2-103">Оператор `~` выполняет операцию поразрядного дополнения операнда, заключающуюся в инвертировании каждого бита.</span><span class="sxs-lookup"><span data-stu-id="defa2-103">The `~` operator performs a bitwise complement operation on its operand, which has the effect of reversing each bit.</span></span> <span data-ttu-id="defa2-104">Операторы поразрядного дополнения предопределены для типов [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md) и [ulong](../../../csharp/language-reference/keywords/ulong.md).</span><span class="sxs-lookup"><span data-stu-id="defa2-104">Bitwise complement operators are predefined for [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md), and [ulong](../../../csharp/language-reference/keywords/ulong.md).</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="defa2-105">Символ `~` также используется для объявления методов завершения.</span><span class="sxs-lookup"><span data-stu-id="defa2-105">The `~` symbol also is used to declare finalizers.</span></span> <span data-ttu-id="defa2-106">Дополнительные сведения см. в разделе [Методы завершения](../../../csharp/programming-guide/classes-and-structs/destructors.md).</span><span class="sxs-lookup"><span data-stu-id="defa2-106">For more information, see [Finalizers](../../../csharp/programming-guide/classes-and-structs/destructors.md).</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="defa2-107">Примечания</span><span class="sxs-lookup"><span data-stu-id="defa2-107">Remarks</span></span>  
 <span data-ttu-id="defa2-108">Определяемые пользователем типы могут перегружать оператор `~`.</span><span class="sxs-lookup"><span data-stu-id="defa2-108">User-defined types can overload the `~` operator.</span></span> <span data-ttu-id="defa2-109">Дополнительные сведения см. в статье [operator](../../../csharp/language-reference/keywords/operator.md).</span><span class="sxs-lookup"><span data-stu-id="defa2-109">For more information, see [operator](../../../csharp/language-reference/keywords/operator.md).</span></span> <span data-ttu-id="defa2-110">Операции с целыми типами обычно разрешены и для перечислений.</span><span class="sxs-lookup"><span data-stu-id="defa2-110">Operations on integral types are generally allowed on enumeration.</span></span>  
  
## <a name="example"></a><span data-ttu-id="defa2-111">Пример</span><span class="sxs-lookup"><span data-stu-id="defa2-111">Example</span></span>  
 <span data-ttu-id="defa2-112">[!code-cs[csRefOperators#25](../../../csharp/language-reference/operators/codesnippet/CSharp/bitwise-complement-operator_1.cs)]</span><span class="sxs-lookup"><span data-stu-id="defa2-112">[!code-cs[csRefOperators#25](../../../csharp/language-reference/operators/codesnippet/CSharp/bitwise-complement-operator_1.cs)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="defa2-113">См. также</span><span class="sxs-lookup"><span data-stu-id="defa2-113">See Also</span></span>  
 <span data-ttu-id="defa2-114">[Справочник по C#](../../../csharp/language-reference/index.md) </span><span class="sxs-lookup"><span data-stu-id="defa2-114">[C# Reference](../../../csharp/language-reference/index.md) </span></span>  
 <span data-ttu-id="defa2-115">[Руководство по программированию на C#](../../../csharp/programming-guide/index.md) </span><span class="sxs-lookup"><span data-stu-id="defa2-115">[C# Programming Guide](../../../csharp/programming-guide/index.md) </span></span>  
 <span data-ttu-id="defa2-116">[Операторы в C#](../../../csharp/language-reference/operators/index.md) </span><span class="sxs-lookup"><span data-stu-id="defa2-116">[C# Operators](../../../csharp/language-reference/operators/index.md) </span></span>  
 [<span data-ttu-id="defa2-117">Методы завершения</span><span class="sxs-lookup"><span data-stu-id="defa2-117">Finalizers</span></span>](../../../csharp/programming-guide/classes-and-structs/destructors.md)
