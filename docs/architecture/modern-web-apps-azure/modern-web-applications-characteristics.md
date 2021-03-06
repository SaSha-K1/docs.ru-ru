---
title: Характеристики современных веб-приложений
description: Разработка современных веб-приложений с помощью ASP.NET Core и Azure | Характеристики современных веб-приложений
author: ardalis
ms.author: wiwagn
no-loc:
- Blazor
- WebAssembly
ms.date: 12/01/2020
ms.openlocfilehash: 2a9e55250018352c8019d30a4d615ec39e619e31
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851234"
---
# <a name="characteristics-of-modern-web-applications"></a>Характеристики современных веб-приложений

> "… правильный подход к проектированию позволяет обеспечить экономичную реализацию функций. Этот путь непрост, но он ведет к успеху".  
> _\- Деннис Ритчи (Dennis Ritchie)_

Пользователи предъявляют к современным веб-приложениям максимально высокие требования. Такие веб-приложения должны быть доступны постоянно из любой точки мира практически с любого устройства, независимо от размера его экрана. Веб-приложения должны быть безопасными, гибкими и масштабируемыми, чтобы эффективно справляться с резкими скачками нагрузки. Полнофункциональные пользовательские интерфейсы реализуют все более сложные сценарии с использованием клиентов на основе JavaScript и обеспечивают эффективное взаимодействие через веб-API.

Платформа ASP.NET Core оптимизирована для современных веб-приложений и сценариев размещения в облаке. Благодаря ее модульной структуре приложения используют только те компоненты, которые им фактически необходимы, что позволяет повысить их безопасность и производительность при одновременном снижении требований к ресурсам размещения.

## <a name="reference-application-eshoponweb"></a>Справочное приложение: eShopOnWeb

В этом руководстве показано справочное приложение _eShopOnWeb_, на примере которого демонстрируются некоторые принципы и рекомендации. Это приложение представляет собой простой интернет-магазин, в котором можно просматривать каталог футболок, кружек и других товаров. Это справочное приложение намеренно упрощено для наилучшего понимания.

![eShopOnWeb](./media/image2-1.png)

**Рис. 2-1.** eShopOnWeb

> ### <a name="reference-application"></a>Справочное приложение
>
> - **eShopOnWeb**  
>   <https://github.com/dotnet/eShopOnWeb>

## <a name="cloud-hosted-and-scalable"></a>Размещение в облаке и масштабируемость

Платформа ASP.NET Core оптимизирована для сценариев размещения в облаке (частное, общедоступное или любое другое облако), обеспечивая низкое потребление памяти при высокой пропускной способности. Благодаря минимальной потребности приложений ASP.NET Core в ресурсах вы можете размещать в облаке больше приложений при меньших затратах в рамках модели оплаты по мере использования. Высокая пропускная способность позволяет обслуживать в приложении больше клиентов при тех же затратах аппаратных ресурсов, благодаря чему сокращается потребность в инвестициях в серверы и инфраструктуру размещения.

## <a name="cross-platform"></a>Кроссплатформенные

Благодаря кроссплатформенной поддержке ASP.NET Core может выполняться в Linux, macOS и Windows. Это открывает перед создателями приложений ASP.NET Core множество новых возможностей для разработки и развертывания. Контейнеры Docker на Linux и Windows могут использоваться для размещения приложений ASP.NET Core, что позволяет им использовать преимущества [контейнеров и микрослужб](../microservices/index.md).

## <a name="modular-and-loosely-coupled"></a>Модульность и слабая связанность

Пакеты NuGet широко применяются в .NET Core, а в приложениях ASP.NET Core используется множество предоставляемых NuGet библиотек. Подобная детализация функций позволяет приложениям использовать и развертывать только те функции, которые им фактически необходимы, благодаря чему сокращается объем потребляемых ими ресурсов и размер контактной зоны, в которой присутствуют уязвимости.

