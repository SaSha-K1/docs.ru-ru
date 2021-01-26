---
title: Выпуски, исправления и поддержка .NET
description: Сведения о выпусках, исправлениях и поддержке .NET 5 (включая .NET Core) и более поздних версий.
ms.date: 10/07/2020
ms.topic: overview
ms.author: tdykstra
author: tdykstra
ms.openlocfilehash: 896b88cbf1f7f31d2d26d69ec7d219da6b27ceff
ms.sourcegitcommit: 6d1ae17e60384f3b5953ca7b45ac859ec6d4c3a0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/20/2020
ms.locfileid: "97866397"
---
# <a name="releases-and-support-for-net-core-and-net-5"></a>Выпуски и поддержка .NET Core и .NET 5

Корпорация Майкрософт предоставляет основные выпуски, дополнительные выпуски и сервисные обновления (исправления) для .NET 5.0 (и .NET Core) и более поздних версий. В этой статье описываются типы выпусков, сервисные обновления, диапазоны функций пакета SDK, периоды поддержки и варианты поддержки.

## <a name="release-types"></a>Типы выпусков

Сведения о типе каждого выпуска закодированы в номере версии в формате *основной.дополнительный.исправление*.

Пример:

* .NET Core 3.0 и NET 5.0 являются основными выпусками.
* .NET Core 3.1 — это первый дополнительный выпуск после основного выпуска .NET Core 3.0.
* .NET Core 3.1.7 — это седьмое исправление для .NET Core 3.1.

### <a name="major-releases"></a>Основные выпуски

Основные выпуски включают новые функции, контактные зоны нового общедоступного API и исправления ошибок. К примерам относятся .NET Core 3.0 и .NET 5.0.  Ввиду характера изменений эти выпуски должны включать критически важные изменения. Основные выпуски устанавливаются параллельно с предыдущими основными выпусками.

### <a name="minor-releases"></a>Дополнительные выпуски

Дополнительные выпуски также включают новые функции, контактные зоны общедоступных API и исправления ошибок, а также могут включать критически важные изменения. К примерам относятся .NET Core 2.1 и .NET Core 3.1. Разница между этими и основными выпусками заключается в том, что важность изменений ниже. Важность обновления приложения с .NET Core 3.0 до 3.1 ниже важности перехода на следующую версию. Дополнительные выпуски устанавливаются параллельно с предыдущими дополнительными выпусками.

### <a name="servicing-updates"></a>Сервисные обновления

Сервисные обновления (исправления) выпускаются почти каждый месяц, и эти обновления включают исправления ошибок в системе безопасности, а также исправления, не связанные с безопасностью. Например, .NET Core 3.1.8 является восьмым обновлением для .NET Core 3.1. Когда эти обновления включают исправления для системы безопасности, они выпускаются в "день установки исправлений", который всегда приходится на второй вторник месяца. Сервисные обновления должны обеспечивать совместимость. Начиная с .NET Core 3.1 сервисные обновления — это обновления, которые удаляют предыдущее обновление. Например, последнее сервисное обновление для 3.1 после успешной установки удаляет предыдущее обновление 3.1.

### <a name="feature-bands-sdk-only"></a>Пакеты функций (только для пакетов SDK)

Управление версиями для пакетов SDK для .NET работает немного иначе, чем для среды выполнения .NET. Для обеспечения соответствия новым выпускам Visual Studio обновления пакета SDK для .NET иногда содержат новые функции или новые версии таких компонентов, как MSBuild и NuGet. Эти новые функции или компоненты могут быть несовместимы с версиями, поставляемыми в предыдущих обновлениях пакета SDK для той же основной или дополнительной версии.

Для различения таких обновлений пакет SDK для .NET использует концепцию пакетов функций. Например, первым пакетом SDK для .NET Core 3.1 был 3.1.100. Этот выпуск соответствует *пакету функций* 3.1.1xx. Пакеты функций определяют сотни в обозначении исправления в номере версии (три последних цифры). Например, в версиях 3.1.101 и 3.1.201 пакеты функций различаются, а в версиях 3.1.101 и 3.1.199 они одинаковы. При установке пакета SDK для .NET Core 3.1.101 пакет SDK для .NET Core 3.1.100, если он есть на компьютере, удаляется. Когда на тот же компьютер устанавливается пакет SDK для .NET Core 3.1.200, пакет SDK для .NET Core 3.1.101 не удаляется.

