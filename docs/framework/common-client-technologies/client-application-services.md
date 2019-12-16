---
title: "Службы клиентских приложений"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- role-based security [.NET Framework], client application services
- client application services
- credentials [.NET Framework]
- Windows-based applications, client application services
- application settings, client application services
- profiles [ASP.NET], client application services
- logins [client application services]
- sharing information and functionality [client application services]
- Web settings [client application services]
- authentication [ASP.NET], client application services
- ASP.NET services, client application services
- client applications, ASP.NET services
- roles [.NET Framework], client application services
- client application services, about client application services
ms.assetid: 1487d8df-089e-4f21-abfb-a791a652b58e
caps.latest.revision: 14
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c776040786a51089c9aa988e9229805c06b28bae
ms.contentlocale: ru-ru
ms.lasthandoff: 07/28/2017

---
# <a name="client-application-services"></a><span data-ttu-id="4ef45-102">Службы клиентских приложений</span><span class="sxs-lookup"><span data-stu-id="4ef45-102">Client Application Services</span></span>
<span data-ttu-id="4ef45-103">Службы клиентских приложений позволяют легко создавать приложения Windows, использующие службы входа, ролей, профилей [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)], которые включены в расширения Microsoft ASP.NET 2.0 AJAX.</span><span class="sxs-lookup"><span data-stu-id="4ef45-103">Client application services make it easy for you to create Windows-based applications that use the [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] login, roles, and profile application services included in the Microsoft ASP.NET 2.0 AJAX Extensions.</span></span> <span data-ttu-id="4ef45-104">Эти службы позволяют нескольким веб-приложениям и приложениям Windows использовать сведения о пользователе и функции управления пользователями с одного сервера.</span><span class="sxs-lookup"><span data-stu-id="4ef45-104">These services enable multiple Web and Windows-based applications to share user information and user-management functionality from a single server.</span></span> <span data-ttu-id="4ef45-105">Например, эти службы можно использовать для решения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="4ef45-105">For example, you can use these services to perform the following tasks:</span></span>  
  
-   <span data-ttu-id="4ef45-106">Проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="4ef45-106">Authenticate a user.</span></span> <span data-ttu-id="4ef45-107">Для проверки удостоверения пользователя можно использовать службу проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4ef45-107">You can use the authentication service to verify a user's identity.</span></span>  
  
-   <span data-ttu-id="4ef45-108">Определение роли или ролей выполнившего проверку подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="4ef45-108">Determine the role or roles of an authenticated user.</span></span> <span data-ttu-id="4ef45-109">Изменить пользовательский интерфейс приложения в соответствии с ролью пользователя можно с помощью службы ролей.</span><span class="sxs-lookup"><span data-stu-id="4ef45-109">You can use the roles service to change the user interface of your application depending on the user's role.</span></span> <span data-ttu-id="4ef45-110">Например, можно предоставить дополнительные функции для пользователей с ролью администратора.</span><span class="sxs-lookup"><span data-stu-id="4ef45-110">For example, you can provide additional features for users who are in an administrator role.</span></span>  
  
