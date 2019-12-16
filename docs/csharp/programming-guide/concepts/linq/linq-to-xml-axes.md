---
title: "Оси LINQ to XML (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 3f7d54ff-b608-43a1-9e2d-e70668b72df8
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 65d64b6082942d702444305d7dfed4d05444b59e
ms.contentlocale: ru-ru
ms.lasthandoff: 07/28/2017

---
# <a name="linq-to-xml-axes-c"></a><span data-ttu-id="04a75-102">Оси LINQ to XML (C#)</span><span class="sxs-lookup"><span data-stu-id="04a75-102">LINQ to XML Axes (C#)</span></span>
<span data-ttu-id="04a75-103">После создания XML-дерева или загрузки XML-документа в XML-дерево можно опросить его для поиска элементов и атрибутов и извлечения их значений.</span><span class="sxs-lookup"><span data-stu-id="04a75-103">After you have created an XML tree or loaded an XML document into an XML tree, you can query it to find elements and attributes and retrieve their values.</span></span>  
  
 <span data-ttu-id="04a75-104">Перед составлением каких-либо запросов необходимо понять назначение осей [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].</span><span class="sxs-lookup"><span data-stu-id="04a75-104">Before you can write any queries, you must understand the [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] axes.</span></span> <span data-ttu-id="04a75-105">Существует два вида методов оси. Во-первых, есть методы, вызываемые применительно к одному объекту <xref:System.Xml.Linq.XElement>, объекту <xref:System.Xml.Linq.XDocument> или объекту <xref:System.Xml.Linq.XNode>.</span><span class="sxs-lookup"><span data-stu-id="04a75-105">There are two kinds of axis methods: First, there are the methods that you call on a single <xref:System.Xml.Linq.XElement> object, <xref:System.Xml.Linq.XDocument> object, or <xref:System.Xml.Linq.XNode> object.</span></span> <span data-ttu-id="04a75-106">Данные методы работают с одним объектом и возвращают коллекцию объектов <xref:System.Xml.Linq.XElement>, <xref:System.Xml.Linq.XAttribute> или <xref:System.Xml.Linq.XNode>.</span><span class="sxs-lookup"><span data-stu-id="04a75-106">These methods operate on a single object and return a collection of <xref:System.Xml.Linq.XElement>, <xref:System.Xml.Linq.XAttribute>, or <xref:System.Xml.Linq.XNode> objects.</span></span> <span data-ttu-id="04a75-107">Во-вторых, существуют методы расширения, работающие с коллекциями и возвращающие коллекции.</span><span class="sxs-lookup"><span data-stu-id="04a75-107">Second, there are extension methods that operate on collections and return collections.</span></span> <span data-ttu-id="04a75-108">В этих методах расширения создается перечисление исходной коллекции, вызывается соответствующий метод оси применительно к каждому элементу коллекции и осуществляется объединение результатов.</span><span class="sxs-lookup"><span data-stu-id="04a75-108">The extension methods enumerate the source collection, call the appropriate axis method on each item in the collection, and concatenate the results.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="04a75-109">Содержание</span><span class="sxs-lookup"><span data-stu-id="04a75-109">In This Section</span></span>  
  
