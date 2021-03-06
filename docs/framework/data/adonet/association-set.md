---
title: набор ассоциаций
ms.date: 03/30/2017
ms.assetid: a65247b6-ce59-44ea-974c-14ae20a7995f
ms.openlocfilehash: 58d8794a21cc37ab84386c820b192fb29946095c
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2020
ms.locfileid: "91153434"
---
# <a name="association-set"></a>набор ассоциаций

*Набор ассоциаций* — это логический контейнер для экземпляров [ассоциаций](association-type.md) того же типа. Набор ассоциаций не является конструктом моделирования данных, то есть не описывает структуру данных или связи. Вместо этого ассоциация обеспечивает конструкт для среды размещения или хранения (например, для среды CLR или базы данных сервера SQL), позволяя группировать экземпляры ассоциаций так, чтобы они были сопоставлены хранилищу данных.  
  
 Набор ассоциаций определяется в [контейнере сущностей](entity-container.md), который является логической группировкой [наборов сущностей](entity-set.md) и наборов ассоциаций.  
  
 Определение набора ассоциаций содержит следующую информацию.  
  
- Имя набора ассоциаций. (обязательно)  
  
- Ассоциация, экземпляры которой будут являться содержимым. (обязательно)  
  
- Два [конца набора ассоциаций](association-set-end.md).  
  
## <a name="example"></a>Пример  

 На приведенной ниже схеме показана концептуальная модель с двумя ассоциациями: `PublishedBy` и `WrittenBy`. Информации о наборах ассоциаций не содержится в схеме, однако на следующей схеме показан пример наборов ассоциаций и наборов сущностей на основе этой модели.  
  
 ![Пример модели с тремя типами сущностей](./media/association-set/example-model-three-entity-types.gif)  
  
 В следующем примере показан набор ассоциаций (`PublishedBy`) и два набора сущностей (`Books` и `Publishers`) на основе приведенной выше концептуальной модели. Бизнес-аналитика в `Books` наборе сущностей представляет экземпляр `Book` типа сущности во время выполнения. Аналогичным образом PJ представляет `Publisher` экземпляр в `Publishers` наборе сущностей. Бипж представляет экземпляр `PublishedBy` ассоциации в `PublishedBy` наборе ассоциаций.  
  
 ![Снимок экрана, на котором показан пример набора.](./media/association-set/sets-example-association.gif)  
  
 [Entity Framework ADO.NET](./ef/index.md) использует доменный язык (DSL), называемый языком определения концептуальной схемы ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)), для определения концептуальных моделей. Далее на языке CSDL определяется контейнер сущностей с одним набором ассоциаций для каждой ассоциации на приведенной выше схеме. Обратите внимание, что имя и ассоциация для каждого набора ассоциаций определены при помощи атрибутов XML.  
  
 [!code-xml[EDM_Example_Model#EntityContainerExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entitycontainerexample)]  
  
 Можно определить несколько наборов ассоциаций для каждой ассоциации, если ни один из двух наборов связей не имеет общего доступа к [концу набора ассоциаций](association-set-end.md). Далее на языке CSDL определяется контейнер сущностей с двумя наборами ассоциаций для ассоциации `WrittenBy`: Обратите внимание, что несколько наборов сущностей были определены для типов сущностей `Book` и `Author` и что наборы ассоциаций не имеют одной и той же конечной точки ассоциации.  
  
 [!code-xml[EDM_Example_Model#MultipleAssociationSets](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books3.edmx#multipleassociationsets)]  
  
## <a name="see-also"></a>См. также раздел

- [Основные понятия модели EDM](entity-data-model-key-concepts.md)
- [EDM (модель данных с использованием сущностей)](entity-data-model.md)
- [свойство внешнего ключа](foreign-key-property.md)