Платформа ASP.NET Core также полностью поддерживает [внедрение зависимостей](https://deviq.com/dependency-injection/) на внутреннем уровне и на уровне приложения. Интерфейсы могут иметь множество реализаций, переключение между которыми осуществляется по мере необходимости. Внедрение зависимостей позволяет реализовать слабое связывание приложений с такими интерфейсами вместо конкретных реализаций, благодаря чему упрощается их расширение, обслуживание и тестирование.

## <a name="easily-tested-with-automated-tests"></a>Простота проверки с использованием автоматических тестов

Приложения ASP.NET Core являются слабо связанными, а также поддерживают модульное тестирование и внедрение зависимостей, благодаря чему упрощается подход к переключению инфраструктур и созданию фиктивных реализаций для тестирования. В состав платформы ASP.NET Core также входит компонент TestServer, который можно использовать для размещения приложений в памяти. Функциональные тесты могут выполнять запросы к этому размещаемому в памяти серверу, используя полный стек приложения (в том числе ПО промежуточного слоя, маршрутизацию, привязку модели фильтры и т. д.) и получая ответы. Все это выполняется за минимальное время, которое затрачивается при размещении приложения на реальном сервере и выполнении запросов через сетевой уровень. Эти тесты для API просты в разработке и крайне полезны, что играет все более важную роль для современных веб-приложений.

## <a name="traditional-and-spa-behaviors-supported"></a>Поддержка поведения традиционных и одностраничных приложений

Традиционные веб-приложения реализуют лишь малую часть функций на стороне клиента и размещают все возможности навигации, обработки запросов и обновления на сервере. Соответственно, каждая выполняемая пользователем новая операция должна преобразовываться в веб-запрос, что влечет за собой полную перезагрузку страницы в браузере конечного пользователя. Такой подход обычно применяется в классических платформах MVC (модель-представление-контроллер), где каждый новый запрос соответствует новому действию контроллера, который, в свою очередь, работает с моделью и возвращает представление. Отдельные операции на конкретной странице могут быть оптимизированы с использованием функций AJAX (асинхронный JavaScript и XML), однако общая архитектура приложения использует множество различных представлений MVC и конечных точек URL-адресов. Кроме того, ASP.NET Core MVC также поддерживает Razor Pages — более простой способ организации страниц в стиле MVC.

В отличие от них, одностраничные приложения используют минимум динамически создаваемых на стороне сервера загрузок страниц или не используют их вовсе. Многие одностраничные приложения инициализируются с использованием статического HTML-файла, который загружает необходимые для запуска и выполнения приложения библиотеки JavaScript. Такие приложения могут активно использовать веб-API для обработки данных и реализовывать гораздо более функциональный пользовательский интерфейс.

Во многих приложениях эффективно сочетаются возможности традиционных (обычно для работы с содержимым) и одностраничных (для реализации интерактивного поведения) веб-приложений. Платформа ASP.NET Core обеспечивает одновременную поддержку MVC (представления или страницы) и веб-API в одном приложении с использованием единого набора средств и базовых библиотек платформы.

## <a name="simple-development-and-deployment"></a>Простота разработки и развертывания

Приложения ASP.NET Core можно создавать как с использованием простых текстовых редакторов и интерфейсов командной строки, так и с помощью полнофункциональных сред разработки, например Visual Studio. Одноуровневые приложения обычно развертываются в одной конечной точке. Развертывание можно легко автоматизировать в рамках конвейера непрерывной интеграции и непрерывной поставки. В дополнение к традиционным средствам непрерывной интеграции и непрерывной поставки в Microsoft Azure предусмотрена встроенная поддержка репозиториев Git и автоматическое развертывание обновлений для указанных ветвей или тегов Git. Azure DevOps предоставляет полнофункциональный конвейер сборки и развертывания CI/CD, а GitHub Actions предоставляет другой вариант для размещенных в нем проектов.

## <a name="traditional-aspnet-and-web-forms"></a>Традиционные модели ASP.NET и веб-формы

Традиционная платформа ASP.NET 4.x дополняет возможности ASP.NET Core и по-прежнему служит надежным и эффективным инструментом для построения веб-приложений. Платформа ASP.NET поддерживает модели разработки MVC и веб-API, а также веб-формы, благодаря чему она оптимально подходит для разработки полнофункциональных приложений на основе страниц и реализует развернутую экосистему сторонних компонентов. Платформа Microsoft Azure хорошо знакома многим разработчикам и на протяжении многих лет обеспечивает поддержку приложений ASP.NET 4.x.

## Blazor

Blazor входит в состав ASP.NET Core 3.0 и более поздних версий. Он предоставляет новый механизм для создания многофункциональных интерактивных клиентских веб-приложений с помощью Razor, C# и ASP.NET Core. Он предлагает еще одно решение, которое следует учитывать при разработке современных веб-приложений. Существует две версии Blazor: на стороне сервера и на стороне клиента.

Функция Blazor на стороне сервера выпущена в 2019 г. с ASP.NET Core 3.0. Как следует из названия, функция работает на сервере, преобразуя изменения в клиентском документе для отображения в браузер по сети. Blazor на стороне сервера обеспечивает широкие возможности для взаимодействия с пользователем, не требуя наличия JavaScript на стороне клиента и отдельной загрузки страниц для каждого взаимодействия с клиентской страницей. Изменения на загруженной странице запрашиваются и обрабатываются сервером, а затем отправляются обратно клиенту с помощью SignalR.

Функция Blazor на стороне клиента, выпущенная в мае 2020 года, устраняет необходимость в отрисовке изменений на сервере. Вместо этого для запуска кода .NET в клиенте функция использует WebAssembly. Клиент по-прежнему сможет выполнять вызовы API на сервер, если необходимо запросить данные, но все поведение на стороне клиента выполняется в клиенте через WebAssembly, которая уже поддерживается всеми основными браузерами и является простой библиотекой JavaScript.

> ### <a name="references--modern-web-applications"></a>Ссылки — современные веб-приложения
>
> - **Введение в ASP.NET Core**  
>   <https://docs.microsoft.com/aspnet/core/>
> - **Тестирование на платформе ASP.NET Core**  
>   <https://docs.microsoft.com/aspnet/core/testing/>
> - **Начало работы с Blazor**  
>   <https://blazor.net/docs/get-started.html>

>[!div class="step-by-step"]
>[Назад](index.md)
>[Вперед](choose-between-traditional-web-and-single-page-apps.md)
