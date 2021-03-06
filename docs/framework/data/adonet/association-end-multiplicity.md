---
title: кратность конечной точки ассоциации
ms.date: 03/30/2017
ms.assetid: 340926ee-aefb-4bef-92cc-453e5251fd03
ms.openlocfilehash: cf9e6b5af0dc6a33af364901c631b4ce66fe0480
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2020
ms.locfileid: "91153512"
---
# <a name="association-end-multiplicity"></a>кратность конечной точки ассоциации

*Кратность окончания ассоциации* определяет количество экземпляров [типа сущности](entity-type.md) , которые могут находиться в одном конце [ассоциации](association-type.md).  
  
 Кратность конечной точки ассоциации может иметь одно из следующих значений.  
  
- «один» (1): показывает, что на конечной точке ассоциации существует ровно один экземпляр типа сущности.  
  
- «ноль или один» (0..1): показывает, что на конечной точке ассоциации существует ноль, один или несколько экземпляров типа сущности.  
  
- Многие ( \* ): указывает, что в конце ассоциации существует ноль, один или несколько экземпляров типа сущности.  
  
 Ассоциация зачастую характеризуется кратностями конечной точки ассоциации. Например, если элементы ассоциации имеют кратность один (1) и многие ( \* ), то Ассоциация называется связью «один ко многим». В следующем примере ассоциация `PublishedBy` является ассоциацией «один-ко-многим» (один издатель публикует много книг, а одна книга публикуется одним издателем). Ассоциация `WrittenBy` является ассоциацией «один-ко-многим» (одна книга может иметь несколько авторов, а один автор может написать несколько книг).  
  
## <a name="example"></a>Пример  

 На приведенной ниже схеме показана концептуальная модель с двумя ассоциациями: `PublishedBy` и `WrittenBy`. Конечные точки ассоциации для ассоциации `PublishedBy` - это типы сущности `Book` и `Publisher`. Кратность `Publisher` конца равна единице (1), а кратность элемента `Book` — many ( \* ).  
  
 ![Пример модели с тремя типами сущностей](./media/association-end-multiplicity/example-model-three-entity-types.gif)  
  
 Entity Framework ADO.NET использует доменный язык (DSL), называемый языком определения концептуальной схемы ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)), для определения концептуальных моделей. Далее язык CSDL определяет ассоциацию `PublishedBy`, которая ранее приводилась в схеме.  
  
 [!code-xml[EDM_Example_Model#AssociationExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#associationexample)]  
  
## <a name="see-also"></a>См. также раздел

- [Основные понятия модели EDM](entity-data-model-key-concepts.md)
- [EDM (модель данных с использованием сущностей)](entity-data-model.md)
