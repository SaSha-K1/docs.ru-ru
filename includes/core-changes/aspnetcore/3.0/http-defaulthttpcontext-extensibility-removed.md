---
ms.openlocfilehash: 7b5ae84d02b83a10a4b9e002fc2ed4ee0833b84c
ms.sourcegitcommit: 5a28f8eb071fcc09b045b0c4ae4b96898673192e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2019
ms.locfileid: "73198554"
---
### <a name="http-defaulthttpcontext-extensibility-removed"></a><span data-ttu-id="b7456-101">HTTP. Удаление расширяемости DefaultHttpContext</span><span class="sxs-lookup"><span data-stu-id="b7456-101">HTTP: DefaultHttpContext extensibility removed</span></span>

<span data-ttu-id="b7456-102">В рамках повышения производительности ASP.NET Core 3.0 расширяемость `DefaultHttpContext` была удалена.</span><span class="sxs-lookup"><span data-stu-id="b7456-102">As part of ASP.NET Core 3.0 performance improvements, the extensibility of `DefaultHttpContext` was removed.</span></span> <span data-ttu-id="b7456-103">Теперь класс является `sealed`.</span><span class="sxs-lookup"><span data-stu-id="b7456-103">The class is now `sealed`.</span></span> <span data-ttu-id="b7456-104">Подробную информацию см. на странице [aspnet/AspNetCore#6504](https://github.com/aspnet/AspNetCore/pull/6504).</span><span class="sxs-lookup"><span data-stu-id="b7456-104">For more information, see [aspnet/AspNetCore#6504](https://github.com/aspnet/AspNetCore/pull/6504).</span></span>

<span data-ttu-id="b7456-105">Если модульные тесты используют `Mock<DefaultHttpContext>`, используйте вместо этого `Mock<HttpContext>`.</span><span class="sxs-lookup"><span data-stu-id="b7456-105">If your unit tests use `Mock<DefaultHttpContext>`, use `Mock<HttpContext>` instead.</span></span>

<span data-ttu-id="b7456-106">Обсуждение этого вопроса см. на странице [aspnet/AspNetCore#6534](https://github.com/aspnet/AspNetCore/issues/6534).</span><span class="sxs-lookup"><span data-stu-id="b7456-106">For discussion, see [aspnet/AspNetCore#6534](https://github.com/aspnet/AspNetCore/issues/6534).</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="b7456-107">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="b7456-107">Version introduced</span></span>

<span data-ttu-id="b7456-108">3.0</span><span class="sxs-lookup"><span data-stu-id="b7456-108">3.0</span></span>

#### <a name="old-behavior"></a><span data-ttu-id="b7456-109">Старое поведение</span><span class="sxs-lookup"><span data-stu-id="b7456-109">Old behavior</span></span>

<span data-ttu-id="b7456-110">Классы могут быть производными от `DefaultHttpContext`.</span><span class="sxs-lookup"><span data-stu-id="b7456-110">Classes can derive from `DefaultHttpContext`.</span></span>

#### <a name="new-behavior"></a><span data-ttu-id="b7456-111">Новое поведение</span><span class="sxs-lookup"><span data-stu-id="b7456-111">New behavior</span></span>

<span data-ttu-id="b7456-112">Классы не могут быть производными от `DefaultHttpContext`.</span><span class="sxs-lookup"><span data-stu-id="b7456-112">Classes can't derive from `DefaultHttpContext`.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="b7456-113">Причина изменения</span><span class="sxs-lookup"><span data-stu-id="b7456-113">Reason for change</span></span>

<span data-ttu-id="b7456-114">Изначально была предоставлена расширяемость, позволяющая выполнять группировку `HttpContext`, но в ней появились ненужные сложности и другие нарушения, влияющие на оптимизацию.</span><span class="sxs-lookup"><span data-stu-id="b7456-114">The extensibility was provided initially to allow pooling of the `HttpContext`, but it introduced unnecessary complexity and impeded other optimizations.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="b7456-115">Рекомендуемое действие</span><span class="sxs-lookup"><span data-stu-id="b7456-115">Recommended action</span></span>

<span data-ttu-id="b7456-116">Если вы используете `Mock<DefaultHttpContext>` в модульных тестах, используйте вместо этого `Mock<HttpContext>`.</span><span class="sxs-lookup"><span data-stu-id="b7456-116">If you're using `Mock<DefaultHttpContext>` in your unit tests, begin using `Mock<HttpContext>` instead.</span></span>

#### <a name="category"></a><span data-ttu-id="b7456-117">Категория</span><span class="sxs-lookup"><span data-stu-id="b7456-117">Category</span></span>

<span data-ttu-id="b7456-118">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="b7456-118">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="b7456-119">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="b7456-119">Affected APIs</span></span>

<xref:Microsoft.AspNetCore.Http.DefaultHttpContext?displayProperty=nameWithType>

<!--

#### Affected APIs

`T:Microsoft.AspNetCore.Http.DefaultHttpContext`

-->