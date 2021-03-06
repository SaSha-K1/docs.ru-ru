---
title: Службы WCF Data Services 4.5
description: Сведения о службы данных WCF, компоненте платформа .NET Framework, который поддерживает службы для предоставления и использования данных с помощью семантики RESTFUL.
ms.date: 03/30/2017
helpviewer_keywords:
- Astoria
- WCF Data Services, getting started
ms.assetid: 73d2bec3-7c92-4110-b905-11bb0462357a
ms.openlocfilehash: 2d3da2ca9cd958fc70d3b91362dde71d68dc9d8a
ms.sourcegitcommit: 8299abfbd5c49b596d61f1e4d09bc6b8ba055b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "98898764"
---
# <a name="wcf-data-services-45"></a>Службы WCF Data Services 4.5

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

## <a name="overview"></a>Обзор

Службы данных WCF (прежнее название — "службы данных ADO.NET") — это компонент платформа .NET Framework, который позволяет создавать службы, использующие Open Data Protocol (OData) для предоставления и использования данных в Интернете или интрасети с помощью семантики [передачи состояния представления (остальное)](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm). OData предоставляет доступ к данным в виде ресурсов, которые адресуются по URI. Доступ и изменение данных производится с помощью таких стандартных команд HTTP, как GET, PUT, POST и DELETE. OData использует соглашения об отношениях отношений сущностей [EDM](../adonet/entity-data-model.md) для предоставления ресурсов в виде наборов сущностей, связанных ассоциациями.

Службы данных WCF использует протокол OData для адресации и обновления ресурсов. Таким образом, доступ к этим службам можно получить с любого клиента, поддерживающего OData. OData позволяет запрашивать и записывать данные в ресурсы с помощью хорошо известных форматов передачи: Atom, набора стандартов для обмена и обновления данных в формате XML, а также нотация объектов JavaScript (JSON), основанный на тексте формат обмена данными, широко применяемый в приложениях AJAX.

Службы данных WCF может предоставлять данные, происходящие из различных источников, в качестве каналов OData. Средства Visual Studio облегчают создание службы на основе OData с помощью модели данных ADO.NET Entity Framework. Можно также создавать веб-каналы OData на основе классов среды CLR и даже данных с поздним связыванием или нетипизированными данными.

Службы данных WCF также включает набор клиентских библиотек, один для общих платформа .NET Framework клиентских приложений и другой специально для приложений на основе Silverlight. Эти клиентские библиотеки предоставляют возможности объектно ориентированного программирования для доступа к каналу OData из таких платформ, как .NET Framework и Silverlight.

## <a name="where-should-i-start"></a>Подготовка к изучению темы

В зависимости от ваших интересов рекомендуется приступить к работе с службы данных WCF в одном из следующих разделов.

Необходимо перейти непосредственно к…

- [Краткое руководство](quickstart-wcf-data-services.md)

- [Начало работы](getting-started-with-wcf-data-services.md)

Просто покажите мне код...

- [Краткое руководство](quickstart-wcf-data-services.md)

- [Практическое руководство. Выполнение запросов к службе данных](how-to-execute-data-service-queries-wcf-data-services.md)

- [Практическое руководство. Привязка данных к элементам Windows Presentation Foundation](bind-data-to-wpf-elements-wcf-data-services.md)

Я хочу узнать больше о OData...

- [Технический документ. Введение в OData](https://download.microsoft.com/download/E/5/A/E5A59052-EE48-4D64-897B-5F7C608165B8/IntroducingOData.pdf)
- [Веб-сайт Open Data Protocol](https://www.odata.org/)
- [OData SDK](https://www.odata.org/ecosystem/)

Я хочу просмотреть полный пример...

- [Краткое руководство по службы данных WCF](https://github.com/microsoftarchive/msdn-code-gallery-community-s-z/tree/master/WCF%20Data%20Services%20Quickstart%20(OData%20Service%20and%20WPF%20Client))
- [Пакет SDK OData — пример кода](https://www.odata.org/ecosystem/#sdk)

Как происходит интеграция со средствами Visual Studio

- [Создание библиотеки клиентов службы данных](generating-the-data-service-client-library-wcf-data-services.md)

- [Создание службы данных](creating-the-data-service.md)

- [Поставщик Entity Framework](entity-framework-provider-wcf-data-services.md)

Что можно сделать?

- [Обзор](wcf-data-services-overview.md)

- [Сценарии приложений](application-scenarios-wcf-data-services.md)

Я хочу использовать LINQ...

- [Выполнение запросов к службе данных](querying-the-data-service-wcf-data-services.md)

- [Рекомендации по LINQ](linq-considerations-wcf-data-services.md)

- [Практическое руководство. Выполнение запросов к службе данных](how-to-execute-data-service-queries-wcf-data-services.md)

Мне по-прежнему нужны дополнительные сведения...

- [Блог группы служб WCF Data Services](/archive/blogs/astoriateam/)

- [Ресурсы](wcf-data-services-resources.md)

## <a name="in-this-section"></a>В этом разделе

[Обзор](wcf-data-services-overview.md)

Содержит общие сведения о функциях и функциях, доступных в службы данных WCF.

[Новые возможности службы данных WCF 5,0](/previous-versions/dotnet/wcf-data-services/ee373845(v=vs.103))

Описание новых функциональных возможностей службы данных WCF и поддержки новых функций OData.

[Начало работы](getting-started-with-wcf-data-services.md)

Описывает, как предоставлять и использовать каналы OData с помощью службы данных WCF.

[Определение служб данных WCF](defining-wcf-data-services.md)

Описывает создание и настройку службы данных, предоставляющей доступ к каналам OData.

[Библиотека клиентов служб данных WCF](wcf-data-services-client-library.md)

Описывает использование клиентских библиотек для использования каналов OData из клиентского приложения платформа .NET Framework.

## <a name="see-also"></a>См. также

- [Передача состояния представления (REST)](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
