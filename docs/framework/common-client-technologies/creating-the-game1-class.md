---
title: "Создание класса Game1"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 47932ce3-2ba5-476f-a26b-3ddfd5226f27
caps.latest.revision: 8
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9c6d0bdfd21f431ae6da38e3868386f91d5b725b
ms.contentlocale: ru-ru
ms.lasthandoff: 07/28/2017

---
# <a name="creating-the-game1-class"></a><span data-ttu-id="22d3b-102">Создание класса Game1</span><span class="sxs-lookup"><span data-stu-id="22d3b-102">Creating the Game1 Class</span></span>
<span data-ttu-id="22d3b-103">Как во всех проектах Microsof XNA, класс Game1 является производным от класса [Microsoft.Xna.Framework.Game](http://msdn.microsoft.com/library/microsoft.xna.framework.game.aspx), который предоставляет инициализацию основного графического устройства, логику игры и код отрисовки для игр XNA.</span><span class="sxs-lookup"><span data-stu-id="22d3b-103">As with all Microsoft XNA projects, the Game1 class derives from the [Microsoft.Xna.Framework.Game](http://msdn.microsoft.com/library/microsoft.xna.framework.game.aspx) class, which provides basic graphics device initialization, game logic, and rendering code for XNA games.</span></span> <span data-ttu-id="22d3b-104">Класс Game1 довольно простой, поскольку большая часть работы выполняется в классах GamePiece и GamePieceCollection.</span><span class="sxs-lookup"><span data-stu-id="22d3b-104">The Game1 class is fairly simple because most of the work in done in the GamePiece and GamePieceCollection classes.</span></span>  
  
## <a name="creating-the-code"></a><span data-ttu-id="22d3b-105">Создание кода</span><span class="sxs-lookup"><span data-stu-id="22d3b-105">Creating the Code</span></span>  
 <span data-ttu-id="22d3b-106">Закрытые члены класса состоят из объекта **GamePieceCollection** для хранения элементов игры, объекта [GraphicsDeviceManager](http://msdn.microsoft.com/library/microsoft.xna.framework.graphicsdevicemanager.aspx) и объекта [SpriteBatch](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.spritebatch.aspx), используемого для отрисовки элементов игры.</span><span class="sxs-lookup"><span data-stu-id="22d3b-106">The private members for the class consist of a **GamePieceCollection** object to hold the game pieces, a [GraphicsDeviceManager](http://msdn.microsoft.com/library/microsoft.xna.framework.graphicsdevicemanager.aspx) object, and a [SpriteBatch](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.spritebatch.aspx) object used to render game pieces.</span></span>  
  
 <span data-ttu-id="22d3b-107">[!code-csharp[ManipulationXNA#_Game1_PrivateMembers](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_privatemembers)]</span><span class="sxs-lookup"><span data-stu-id="22d3b-107">[!code-csharp[ManipulationXNA#_Game1_PrivateMembers](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_privatemembers)]</span></span>  
  
 <span data-ttu-id="22d3b-108">Экземпляры этих объектов создаются во время инициализации игры.</span><span class="sxs-lookup"><span data-stu-id="22d3b-108">During game initialization, these objects are instantiated.</span></span>  
  
 <span data-ttu-id="22d3b-109">[!code-csharp[ManipulationXNA#_Game1_ConstructorInitialize](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_constructorinitialize)]</span><span class="sxs-lookup"><span data-stu-id="22d3b-109">[!code-csharp[ManipulationXNA#_Game1_ConstructorInitialize](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_constructorinitialize)]</span></span>  
  
 <span data-ttu-id="22d3b-110">При вызове метода [LoadContent](http://msdn.microsoft.com/library/microsoft.xna.framework.game.loadcontent.aspx) создаются элементы игры и назначаются объекту **GamePieceCollection**.</span><span class="sxs-lookup"><span data-stu-id="22d3b-110">When the [LoadContent](http://msdn.microsoft.com/library/microsoft.xna.framework.game.loadcontent.aspx) method is called, the game pieces are created and assigned to the **GamePieceCollection** object.</span></span> <span data-ttu-id="22d3b-111">Существует два типа элементов игры.</span><span class="sxs-lookup"><span data-stu-id="22d3b-111">There are two types of game pieces.</span></span> <span data-ttu-id="22d3b-112">Коэффициент масштабирования для элементов слегка отличается, поэтому одни элементы могут стать меньше, а другие больше.</span><span class="sxs-lookup"><span data-stu-id="22d3b-112">The scale factor for the pieces is changed slightly so that there are some smaller and some larger pieces.</span></span>  
  
 <span data-ttu-id="22d3b-113">[!code-csharp[ManipulationXNA#_Game1_LoadContent](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_loadcontent)]</span><span class="sxs-lookup"><span data-stu-id="22d3b-113">[!code-csharp[ManipulationXNA#_Game1_LoadContent](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_loadcontent)]</span></span>  
  
 <span data-ttu-id="22d3b-114">Метод [Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) несколько раз вызывается XNA Framework во время выполнения игры.</span><span class="sxs-lookup"><span data-stu-id="22d3b-114">The [Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) method is called repeatedly by the XNA Framework while the game is running.</span></span> <span data-ttu-id="22d3b-115">Метод [Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) вызывает методы **ProcessInertia** и **UpdateFromMouse** в коллекции элементов игры.</span><span class="sxs-lookup"><span data-stu-id="22d3b-115">The [Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) method calls the **ProcessInertia** and the **UpdateFromMouse** methods on the game piece collection.</span></span> <span data-ttu-id="22d3b-116">Эти методы описаны в разделе [Создание класса GamePieceCollection](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md).</span><span class="sxs-lookup"><span data-stu-id="22d3b-116">These methods are described in [Creating the GamePieceCollection Class](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md).</span></span>  
  
 <span data-ttu-id="22d3b-117">[!code-csharp[ManipulationXNA#_Game1_UpdateGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_updategame)]</span><span class="sxs-lookup"><span data-stu-id="22d3b-117">[!code-csharp[ManipulationXNA#_Game1_UpdateGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_updategame)]</span></span>  
  
 <span data-ttu-id="22d3b-118">Метод [Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) также вызывается XNA Framework несколько раз во время выполнения игры.</span><span class="sxs-lookup"><span data-stu-id="22d3b-118">The [Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) method is also called repeatedly by the XNA Framework while the game is running.</span></span> <span data-ttu-id="22d3b-119">Метод [Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) выполняет отрисовку элементов игры путем вызова метода **Draw** объекта **GamePieceCollection**.</span><span class="sxs-lookup"><span data-stu-id="22d3b-119">The [Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) method performs the rendering of game pieces by calling the **Draw** method of the **GamePieceCollection** object.</span></span> <span data-ttu-id="22d3b-120">Этот метод описывается в разделе [Создание класса GamePieceCollection](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md).</span><span class="sxs-lookup"><span data-stu-id="22d3b-120">This method is described in[Creating the GamePieceCollection Class](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md).</span></span>  
  
 <span data-ttu-id="22d3b-121">[!code-csharp[ManipulationXNA#_Game1_DrawGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_drawgame)]</span><span class="sxs-lookup"><span data-stu-id="22d3b-121">[!code-csharp[ManipulationXNA#_Game1_DrawGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_drawgame)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="22d3b-122">См. также</span><span class="sxs-lookup"><span data-stu-id="22d3b-122">See Also</span></span>  
 <span data-ttu-id="22d3b-123">[Манипуляции и инерция](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md) </span><span class="sxs-lookup"><span data-stu-id="22d3b-123">[Manipulations and Inertia](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md) </span></span>  
 <span data-ttu-id="22d3b-124">[Использование манипуляций и инерции в приложении XNA](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md) </span><span class="sxs-lookup"><span data-stu-id="22d3b-124">[Using Manipulations and Inertia in an XNA Application](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md) </span></span>  
 <span data-ttu-id="22d3b-125">[Создание класса GamePiece](../../../docs/framework/common-client-technologies/creating-the-gamepiece-class.md) </span><span class="sxs-lookup"><span data-stu-id="22d3b-125">[Creating the GamePiece Class](../../../docs/framework/common-client-technologies/creating-the-gamepiece-class.md) </span></span>  
 <span data-ttu-id="22d3b-126">[Создание класса GamePieceCollection](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md) </span><span class="sxs-lookup"><span data-stu-id="22d3b-126">[Creating the GamePieceCollection Class](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md) </span></span>  
 [<span data-ttu-id="22d3b-127">Полные листинги кода</span><span class="sxs-lookup"><span data-stu-id="22d3b-127">Full Code Listings</span></span>](../../../docs/framework/common-client-technologies/full-code-listings.md)
