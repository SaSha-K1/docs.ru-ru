---
title: Рабочий процесс DevOps для приложения Docker с использованием средств Майкрософт
description: Рабочий процесс "Жизненный цикл контейнерного приложения Docker на основе платформы и средств Майкрософт" с использованием средств Майкрософт
ms.date: 01/06/2021
ms.openlocfilehash: 7f2d380dec046804772ea7d13e764ab6f3224c12
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970158"
---
# <a name="docker-application-devops-workflow-with-microsoft-tools"></a>Рабочий процесс DevOps для приложения Docker с использованием средств Майкрософт

*Microsoft Visual Studio, Azure DevOps Services, Team Foundation Server и Azure Monitor формируют комплексную экосистему для разработки и выполнения ИТ-операций, которые предоставляют командам средства для управления проектами и быстрого создания, тестирования и развертывания контейнерных приложений.*

С помощью Visual Studio и Azure DevOps Services в облаке и Team Foundation Server в локальной среде команды разработчиков могут эффективно создавать, тестировать и выпускать контейнерные приложения, предназначенные для работы на Windows или Linux.

Средства Майкрософт позволяют автоматизировать конвейер для конкретных реализаций контейнерных приложений (Docker, .NET или любое сочетание других платформ), начиная от глобальных сборок, непрерывной интеграции (CI) и тестов в Azure DevOps Services или Team Foundation Server и заканчивая непрерывным развертыванием (CD) в средах Docker (среда разработки, промежуточное хранение и рабочая среда). Они также позволяют передавать аналитические сведения о службах команде разработчиков через Azure Monitor. Каждая фиксация кода может стать отправной точкой для сборки (CI) и автоматического развертывания служб в определенных контейнерных средах (CD).

С помощью шаблонов в Microsoft Azure разработчики и тест-инженеры могут легко и быстро подготавливать среды разработки и тестирования на базе Docker.

Многозадачность бизнеса и потребности в масштабируемости приводят к неуклонному усложнению процесса разработки контейнерных приложений. Хорошим примером такой сложности являются приложения на основе архитектур микрослужб. Для достижения успеха в таких условиях проект должен автоматизировать весь жизненный цикл — не только сборку и развертывание, но и управление версиями, и сбор данных телеметрии. Azure DevOps Services и Azure предоставляют следующие возможности:

- Управление исходным кодом Azure DevOps Services или Team Foundation Server (на основе Git или системы управления версиями Team Foundation), планирование гибких методик разработки ПО (поддерживаются практики Agile, Scrum и CMMI), непрерывная интеграция, управление выпусками и другие средства для Agile-команд.

- Azure DevOps Services и Team Foundation Server предлагают мощную и развивающуюся экосистему собственных и сторонних расширений для быстрого создания конвейера сборки, тестирования, доставки и управления выпусками для микрослужб.

- Выполнение автоматических тестов в рамках конвейера сборки в Azure DevOps Services.

- Azure DevOps Services может укрепить жизненный цикл DevOps за счет доставки в различные среды (не только в рабочие), например в тестовые, включая A/B-тестирование, [начальные выпуски](https://martinfowler.com/bliki/CanaryRelease.html) и т. д.

- Организации могут легко создавать контейнеры Docker из частных образов, хранящихся в реестре контейнеров Azure вместе с любыми зависимостями от компонентов Azure (данные, PaaS и т. д.), используя шаблоны Azure Resource Manager и хорошо знакомые инструменты.

>[!div class="step-by-step"]
>[Назад](../design-develop-containerized-apps/build-aspnet-core-applications-linux-containers-aks-kubernetes.md)
>[Вперед](docker-application-outer-loop-devops-workflow.md)
