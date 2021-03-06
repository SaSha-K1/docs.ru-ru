---
title: Интерфейс ICorDebugFunctionBreakpoint
ms.date: 03/30/2017
api_name:
- ICorDebugFunctionBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunctionBreakpoint
helpviewer_keywords:
- ICorDebugFunctionBreakpoint interface [.NET Framework debugging]
ms.assetid: 9c149303-14b1-4138-83d7-e8c3e0fcd332
topic_type:
- apiref
ms.openlocfilehash: 0f1e6bbdf16c953b0dd22d9dfa44bc3585f1269e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726253"
---
# <a name="icordebugfunctionbreakpoint-interface"></a>Интерфейс ICorDebugFunctionBreakpoint

Расширяет интерфейс Икордебугбреакпоинт для поддержки точек останова в функциях.  
  
## <a name="methods"></a>Методы  
  
|Метод|Описание|  
|------------|-----------------|  
|[Метод GetFunction](icordebugfunctionbreakpoint-getfunction-method.md)|Возвращает указатель на интерфейс ICorDebugFunction, ссылающийся на функцию, в которой задана точка останова.|  
|[Метод GetOffset](icordebugfunctionbreakpoint-getoffset-method.md)|Возвращает смещение точки останова внутри функции.|  
  
## <a name="remarks"></a>Комментарии  
  
> [!NOTE]
> Этот интерфейс не поддерживает удаленные вызовы между компьютерами или между процессами.  
  
## <a name="requirements"></a>Требования  

 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **.NET Framework версии:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также раздел

- [Интерфейсы отладки](debugging-interfaces.md)