-   <span data-ttu-id="4ef45-111">Хранение параметров пользовательских приложений на сервере и доступ к ним.</span><span class="sxs-lookup"><span data-stu-id="4ef45-111">Store and access per-user application settings located on the server.</span></span> <span data-ttu-id="4ef45-112">Вы можете использовать веб-службу параметров (другое название — служба профилей) для разделения параметров между несколькими приложениями и расположениями.</span><span class="sxs-lookup"><span data-stu-id="4ef45-112">You can use the Web settings service (also known as the profile service) to share settings across multiple applications and locations.</span></span>  
  
 <span data-ttu-id="4ef45-113">Службы клиентских приложений используют преимущество модели расширяемости веб-служб через поставщиков клиентских служб, которых можно указать в файлах конфигурации приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef45-113">Client application services take advantage of the Web services extensibility model through client service providers that you can specify in your application configuration files.</span></span> <span data-ttu-id="4ef45-114">Эти поставщики служб предоставляют автономную функциональность, использующую локальный кэш для проверки подлинности, хранения данных о ролях и параметрах, если сетевое подключение недоступно.</span><span class="sxs-lookup"><span data-stu-id="4ef45-114">These service providers include offline functionality that uses a local cache for authentication, roles, and settings data when a network connection is unavailable.</span></span>  
  
 <span data-ttu-id="4ef45-115">Дополнительные сведения о службах приложений [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] см. в разделе [Общие сведения о службах приложений ASP.NET](http://msdn.microsoft.com/library/1162e529-0d70-44b2-b3ab-83e60c695013).</span><span class="sxs-lookup"><span data-stu-id="4ef45-115">For more information about the [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] application services, see [ASP.NET Application Services Overview](http://msdn.microsoft.com/library/1162e529-0d70-44b2-b3ab-83e60c695013).</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="4ef45-116">Содержание</span><span class="sxs-lookup"><span data-stu-id="4ef45-116">In This Section</span></span>  
 [<span data-ttu-id="4ef45-117">Общие сведения о службах клиентских приложений</span><span class="sxs-lookup"><span data-stu-id="4ef45-117">Client Application Services Overview</span></span>](../../../docs/framework/common-client-technologies/client-application-services-overview.md)  
 <span data-ttu-id="4ef45-118">Описание возможностей, доступных через поставщиков служб клиентских приложений.</span><span class="sxs-lookup"><span data-stu-id="4ef45-118">Describes the features available through the client application service providers.</span></span>  
  
 [<span data-ttu-id="4ef45-119">Практическое руководство. Настройка служб клиентских приложений</span><span class="sxs-lookup"><span data-stu-id="4ef45-119">How to: Configure Client Application Services</span></span>](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)  
 <span data-ttu-id="4ef45-120">Описание использования конструктора проектов [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] для включения и настройки служб клиентских приложений,</span><span class="sxs-lookup"><span data-stu-id="4ef45-120">Describes how to use the [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] project designer to enable and configuration application services.</span></span> <span data-ttu-id="4ef45-121">а также описание соответствующих изменений в файле App.config.</span><span class="sxs-lookup"><span data-stu-id="4ef45-121">Also describes the corresponding changes to your App.config file.</span></span>  
  
 [<span data-ttu-id="4ef45-122">Практическое руководство. Реализация входа пользователя с помощью служб клиентских приложений</span><span class="sxs-lookup"><span data-stu-id="4ef45-122">How to: Implement User Login with Client Application Services</span></span>](../../../docs/framework/common-client-technologies/how-to-implement-user-login-with-client-application-services.md)  
 <span data-ttu-id="4ef45-123">Описание процедуры проверки пользователя, если в приложении настроено использование поставщика службы проверки подлинности клиента.</span><span class="sxs-lookup"><span data-stu-id="4ef45-123">Describes how to validate a user when your application is configured to use a client authentication service provider.</span></span>  
  
 [<span data-ttu-id="4ef45-124">Пошаговое руководство. Использование служб клиентских приложений</span><span class="sxs-lookup"><span data-stu-id="4ef45-124">Walkthrough: Using Client Application Services</span></span>](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md)  
 <span data-ttu-id="4ef45-125">Описание совмещения всех возможностей службы клиентских приложений в одном приложении.</span><span class="sxs-lookup"><span data-stu-id="4ef45-125">Describes how to combine all client application services features in a single application.</span></span> <span data-ttu-id="4ef45-126">Это пошаговое руководство содержит подробные инструкции.</span><span class="sxs-lookup"><span data-stu-id="4ef45-126">This walkthrough provides end-to-end guidance.</span></span> <span data-ttu-id="4ef45-127">Например, в него входят инструкции по созданию приложения веб-службы ASP.NET, которое можно использовать для тестирования служб клиентских приложений.</span><span class="sxs-lookup"><span data-stu-id="4ef45-127">For example, it includes instructions on how to create an ASP.NET Web Service Application that you can use to test client application services.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="4ef45-128">Ссылка</span><span class="sxs-lookup"><span data-stu-id="4ef45-128">Reference</span></span>  
 <xref:System.Web.ClientServices.ClientFormsIdentity>  
 <xref:System.Web.ClientServices.ClientRolePrincipal>  
 <xref:System.Web.ClientServices.ConnectivityStatus>  
 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationCredentials>  
 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider>  
 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider>  
 <xref:System.Web.ClientServices.Providers.ClientWindowsAuthenticationMembershipProvider>  
 <xref:System.Web.ClientServices.Providers.ClientRoleProvider>  
 <xref:System.Web.ClientServices.Providers.ClientSettingsProvider>  
 <xref:System.Web.ClientServices.Providers.SettingsSavedEventArgs>  
 <xref:System.Web.ClientServices.Providers.UserValidatedEventArgs>  
  
## <a name="see-also"></a><span data-ttu-id="4ef45-129">См. также</span><span class="sxs-lookup"><span data-stu-id="4ef45-129">See Also</span></span>  
 <span data-ttu-id="4ef45-130">[Общие сведения о службах клиентских приложений ASP.NET](http://msdn.microsoft.com/library/1162e529-0d70-44b2-b3ab-83e60c695013) </span><span class="sxs-lookup"><span data-stu-id="4ef45-130">[ASP.NET Application Services Overview](http://msdn.microsoft.com/library/1162e529-0d70-44b2-b3ab-83e60c695013) </span></span>  
 <span data-ttu-id="4ef45-131">[Использование проверки подлинности с помощью форм в Microsoft Ajax](http://msdn.microsoft.com/library/c50f7dc5-323c-4c63-b4f3-96edfc1e815e) </span><span class="sxs-lookup"><span data-stu-id="4ef45-131">[Using Forms Authentication with Microsoft Ajax](http://msdn.microsoft.com/library/c50f7dc5-323c-4c63-b4f3-96edfc1e815e) </span></span>  
 <span data-ttu-id="4ef45-132">[Использование сведений о ролях в Microsoft Ajax](http://msdn.microsoft.com/library/280f6ad9-ba1a-4fc9-b0cc-22e39e54a82d) </span><span class="sxs-lookup"><span data-stu-id="4ef45-132">[Using Roles Information with Microsoft Ajax](http://msdn.microsoft.com/library/280f6ad9-ba1a-4fc9-b0cc-22e39e54a82d) </span></span>  
 <span data-ttu-id="4ef45-133">[Использование сведений о профилях в Microsoft Ajax](http://msdn.microsoft.com/library/91239ae6-d01c-4f4e-a433-eb9040dbed61) </span><span class="sxs-lookup"><span data-stu-id="4ef45-133">[Using Profile Information with Microsoft Ajax](http://msdn.microsoft.com/library/91239ae6-d01c-4f4e-a433-eb9040dbed61) </span></span>  
 <span data-ttu-id="4ef45-134">[Проверка подлинности ASP.NET](http://msdn.microsoft.com/library/fc10b0ef-4ce4-4a7f-9174-886325221ee1) </span><span class="sxs-lookup"><span data-stu-id="4ef45-134">[ASP.NET Authentication](http://msdn.microsoft.com/library/fc10b0ef-4ce4-4a7f-9174-886325221ee1) </span></span>  
 <span data-ttu-id="4ef45-135">[Управление авторизацией с помощью ролей](http://msdn.microsoft.com/library/01954ce4-39a2-487f-8153-a69f6f6f3195)  </span><span class="sxs-lookup"><span data-stu-id="4ef45-135">[Managing Authorization Using Roles](http://msdn.microsoft.com/library/01954ce4-39a2-487f-8153-a69f6f6f3195)  </span></span>  
 [<span data-ttu-id="4ef45-136">Общие сведения о параметрах приложений</span><span class="sxs-lookup"><span data-stu-id="4ef45-136">Application Settings Overview</span></span>](../../../docs/framework/winforms/advanced/application-settings-overview.md)
