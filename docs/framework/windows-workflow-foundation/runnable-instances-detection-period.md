---
title: Период обнаружения запускаемых экземпляров
ms.date: 03/30/2017
ms.assetid: 4ea5c787-b638-47fd-bfc8-ede8c2898ce6
ms.openlocfilehash: aefde2726bb2ccc15f9e68009e5e141602b13b10
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/26/2020
ms.locfileid: "96245774"
---
# <a name="runnable-instances-detection-period"></a>Период обнаружения запускаемых экземпляров

Хранилище экземпляров рабочих процессов SQL выполняется в форме внутренней задачи, которая периодически активизируется и обнаруживает в базе данных сохраняемости экземпляры, которые могут быть запущены или активированы. Свойство **периода обнаружения готовых экземпляров** в хранилище экземпляров рабочих процессов SQL определяет период времени, по истечении которого в хранилище экземпляров рабочих процессов SQL выполняется задача обнаружения для обнаружения любых готовых к запуску или активируемого экземпляров рабочих процессов в базе данных сохраняемости после предыдущего цикла обнаружения.  
  
 Установка более короткого интервала для этого свойства сокращает временной интервал между завершением отсчета таймера, связанного с экземпляром рабочего процесса, и оповещением о событии с последующей загрузкой экземпляра. Однако это также увеличивает нагрузку по обработке на узел и может быть нежелательным в ситуациях, в которых отказы постоянных таймеров и/или узлов случаются редко. Свойство имеет тип TimeSpan; значение свойства соответствует формату «чч:мм:сс». Минимальное значение данного свойства равно 00:00:01. Значение свойства по умолчанию равно 00:00:05.  
  
 Дополнительные сведения об обнаружении и активации готовых экземпляров рабочих процессов активируемого см. в статье [Активация экземпляра](instance-activation.md).
