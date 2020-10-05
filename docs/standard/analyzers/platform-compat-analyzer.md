---
title: Анализатор совместимости платформ
description: Анализатор Roslyn, который помогает обнаруживать проблемы совместимости платформ в кросс-платформенных приложениях и библиотеках.
author: buyaa-n
ms.date: 09/17/2020
ms.openlocfilehash: 4e842e5bbe90dd5006d9b27d0365f908b6441997
ms.sourcegitcommit: 1274a1a4a4c7e2eaf56b38da76ef7cec789726ef
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2020
ms.locfileid: "91406591"
---
# <a name="platform-compatibility-analyzer"></a><span data-ttu-id="146de-103">Анализатор совместимости платформ</span><span class="sxs-lookup"><span data-stu-id="146de-103">Platform compatibility analyzer</span></span>

<span data-ttu-id="146de-104">Вероятно, вы слышали девиз "единой платформы .NET" — единая, унифицированная платформа для создания приложений любого типа.</span><span class="sxs-lookup"><span data-stu-id="146de-104">You've probably heard the motto of "One .NET": a single, unified platform for building any type of application.</span></span> <span data-ttu-id="146de-105">Пакет SDK .NET 5.0 включает ASP.NET Core, Entity Framework Core, WinForms, WPF, Xamarin и ML.NET. В будущем будет реализована поддержка и других платформ.</span><span class="sxs-lookup"><span data-stu-id="146de-105">The .NET 5.0 SDK includes ASP.NET Core, Entity Framework Core, WinForms, WPF, Xamarin, and ML.NET, and will add support for more platforms over time.</span></span> <span data-ttu-id="146de-106">ПО .NET 5.0 призвано предоставить вам возможности для работы с любыми вариантами .NET, но не пытается полностью абстрагировать базовую операционную систему (ОС).</span><span class="sxs-lookup"><span data-stu-id="146de-106">.NET 5.0 strives to provide an experience where you don't have to reason about the different flavors of .NET, but doesn't attempt to fully abstract away the underlying operating system (OS).</span></span> <span data-ttu-id="146de-107">Вы сможете и далее вызывать API, зависящие от платформы, например привязки P/Invokes, WinRT или привязки Xamarin для iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="146de-107">You'll continue to be able to call platform-specific APIs, for example, P/Invokes, WinRT, or the Xamarin bindings for iOS and Android.</span></span>

<span data-ttu-id="146de-108">Но использование в компоненте API, зависящих от платформы, означает, что код не будет работать на всех платформах.</span><span class="sxs-lookup"><span data-stu-id="146de-108">But using platform-specific APIs on a component means the code no longer works across all platforms.</span></span> <span data-ttu-id="146de-109">Нам требовался способ для выявления таких проблем на этапе разработки, чтобы разработчики могли получать диагностические сведения при неосмотрительном использовании зависящих от платформы API.</span><span class="sxs-lookup"><span data-stu-id="146de-109">We needed a way to detect this at design time so developers get diagnostics when they inadvertently use platform-specific APIs.</span></span> <span data-ttu-id="146de-110">Для этого .NET 5.0 в представлен [анализатор совместимости платформ](/visualstudio/code-quality/ca1416) и дополнительные API, которые позволяют разработчикам идентифицировать и при необходимости использовать API, зависящие от платформы.</span><span class="sxs-lookup"><span data-stu-id="146de-110">To achieve this goal, .NET 5.0 introduces the [platform compatibility analyzer](/visualstudio/code-quality/ca1416) and complementary APIs to help developers identify and use platform-specific APIs where appropriate.</span></span>
<span data-ttu-id="146de-111">Новые API включают следующее:</span><span class="sxs-lookup"><span data-stu-id="146de-111">The new APIs include:</span></span>