|<span data-ttu-id="04a75-110">Раздел</span><span class="sxs-lookup"><span data-stu-id="04a75-110">Topic</span></span>|<span data-ttu-id="04a75-111">Описание</span><span class="sxs-lookup"><span data-stu-id="04a75-111">Description</span></span>|  
|-----------|-----------------|  
|[<span data-ttu-id="04a75-112">Общие сведения об осях LINQ to XML (C#)</span><span class="sxs-lookup"><span data-stu-id="04a75-112">LINQ to XML Axes Overview (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes-overview.md)|<span data-ttu-id="04a75-113">Определяет оси и содержит описание того, как они используются в контексте запросов [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].</span><span class="sxs-lookup"><span data-stu-id="04a75-113">Defines axes, and explains how they are used in the context of [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] queries.</span></span>|  
|[<span data-ttu-id="04a75-114">Практическое руководство. Извлечение коллекции элементов (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="04a75-114">How to: Retrieve a Collection of Elements (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-a-collection-of-elements-linq-to-xml.md)|<span data-ttu-id="04a75-115">Вводит метод <xref:System.Xml.Linq.XContainer.Elements%2A>.</span><span class="sxs-lookup"><span data-stu-id="04a75-115">Introduces the <xref:System.Xml.Linq.XContainer.Elements%2A> method.</span></span> <span data-ttu-id="04a75-116">Этот метод получает коллекцию дочерних элементов того или иного элемента.</span><span class="sxs-lookup"><span data-stu-id="04a75-116">This method retrieves a collection of the child elements of an element.</span></span>|  
|[<span data-ttu-id="04a75-117">Практическое руководство. Извлечение значений элемента (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="04a75-117">How to: Retrieve the Value of an Element (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-element-linq-to-xml.md)|<span data-ttu-id="04a75-118">Показывает способ получения значений элементов.</span><span class="sxs-lookup"><span data-stu-id="04a75-118">Shows how to get the values of elements.</span></span>|  
|[<span data-ttu-id="04a75-119">Практическое руководство. Фильтрация по именам элементов (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="04a75-119">How to: Filter on Element Names (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/how-to-filter-on-element-names-linq-to-xml.md)|<span data-ttu-id="04a75-120">Показывает способ фильтрации по именам элементов при использовании осей.</span><span class="sxs-lookup"><span data-stu-id="04a75-120">Shows how to filter on element names when using axes.</span></span>|  
|[<span data-ttu-id="04a75-121">Практическое руководство. Связанные вызовы метода оси (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="04a75-121">How to: Chain Axis Method Calls (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/how-to-chain-axis-method-calls-linq-to-xml.md)|<span data-ttu-id="04a75-122">Показывает, как соединять в цепочку вызовы для методов осей.</span><span class="sxs-lookup"><span data-stu-id="04a75-122">Shows how to chain calls to axes methods.</span></span>|  
|[<span data-ttu-id="04a75-123">Практическое руководство. Извлечение одного дочернего элемента (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="04a75-123">How to: Retrieve a Single Child Element (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-a-single-child-element-linq-to-xml.md)|<span data-ttu-id="04a75-124">Показывает способ получения одного дочернего элемента того или иного элемента по имени тега дочернего элемента.</span><span class="sxs-lookup"><span data-stu-id="04a75-124">Shows how to retrieve a single child element of an element, given the tag name of the child element.</span></span>|  
|[<span data-ttu-id="04a75-125">Практическое руководство. Извлечение коллекции атрибутов (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="04a75-125">How to: Retrieve a Collection of Attributes (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-a-collection-of-attributes-linq-to-xml.md)|<span data-ttu-id="04a75-126">Вводит метод <xref:System.Xml.Linq.XElement.Attributes%2A>.</span><span class="sxs-lookup"><span data-stu-id="04a75-126">Introduces the <xref:System.Xml.Linq.XElement.Attributes%2A> method.</span></span> <span data-ttu-id="04a75-127">Этот метод извлекает атрибуты того или иного элемента.</span><span class="sxs-lookup"><span data-stu-id="04a75-127">This method retrieves the attributes of an element.</span></span>|  
|[<span data-ttu-id="04a75-128">Практическое руководство. Извлечение одного атрибута (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="04a75-128">How to: Retrieve a Single Attribute (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-a-single-attribute-linq-to-xml.md)|<span data-ttu-id="04a75-129">Показывает способ получения одного атрибута элемента по имени атрибута.</span><span class="sxs-lookup"><span data-stu-id="04a75-129">Shows how to retrieve a single attribute of an element, given the attribute name.</span></span>|  
|[<span data-ttu-id="04a75-130">Практическое руководство. Получение значения атрибута (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="04a75-130">How to: Retrieve the Value of an Attribute (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-attribute-linq-to-xml.md)|<span data-ttu-id="04a75-131">Показывает способ получения значений атрибутов.</span><span class="sxs-lookup"><span data-stu-id="04a75-131">Shows how to get the values of attributes.</span></span>|  
|[<span data-ttu-id="04a75-132">Практическое руководство. Извлечение поверхностного значения элемента (C#)</span><span class="sxs-lookup"><span data-stu-id="04a75-132">How to: Retrieve the Shallow Value of an Element (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-the-shallow-value-of-an-element.md)|<span data-ttu-id="04a75-133">Показывает способ получения поверхностного значения элемента.</span><span class="sxs-lookup"><span data-stu-id="04a75-133">Shows how to retrieve the shallow value of an element.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="04a75-134">См. также</span><span class="sxs-lookup"><span data-stu-id="04a75-134">See Also</span></span>  
 <span data-ttu-id="04a75-135">[Методы расширения](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md) </span><span class="sxs-lookup"><span data-stu-id="04a75-135">[Extension Methods](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md) </span></span>  
 [<span data-ttu-id="04a75-136">Руководство по программированию (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="04a75-136">Programming Guide (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/programming-guide-linq-to-xml.md)
