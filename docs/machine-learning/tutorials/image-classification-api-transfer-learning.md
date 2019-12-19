---
title: Учебник. Автоматизированная визуальная проверка с использованием передачи обучения
description: В этом учебнике показано, как применить передачу обучения для обучения модели глубокого обучения TensorFlow в ML.NET, используя API обнаружения изображений для классификации изображений бетонных поверхностей как растрескавшихся или нерастрескавшихся.
author: luisquintanilla
ms.author: luquinta
ms.date: 11/14/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 443f9e9a83ebf31bb6c62323015af4a554323b67
ms.sourcegitcommit: 81ad1f09b93f3b3e6706a7f2e4ddf50ef229ea3d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/20/2019
ms.locfileid: "74205056"
---
# <a name="tutorial-automated-visual-inspection-using-transfer-learning-with-the-mlnet-image-classification-api"></a><span data-ttu-id="7a138-103">Учебник. Автоматизированная визуальная проверка с использованием передачи обучения и API классификации изображений ML.NET</span><span class="sxs-lookup"><span data-stu-id="7a138-103">Tutorial: Automated visual inspection using transfer learning with the ML.NET Image Classification API</span></span>

<span data-ttu-id="7a138-104">Сведения о том, как обучить пользовательскую модель глубокого обучения с использованием передачи обучения, предварительно обученной модели TensorFlow и API классификации изображений ML.NET для классификации изображений бетонных поверхностей как растрескавшихся или нерастрескавшихся.</span><span class="sxs-lookup"><span data-stu-id="7a138-104">Learn how to train a custom deep learning model using transfer learning, a pretrained TensorFlow model and the ML.NET Image Classification API to classify images of concrete surfaces as cracked or uncracked.</span></span>

<span data-ttu-id="7a138-105">В этом руководстве вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="7a138-105">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
>
> - <span data-ttu-id="7a138-106">Определение проблемы</span><span class="sxs-lookup"><span data-stu-id="7a138-106">Understand the problem</span></span>
> - <span data-ttu-id="7a138-107">Сведения об API классификации изображений ML.NET</span><span class="sxs-lookup"><span data-stu-id="7a138-107">Learn about ML.NET Image Classification API</span></span>
> - <span data-ttu-id="7a138-108">Описание предварительно обученной модели</span><span class="sxs-lookup"><span data-stu-id="7a138-108">Understand the pretrained model</span></span>
> - <span data-ttu-id="7a138-109">Использование передачи обучения для обучения пользовательской модели классификации изображений TensorFlow</span><span class="sxs-lookup"><span data-stu-id="7a138-109">Use transfer learning to train a custom TensorFlow image classification model</span></span>
> - <span data-ttu-id="7a138-110">Классификация изображений с помощью пользовательской модели</span><span class="sxs-lookup"><span data-stu-id="7a138-110">Classify images with the custom model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a138-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7a138-111">Prerequisites</span></span>

- <span data-ttu-id="7a138-112">[Visual Studio 2017 15.6 или более поздней версии](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017) с установленной рабочей нагрузкой "Кроссплатформенная разработка .NET Core".</span><span class="sxs-lookup"><span data-stu-id="7a138-112">[Visual Studio 2017 15.6 or later](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017) with the ".NET Core cross-platform development" workload installed.</span></span>

## <a name="image-classification-transfer-learning-sample-overview"></a><span data-ttu-id="7a138-113">Обзор примера с передачей обучения для классификации изображений</span><span class="sxs-lookup"><span data-stu-id="7a138-113">Image classification transfer learning sample overview</span></span>

<span data-ttu-id="7a138-114">Этот пример представляет собой консольное приложение C# .NET Core, которое классифицирует изображения с помощью предварительно обученной модели TensorFlow для глубокого обучения.</span><span class="sxs-lookup"><span data-stu-id="7a138-114">This sample is a C# .NET Core console application that classifies images using a pretrained deep learning TensorFlow model.</span></span> <span data-ttu-id="7a138-115">Код для этого примера можно найти в репозитории [dotnet/machinelearning-samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="7a138-115">The code for this sample can be found on the [dotnet/machinelearning-samples repository](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary) on GitHub.</span></span>

## <a name="understand-the-problem"></a><span data-ttu-id="7a138-116">Определение проблемы</span><span class="sxs-lookup"><span data-stu-id="7a138-116">Understand the problem</span></span>

<span data-ttu-id="7a138-117">Классификация изображений — это задача из области компьютерного зрения.</span><span class="sxs-lookup"><span data-stu-id="7a138-117">Image classification is a computer vision problem.</span></span> <span data-ttu-id="7a138-118">Классификация изображений принимает изображение в качестве входных данных и классифицирует его, относя к предписанному классу.</span><span class="sxs-lookup"><span data-stu-id="7a138-118">Image classification takes an image as input and categorizes it into a prescribed class.</span></span> <span data-ttu-id="7a138-119">Ниже описаны сценарии, в которых удобно использовать классификацию изображений.</span><span class="sxs-lookup"><span data-stu-id="7a138-119">Some scenarios where image classification is useful include:</span></span>

- <span data-ttu-id="7a138-120">Распознавание лиц</span><span class="sxs-lookup"><span data-stu-id="7a138-120">Facial recognition</span></span>
- <span data-ttu-id="7a138-121">Распознавание эмоций</span><span class="sxs-lookup"><span data-stu-id="7a138-121">Emotion detection</span></span>
- <span data-ttu-id="7a138-122">Постановка медицинских диагнозов</span><span class="sxs-lookup"><span data-stu-id="7a138-122">Medical diagnosis</span></span>
- <span data-ttu-id="7a138-123">Распознавание ориентиров</span><span class="sxs-lookup"><span data-stu-id="7a138-123">Landmark detection</span></span>

<span data-ttu-id="7a138-124">В этом учебнике обучается пользовательская модель классификации изображений для проведения автоматизированной визуальной проверки эстакад моста для выявления конструкций с трещинами.</span><span class="sxs-lookup"><span data-stu-id="7a138-124">This tutorial trains a custom image classification model to perform automated visual inspection of bridge decks to identify structures that are damaged by cracks.</span></span>

## <a name="mlnet-image-classification-api"></a><span data-ttu-id="7a138-125">API классификации изображений ML.NET</span><span class="sxs-lookup"><span data-stu-id="7a138-125">ML.NET Image Classification API</span></span>