### <a name="runtime-roll-forward-and-compatibility"></a>Накат и совместимость среды выполнения

Основные и дополнительные обновления устанавливаются параллельно с предыдущими версиями. Приложение, созданное для конкретной *основной.дополнительной* версии, по-прежнему будет использовать эту целевую среду выполнения, даже если установлена более новая версия. Приложение не выполняет автоматический накат для использования более новой *основной.дополнительной* версии среды выполнения, если только вы не выберете это поведение. Приложение, разработанное для .NET Core 3.0, не запускается автоматически с .NET Core 3.1. Перед развертыванием в рабочей среде рекомендуется перестроить приложение и выполнить тестирование на соответствие более новой основной или дополнительной версии среды выполнения. Дополнительные сведения см. в статьях [Накат платформозависимых приложений](versions/selection.md#framework-dependent-apps-roll-forward) и [Обновление версии среды выполнения автономного развертывания](deploying/runtime-patch-selection.md).

Сервисные обновления обрабатываются иначе, чем основные и дополнительные выпуски. Приложение, созданное для платформы .NET Core 3.1, по умолчанию выполняется в среде выполнения 3.1.0. При установке сервисного обновления оно автоматически выполняет накат, чтобы использовать более новую среду выполнения 3.1.1. Это поведение используется по умолчанию, поскольку требуется, чтобы исправления для системы безопасности использовались сразу после установки без каких-либо других действий. Можно отказаться от такого поведения наката по умолчанию.

## <a name="net-core-and-net-5-version-lifecycles"></a>Жизненные циклы версий .NET Core и .NET 5

.NET Core, а также .NET 5 и более поздних версий применяют [современный жизненный цикл](/lifecycle/policies/modern), а не [фиксированный жизненный цикл](/lifecycle/policies/fixed), который использовался для выпусков .NET Framework. Продукты с фиксированным жизненным циклом предоставляют постоянный фиксированный период поддержки, например 5 лет основной поддержки и еще 5 лет расширенной поддержки. Основная поддержка включает в себя исправления для системы безопасности и исправления, не связанные с безопасностью, а в рамках расширенной поддержки предоставляются только исправления для системы безопасности. Модель поддержки продуктов, которые используют современный жизненный цикл, более ориентирована на обслуживание, с более короткими периодами поддержки и более частыми выпусками.

### <a name="release-tracks"></a>Программы выпуска

Существует две программы поддержки для выпусков:

* *Текущие* выпуски

  Эти версии поддерживаются до 3 месяцев после выпуска следующей основной или дополнительной версии.

  Пример

  * .NET Core 3.0 предоставлена в сентябре 2019 г., после чего в декабре 2019 г. была выпущена версия .NET Core 3.1.
  * Поддержка .NET Core 3.0 закончилась в марте 2020 г., через 3 месяца после выпуска версии 3.1.

* Выпуски с *долгосрочным предоставлением поддержки* (LTS)

  Эти версии поддерживаются не менее 3 лет или 1 год после следующего выпуска LTS, если дата будет позже.

  Пример

  * Версия .NET Core 2.1 была выпущена в мае 2018 г., а в августе 2018 г. она была признана выпуском LTS.
  * .NET Core 3.1 был следующим выпуском LTS, выпущенным в декабре 2019 г.
  * Поскольку август 2021 г. (3 года) позже, чем декабрь 2020 г. (один год после выпуска 3.1), поддержка .NET Core 2.1 продлевается до августа 2021 г.

Выпуски LTS и текущие выпуски чередуются, поэтому более ранний выпуск может поддерживаться дольше, чем более поздний выпуск. Например, .NET Core 2.1 — это выпуск LTS с поддержкой до августа 2021 г. Выпуск 3.0 был предоставлен почти на год позже, но его поддержка была прекращена раньше, в декабре 2019 г.

Сервисные обновления поставляются ежемесячно и включают как исправления для системы безопасности, так и исправления, не связанные с безопасностью (надежность, совместимость и стабильность). Сервисные обновления поддерживаются, пока не будет выпущено следующее сервисное обновление. Для сервисных обновлений характерен накат среды выполнения. Это означает, что приложения по умолчанию выполняются с последней установленной версией сервисного обновления для среды выполнения.

## <a name="how-to-choose-a-release"></a>Выбор выпуска

Если вы создаете службу и предполагаете, что регулярно будете обновлять ее, то лучшим вариантом для поддержания новейших возможностей, предлагаемых .NET, может оказаться текущий выпуск, такой как .NET 5.0.

Если вы создаете клиентское приложение, которое будет распространяться пользователям, стабильность может оказаться важнее, чем доступ к новейшим функциям. Может потребоваться поддержка приложения в течение определенного периода времени, по истечении которого пользователь может выполнить обновление до следующей версии приложения. В этом случае подходит выпуск LTS, такой как .NET Core 3.1.

### <a name="servicing-updates"></a>Сервисные обновления

Сервисные обновления .NET поддерживаются, пока не будет выпущено следующее сервисное обновление. Периодичность выпуска — ежемесячно.

Необходимо регулярно устанавливать сервисные обновления, чтобы гарантировать, что ваши приложения защищены и находятся в поддерживаемом состоянии. Например, если последним сервисным обновлением для .NET Core 3.1 является 3.1.8, а мы поставляем 3.1.9, то 3.1.8 больше не является последним выпуском. Поддерживаемый уровень обслуживания для 3.1 будет 3.1.9.

Сведения об актуальных сервисных обновлениях для каждой основной и дополнительной версий см. на [странице загрузки .NET](https://dotnet.microsoft.com/download/dotnet-core).

## <a name="end-of-support"></a>Дата окончания поддержки

Дата окончания поддержки — это дата, после которой корпорация Майкрософт больше не предоставляет исправления, обновления или техническую поддержку для версии продукта. До этой даты следует перейти на использование поддерживаемой версии. Версии, которые не поддерживаются, больше не получают обновления для системы безопасности, защищающие приложения и данные.

## <a name="supported-operating-systems"></a>Поддерживаемые операционные системы

.NET 5 (и .NET Core) и более поздние версии могут работать в различных операционных системах. Каждая из этих операционных систем имеет жизненный цикл, определенный ее спонсорской организацией (например, Майкрософт, Red Hat или Apple). Эти расписания жизненных циклов следует учитывать при добавлении и удалении поддержки версий операционной системы.

Если версия операционной системы выходит за пределы поддержки, мы прекращаем тестирование этой версии и предоставляем поддержку этой версии. Для получения поддержки пользователям необходимо перейти на поддерживаемую версию операционной системы.

Дополнительные сведения см. в статье [Политика поддержки операционных систем .NET](https://github.com/dotnet/core/blob/master/os-lifecycle-policy.md).

## <a name="get-support"></a>Техническая поддержка

У вас есть возможность выбрать между технической поддержкой Майкрософт и поддержкой сообщества.

### <a name="microsoft-support"></a>Служба поддержки Майкрософт

Для получения технической поддержки [обратитесь к специалисту службы технической поддержки Майкрософт](https://support.microsoft.com/supportforbusiness/productselection/?sapid=4fd4947b-15ea-ce01-080f-97f2ca3c76e8).

Чтобы получить поддержку, требуется поддерживаемый уровень обслуживания (последнее доступное сервисное обновление). Если в системе установлена версия 3.1 и выпущено сервисное обновление 3.1.8, то для начала необходимо установить версию 3.1.8.

### <a name="community-support"></a>Поддержка сообщества

Сведения о поддержке сообщества см. на [странице сообщества](https://dotnet.microsoft.com/platform/community).

## <a name="see-also"></a>См. также раздел

Дополнительные сведения, включая поддерживаемые диапазоны дат для каждой версии .NET Core и .NET 5, см. в [политике поддержки](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).