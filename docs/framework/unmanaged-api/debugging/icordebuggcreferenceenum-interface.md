---
title: Интерфейс ICorDebugGCReferenceEnum
ms.date: 03/30/2017
api_name:
- ICorDebugGCReferenceEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugGCReferenceEnum
helpviewer_keywords:
- ICorDebugGCReferenceEnum interface [.NET Framework debugging]
ms.assetid: 5f3c91c9-c035-454f-96cc-011cab1ea06b
topic_type:
- apiref
ms.openlocfilehash: 12ce800cb83ef4f79710aa441b50be860526023c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2020
ms.locfileid: "95728125"
---
# <a name="icordebuggcreferenceenum-interface"></a>Интерфейс ICorDebugGCReferenceEnum

Предоставляет перечислитель для объектов, для которых будет выполнена сборка мусора.  
  
## <a name="methods"></a>Методы  
  
|Метод|Описание|  
|------------|-----------------|  
|[Метод Next](icordebuggcreferenceenum-next-method.md)|Возвращает указанное число экземпляров [COR_GC_REFERENCE](cor-gc-reference-structure.md) , содержащих сведения об объектах, которые будут собираться сборщиком мусора.|  
  
## <a name="remarks"></a>Комментарии  

 `ICorDebugGCReferenceEnum`Интерфейс реализует интерфейс "ICorDebugEnum".  
  
 `ICorDebugGCReferenceEnum`Экземпляр заполняется [COR_GC_REFERENCE](cor-gc-reference-structure.md) экземплярами путем вызова метода [метод ICorDebugProcess5:: енумератегкреференцес](icordebugprocess5-enumerategcreferences-method.md) . [COR_GC_REFERENCE](cor-gc-reference-structure.md) объекты можно перечислить, вызвав метод [Икордебуггкреференце:: Next](icordebuggcreferenceenum-next-method.md) .  
  
 [COR_GC_REFERENCE](cor-gc-reference-structure.md) объекты в коллекции, заполненной этим методом, представляют три вида объектов:  
  
- Объекты из всех управляемых стеков. Сюда входят динамические ссылки в управляемом коде, а также объекты, созданные средой CLR.  
  
- Объекты из таблицы Handle. Это включает в себя строгие ссылки ( `HNDTYPE_STRONG` и `HNDTYPE_REFCOUNT` ) и статические переменные в модуле.  
  
- Объекты из очереди метода завершения. Очередь метода завершения помещает объекты в корни до запуска метода завершения.  
  
## <a name="requirements"></a>Требования  

 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **.NET Framework версии:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>См. также раздел

- [Интерфейсы отладки](debugging-interfaces.md)