<span data-ttu-id="7a138-126">ML.NET предоставляет различные способы для классификации изображений.</span><span class="sxs-lookup"><span data-stu-id="7a138-126">ML.NET provides various ways of performing image classification.</span></span> <span data-ttu-id="7a138-127">В этом учебнике применяется передача обучения с помощью API классификации изображений.</span><span class="sxs-lookup"><span data-stu-id="7a138-127">This tutorial applies transfer learning using the Image Classification API.</span></span> <span data-ttu-id="7a138-128">API классификации изображений использует [TensorFlow.NET](https://github.com/SciSharp/TensorFlow.NET), низкоуровневую библиотеку, которая предоставляет привязки C# для API TensorFlow C++.</span><span class="sxs-lookup"><span data-stu-id="7a138-128">The Image Classification API makes use of [TensorFlow.NET](https://github.com/SciSharp/TensorFlow.NET), a low-level library that provides C# bindings for the TensorFlow C++ API.</span></span>

## <a name="what-is-transfer-learning"></a><span data-ttu-id="7a138-129">Что собой представляет передача обучения?</span><span class="sxs-lookup"><span data-stu-id="7a138-129">What is transfer learning?</span></span>

<span data-ttu-id="7a138-130">Передача обучения позволяет применить знания, полученные при решении одной проблемы, для другой связанной проблемы.</span><span class="sxs-lookup"><span data-stu-id="7a138-130">Transfer learning applies knowledge gained from solving one problem to another related problem.</span></span>

<span data-ttu-id="7a138-131">Обучение модели глубокого обучения с нуля предусматривает настройку нескольких параметров, а также использование больших объемов помеченных данных обучения и вычислительных ресурсов (сотни часов работы GPU).</span><span class="sxs-lookup"><span data-stu-id="7a138-131">Training a deep learning model from scratch requires setting several parameters, a large amount of labeled training data, and a vast amount of compute resources (hundreds of GPU hours).</span></span> <span data-ttu-id="7a138-132">Использование предварительно обученной модели вместе с передачей обучения позволяет упростить процесс обучения.</span><span class="sxs-lookup"><span data-stu-id="7a138-132">Using a pretrained model along with transfer learning allows you to shortcut the training process.</span></span>

## <a name="training-process"></a><span data-ttu-id="7a138-133">Процесс обучения</span><span class="sxs-lookup"><span data-stu-id="7a138-133">Training process</span></span>

<span data-ttu-id="7a138-134">API классификации изображений начинает процесс обучения с загрузки предварительно обученной модели TensorFlow.</span><span class="sxs-lookup"><span data-stu-id="7a138-134">The Image Classification API starts the training process by loading a pretrained TensorFlow model.</span></span> <span data-ttu-id="7a138-135">Процесс обучения состоит из двух этапов:</span><span class="sxs-lookup"><span data-stu-id="7a138-135">The training process consists of two steps:</span></span>

1. <span data-ttu-id="7a138-136">Этап узкого места</span><span class="sxs-lookup"><span data-stu-id="7a138-136">Bottleneck phase</span></span>
2. <span data-ttu-id="7a138-137">Этап обучения</span><span class="sxs-lookup"><span data-stu-id="7a138-137">Training phase</span></span>

![Этапы обучения](./media/image-classification-api-transfer-learning/training.png)

### <a name="bottleneck-phase"></a><span data-ttu-id="7a138-139">Этап узкого места</span><span class="sxs-lookup"><span data-stu-id="7a138-139">Bottleneck phase</span></span>

<span data-ttu-id="7a138-140">На этапе узкого места загружается набор обучающих изображений, а значения пикселей используются в качестве входных данных или признаков для зафиксированных слоев предварительно обученной модели.</span><span class="sxs-lookup"><span data-stu-id="7a138-140">During the bottleneck phase, the set of training images is loaded and the pixel values are used as input, or features, for the frozen layers of the pretrained model.</span></span> <span data-ttu-id="7a138-141">Зафиксированные слои включают все слои нейронной сети вплоть до предпоследнего, который неофициально называют слоем узкого места.</span><span class="sxs-lookup"><span data-stu-id="7a138-141">The frozen layers include all of the layers in the neural network up to the penultimate layer, informally known as the bottleneck layer.</span></span> <span data-ttu-id="7a138-142">Эти слои называются зафиксированными, так как обучение на них производиться не будет, а операции просто передаются через них.</span><span class="sxs-lookup"><span data-stu-id="7a138-142">These layers are referred to as frozen because no training will occur on these layers and operations are pass-through.</span></span> <span data-ttu-id="7a138-143">Именно в этих зафиксированных слоях вычисляются шаблоны более низкого уровня, которые помогают модели различать различные классы.</span><span class="sxs-lookup"><span data-stu-id="7a138-143">It's at these frozen layers where the lower-level patterns that help a model differentiate between the different classes are computed.</span></span> <span data-ttu-id="7a138-144">Чем больше количество слоев, тем больше вычислительных ресурсов используется на этом шаге.</span><span class="sxs-lookup"><span data-stu-id="7a138-144">The larger the number of layers, the more computationally intensive this step is.</span></span> <span data-ttu-id="7a138-145">К счастью, так как это разовое вычисление, результаты можно кэшировать и использовать в последующих запусках при экспериментах с различными параметрами.</span><span class="sxs-lookup"><span data-stu-id="7a138-145">Fortunately, since this is a one-time calculation, the results can be cached and used in later runs when experimenting with different parameters.</span></span>

### <a name="training-phase"></a><span data-ttu-id="7a138-146">Этап обучения</span><span class="sxs-lookup"><span data-stu-id="7a138-146">Training phase</span></span>

<span data-ttu-id="7a138-147">После вычисления выходных значений на этапе узкого места они используются в качестве входных данных для переобучения последнего слоя модели.</span><span class="sxs-lookup"><span data-stu-id="7a138-147">Once the output values from the bottleneck phase are computed, they are used as input to retrain the final layer of the model.</span></span> <span data-ttu-id="7a138-148">Этот процесс является итеративным и выполняется то количество раз, которое указано в параметрах модели.</span><span class="sxs-lookup"><span data-stu-id="7a138-148">This process is iterative and runs for the number of times specified by model parameters.</span></span> <span data-ttu-id="7a138-149">При каждом запуске вычисляются потери и точность.</span><span class="sxs-lookup"><span data-stu-id="7a138-149">During each run, the loss and accuracy are evaluated.</span></span> <span data-ttu-id="7a138-150">Затем вносятся соответствующие корректировки для улучшения модели с целью минимизации потерь и максимизации точности.</span><span class="sxs-lookup"><span data-stu-id="7a138-150">Then, the appropriate adjustments are made to improve the model with the goal of minimizing the loss and maximizing the accuracy.</span></span> <span data-ttu-id="7a138-151">После завершения обучения выводятся два формата модели.</span><span class="sxs-lookup"><span data-stu-id="7a138-151">Once training is finished, two model formats are output.</span></span> <span data-ttu-id="7a138-152">Один из них — это версия модели `.pb`, а другой — сериализованная ML.NET версия модели `.zip`.</span><span class="sxs-lookup"><span data-stu-id="7a138-152">One of them is the `.pb` version of the model and the other is the `.zip` ML.NET serialized version of the model.</span></span> <span data-ttu-id="7a138-153">При работе в средах, поддерживаемых ML.NET, рекомендуется использовать версию модели `.zip`.</span><span class="sxs-lookup"><span data-stu-id="7a138-153">When working in environments supported by ML.NET, it is recommended to use the `.zip` version of the model.</span></span> <span data-ttu-id="7a138-154">Однако в средах, где ML.NET не поддерживается, можно использовать версию `.pb`.</span><span class="sxs-lookup"><span data-stu-id="7a138-154">However, in environments where ML.NET is not supported, you have the option of using the `.pb` version.</span></span>

## <a name="understand-the-pretrained-model"></a><span data-ttu-id="7a138-155">Описание предварительно обученной модели</span><span class="sxs-lookup"><span data-stu-id="7a138-155">Understand the pretrained model</span></span>

<span data-ttu-id="7a138-156">Предварительно обученная модель, используемая в этом учебнике, представляет собой 101-слойный вариант модели остаточной сети (ResNet) версии 2.</span><span class="sxs-lookup"><span data-stu-id="7a138-156">The pretrained model used in this tutorial is the 101-layer variant of the Residual Network (ResNet) v2 model.</span></span> <span data-ttu-id="7a138-157">Исходная модель обучается для классификации изображений по тысячам категорий.</span><span class="sxs-lookup"><span data-stu-id="7a138-157">The original model is trained to classify images into a thousand categories.</span></span> <span data-ttu-id="7a138-158">Она принимает в качестве входных данных изображение размером 224 на 224 и выводит вероятности для каждого из классов, по которым она обучена.</span><span class="sxs-lookup"><span data-stu-id="7a138-158">The model takes as input an image of size 224 x 224 and outputs the class probabilities for each of the classes it's trained on.</span></span> <span data-ttu-id="7a138-159">Часть этой модели используется для обучения новой модели с помощью пользовательских изображений, чтобы делать прогнозы между двумя классами.</span><span class="sxs-lookup"><span data-stu-id="7a138-159">Part of this model is used to train a new model using custom images to make predictions between two classes.</span></span>

## <a name="create-console-application"></a><span data-ttu-id="7a138-160">Создание консольного приложения</span><span class="sxs-lookup"><span data-stu-id="7a138-160">Create console application</span></span>

<span data-ttu-id="7a138-161">Теперь, когда у вас есть общее представление о передаче обучения и API классификации изображений, пришло время создать приложение.</span><span class="sxs-lookup"><span data-stu-id="7a138-161">Now that you have a general understanding of transfer learning and the Image Classification API, it's time to build the application.</span></span>

1. <span data-ttu-id="7a138-162">Создайте **консольное приложение C# .NET Core** с именем DeepLearning_ImageClassification_Binary.</span><span class="sxs-lookup"><span data-stu-id="7a138-162">Create a **C# .NET Core Console Application** called "DeepLearning_ImageClassification_Binary".</span></span>
1. <span data-ttu-id="7a138-163">Установите пакет NuGet для **Microsoft.ML** версии **1.4.0**.</span><span class="sxs-lookup"><span data-stu-id="7a138-163">Install the **Microsoft.ML** version **1.4.0** NuGet Package:</span></span>
    1. <span data-ttu-id="7a138-164">В обозревателе решений щелкните проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7a138-164">In Solution Explorer, right-click on your project and select **Manage NuGet Packages**.</span></span>
    1. <span data-ttu-id="7a138-165">Выберите nuget.org в качестве источника пакета.</span><span class="sxs-lookup"><span data-stu-id="7a138-165">Choose "nuget.org" as the Package source.</span></span>
    1. <span data-ttu-id="7a138-166">Выберите вкладку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="7a138-166">Select the **Browse** tab.</span></span>
    1. <span data-ttu-id="7a138-167">Установите флажок **Включить предварительные версии**.</span><span class="sxs-lookup"><span data-stu-id="7a138-167">Check the **Include prerelease** checkbox.</span></span>
    1. <span data-ttu-id="7a138-168">Выполните поиск **Microsoft.ML**.</span><span class="sxs-lookup"><span data-stu-id="7a138-168">Search for **Microsoft.ML**.</span></span>
    1. <span data-ttu-id="7a138-169">Нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="7a138-169">Select the **Install** button.</span></span>
    1. <span data-ttu-id="7a138-170">Нажмите кнопку **ОК** в диалоговом окне **Предварительный просмотр изменений**, а затем нажмите кнопку **Принимаю** в диалоговом окне **Принятие условий лицензионного соглашения**, если вы согласны с указанными условиями лицензионного соглашения для выбранных пакетов.</span><span class="sxs-lookup"><span data-stu-id="7a138-170">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the **License Acceptance** dialog if you agree with the license terms for the packages listed.</span></span>
    1. <span data-ttu-id="7a138-171">Повторите эти действия для пакетов NuGet **Microsoft.ML.Vision** версии **1.4.0**, **SciSharp.TensorFlow.Redist** версии **1.15.0** и **Microsoft.ML.ImageAnalytics** версии **1.4.0**.</span><span class="sxs-lookup"><span data-stu-id="7a138-171">Repeat these steps for the **Microsoft.ML.Vision** version **1.4.0**, **SciSharp.TensorFlow.Redist** version **1.15.0**, and **Microsoft.ML.ImageAnalytics** version **1.4.0** NuGet packages.</span></span>

### <a name="prepare-and-understand-the-data"></a><span data-ttu-id="7a138-172">Подготовка и анализ данных</span><span class="sxs-lookup"><span data-stu-id="7a138-172">Prepare and understand the data</span></span>

> [!NOTE]
> <span data-ttu-id="7a138-173">Наборы данных для этого учебника взяты из следующего источника: Maguire, Marc; Dorafshan, Sattar и Thomas, Robert J., "SDNET2018: A concrete crack image dataset for machine learning applications" (2018).</span><span class="sxs-lookup"><span data-stu-id="7a138-173">The datasets for this tutorial are from Maguire, Marc; Dorafshan, Sattar; and Thomas, Robert J., "SDNET2018: A concrete crack image dataset for machine learning applications" (2018).</span></span> <span data-ttu-id="7a138-174">Просмотрите все наборы данных.</span><span class="sxs-lookup"><span data-stu-id="7a138-174">Browse all Datasets.</span></span> <span data-ttu-id="7a138-175">Документ 48.</span><span class="sxs-lookup"><span data-stu-id="7a138-175">Paper 48.</span></span> <span data-ttu-id="7a138-176">https://digitalcommons.usu.edu/all_datasets/48</span><span class="sxs-lookup"><span data-stu-id="7a138-176">https://digitalcommons.usu.edu/all_datasets/48</span></span>

<span data-ttu-id="7a138-177">SDNET2018 — это набор данных изображений, который содержит аннотации для растрескавшихся и нерастрескавшихся бетонных конструкций (эстакады моста, стены и покрытие).</span><span class="sxs-lookup"><span data-stu-id="7a138-177">SDNET2018 is an image dataset that contains annotations for cracked and non-cracked concrete structures (bridge decks, walls, and pavement).</span></span>

![Примеры для эстакад моста из набора данных SDNET2018](./media/image-classification-api-transfer-learning/sdnet2018decksamples.png)

<span data-ttu-id="7a138-179">Эти данные упорядочены по трем подкаталогам:</span><span class="sxs-lookup"><span data-stu-id="7a138-179">The data is organized in three subdirectories:</span></span>

- <span data-ttu-id="7a138-180">D содержит изображения эстакад моста.</span><span class="sxs-lookup"><span data-stu-id="7a138-180">D contains bridge deck images</span></span>
- <span data-ttu-id="7a138-181">P содержит изображения покрытия.</span><span class="sxs-lookup"><span data-stu-id="7a138-181">P contains pavement images</span></span>
- <span data-ttu-id="7a138-182">W содержит изображения стен.</span><span class="sxs-lookup"><span data-stu-id="7a138-182">W contains wall images</span></span>

<span data-ttu-id="7a138-183">Каждый из этих подкаталогов содержит еще два вложенных каталога с префиксами:</span><span class="sxs-lookup"><span data-stu-id="7a138-183">Each of these subdirectories contains two additional prefixed subdirectories:</span></span>

- <span data-ttu-id="7a138-184">Префикс C используется для растрескавшихся поверхностей.</span><span class="sxs-lookup"><span data-stu-id="7a138-184">C is the prefix used for cracked surfaces</span></span>
- <span data-ttu-id="7a138-185">Префикс U используется для нерастрескавшихся поверхностей.</span><span class="sxs-lookup"><span data-stu-id="7a138-185">U is the prefix used for uncracked surfaces</span></span>

<span data-ttu-id="7a138-186">В этом учебнике используются только изображения эстакад моста.</span><span class="sxs-lookup"><span data-stu-id="7a138-186">In this tutorial, only bridge deck images are used.</span></span>

1. <span data-ttu-id="7a138-187">Скачайте [набор данных](https://github.com/dotnet/machinelearning-samples/raw/master/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/assets.zip) и распакуйте его.</span><span class="sxs-lookup"><span data-stu-id="7a138-187">Download the [dataset](https://github.com/dotnet/machinelearning-samples/raw/master/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/assets.zip) and unzip.</span></span>
1. <span data-ttu-id="7a138-188">Создайте каталог с именем "assets" в проекте, чтобы сохранять файлы набора данных.</span><span class="sxs-lookup"><span data-stu-id="7a138-188">Create a directory named "assets" in your project to save your dataset files.</span></span>
1. <span data-ttu-id="7a138-189">Скопируйте подкаталоги *CD* и *UD* из недавно распакованного каталога в каталог *assets*.</span><span class="sxs-lookup"><span data-stu-id="7a138-189">Copy the *CD* and *UD* subdirectories from the recently unzipped directory to the *assets* directory.</span></span>

### <a name="create-input-and-output-classes"></a><span data-ttu-id="7a138-190">Создание классов входных и выходных данных</span><span class="sxs-lookup"><span data-stu-id="7a138-190">Create input and output classes</span></span>

1. <span data-ttu-id="7a138-191">Откройте файл *Program.cs* и замените операторы `using` в его начале следующими:</span><span class="sxs-lookup"><span data-stu-id="7a138-191">Open the *Program.cs* file and replace the existing `using` statements at the top of the file with the following:</span></span>

    [!code-csharp [ProgramUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L1-L7)]

1. <span data-ttu-id="7a138-192">Под классом `Program` в *Program.cs* создайте класс `ImageData`.</span><span class="sxs-lookup"><span data-stu-id="7a138-192">Below the `Program` class in *Program.cs*, create a class called `ImageData`.</span></span> <span data-ttu-id="7a138-193">Этот класс служит для представления начальных загруженных данных.</span><span class="sxs-lookup"><span data-stu-id="7a138-193">This class is used to represent the initially loaded data.</span></span>

    [!code-csharp [ImageDataClass](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L137-L142)]

    <span data-ttu-id="7a138-194">`ImageData` содержит следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="7a138-194">`ImageData` contains the following properties:</span></span>

    - <span data-ttu-id="7a138-195">`ImagePath` — полный путь, по которому хранится изображение.</span><span class="sxs-lookup"><span data-stu-id="7a138-195">`ImagePath` is the fully qualified path where the image is stored.</span></span>
    - <span data-ttu-id="7a138-196">`Label` — категория, к которой принадлежит это изображение.</span><span class="sxs-lookup"><span data-stu-id="7a138-196">`Label` is the category the image belongs to.</span></span> <span data-ttu-id="7a138-197">Это прогнозируемое значение.</span><span class="sxs-lookup"><span data-stu-id="7a138-197">This is the value to predict.</span></span>

1. <span data-ttu-id="7a138-198">Создайте классы для входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="7a138-198">Create classes for your input and output data</span></span>

    1. <span data-ttu-id="7a138-199">Под классом `ImageData` определите схему входных данных в новом классе `ModelInput`.</span><span class="sxs-lookup"><span data-stu-id="7a138-199">Below the `ImageData` class, define the schema of your input data in a new class called `ModelInput`.</span></span>

        [!code-csharp [ModelInputClass](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L144-L153)]

        <span data-ttu-id="7a138-200">`ModelInput` содержит следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="7a138-200">`ModelInput` contains the following properties:</span></span>

        - <span data-ttu-id="7a138-201">`ImagePath` — полный путь, по которому хранится изображение.</span><span class="sxs-lookup"><span data-stu-id="7a138-201">`ImagePath` is the fully qualified path where the image is stored.</span></span>
        - <span data-ttu-id="7a138-202">`Label` — категория, к которой принадлежит это изображение.</span><span class="sxs-lookup"><span data-stu-id="7a138-202">`Label` is the category the image belongs to.</span></span> <span data-ttu-id="7a138-203">Это прогнозируемое значение.</span><span class="sxs-lookup"><span data-stu-id="7a138-203">This is the value to predict.</span></span>
        - <span data-ttu-id="7a138-204">`Image` является представлением изображения `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="7a138-204">`Image` is the `byte[]` representation of the image.</span></span> <span data-ttu-id="7a138-205">Модель ожидает, что для обучения используются данные изображений этого типа.</span><span class="sxs-lookup"><span data-stu-id="7a138-205">The model expects image data to be of this type for training.</span></span>
        - <span data-ttu-id="7a138-206">`LabelAsKey` является численным представлением `Label`.</span><span class="sxs-lookup"><span data-stu-id="7a138-206">`LabelAsKey` is the numerical representation of the `Label`.</span></span>

        <span data-ttu-id="7a138-207">Только `Image` и `LabelAsKey` используются для обучения модели и составления прогнозов.</span><span class="sxs-lookup"><span data-stu-id="7a138-207">Only `Image` and `LabelAsKey` are used to train the model and make predictions.</span></span> <span data-ttu-id="7a138-208">Свойства `ImagePath` и `Label` хранятся на случай обращения к имени и категории исходного файла изображения.</span><span class="sxs-lookup"><span data-stu-id="7a138-208">The `ImagePath` and `Label` properties are kept for convenience to access the original image file name and category.</span></span>

    1. <span data-ttu-id="7a138-209">Затем под классом `ModelInput` определите схему выходных данных в новом классе `ModelOutput`.</span><span class="sxs-lookup"><span data-stu-id="7a138-209">Then, below the `ModelInput` class, define the schema of your output data in a new class called `ModelOutput`.</span></span>

        [!code-csharp [ModelOutputClass](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L155-L162)]

        <span data-ttu-id="7a138-210">`ModelOutput` содержит следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="7a138-210">`ModelOutput` contains the following properties:</span></span>

        - <span data-ttu-id="7a138-211">`ImagePath` — полный путь, по которому хранится изображение.</span><span class="sxs-lookup"><span data-stu-id="7a138-211">`ImagePath` is the fully qualified path where the image is stored.</span></span>
        - <span data-ttu-id="7a138-212">`Label` — исходная категория, к которой принадлежит это изображение.</span><span class="sxs-lookup"><span data-stu-id="7a138-212">`Label` is the original category the image belongs to.</span></span> <span data-ttu-id="7a138-213">Это прогнозируемое значение.</span><span class="sxs-lookup"><span data-stu-id="7a138-213">This is the value to predict.</span></span>
        - <span data-ttu-id="7a138-214">`PredictedLabel` — значение, спрогнозированное моделью.</span><span class="sxs-lookup"><span data-stu-id="7a138-214">`PredictedLabel` is the value predicted by the model.</span></span>

        <span data-ttu-id="7a138-215">По аналогии с `ModelInput`, для создания прогнозов требуется только `PredictedLabel`, так как оно содержит прогноз, выполненный моделью.</span><span class="sxs-lookup"><span data-stu-id="7a138-215">Similar to `ModelInput`, only the `PredictedLabel` is required to make predictions since it contains the prediction made by the model.</span></span> <span data-ttu-id="7a138-216">Свойства `ImagePath` и `Label` хранятся на случай обращения к имени и категории исходного файла изображения.</span><span class="sxs-lookup"><span data-stu-id="7a138-216">The `ImagePath` and `Label` properties are retained for convenience to access the original image file name and category.</span></span>

### <a name="create-workspace-directory"></a><span data-ttu-id="7a138-217">Создание каталога рабочей области</span><span class="sxs-lookup"><span data-stu-id="7a138-217">Create workspace directory</span></span>

<span data-ttu-id="7a138-218">Если данные для обучения и проверки не изменяются часто, рекомендуется кэшировать вычисленные значения узких мест для дальнейших запусков.</span><span class="sxs-lookup"><span data-stu-id="7a138-218">When training and validation data do not change often, it is good practice to cache the computed bottleneck values for further runs.</span></span>

1. <span data-ttu-id="7a138-219">Создайте в проекте новый каталог с именем *workspace*, чтобы сохранить вычисленные значения узких мест и версию `.pb` модели.</span><span class="sxs-lookup"><span data-stu-id="7a138-219">In your project, create a new directory called *workspace* to store the computed bottleneck values and `.pb` version of the model.</span></span>

### <a name="define-paths-and-initialize-variables"></a><span data-ttu-id="7a138-220">Определение путей и инициализация переменных</span><span class="sxs-lookup"><span data-stu-id="7a138-220">Define paths and initialize variables</span></span>

1. <span data-ttu-id="7a138-221">В методе `Main` определите расположение ресурсов, вычисленные значения узких мест и версию `.pb` модели.</span><span class="sxs-lookup"><span data-stu-id="7a138-221">Inside the `Main` method, define the location of your assets, computed bottleneck values and `.pb` version of the model.</span></span>

    [!code-csharp [DefinePaths](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L15-L17)]

1. <span data-ttu-id="7a138-222">Затем инициализируйте переменную `mlContext` с помощью нового экземпляра [MLContext](xref:Microsoft.ML.MLContext).</span><span class="sxs-lookup"><span data-stu-id="7a138-222">Then, initialize the `mlContext` variable with a new instance of [MLContext](xref:Microsoft.ML.MLContext).</span></span>

    [!code-csharp [MLContext](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L19)]

    <span data-ttu-id="7a138-223">Класс [MLContext](xref:Microsoft.ML.MLContext) является отправной точкой для любых операций ML.NET. В результате инициализации mlContext создается среда ML.NET, которая может использоваться всеми объектами в рамках процесса создания модели.</span><span class="sxs-lookup"><span data-stu-id="7a138-223">The [MLContext](xref:Microsoft.ML.MLContext) class is a starting point for all ML.NET operations, and initializing mlContext creates a new ML.NET environment that can be shared across the model creation workflow objects.</span></span> <span data-ttu-id="7a138-224">По существу он аналогичен классу `DBContext` в Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="7a138-224">It's similar, conceptually, to `DBContext` in Entity Framework.</span></span>

## <a name="load-the-data"></a><span data-ttu-id="7a138-225">Загрузка данных</span><span class="sxs-lookup"><span data-stu-id="7a138-225">Load the data</span></span>

### <a name="create-data-loading-utility-method"></a><span data-ttu-id="7a138-226">Создание служебного метода для загрузки данных</span><span class="sxs-lookup"><span data-stu-id="7a138-226">Create data loading utility method</span></span>

<span data-ttu-id="7a138-227">Изображения хранятся в двух подкаталогах.</span><span class="sxs-lookup"><span data-stu-id="7a138-227">The images are stored in two subdirectories.</span></span> <span data-ttu-id="7a138-228">Перед загрузкой данных их необходимо отформатировать в виде списка объектов `ImageData`.</span><span class="sxs-lookup"><span data-stu-id="7a138-228">Before loading the data, it needs to be formatted into a list of `ImageData` objects.</span></span> <span data-ttu-id="7a138-229">Для этого создайте метод `LoadImagesFromDirectory` под методом `Main`.</span><span class="sxs-lookup"><span data-stu-id="7a138-229">To do so, create the `LoadImagesFromDirectory` method below the `Main` method.</span></span>

```csharp
public static IEnumerable<ImageData> LoadImagesFromDirectory(string folder, bool useFolderNameAsLabel = true)
{

}
```

1. <span data-ttu-id="7a138-230">Внутри `LoadImagesDirectory` добавьте следующий код, чтобы получить все пути к файлам из подкаталогов:</span><span class="sxs-lookup"><span data-stu-id="7a138-230">Inside the `LoadImagesDirectory` add the following code to get all of the file paths from the subdirectories:</span></span>

    [!code-csharp [GetFiles](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L104-L105)]

1. <span data-ttu-id="7a138-231">Затем выполните итерацию по каждому из файлов, используя оператор `foreach`.</span><span class="sxs-lookup"><span data-stu-id="7a138-231">Then, iterate through each of the files using a `foreach` statement.</span></span>

    ```csharp
    foreach (var file in files)
    {

    }
    ```

1. <span data-ttu-id="7a138-232">Внутри оператора `foreach` убедитесь, что поддерживаются расширения файлов.</span><span class="sxs-lookup"><span data-stu-id="7a138-232">Inside the `foreach` statement, check that the file extensions are supported.</span></span> <span data-ttu-id="7a138-233">API классификации изображений поддерживает форматы JPEG и PNG.</span><span class="sxs-lookup"><span data-stu-id="7a138-233">The Image Classification API supports JPEG and PNG formats.</span></span>

    [!code-csharp [CheckExtension](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L109-L110)]

1. <span data-ttu-id="7a138-234">Затем получите метку для файла.</span><span class="sxs-lookup"><span data-stu-id="7a138-234">Then, get the label for the file.</span></span> <span data-ttu-id="7a138-235">Если параметр `useFolderNameAsLabel` имеет значение `true`, то в качестве метки используется родительский каталог, где сохранен файл.</span><span class="sxs-lookup"><span data-stu-id="7a138-235">If the `useFolderNameAsLabel` parameter is set to `true`, then the parent directory where the file is saved is used as the label.</span></span> <span data-ttu-id="7a138-236">В противном случае ожидается, что метка будет именем файла или его префиксом.</span><span class="sxs-lookup"><span data-stu-id="7a138-236">Otherwise, it expects the label to be a prefix of the file name or the file name itself.</span></span>

    [!code-csharp [GetLabel](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L112-L126)]

1. <span data-ttu-id="7a138-237">Наконец, создайте экземпляр класса `ModelInput`.</span><span class="sxs-lookup"><span data-stu-id="7a138-237">Finally, create a new instance of `ModelInput`.</span></span>

    [!code-csharp [CreateImageData](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L128-L132)]

### <a name="prepare-the-data"></a><span data-ttu-id="7a138-238">Подготовка данных</span><span class="sxs-lookup"><span data-stu-id="7a138-238">Prepare the data</span></span>

1. <span data-ttu-id="7a138-239">Вернувшись в метод `Main`, используйте служебный метод `LoadFromDirectory`, чтобы получить список изображений, используемых для обучения.</span><span class="sxs-lookup"><span data-stu-id="7a138-239">Back in the `Main` method, use the `LoadFromDirectory` utility method to get the list of images used for training.</span></span>

    [!code-csharp [LoadImages](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L21)]

1. <span data-ttu-id="7a138-240">Затем загрузите эти изображения в [`IDataView`](xref:Microsoft.ML.IDataView) с помощью метода [`LoadFromEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.LoadFromEnumerable*).</span><span class="sxs-lookup"><span data-stu-id="7a138-240">Then, load the images into an [`IDataView`](xref:Microsoft.ML.IDataView) using the [`LoadFromEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.LoadFromEnumerable*) method.</span></span>

    [!code-csharp [CreateIDataView](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L23)]

1. <span data-ttu-id="7a138-241">Данные загружаются в том порядке, в котором они были считаны из каталогов.</span><span class="sxs-lookup"><span data-stu-id="7a138-241">The data is loaded in the order it was read from the directories.</span></span> <span data-ttu-id="7a138-242">Чтобы сбалансировать данные, перемешайте их в случайном порядке с помощью метода [`ShuffleRows`](xref:Microsoft.ML.DataOperationsCatalog.ShuffleRows*).</span><span class="sxs-lookup"><span data-stu-id="7a138-242">To balance the data, shuffle it using the [`ShuffleRows`](xref:Microsoft.ML.DataOperationsCatalog.ShuffleRows*) method.</span></span>

    [!code-csharp [ShuffleRows](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L25)]

1. <span data-ttu-id="7a138-243">Модели машинного обучения ожидают входные данные в числовом формате.</span><span class="sxs-lookup"><span data-stu-id="7a138-243">Machine learning models expect input to be in numerical format.</span></span> <span data-ttu-id="7a138-244">Поэтому перед обучением необходимо выполнить некоторую предварительную обработку данных.</span><span class="sxs-lookup"><span data-stu-id="7a138-244">Therefore, some preprocessing needs to be done on the data prior to training.</span></span> <span data-ttu-id="7a138-245">Создайте класс [`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601), состоящий из преобразований [`MapValueToKey`](xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValueToKey*) и `LoadRawImageBytes`.</span><span class="sxs-lookup"><span data-stu-id="7a138-245">Create an [`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601) made up of the [`MapValueToKey`](xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValueToKey*) and `LoadRawImageBytes` transforms.</span></span> <span data-ttu-id="7a138-246">Преобразование `MapValueToKey` принимает значение категории в столбце `Label`, преобразует его в числовое значение `KeyType` и сохраняет в новом столбце `LabelAsKey`.</span><span class="sxs-lookup"><span data-stu-id="7a138-246">The `MapValueToKey` transform takes the categorical value in the `Label` column, converts it to a numerical `KeyType` value and stores it in a new column called `LabelAsKey`.</span></span> <span data-ttu-id="7a138-247">`LoadImages` принимает значения из столбца `ImagePath` вместе с параметром `imageFolder` для загрузки изображений для обучения.</span><span class="sxs-lookup"><span data-stu-id="7a138-247">The `LoadImages` takes the values from the `ImagePath` column along with the `imageFolder` parameter to load images for training.</span></span>

    [!code-csharp [PreprocessingPipeline](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L27-L33)]

1. <span data-ttu-id="7a138-248">Используйте метод [`Fit`](xref:Microsoft.ML.Data.EstimatorChain%601.Fit*), чтобы применить данные к `preprocessingPipeline` [`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601), а затем метод [`Transform`](xref:Microsoft.ML.Data.TransformerChain`1.Transform*), который возвращает [`IDataView`](xref:Microsoft.ML.IDataView), содержащий предварительно обработанные данные.</span><span class="sxs-lookup"><span data-stu-id="7a138-248">Use the [`Fit`](xref:Microsoft.ML.Data.EstimatorChain%601.Fit*) method to apply the data to the `preprocessingPipeline` [`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601) followed by the [`Transform`](xref:Microsoft.ML.Data.TransformerChain`1.Transform*) method, which returns an [`IDataView`](xref:Microsoft.ML.IDataView) containing the pre-processed data.</span></span>

    [!code-csharp [PreprocessData](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L35-L37)]

1. <span data-ttu-id="7a138-249">Для обучения модели важно иметь набор данных для обучения и проверочный набор данных.</span><span class="sxs-lookup"><span data-stu-id="7a138-249">To train a model, it's important to have a training dataset as well as a validation dataset.</span></span> <span data-ttu-id="7a138-250">Модель обучается на наборе для обучения.</span><span class="sxs-lookup"><span data-stu-id="7a138-250">The model is trained on the training set.</span></span> <span data-ttu-id="7a138-251">То, насколько точно она делает прогнозы по неизвестным данным, оценивается с точки зрения эффективности по сравнению с проверочным набором.</span><span class="sxs-lookup"><span data-stu-id="7a138-251">How well it makes predictions on unseen data is measured by the performance against the validation set.</span></span> <span data-ttu-id="7a138-252">В зависимости от достигнутой эффективности модель вносит корректировки в то, что она изучила, для улучшения результата.</span><span class="sxs-lookup"><span data-stu-id="7a138-252">Based on the results of that performance, the model makes adjustments to what it has learned in an effort to improve.</span></span> <span data-ttu-id="7a138-253">Проверочный набор можно получить, разделив исходный набор данных, либо из другого источника, который уже был подобран специально для этого.</span><span class="sxs-lookup"><span data-stu-id="7a138-253">The validation set can come from either splitting your original dataset or from another source that has already been set aside for this purpose.</span></span> <span data-ttu-id="7a138-254">В данном случае предварительно обработанный набор данных разделяется на наборы для обучения, проверки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="7a138-254">In this case, the pre-processed dataset is split into training, validation and test sets.</span></span>

    [!code-csharp [CreateDataSplits](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L39-L40)]

    <span data-ttu-id="7a138-255">В приведенном выше примере кода выполняется два разделения.</span><span class="sxs-lookup"><span data-stu-id="7a138-255">The code sample above performs two splits.</span></span> <span data-ttu-id="7a138-256">Сначала предварительно обработанные данные разделяются в следующей пропорции: 70 % для обучения и оставшиеся 30 % для проверки.</span><span class="sxs-lookup"><span data-stu-id="7a138-256">First, the pre-processed data is split and 70% is used for training while the remaining 30% is used for validation.</span></span> <span data-ttu-id="7a138-257">Затем 30-процентный проверочный набор снова разделяется на наборы для проверки и тестирования в следующей пропорции: 90 % для проверки и 10 % для тестирования.</span><span class="sxs-lookup"><span data-stu-id="7a138-257">Then, the 30% validation set is further split into validation and test sets where 90% is used for validation and 10% is used for testing.</span></span>

    <span data-ttu-id="7a138-258">Аналогом такого разделения данных может быть сдача экзамена.</span><span class="sxs-lookup"><span data-stu-id="7a138-258">A way to think about the purpose of these data partitions is taking an exam.</span></span> <span data-ttu-id="7a138-259">При подготовке к экзамену вы изучаете заметки, книги или другие ресурсы, чтобы получить представление об основных понятиях, о которых спрашивают на экзамене.</span><span class="sxs-lookup"><span data-stu-id="7a138-259">When studying for an exam, you review your notes, books, or other resources to get a grasp on the concepts that are on the exam.</span></span> <span data-ttu-id="7a138-260">Именно для этого и предназначен набор обучения.</span><span class="sxs-lookup"><span data-stu-id="7a138-260">This is what the train set is for.</span></span> <span data-ttu-id="7a138-261">Затем вы можете пройти пробный экзамен, чтобы проверить свои знания.</span><span class="sxs-lookup"><span data-stu-id="7a138-261">Then, you might take a mock exam to validate your knowledge.</span></span> <span data-ttu-id="7a138-262">Именно здесь может пригодиться набор проверки.</span><span class="sxs-lookup"><span data-stu-id="7a138-262">This is where the validation set comes in handy.</span></span> <span data-ttu-id="7a138-263">Вы хотите убедиться, что правильно уловили смысл основных понятий, прежде сдавать настоящий экзамен.</span><span class="sxs-lookup"><span data-stu-id="7a138-263">You want to check whether you have a good grasp of the concepts before taking the actual exam.</span></span> <span data-ttu-id="7a138-264">Основываясь на этих результатах, вы определяете, что именно вы недопоняли или поняли неправильно, и вносите соответствующие изменения в процесс подготовки к настоящему экзамену.</span><span class="sxs-lookup"><span data-stu-id="7a138-264">Based on those results, you take note of what you got wrong or didn't understand well and incorporate your changes as you review for the real exam.</span></span> <span data-ttu-id="7a138-265">Наконец, вы сдаете сам экзамен.</span><span class="sxs-lookup"><span data-stu-id="7a138-265">Finally, you take the exam.</span></span> <span data-ttu-id="7a138-266">Именно для этого и предназначен набор для тестирования.</span><span class="sxs-lookup"><span data-stu-id="7a138-266">This is what the test set is used for.</span></span> <span data-ttu-id="7a138-267">Вы никогда не сталкивались с вопросами, которые спрашивают на экзамене, и теперь применяете знания, полученные в ходе обучения и проверки, для решения рассматриваемой задачи.</span><span class="sxs-lookup"><span data-stu-id="7a138-267">You've never seen the questions that are on the exam and now use what you learned from training and validation to apply your knowledge to the task at hand.</span></span>

1. <span data-ttu-id="7a138-268">Назначьте сегментам соответствующие значения для данных обучения, проверки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="7a138-268">Assign the partitions their respective values for the train, validation and test data.</span></span>

    [!code-csharp [CreateDatasets](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L42-L44)]

## <a name="define-the-training-pipeline"></a><span data-ttu-id="7a138-269">Определение конвейера обучения</span><span class="sxs-lookup"><span data-stu-id="7a138-269">Define the training pipeline</span></span>

<span data-ttu-id="7a138-270">Обучение модели состоит из нескольких шагов.</span><span class="sxs-lookup"><span data-stu-id="7a138-270">Model training consists of a couple of steps.</span></span> <span data-ttu-id="7a138-271">Сначала для обучения модели используется API классификации изображений.</span><span class="sxs-lookup"><span data-stu-id="7a138-271">First, Image Classification API is used to train the model.</span></span> <span data-ttu-id="7a138-272">Затем закодированные метки в столбце `PredictedLabel` преобразуются обратно в исходное значение категории с помощью преобразования `MapKeyToValue`.</span><span class="sxs-lookup"><span data-stu-id="7a138-272">Then, the encoded labels in the `PredictedLabel` column are converted back to their original categorical value using the `MapKeyToValue` transform.</span></span>

1. <span data-ttu-id="7a138-273">Создайте новую переменную для хранения набора обязательных и необязательных параметров для `ImageClassificationTrainer`.</span><span class="sxs-lookup"><span data-stu-id="7a138-273">Create a new variable to store a set of required and optional parameters for an `ImageClassificationTrainer`.</span></span> 

    [!code-csharp [ClassifierOptions](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L46-L57)]

    <span data-ttu-id="7a138-274">`ImageClassificationTrainer` принимает несколько необязательных параметров:</span><span class="sxs-lookup"><span data-stu-id="7a138-274">An `ImageClassificationTrainer` takes several optional parameters:</span></span>

    - <span data-ttu-id="7a138-275">`FeatureColumnName` — столбец, используемый в качестве входных данных для модели.</span><span class="sxs-lookup"><span data-stu-id="7a138-275">`FeatureColumnName` is the column that is used as input for the model.</span></span>
    - <span data-ttu-id="7a138-276">`LabelColumnName` — столбец для прогнозируемого значения.</span><span class="sxs-lookup"><span data-stu-id="7a138-276">`LabelColumnName` is the column for the value to predict.</span></span>
    - <span data-ttu-id="7a138-277">`ValidationSet` является [`IDataView`](xref:Microsoft.ML.IDataView), содержащим проверочные данные.</span><span class="sxs-lookup"><span data-stu-id="7a138-277">`ValidationSet` is the [`IDataView`](xref:Microsoft.ML.IDataView) containing the validation data.</span></span>
    - <span data-ttu-id="7a138-278">`Arch` определяет, какую из архитектур предварительно обученной модели нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="7a138-278">`Arch` defines which of the pretrained model architectures to use.</span></span> <span data-ttu-id="7a138-279">В этом учебнике используется 101-слойный вариант модели ResNetv2.</span><span class="sxs-lookup"><span data-stu-id="7a138-279">This tutorial uses the 101-layer variant of the ResNetv2 model.</span></span>
    - <span data-ttu-id="7a138-280">`MetricsCallback` привязывает функцию для отслеживания хода выполнения во время обучения.</span><span class="sxs-lookup"><span data-stu-id="7a138-280">`MetricsCallback` binds a function to track the progress during training.</span></span>
    - <span data-ttu-id="7a138-281">`TestOnTrainSet` указывает модели измерять эффективность относительно обучающего набора, если проверочный набор отсутствует.</span><span class="sxs-lookup"><span data-stu-id="7a138-281">`TestOnTrainSet` tells the model to measure performance against the training set when no validation set is present.</span></span>
    - <span data-ttu-id="7a138-282">`ReuseTrainSetBottleneckCachedValues` сообщает модели, следует ли использовать кэшированные значения из этапа узкого места при последующих запусках.</span><span class="sxs-lookup"><span data-stu-id="7a138-282">`ReuseTrainSetBottleneckCachedValues` tells the model whether to use the cached values from the bottleneck phase in subsequent runs.</span></span> <span data-ttu-id="7a138-283">Этап узкого места представляет собой однократное сквозное вычисление, которое потребляет много ресурсов при первом выполнении.</span><span class="sxs-lookup"><span data-stu-id="7a138-283">The bottleneck phase is a one-time pass-through computation that is computationally intensive the first time it is performed.</span></span> <span data-ttu-id="7a138-284">Если данные для обучения не изменяются и вы хотите поэкспериментировать с разным числом эпох или разными размерами пакета, использование кэшированных значений значительно сокращает время, необходимое для обучения модели.</span><span class="sxs-lookup"><span data-stu-id="7a138-284">If the training data does not change and you want to experiment using a different number of epochs or batch size, using the cached values significantly reduces the amount of time required to train a model.</span></span>
    - <span data-ttu-id="7a138-285">`ReuseValidationSetBottleneckCachedValues` аналогичен `ReuseTrainSetBottleneckCachedValues`, только в данном случае он предназначен для проверочного набора данных.</span><span class="sxs-lookup"><span data-stu-id="7a138-285">`ReuseValidationSetBottleneckCachedValues` is similar to `ReuseTrainSetBottleneckCachedValues` only that in this case it's for the validation dataset.</span></span>
    - <span data-ttu-id="7a138-286">`WorkspacePath`определяет каталог, в котором хранятся вычисленные значения узких мест и версия `.pb` модели.</span><span class="sxs-lookup"><span data-stu-id="7a138-286">`WorkspacePath` defines the directory where to store the computed bottleneck values and `.pb` version of the model.</span></span>

1. <span data-ttu-id="7a138-287">Определите конвейер обучения [`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601), состоящий из преобразований `mapLabelEstimator` и `ImageClassificationTrainer`.</span><span class="sxs-lookup"><span data-stu-id="7a138-287">Define the [`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601) training pipeline that consists of both the `mapLabelEstimator` and the `ImageClassificationTrainer`.</span></span>

    [!code-csharp [TrainingPipeline](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L59-L60)]

1. <span data-ttu-id="7a138-288">Используйте метод [`Fit`](xref:Microsoft.ML.Data.EstimatorChain%601.Fit*) для обучения модели.</span><span class="sxs-lookup"><span data-stu-id="7a138-288">Use the [`Fit`](xref:Microsoft.ML.Data.EstimatorChain%601.Fit*) method to train your model.</span></span>

    [!code-csharp [TrainModel](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L62)]

## <a name="use-the-model"></a><span data-ttu-id="7a138-289">Использование модели</span><span class="sxs-lookup"><span data-stu-id="7a138-289">Use the model</span></span>

<span data-ttu-id="7a138-290">Теперь, когда вы обучили модель, пора использовать ее для классификации изображений.</span><span class="sxs-lookup"><span data-stu-id="7a138-290">Now that you have trained your model, it's time to use it to classify images.</span></span>

<span data-ttu-id="7a138-291">Под методом `Main` создайте служебный метод `OutputPrediction`, чтобы отобразить сведения о прогнозе в консоли.</span><span class="sxs-lookup"><span data-stu-id="7a138-291">Below the `Main` method, create a new utility method called `OutputPrediction` to display prediction information in the console.</span></span>

[!code-csharp [OuputPredictionMethod](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L96-L100)]

### <a name="classify-a-single-image"></a><span data-ttu-id="7a138-292">Классификация одного изображения</span><span class="sxs-lookup"><span data-stu-id="7a138-292">Classify a single image</span></span>

1. <span data-ttu-id="7a138-293">Добавьте новый метод `ClassifySingleImage` под методом `Main`, чтобы создать и вывести прогноз для одного изображения.</span><span class="sxs-lookup"><span data-stu-id="7a138-293">Add a new method called `ClassifySingleImage` below the `Main` method to make and output a single image prediction.</span></span>

    ```csharp
    public static void ClassifySingleImage(MLContext mlContext, IDataView data, ITransformer trainedModel)
    {

    }
    ```

1. <span data-ttu-id="7a138-294">Создайте [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) в методе `ClassifySingleImage`.</span><span class="sxs-lookup"><span data-stu-id="7a138-294">Create a [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) inside the `ClassifySingleImage` method.</span></span> <span data-ttu-id="7a138-295">[`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) представляет собой удобный API, позволяющий передать один экземпляр данных и осуществить прогнозирование на его основе.</span><span class="sxs-lookup"><span data-stu-id="7a138-295">The [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) is a convenience API, which allows you to pass in and then perform a prediction on a single instance of data.</span></span>

    [!code-csharp [CreatePredictionEngine](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L73)]

1. <span data-ttu-id="7a138-296">Чтобы обратиться к одному экземпляру `ModelInput`, преобразуйте `data` [`IDataView`](xref:Microsoft.ML.IDataView) в [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) с помощью метода [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*), а затем получите первое наблюдение.</span><span class="sxs-lookup"><span data-stu-id="7a138-296">To access a single `ModelInput` instance, convert the `data` [`IDataView`](xref:Microsoft.ML.IDataView) into an [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) using the [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*) method and then get the first observation.</span></span>

    [!code-csharp [GetTestInputData](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L75)]

1. <span data-ttu-id="7a138-297">Используйте метод [`Predict`](xref:Microsoft.ML.PredictionEngine%602.Predict*) для классификации изображения.</span><span class="sxs-lookup"><span data-stu-id="7a138-297">Use the [`Predict`](xref:Microsoft.ML.PredictionEngine%602.Predict*) method to classify the image.</span></span>

    [!code-csharp [MakeSinglePrediction](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L77)]

1. <span data-ttu-id="7a138-298">Выведите прогноз на консоль с помощью метода `OutputPrediction`.</span><span class="sxs-lookup"><span data-stu-id="7a138-298">Output the prediction to the console with the `OutputPrediction` method.</span></span>

    [!code-csharp [OuputSinglePrediction](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L79-L80)]

1. <span data-ttu-id="7a138-299">В методе `Main` вызовите `ClassifySingleImage`, используя тестовый набор изображений.</span><span class="sxs-lookup"><span data-stu-id="7a138-299">Inside the `Main` method, call `ClassifySingleImage` using the test set of images.</span></span>

    [!code-csharp [ClassifySingleImage](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L64)]

### <a name="classify-multiple-images"></a><span data-ttu-id="7a138-300">Классификация нескольких изображений</span><span class="sxs-lookup"><span data-stu-id="7a138-300">Classify multiple images</span></span>

1. <span data-ttu-id="7a138-301">Добавьте новый метод `ClassifyImages` под методом `ClassifySingleImage`, чтобы создать и вывести прогноз для нескольких изображений.</span><span class="sxs-lookup"><span data-stu-id="7a138-301">Add a new method called `ClassifyImages` below the `ClassifySingleImage` method to make and output multiple image predictions.</span></span>

    ```csharp
    public static void ClassifyImages(MLContext mlContext, IDataView data, ITransformer trainedModel)
    {

    }
    ```

1. <span data-ttu-id="7a138-302">Создайте [`IDataView`](xref:Microsoft.ML.IDataView), содержащий прогнозы, с помощью метода [`Transform`](xref:Microsoft.ML.ITransformer.Transform*).</span><span class="sxs-lookup"><span data-stu-id="7a138-302">Create an [`IDataView`](xref:Microsoft.ML.IDataView) containing the predictions by using the [`Transform`](xref:Microsoft.ML.ITransformer.Transform*) method.</span></span> <span data-ttu-id="7a138-303">Добавьте следующий код в метод `ClassifyImages`.</span><span class="sxs-lookup"><span data-stu-id="7a138-303">Add the following code inside the `ClassifyImages` method.</span></span>

    [!code-csharp [MakeMultiplePredictions](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L85)]

1. <span data-ttu-id="7a138-304">Чтобы выполнить итерацию по прогнозам, преобразуйте `predictionData` [`IDataView`](xref:Microsoft.ML.IDataView) в [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) с помощью метода [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*), а затем получите первые 10 наблюдений.</span><span class="sxs-lookup"><span data-stu-id="7a138-304">In order to iterate over the predictions, convert the `predictionData` [`IDataView`](xref:Microsoft.ML.IDataView) into an [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601) using the [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*) method and then get the first 10 observations.</span></span>

    [!code-csharp [IEnumerablePredictions](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L87)]

1. <span data-ttu-id="7a138-305">Выполните итерацию и выведите исходные и прогнозируемые метки для прогнозов.</span><span class="sxs-lookup"><span data-stu-id="7a138-305">Iterate and output the original and predicted labels for the predictions.</span></span>

    [!code-csharp [OutputMultiplePredictions](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L89-L93)]

1. <span data-ttu-id="7a138-306">Наконец, в методе `Main` вызовите `ClassifyImages`, используя тестовый набор изображений.</span><span class="sxs-lookup"><span data-stu-id="7a138-306">Finally, inside the `Main` method, call `ClassifyImages` using the test set of images.</span></span>

    [!code-csharp [ClassifyImages](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ImageClassification_Binary/DeepLearning_ImageClassification_Binary/Program.cs#L66)]

## <a name="run-the-application"></a><span data-ttu-id="7a138-307">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="7a138-307">Run the application</span></span>

<span data-ttu-id="7a138-308">Запустите консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="7a138-308">Run your console app.</span></span> <span data-ttu-id="7a138-309">Должен быть получен результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="7a138-309">The output should be similar to that below.</span></span> <span data-ttu-id="7a138-310">Кроме того, могут выводиться предупреждения или сообщения об обработке, но для удобства здесь мы убрали их.</span><span class="sxs-lookup"><span data-stu-id="7a138-310">You may see warnings or processing messages, but these messages have been removed from the following results for clarity.</span></span> <span data-ttu-id="7a138-311">Для краткости выходные данные были сжаты.</span><span class="sxs-lookup"><span data-stu-id="7a138-311">For brevity, the output has been condensed.</span></span>

<span data-ttu-id="7a138-312">**Этап узкого места**</span><span class="sxs-lookup"><span data-stu-id="7a138-312">**Bottleneck phase**</span></span>

<span data-ttu-id="7a138-313">Значение для имени изображения не выводится, так как изображения загружаются в виде `byte[]`, поэтому выводимое имя изображения отсутствует.</span><span class="sxs-lookup"><span data-stu-id="7a138-313">No value is printed for the image name because the images are loaded as a `byte[]` therefore there is no image name to display.</span></span>

```test
Phase: Bottleneck Computation, Dataset used:      Train, Image Index: 279
Phase: Bottleneck Computation, Dataset used:      Train, Image Index: 280
Phase: Bottleneck Computation, Dataset used: Validation, Image Index:   1
Phase: Bottleneck Computation, Dataset used: Validation, Image Index:   2
```

<span data-ttu-id="7a138-314">**Этап обучения**</span><span class="sxs-lookup"><span data-stu-id="7a138-314">**Training phase**</span></span>

```text
Phase: Training, Dataset used: Validation, Batch Processed Count:   6, Epoch:  21, Accuracy:  0.6797619
Phase: Training, Dataset used: Validation, Batch Processed Count:   6, Epoch:  22, Accuracy:  0.7642857
Phase: Training, Dataset used: Validation, Batch Processed Count:   6, Epoch:  23, Accuracy:  0.7916667
```

<span data-ttu-id="7a138-315">**Выходные данные классификации изображений**</span><span class="sxs-lookup"><span data-stu-id="7a138-315">**Classify images output**</span></span>

```text
Classifying single image
Image: 7001-220.jpg | Actual Value: UD | Predicted Value: UD

Classifying multiple images
Image: 7001-220.jpg | Actual Value: UD | Predicted Value: UD
Image: 7001-163.jpg | Actual Value: UD | Predicted Value: UD
Image: 7001-210.jpg | Actual Value: UD | Predicted Value: UD
```

<span data-ttu-id="7a138-316">После проверки изображения *7001-220.jpg* можно увидеть, что на самом деле на нем отсутствуют трещины.</span><span class="sxs-lookup"><span data-stu-id="7a138-316">Upon inspection of the *7001-220.jpg* image, you can see that it in fact is not cracked.</span></span>

![Изображение набора данных SDNET2018, используемое для прогнозирования](./media/image-classification-api-transfer-learning/predictedimage.jpg)

<span data-ttu-id="7a138-318">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="7a138-318">Congratulations!</span></span> <span data-ttu-id="7a138-319">Вы успешно создали модель глубокого обучения для классификации изображений.</span><span class="sxs-lookup"><span data-stu-id="7a138-319">You've now successfully built a deep learning model for classifying images.</span></span>

### <a name="improve-the-model"></a><span data-ttu-id="7a138-320">Улучшение модели</span><span class="sxs-lookup"><span data-stu-id="7a138-320">Improve the model</span></span>

<span data-ttu-id="7a138-321">Если вы не удовлетворены результатами работы модели, можно попытаться улучшить ее эффективность с помощью следующих подходов:</span><span class="sxs-lookup"><span data-stu-id="7a138-321">If you're not satisfied with the results of your model, you can try to improve its performance by trying some of the following approaches:</span></span>

- <span data-ttu-id="7a138-322">**Увеличение объема данных**: чем больше примеров, на которых обучается модель, тем лучше она работает.</span><span class="sxs-lookup"><span data-stu-id="7a138-322">**More Data**: The more examples a model learns from, the better it performs.</span></span> <span data-ttu-id="7a138-323">Скачайте полный [набор данных SDNET2018](https://digitalcommons.usu.edu/cgi/viewcontent.cgi?filename=2&article=1047&context=all_datasets&type=additional) и используйте его для обучения.</span><span class="sxs-lookup"><span data-stu-id="7a138-323">Download the full [SDNET2018 dataset](https://digitalcommons.usu.edu/cgi/viewcontent.cgi?filename=2&article=1047&context=all_datasets&type=additional) and use it to train.</span></span>
- <span data-ttu-id="7a138-324">**Дополнение данных**: часто, чтобы сделать данные более разнообразными, их дополняют, преобразуя изображение различным образом (поворот, отражение, сдвиг, обрезка).</span><span class="sxs-lookup"><span data-stu-id="7a138-324">**Augment the data**: A common technique to add variety to the data is to augment the data by taking an image and applying different transforms (rotate, flip, shift, crop).</span></span> <span data-ttu-id="7a138-325">Это позволяет модели обучаться на более разнообразных примерах.</span><span class="sxs-lookup"><span data-stu-id="7a138-325">This adds more varied examples for the model to learn from.</span></span>
- <span data-ttu-id="7a138-326">**Более длительное обучение**: чем дольше длится обучение, тем лучше будет настроена модель.</span><span class="sxs-lookup"><span data-stu-id="7a138-326">**Train for a longer time**: The longer you train, the more tuned the model will be.</span></span> <span data-ttu-id="7a138-327">Увеличение числа эпох может повысить эффективность модели.</span><span class="sxs-lookup"><span data-stu-id="7a138-327">Increasing the number of epochs may improve the performance of your model.</span></span>
- <span data-ttu-id="7a138-328">**Эксперименты с гиперпараметрами**: в дополнение к параметрам, используемым в этом учебнике, можно настроить и другие параметры, способные повысить эффективность.</span><span class="sxs-lookup"><span data-stu-id="7a138-328">**Experiment with the hyper-parameters**: In addition to the parameters used in this tutorial, other parameters can be tuned to potentially improve performance.</span></span> <span data-ttu-id="7a138-329">Изменение скорости обучения, которая определяет величину изменений, вносимых в модель после каждой эпохи, может повысить эффективность.</span><span class="sxs-lookup"><span data-stu-id="7a138-329">Changing the learning rate, which determines the magnitude of updates made to the model after each epoch may improve performance.</span></span>
- <span data-ttu-id="7a138-330">**Использование другой архитектуры модели**: в зависимости от характера ваших данных модель, способная лучше изучить их признаки, может отличаться.</span><span class="sxs-lookup"><span data-stu-id="7a138-330">**Use a different model architecture**: Depending on what your data looks like, the model that can best learn its features may differ.</span></span> <span data-ttu-id="7a138-331">Если вы не удовлетворены эффективностью модели, попробуйте изменить архитектуру.</span><span class="sxs-lookup"><span data-stu-id="7a138-331">If you're not satisfied with the performance of your model, try changing the architecture.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="7a138-332">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7a138-332">Additional Resources</span></span>

- <span data-ttu-id="7a138-333">[Сравнение глубокого и машинного обучения](/azure/machine-learning/service/concept-deep-learning-vs-machine-learning).</span><span class="sxs-lookup"><span data-stu-id="7a138-333">[Deep Learning vs Machine Learning](/azure/machine-learning/service/concept-deep-learning-vs-machine-learning).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a138-334">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="7a138-334">Next steps</span></span>

<span data-ttu-id="7a138-335">В этом учебнике вы узнали, как создать пользовательскую модель глубокого обучения с использованием передачи обучения, предварительно обученной модели классификации изображений TensorFlow и API классификации изображений ML.NET для классификации изображений бетонных поверхностей как растрескавшихся или нерастрескавшихся.</span><span class="sxs-lookup"><span data-stu-id="7a138-335">In this tutorial, you learned how to build a custom deep learning model using transfer learning, a pretrained image classification TensorFlow model and the ML.NET Image Classification API to classify images of concrete surfaces as cracked or uncracked.</span></span>

<span data-ttu-id="7a138-336">Переходите к следующему руководству.</span><span class="sxs-lookup"><span data-stu-id="7a138-336">Advance to the next tutorial to learn more.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a138-337">Обнаружение объектов</span><span class="sxs-lookup"><span data-stu-id="7a138-337">Object Detection</span></span>](object-detection-onnx.md)