- <span data-ttu-id="146de-112"><xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> для аннотации API как зависящих от платформы и <xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> для аннотации API как неподдерживаемых в определенной ОС.</span><span class="sxs-lookup"><span data-stu-id="146de-112"><xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> to annotate APIs as being platform-specific and <xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> to annotate APIs as being unsupported on a particular OS.</span></span> <span data-ttu-id="146de-113">При необходимости эти атрибуты могут включать номер версии и уже применяться к некоторым API, зависящим от платформы, в основных библиотеках .NET.</span><span class="sxs-lookup"><span data-stu-id="146de-113">These attributes can optionally include the version number, and have already been applied to some platform-specific APIs in the core .NET libraries.</span></span>
- <span data-ttu-id="146de-114">Статические методы `Is<Platform>()` и `Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)` в классе <xref:System.OperatingSystem?displayProperty=nameWithType> для безопасного вызова API, зависящих от платформы.</span><span class="sxs-lookup"><span data-stu-id="146de-114">`Is<Platform>()` and `Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)` static methods in the <xref:System.OperatingSystem?displayProperty=nameWithType> class for safely calling platform-specific APIs.</span></span> <span data-ttu-id="146de-115">Например, <xref:System.OperatingSystem.IsWindows?displayProperty=nameWithType> можно использовать для предложения условия вызова к API для Windows, а <xref:System.OperatingSystem.IsWindowsVersionAtLeast%2A?displayProperty=nameWithType>() — для предложения условия вызова к API для Windows с определенной версией.</span><span class="sxs-lookup"><span data-stu-id="146de-115">For example, <xref:System.OperatingSystem.IsWindows?displayProperty=nameWithType> can be used to guard a call to a Windows-specific API, and <xref:System.OperatingSystem.IsWindowsVersionAtLeast%2A?displayProperty=nameWithType>() can be used to guard a versioned Windows-specific API call.</span></span> <span data-ttu-id="146de-116">Подробные сведения о том, как такие методы можно использовать в качестве условий для ссылок на API, зависящие от платформы, см. в [этих примерах](#guard-platform-specific-apis-with-guard-methods).</span><span class="sxs-lookup"><span data-stu-id="146de-116">See these [examples](#guard-platform-specific-apis-with-guard-methods) of how these methods can be used as guards of platform-specific API references.</span></span>

> [!TIP]
> <span data-ttu-id="146de-117">Анализатор совместимости платформ обновляет и заменяет функцию [Обнаружение проблем с межплатформенным взаимодействием](../../standard/analyzers/api-analyzer.md#discover-cross-platform-issues) в [анализаторе API .NET](../../standard/analyzers/api-analyzer.md).</span><span class="sxs-lookup"><span data-stu-id="146de-117">The platform compatibility analyzer upgrades and replaces the [Discovering cross-platform issues](../../standard/analyzers/api-analyzer.md#discover-cross-platform-issues) feature of the [.NET API analyzer](../../standard/analyzers/api-analyzer.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="146de-118">предварительные требования</span><span class="sxs-lookup"><span data-stu-id="146de-118">Prerequisites</span></span>

<span data-ttu-id="146de-119">Анализатор совместимости платформ является одним из анализаторов качества кода Roslyn.</span><span class="sxs-lookup"><span data-stu-id="146de-119">The platform compatibility analyzer is one of the Roslyn code quality analyzers.</span></span> <span data-ttu-id="146de-120">Начиная с .NET 5.0 эти анализаторы входят в состав [пакета SDK .NET](../../fundamentals/productivity/code-analysis.md).</span><span class="sxs-lookup"><span data-stu-id="146de-120">Starting in .NET 5.0, these analyzers are [included with the .NET SDK](../../fundamentals/productivity/code-analysis.md).</span></span> <span data-ttu-id="146de-121">Анализатор совместимости платформ включен по умолчанию только для проектов, ориентированных на `net5.0` или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="146de-121">The platform compatibility analyzer is enabled by default only for projects that target `net5.0` or a later version.</span></span> <span data-ttu-id="146de-122">Но вы можете [включить](/visualstudio/code-quality/ca1416.md#configurability) его для проектов, ориентированных на другие платформы.</span><span class="sxs-lookup"><span data-stu-id="146de-122">However, you can [enable](/visualstudio/code-quality/ca1416.md#configurability) it for projects that target other frameworks.</span></span>

## <a name="how-the-analyzer-determines-platform-dependency"></a><span data-ttu-id="146de-123">Как анализатор определяет зависимость платформы</span><span class="sxs-lookup"><span data-stu-id="146de-123">How the analyzer determines platform dependency</span></span>

- <span data-ttu-id="146de-124">Считается, что **API без атрибутов** работает на **всех платформах ОС**.</span><span class="sxs-lookup"><span data-stu-id="146de-124">An **unattributed API** is considered to work on **all OS platforms**.</span></span>
- <span data-ttu-id="146de-125">Считается, что API с меткой `[SupportedOSPlatform("platform")]` можно переносить только на указанную платформу ОС `platform`.</span><span class="sxs-lookup"><span data-stu-id="146de-125">An API marked with `[SupportedOSPlatform("platform")]` is considered only portable to the specified OS `platform`.</span></span>
  - <span data-ttu-id="146de-126">Этот атрибут может применяться несколько раз для указания **поддержки нескольких платформ** (`[SupportedOSPlatform("windows"), SupportedOSPlatform("Android6.0")]`).</span><span class="sxs-lookup"><span data-stu-id="146de-126">The attribute can be applied multiple times to indicate **multiple platform support** (`[SupportedOSPlatform("windows"), SupportedOSPlatform("Android6.0")]`).</span></span>
  - <span data-ttu-id="146de-127">Анализатор выдаст **предупреждение**, если ссылки на API, зависящие от платформы, не включают надлежащий **контекст платформы**:</span><span class="sxs-lookup"><span data-stu-id="146de-127">The analyzer will produce a **warning** if platform-specific APIs are referenced without a proper **platform context**:</span></span>
    - <span data-ttu-id="146de-128">**Выдает предупреждение**, если проект не ориентирован на поддерживаемую платформу (например, вызов API ориентирован на Windows, а проект — на `<TargetFramework>net5.0-ios14.0</TargetFramework>`).</span><span class="sxs-lookup"><span data-stu-id="146de-128">**Warns** if the project doesn't target the supported platform (for example, a Windows-specific API call and the project targets `<TargetFramework>net5.0-ios14.0</TargetFramework>`).</span></span>
    - <span data-ttu-id="146de-129">**Выдает предупреждение**, если проект ориентирован на несколько платформ (`<TargetFramework>net5.0</TargetFramework>`).</span><span class="sxs-lookup"><span data-stu-id="146de-129">**Warns** if the project is multi-targeted (`<TargetFramework>net5.0</TargetFramework>`).</span></span>
    - <span data-ttu-id="146de-130">**Не выдает предупреждение**, если ссылки на API, зависящий от платформы, присутствуют в проекте, ориентированном на любую из **указанных платформ** (например, вызов API ориентирован на Windows, а проект — на `<TargetFramework>net5.0-windows</TargetFramework>`).</span><span class="sxs-lookup"><span data-stu-id="146de-130">**Doesn't warn** if the platform-specific API is referenced within a project that targets any of the **specified platforms** (for example, for a Windows-specific API call and the project targets `<TargetFramework>net5.0-windows</TargetFramework>`).</span></span>
    - <span data-ttu-id="146de-131">**Не выдает предупреждение**, если для API, зависящего от платформы, предлагается условие соответствующими методами проверки платформы (например, `if(OperatingSystem.IsWindows())`).</span><span class="sxs-lookup"><span data-stu-id="146de-131">**Doesn't warn** if the platform-specific API call is guarded by corresponding platform-check methods (for example, `if(OperatingSystem.IsWindows())`).</span></span>
    - <span data-ttu-id="146de-132">**Не выдает предупреждение**, если ссылки на API, зависящий от платформы, указаны в таком же зависящем от платформы контексте (**место вызова также имеет атрибут** `[SupportedOSPlatform("platform")`).</span><span class="sxs-lookup"><span data-stu-id="146de-132">**Doesn't warn** if the platform-specific API is referenced from the same platform-specific context (**call site also attributed** with `[SupportedOSPlatform("platform")`).</span></span>
- <span data-ttu-id="146de-133">API, помеченный `[UnsupportedOSPlatform("platform")]`, считается неподдерживаемым только на указанной платформе ОС `platform`, но поддерживается на всех других платформах.</span><span class="sxs-lookup"><span data-stu-id="146de-133">An API marked with `[UnsupportedOSPlatform("platform")]` is considered unsupported only on the specified OS `platform` but supported for all other platforms.</span></span>
  - <span data-ttu-id="146de-134">Этот атрибут может применяться несколько раз с разными платформами, например `[UnsupportedOSPlatform("iOS"), UnsupportedOSPlatform("Android6.0")]`.</span><span class="sxs-lookup"><span data-stu-id="146de-134">The attribute can be applied multiple times with different platforms, for example, `[UnsupportedOSPlatform("iOS"), UnsupportedOSPlatform("Android6.0")]`.</span></span>
  - <span data-ttu-id="146de-135">Анализатор выдает **предупреждение** только в том случае, если `platform` действует для места вызова:</span><span class="sxs-lookup"><span data-stu-id="146de-135">The analyzer produces a **warning** only if the `platform` is effective for the call site:</span></span>
    - <span data-ttu-id="146de-136">**Выдает предупреждение**, если проект ориентирован на платформу, которая имеет атрибут неподдерживаемой (например, если API имеет атрибут `[UnsupportedOSPlatform("windows")]`, а место вызова ориентировано на `<TargetFramework>net5.0-windows</TargetFramework>`).</span><span class="sxs-lookup"><span data-stu-id="146de-136">**Warns** if the project targets the platform that's attributed as unsupported (for example, if the API is attributed with `[UnsupportedOSPlatform("windows")]` and the call site targets `<TargetFramework>net5.0-windows</TargetFramework>`).</span></span>
    - <span data-ttu-id="146de-137">**Выдает предупреждение**, если проект ориентирован на несколько платформ, а атрибут `platform` включен в группу элементов [MSBuild `<SupportedPlatform>`](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) или атрибут `platform` вручную включен в группу элементов `MSBuild` \<SupportedPlatform>:</span><span class="sxs-lookup"><span data-stu-id="146de-137">**Warns** if the project is multi-targeted and the `platform` is included in the default [MSBuild `<SupportedPlatform>`](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) items group, or the `platform` is manually included within the `MSBuild` \<SupportedPlatform> items group:</span></span>

      ```XML
      <ItemGroup>
          <SupportedPlatform Include="platform" />
      </ItemGroup>
      ```

    - <span data-ttu-id="146de-138">**Не выдает предупреждение**, если вы выполняете сборку приложения, которое не ориентировано на неподдерживаемую платформу или ориентировано на несколько платформ, и платформа не включена в группу элементов [MSBuild `<SupportedPlatform>`](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="146de-138">**Doesn't warn** if you're building an app that doesn't target the unsupported platform or is multi-targeted and the platform is not included in the default [MSBuild `<SupportedPlatform>`](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) items group.</span></span>
- <span data-ttu-id="146de-139">Экземпляры обоих атрибутов могут быть созданы с номерами версий в составе имени платформы или без них.</span><span class="sxs-lookup"><span data-stu-id="146de-139">Both attributes can be instantiated with or without version numbers as part of the platform name.</span></span>
  - <span data-ttu-id="146de-140">Номера версий имеют формат `major.minor[.build[.revision]]`; `major.minor` — это обязательная часть, а `build` и `revision` — необязательные.</span><span class="sxs-lookup"><span data-stu-id="146de-140">Version numbers are in the format of `major.minor[.build[.revision]]`; `major.minor` is required and the `build` and `revision` parts are optional.</span></span> <span data-ttu-id="146de-141">Например, "Windows7.0" указывает на Windows версии 7.0, но часть "Windows" интерпретируется как Windows 0.0.</span><span class="sxs-lookup"><span data-stu-id="146de-141">For example, "Windows7.0" indicates Windows version 7.0, but "Windows" is interpreted as Windows 0.0.</span></span>

<span data-ttu-id="146de-142">Дополнительные сведения см. в разделе с [примерами работы атрибутов и выдаваемых ими диагностических данных](#examples-of-how-the-attributes-work-and-what-diagnostics-they-produce).</span><span class="sxs-lookup"><span data-stu-id="146de-142">For more information, see [examples of how the attributes work and what diagnostics they cause](#examples-of-how-the-attributes-work-and-what-diagnostics-they-produce).</span></span>

### <a name="advanced-scenarios-for-combining-attributes"></a><span data-ttu-id="146de-143">Расширенные сценарии для сочетания атрибутов</span><span class="sxs-lookup"><span data-stu-id="146de-143">Advanced scenarios for combining attributes</span></span>

- <span data-ttu-id="146de-144">Если задано сочетание атрибутов `[SupportedOSPlatform]` и `[UnsupportedOSPlatform]`, все атрибуты группируются по идентификатору платформы ОС:</span><span class="sxs-lookup"><span data-stu-id="146de-144">If a combination of `[SupportedOSPlatform]` and `[UnsupportedOSPlatform]` attributes are present, all attributes are grouped by OS platform identifier:</span></span>
  - <span data-ttu-id="146de-145">**Список "Только поддерживаемые".**</span><span class="sxs-lookup"><span data-stu-id="146de-145">**Supported only list**.</span></span> <span data-ttu-id="146de-146">Если самая ранняя версия для каждой платформы ОС задана атрибутом `[SupportedOSPlatform]`, API считается таким, который поддерживается только указанными платформами и не поддерживается всеми другими.</span><span class="sxs-lookup"><span data-stu-id="146de-146">If the lowest version for each OS platform is a `[SupportedOSPlatform]` attribute, the API is considered to only be supported by the listed platforms and unsupported by all other platforms.</span></span> <span data-ttu-id="146de-147">Необязательные атрибуты `[UnsupportedOSPlatform]` для каждой платформы могут иметь только более позднюю версию минимально поддерживаемой версии, что обозначает удаление API начиная с указанной версии.</span><span class="sxs-lookup"><span data-stu-id="146de-147">The optional `[UnsupportedOSPlatform]` attributes for each platform can only have higher version of the minimum supported version, which denotes that the API is removed starting from the specified version.</span></span>

    ```csharp
    // The API only supported on Windows 8.0 and later, not supported for all other.
    // The API is removed/unsupported from version 10.0.19041.0.
    [SupportedOSPlatform("windows8.0")]
    [UnsupportedOSPlatform("windows10.0.19041.0")]
    public void ApiSupportedFromWindows80SupportFromCertainVersion();
    ```

  - <span data-ttu-id="146de-148">**Список "Только неподдерживаемые".**</span><span class="sxs-lookup"><span data-stu-id="146de-148">**Unsupported only list**.</span></span> <span data-ttu-id="146de-149">Если самая ранняя версия для каждой платформы ОС задана атрибутом `[UnsupportedOSPlatform]`, API считается таким, который не поддерживается только указанными платформами и поддерживается всеми другими.</span><span class="sxs-lookup"><span data-stu-id="146de-149">If the lowest version for each OS platform is an `[UnsupportedOSPlatform]` attribute, then the API is considered to only be unsupported by the listed platforms and supported by all other platforms.</span></span> <span data-ttu-id="146de-150">Список может включать атрибут `[SupportedOSPlatform]` с такой же платформой, но более поздней версии, что означает поддержку API начиная с такой версии.</span><span class="sxs-lookup"><span data-stu-id="146de-150">The list could have `[SupportedOSPlatform]` attribute with the same platform but a higher version, which denotes that the API is supported starting from that version.</span></span>
  
    ```csharp
    // The API was unsupported on Windows until version 10.0.19041.0.
    // The API is considered supported everywhere else without constraints.
    [UnsupportedOSPlatform("windows")]
    [SupportedOSPlatform("windows10.0.19041.0")]
    public void ApiSupportedFromWindows8UnsupportFromWindows10();
    ```

  - <span data-ttu-id="146de-151">**Список "Несогласованные".**</span><span class="sxs-lookup"><span data-stu-id="146de-151">**Inconsistent list**.</span></span> <span data-ttu-id="146de-152">Если самая ранняя версия для некоторых платформ указана как `[SupportedOSPlatform]`, но для других платформ — как `[UnsupportedOSPlatform]`, она считается несогласованной, что не поддерживается в анализаторе.</span><span class="sxs-lookup"><span data-stu-id="146de-152">If the lowest version for some platforms is `[SupportedOSPlatform]` while it is `[UnsupportedOSPlatform]` for other platforms, is considered inconsistent, which is not supported for the analyzer.</span></span>
  - <span data-ttu-id="146de-153">Если самые ранние версии `[SupportedOSPlatform]` и атрибуты `[UnsupportedOSPlatform]` равны, анализатор считает, что платформа входит в **список только поддерживаемых**.</span><span class="sxs-lookup"><span data-stu-id="146de-153">If the lowest versions of `[SupportedOSPlatform]` and `[UnsupportedOSPlatform]` attributes are equal, the analyzer considers the platform as part of the **Supported only list**.</span></span>
- <span data-ttu-id="146de-154">Атрибуты платформы могут применяться к типам, элементам (методам, полям, свойствам и событиями) и сборкам с разными именами и (или) версиями платформ.</span><span class="sxs-lookup"><span data-stu-id="146de-154">Platform attributes can be applied to types, members (methods, fields, properties, and events) and assemblies with different platform name and / or version.</span></span>
  - <span data-ttu-id="146de-155">Атрибуты, применяемые к целевой платформе `target` верхнего уровня, также применяются ко всем ее элементам и типам.</span><span class="sxs-lookup"><span data-stu-id="146de-155">Attributes applied at the top level `target` affect all of its members and types.</span></span>
  - <span data-ttu-id="146de-156">Атрибуты дочернего уровня применяются только в том случае, если они соответствуют правилу "Дочерние аннотации могут ограничивать поддержку платформ, но не могут расширять ее".</span><span class="sxs-lookup"><span data-stu-id="146de-156">Child level attributes only apply if they adhere to the rule "child annotations can narrow the platforms support, but they cannot widen it".</span></span>
    - <span data-ttu-id="146de-157">Если родительский элемент включает список **Только поддерживаемые**, атрибуты дочернего элемента не смогут добавить поддержку новой платформы, так как это приведет к расширению поддержки родительского элемента. Поддержку новой платформы можно добавить только к самому родительскому элементу.</span><span class="sxs-lookup"><span data-stu-id="146de-157">When parent has **Supported only** list, then child member attributes could not add a new platform support as that would be extending parent support, a new platform support can only added to the parent itself.</span></span> <span data-ttu-id="146de-158">Но он может включать атрибут `Supported` для такой же платформы более поздних версий, поскольку это сужает поддержку.</span><span class="sxs-lookup"><span data-stu-id="146de-158">But it can have `Supported` attribute for same platform with later versions as that will narrow the support.</span></span> <span data-ttu-id="146de-159">Кроме того, он может включать атрибут `Unsupported` с такой же платформой, так как это также сужает поддержку в родительском элементе.</span><span class="sxs-lookup"><span data-stu-id="146de-159">Also it can have `Unsupported` attribute with same platform as that will also narrow parent support.</span></span>
    - <span data-ttu-id="146de-160">Если родительский элемент включает список **Только неподдерживаемые**, атрибуты дочернего элемента могут добавить поддержку новой платформы, так как это сужает поддержку в родительском элементе. Но он не может включать атрибут `Supported` для такой же платформы, которая задана родительским элементом, ведь это приведет к расширению поддержки последнего.</span><span class="sxs-lookup"><span data-stu-id="146de-160">When parent has **Unsupported only** list, then child member attributes could add a new platform support as that would be narrowing parent support, but it cannot have `Supported` attribute for same platform as in the parent, that would extend parent support.</span></span> <span data-ttu-id="146de-161">Поддержку одной платформы можно добавить только на уровне родительского элемента, на котором применяется исходный атрибут `Unsupported`.</span><span class="sxs-lookup"><span data-stu-id="146de-161">Support for the same platform can be added only to parent level where the original `Unsupported` attribute applied.</span></span>
  - <span data-ttu-id="146de-162">Если `[SupportedOSPlatform("platformVersion")]` применяется более одного раза для API с одинаковым именем `platform`, анализатор будет обрабатывать только атрибут с минимальной версией.</span><span class="sxs-lookup"><span data-stu-id="146de-162">If `[SupportedOSPlatform("platformVersion")]` is applied more than once for an API with the same `platform` name only the one with minimum version is considered by the analyzer.</span></span>
  - <span data-ttu-id="146de-163">Если `[UnsupportedOSPlatform("platformVersion")]` применяется более двух раз для API с одинаковым именем `platform`, анализатор будет обрабатывать только два атрибута с минимальными версиями.</span><span class="sxs-lookup"><span data-stu-id="146de-163">If `[UnsupportedOSPlatform("platformVersion")]` is applied more than twice for an API with the same `platform` name, only the two with earliest versions are considered by the analyzer.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="146de-164">Поддержка API, который изначально поддерживался, но больше не поддерживается в поздней версии, не будет возобновлена в еще более поздних версиях.</span><span class="sxs-lookup"><span data-stu-id="146de-164">An API that was supported initially but unsupported (removed) in a later version is not expected to get resupported in an even later version.</span></span>

### <a name="examples-of-how-the-attributes-work-and-what-diagnostics-they-produce"></a><span data-ttu-id="146de-165">Примеры работы атрибутов и выдаваемых ими диагностических данных</span><span class="sxs-lookup"><span data-stu-id="146de-165">Examples of how the attributes work and what diagnostics they produce</span></span>

  ```csharp
  // An API supported only on Windows.
  [SupportedOSPlatform("Windows")]
  public void WindowsOnlyApi() { }

  // an API supported on Windows and Linux.
  [SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("Linux")]
  public void SupportedOnWindowsAndLinuxOnly() { }

  // an API only supported on Windows 8.0 and later, not supported for all other.
  // an API is removed/unsupported from version 10.0.19041.0.
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void ApiSupportedFromWindows8UnsupportFromWindows10() { }

  // an Assembly supported on Windows, the API added from version 10.0.19041.0.
  [assembly: SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("windows10.0.19041.0")]
  public void AssemblySupportedOnWindowsApiSupportedFromWindows10() { }

  public void Caller()
  {
      WindowsOnlyApi(); // warns: 'WindowsOnlyApi' is supported on 'windows'

      // warns: 'SupportedOnWindowsAndLinuxOnly' is supported on 'Windows'
      // warns: 'SupportedOnWindowsAndLinuxOnly' is supported on 'Linux'
      SupportedOnWindowsAndLinuxOnly();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 8.0 and later  
      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // for same platform analyzer only warn for the latest version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  // an API not supported on android but supported on all other.
  [UnsupportedOSPlatform("android")]  
  public void DoesNotWorkOnAndroid() { }

  // an API was unsupported on Windows until version 8.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  public void StartedWindowsSupportFromVersion8() { }

  // an API was unsupported on Windows until version8.0.
  // Then the API is removed (unsupported) from version 10.0.19041.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void StartedWindowsSupportFrom8UnsupportedFrom10() { }

  public void Caller2()
  {
      DoesNotWorkOnAndroid(); // warns 'DoesNotWorkOnAndroid' is unsupported on 'android'

      // warns:'StartedWindowsSupportFromVersion8' is unsupported on 'windows'  
      // warns:'StartedWindowsSupportFromVersion8' is supported on 'windows' 8.0 and later
      StartedWindowsSupportFromVersion8();

      // warns:'StartedWindowsSupportFrom8UnsupportedFrom10' is unsupported on 'windows'  
      // warns:'StartedWindowsSupportFrom8UnsupportedFrom10' is supported on 'windows' 8.0 and later
      // even there were 3 diagnostics found analyzer warn only for the first 2.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }
  ```

## <a name="handle-reported-warnings"></a><span data-ttu-id="146de-166">Обработка выданных предупреждений</span><span class="sxs-lookup"><span data-stu-id="146de-166">Handle reported warnings</span></span>

<span data-ttu-id="146de-167">При анализе таких диагностических данных рекомендуется использовать только соответствующие для конкретной платформы API, зависящие от платформы.</span><span class="sxs-lookup"><span data-stu-id="146de-167">The recommended way to deal with these diagnostics is to make sure you only call platform-specific APIs when running on an appropriate platform.</span></span> <span data-ttu-id="146de-168">Ниже приведены варианты по обработке предупреждений. Выберите оптимальный вариант для своей ситуации:</span><span class="sxs-lookup"><span data-stu-id="146de-168">Following are the options you can use to address the warnings; choose whichever is most appropriate for your situation:</span></span>

- <span data-ttu-id="146de-169">**Предложение условий для вызова.**</span><span class="sxs-lookup"><span data-stu-id="146de-169">**Guard the call**.</span></span> <span data-ttu-id="146de-170">Это можно сделать, направив условный вызов к коду во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="146de-170">You can achieve this by conditionally calling the code at run time.</span></span> <span data-ttu-id="146de-171">Проверьте, выполняется ли код на нужной платформе `Platform` с помощью одного из методов проверки платформы, например `OperatingSystem.Is<Platform>()` или `OperatingSystem.Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)`.</span><span class="sxs-lookup"><span data-stu-id="146de-171">Check whether you’re running on a desired `Platform` by using one of platform-check methods, for example, `OperatingSystem.Is<Platform>()` or `OperatingSystem.Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)`.</span></span>

- <span data-ttu-id="146de-172">**Установка для места вызова метки зависимости от платформы.**</span><span class="sxs-lookup"><span data-stu-id="146de-172">**Mark the call site as platform-specific**.</span></span> <span data-ttu-id="146de-173">Вы также можете пометить свои API как зависящие от платформы, благодаря чему требования будут смещены на вызывающие методы.</span><span class="sxs-lookup"><span data-stu-id="146de-173">You can also choose to mark your own APIs as being platform-specific, thus effectively just forwarding the requirements to your callers.</span></span> <span data-ttu-id="146de-174">Пометьте содержащий метод, тип или всю сборку такими же атрибутами, что и зависящий от платформы вызов, на который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="146de-174">Mark the containing method or type or the entire assembly with the same attributes as the referenced platform-dependent call.</span></span> <span data-ttu-id="146de-175">[Примеры](#mark-call-site-as-platform-specific).</span><span class="sxs-lookup"><span data-stu-id="146de-175">[Examples](#mark-call-site-as-platform-specific).</span></span>

- <span data-ttu-id="146de-176">**Утверждение места вызова с помощью проверки платформы.**</span><span class="sxs-lookup"><span data-stu-id="146de-176">**Assert the call site with platform check**.</span></span> <span data-ttu-id="146de-177">Если вы не хотите применять дополнительную инструкцию `if` во время выполнения, используйте <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="146de-177">If you don't want the overhead of an additional `if` statement at run time, use <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType>.</span></span> <span data-ttu-id="146de-178">[Пример.](#assert-the-call-site-with-platform-check)</span><span class="sxs-lookup"><span data-stu-id="146de-178">[Example](#assert-the-call-site-with-platform-check).</span></span>

- <span data-ttu-id="146de-179">**Удаление кода.**</span><span class="sxs-lookup"><span data-stu-id="146de-179">**Delete the code**.</span></span> <span data-ttu-id="146de-180">Обычно это нежелательно, так как в таком случае теряется точность, если с вашим кодом работают пользователи Windows.</span><span class="sxs-lookup"><span data-stu-id="146de-180">Generally not what you want because it means you lose fidelity when your code is used by Windows users.</span></span> <span data-ttu-id="146de-181">В случаях с доступностью кросс-платформенной альтернативы чаще оптимальнее использовать ее, а не API, зависимые от платформы.</span><span class="sxs-lookup"><span data-stu-id="146de-181">For cases where a cross-platform alternative exists, you’re likely better off using that over platform-specific APIs.</span></span>

- <span data-ttu-id="146de-182">**Блокировать предупреждение.**</span><span class="sxs-lookup"><span data-stu-id="146de-182">**Suppress the warning**.</span></span> <span data-ttu-id="146de-183">Вы также можете заблокировать предупреждение с помощью файла editor.config или инструкции `#pragma warning disable ca1416`.</span><span class="sxs-lookup"><span data-stu-id="146de-183">You can also simply suppress the warning, either via editor.config or `#pragma warning disable ca1416`.</span></span> <span data-ttu-id="146de-184">Но прибегайте к этому варианту только в исключительных случаях при использовании API, зависящих от платформы.</span><span class="sxs-lookup"><span data-stu-id="146de-184">However, this option should be a last resort when using platform-specific APIs.</span></span>

### <a name="guard-platform-specific-apis-with-guard-methods"></a><span data-ttu-id="146de-185">Предложение условий для API, зависящих от платформы, с помощью методов условий</span><span class="sxs-lookup"><span data-stu-id="146de-185">Guard platform-specific APIs with guard methods</span></span>

<span data-ttu-id="146de-186">Имя платформы в методе условия должно совпадать с именем платформы вызывающего API, зависимого от платформы.</span><span class="sxs-lookup"><span data-stu-id="146de-186">The guard method's platform name should match with the calling platform-dependent API platform name.</span></span> <span data-ttu-id="146de-187">Если строка платформы вызывающего API включает версию:</span><span class="sxs-lookup"><span data-stu-id="146de-187">If the platform string of the calling API includes the version:</span></span>

- <span data-ttu-id="146de-188">Для атрибута `[SupportedOSPlatform("platformVersion")]` значение для платформы метода условия `version` должно быть больше или равно значению `Version` вызывающей платформы.</span><span class="sxs-lookup"><span data-stu-id="146de-188">For the `[SupportedOSPlatform("platformVersion")]` attribute, the guard method platform `version` should be greater than or equal to the calling platform's `Version`.</span></span>
- <span data-ttu-id="146de-189">Для атрибута `[UnsupportedOSPlatform("platformVersion")]` значение для платформы метода условия `version` должно быть меньше или равно значению `Version` вызывающей платформы.</span><span class="sxs-lookup"><span data-stu-id="146de-189">For the `[UnsupportedOSPlatform("platformVersion")]` attribute, the guard method's platform `version` should be less than or equal to the calling platform's `Version`.</span></span>

  ```csharp
  public void CallingSupportedOnlyApis() // Allow list calls
  {
      if (OperatingSystem.IsWindows())
      {
          WindowsOnlyApi(); // will not warn
      }

      if (OperatingSystem.IsLinux())
      {
          SupportedOnWindowsAndLinuxOnly(); // will not warn, within one of the supported context
      }

      // Can use &&, || logical operators to guard combined attributes
      if (OperatingSystem.IsWindowsVersionAtLeast(8) && !OperatingSystem.IsWindowsVersionAtLeast(10.0.19041)))
      {
          ApiSupportedFromWindows8UnsupportFromWindows10();
      }

      if (OperatingSystem.IsWindowsVersionAtLeast(10, 0, 1903))
      {
          AssemblySupportedOnWindowsApiSupportedFromWindows10(); // Only need to check latest supported version
      }
  }

  public void CallingUnsupportedApis()
  {
      if (!OperatingSystem.IsAndroid())
      {
          DoesNotWorkOnAndroid(); // will not warn
      }

      if (!OperatingSystem.IsWindows() || OperatingSystem.IsWindowsVersionAtLeast(8))
      {
          StartedWindowsSupportFromVersion8(); // will not warn
      }

      if (!OperatingSystem.IsWindows() || // supported all other platforms
         (OperatingSystem.IsWindowsVersionAtLeast(8) && !OperatingSystem.IsWindowsVersionAtLeast(10, 0, 1903)))
      {
          StartedWindowsSupportFrom8UnsupportedFrom10(); // will not warn
      }
  }
  ```

- <span data-ttu-id="146de-190">Если вам необходимо предложить условие для кода, который ориентирован на netstandard или netcoreapp, в которых новые API <xref:System.OperatingSystem> недоступны, вы можете использовать API <xref:System.Runtime.InteropServices.RuntimeInformation.IsOSPlatform%2A?displayProperty=nameWithType>, который обрабатывается анализатором.</span><span class="sxs-lookup"><span data-stu-id="146de-190">if you need to guard a code that targets netstandard or netcoreapp where new <xref:System.OperatingSystem> APIs are not available <xref:System.Runtime.InteropServices.RuntimeInformation.IsOSPlatform%2A?displayProperty=nameWithType> API can be used and will be respected by the analyzer.</span></span> <span data-ttu-id="146de-191">Но он менее производителен, чем API, добавленные в <xref:System.OperatingSystem>.</span><span class="sxs-lookup"><span data-stu-id="146de-191">But it's not as optimized as the new APIs added in <xref:System.OperatingSystem>.</span></span> <span data-ttu-id="146de-192">Если платформа не поддерживается в структуре <xref:System.Runtime.InteropServices.OSPlatform>, вы можете использовать метод <xref:System.Runtime.InteropServices.OSPlatform.Create%2A?displayProperty=nameWithType> который также обрабатывается анализатором.</span><span class="sxs-lookup"><span data-stu-id="146de-192">In case the platform is not supported in <xref:System.Runtime.InteropServices.OSPlatform> struct, you can use <xref:System.Runtime.InteropServices.OSPlatform.Create%2A?displayProperty=nameWithType>("platform") which is also respected by the analyzer.</span></span>

  ```csharp
  public void CallingSupportedOnlyApis()
  {
      if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
      {
          SupportedOnWindowsAndLinuxOnly(); // will not warn
      }

      if (RuntimeInformation.IsOSPlatform(OSPlatform.Create("browser")))
      {
          ApiOnlySupportedOnBrowser(); // call of browser specific API
      }
  }
  ```

### <a name="mark-call-site-as-platform-specific"></a><span data-ttu-id="146de-193">Установка для места вызова метки зависимости от платформы</span><span class="sxs-lookup"><span data-stu-id="146de-193">Mark call site as platform-specific</span></span>

<span data-ttu-id="146de-194">Имена платформ должны совпадать с API, зависимым от вызывающей платформы.</span><span class="sxs-lookup"><span data-stu-id="146de-194">Platform names should match the calling platform-dependent API.</span></span> <span data-ttu-id="146de-195">Если строка платформы включает версию:</span><span class="sxs-lookup"><span data-stu-id="146de-195">If the platform string includes a version:</span></span>

- <span data-ttu-id="146de-196">Для атрибута `[SupportedOSPlatform("platformVersion")]` значение для платформы места вызова `version` должно быть больше или равно значению `Version` вызывающей платформы.</span><span class="sxs-lookup"><span data-stu-id="146de-196">For the `[SupportedOSPlatform("platformVersion")]` attribute, the call site platform `version` should be greater than or equal to the calling platform's `Version`</span></span>
- <span data-ttu-id="146de-197">Для атрибута `[UnsupportedOSPlatform("platformVersion")]` значение для платформы места вызова `version` должно быть меньше или равно значению `Version` вызывающей платформы.</span><span class="sxs-lookup"><span data-stu-id="146de-197">For the `[UnsupportedOSPlatform("platformVersion")]` attribute, the call site platform `version` should be less than or equal to the calling platform's `Version`</span></span>

  ```csharp
  // an API supported only on Windows.
  [SupportedOSPlatform("windows")]
  public void WindowsOnlyApi() { }

  // an API supported on Windows and Linux.
  [SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("Linux")]
  public void SupportedOnWindowsAndLinuxOnly() { }

  // an API only supported on Windows 8.0 and later, not supported for all other.
  // an API is removed/unsupported from version 10.0.19041.0.
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void ApiSupportedFromWindows8UnsupportFromWindows10() { }

  // an Assembly supported on Windows, the API added from version 10.0.19041.0.
  [assembly: SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("windows10.0.19041.0")]
  public void AssemblySupportedOnWindowsApiSupportedFromWindows10() { }

  [SupportedOSPlatform("windows8.0")] // call site attributed Windows 8.0 or above.
  public void Caller()
  {
      WindowsOnlyApi(); // will not warn as call site is for Windows.

      // will not warn as call site is for Windows.
      SupportedOnWindowsAndLinuxOnly();

      // will not warn for the API's [SupportedOSPlatform("windows8.0")] attribute.
      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // as the call site version is lower than calling version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  [SupportedOSPlatform("windows11.0")] // call site attributed with windows 11.0 or above.
  public void Caller2()
  {
      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // will not warn as call site version higher than calling API.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")] // call site supports Windows from version 8.0 to 10.0.19041.0.
  public void Caller3()
  {
      // will not warn as caller has exact same attributes.
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // As call site stopped support from that version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  // an API not supported on Android but supported on all other.
  [UnsupportedOSPlatform("android")]  
  public void DoesNotWorkOnAndroid() { }

  // an API was unsupported on Windows until version 8.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  public void StartedWindowsSupportFromVersion8() { }

  // an API was unsupported on Windows until version8.0.
  // Then the API is removed (unsupported) from version 10.0.19041.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void StartedWindowsSupportFrom8UnsupportedFrom10() { }

  [UnsupportedOSPlatform("windows")] // Caller no support Windows for any version.
  public void Caller4()
  {
      DoesNotWorkOnAndroid(); // warns 'DoesNotWorkOnAndroid' is unsupported on 'Android'.

      // will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFromVersion8();

      // same, will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }

  [UnsupportedOSPlatform("windows")]
  [UnsupportedOSPlatform("android")] // Caller not support Windows and Android for any version.
  public void Caller4()
  {
      DoesNotWorkOnAndroid(); // will not warn as call site not supports Android.

      // will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFromVersion8();

      // same, will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }
  ```

### <a name="assert-the-call-site-with-platform-check"></a><span data-ttu-id="146de-198">Утверждение места вызова с помощью проверки платформы</span><span class="sxs-lookup"><span data-stu-id="146de-198">Assert the call-site with platform check</span></span>

<span data-ttu-id="146de-199">Все условные проверки, используемые в [примерах условий платформы](#guard-platform-specific-apis-with-guard-methods), также можно использовать в качестве условия для <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="146de-199">All the conditional checks used in the [platform guard examples](#guard-platform-specific-apis-with-guard-methods) can also be used as the condition for <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType>.</span></span>

  ```csharp
  // An API supported only on Linux.
  [SupportedOSPlatform("linux")]
  public void LinuxOnlyApi() { }

  public void Caller()
  {
      Debug.Assert(OperatingSystem.IsLinux());

      LinuxOnlyApi(); // will not warn
  }
  ```

## <a name="see-also"></a><span data-ttu-id="146de-200">См. также раздел</span><span class="sxs-lookup"><span data-stu-id="146de-200">See also</span></span>

- [<span data-ttu-id="146de-201">Имена целевых платформ в .NET 5</span><span class="sxs-lookup"><span data-stu-id="146de-201">Target Framework Names in .NET 5</span></span>](https://github.com/dotnet/designs/blob/master/accepted/2020/net5/net5.md)
- [<span data-ttu-id="146de-202">Создание аннотаций для API, зависящих от платформ, и обнаружение использования этой функции</span><span class="sxs-lookup"><span data-stu-id="146de-202">Annotating platform-specific APIs and detecting its use</span></span>](https://github.com/dotnet/designs/blob/master/accepted/2020/platform-checks/platform-checks.md)
- [<span data-ttu-id="146de-203">Создание аннотаций для API как неподдерживаемых на конкретных платформах</span><span class="sxs-lookup"><span data-stu-id="146de-203">Annotating APIs as unsupported on specific platforms</span></span>](https://github.com/dotnet/designs/blob/master/accepted/2020/platform-exclusion/platform-exclusion.md)
- [<span data-ttu-id="146de-204">CA1416: анализатор совместимости платформ</span><span class="sxs-lookup"><span data-stu-id="146de-204">CA1416 Platform compatibility analyzer</span></span>](/visualstudio/code-quality/ca1416)
- [<span data-ttu-id="146de-205">Анализатор .NET API</span><span class="sxs-lookup"><span data-stu-id="146de-205">.NET API analyzer</span></span>](../../standard/analyzers/api-analyzer.md)