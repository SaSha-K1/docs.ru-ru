---
title: Предложение Skip While
ms.date: 07/20/2015
f1_keywords:
- vb.QuerySkipWhile
helpviewer_keywords:
- Skip While statement [Visual Basic]
- Skip While clause [Visual Basic]
- queries [Visual Basic], Skip While
ms.assetid: 5dee8350-7520-4f1a-b00d-590cacd572d6
ms.openlocfilehash: af722f7aee021f244b411cdc61619b7de3c20607
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/22/2020
ms.locfileid: "90866230"
---
# <a name="skip-while-clause-visual-basic"></a>Предложение Skip While (Visual Basic)

Пропускает элементы в коллекции, если заданное условие имеет значение `true`, и возвращает остальные элементы.  
  
## <a name="syntax"></a>Синтаксис  
  
```vb  
Skip While expression  
```  
  
## <a name="parts"></a>Компоненты  
  
|Термин|Определение|  
|---|---|  
|`expression`|Обязательный. Выражение, представляющее условие для проверки элементов. Выражение должно возвращать `Boolean` значение или функциональный эквивалент, например, `Integer` для вычисления в виде `Boolean` .|  
  
## <a name="remarks"></a>Remarks  

 `Skip While`Предложение обходит элементы из начала результата запроса до тех пор, пока не будут `expression` возвращены `false` . После `expression` возврата `false` запрос возвращает все остальные элементы. `expression`Для оставшихся результатов игнорируется.  
  
 `Skip While`Предложение отличается от `Where` предложения в том, что `Where` предложение может использоваться для исключения всех элементов из запроса, которые не соответствуют определенному условию. `Skip While`Предложение исключает элементы только до первого момента, когда условие не будет удовлетворено. `Skip While`Предложение наиболее полезно при работе с упорядоченным результатом запроса.  
  
 Можно обойти определенное количество результатов с начала результата запроса с помощью `Skip` предложения.  
  
## <a name="example"></a>Пример  

 В следующем примере кода предложение используется `Skip While` для обхода результатов до тех пор, пока не будет найден первый клиент из США.  
  
 [!code-vb[VbSimpleQuerySamples#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#3)]  
  
## <a name="see-also"></a>См. также

- [Introduction to LINQ in Visual Basic](../../programming-guide/language-features/linq/introduction-to-linq.md) (Знакомство с LINQ в Visual Basic)
- [Запросы](index.md)
- [Предложение SELECT](select-clause.md)
- [Предложение FROM](from-clause.md)
- [Предложение Skip](skip-clause.md)
- [Предложение Take While](take-while-clause.md)
- [Предложение WHERE](where-clause.md)
