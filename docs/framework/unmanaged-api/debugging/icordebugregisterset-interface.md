---
title: Интерфейс ICorDebugRegisterSet
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet
helpviewer_keywords:
- ICorDebugRegisterSet interface [.NET Framework debugging]
ms.assetid: d3d9676d-0b87-4bc3-b679-7bbc7a186c88
topic_type:
- apiref
ms.openlocfilehash: 940810288b72be0d4dfc5366176663c22c369ebb
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2020
ms.locfileid: "95712382"
---
# <a name="icordebugregisterset-interface"></a>Интерфейс ICorDebugRegisterSet

Представляет набор регистров, доступных на компьютере, который выполняет код в данный момент.  
  
## <a name="methods"></a>Методы  
  
|Метод|Описание|  
|------------|-----------------|  
|[Метод GetRegisters](icordebugregisterset-getregisters-method.md)|Возвращает значение каждого регистра (на компьютере, выполняющем в данный момент код), который задается битовой маской.|  
|[Метод GetRegistersAvailable](icordebugregisterset-getregistersavailable-method.md)|Возвращает битовую маску, указывающую, какие регистры в данный `ICorDebugRegisterSet` момент доступны.|  
|[Метод GetThreadContext](icordebugregisterset-getthreadcontext-method.md)|Возвращает контекст текущего потока.|  
|[Метод SetRegisters](icordebugregisterset-setregisters-method.md)|Не реализовано для .NET Framework версии 2,0.|  
|[Метод SetThreadContext](icordebugregisterset-setthreadcontext-method.md)|Не реализовано для .NET Framework 2,0.|  
  
## <a name="remarks"></a>Комментарии  

 `ICorDebugRegisterSet`Интерфейс поддерживает только 32-разрядные регистры. Используйте интерфейс [ICorDebugRegisterSet2](icordebugregisterset2-interface.md) на платформах, таких как IA-64, требующих дополнительных регистров.  
  
> [!NOTE]
> Этот интерфейс не поддерживает удаленные вызовы между компьютерами или между процессами.  
  
## <a name="requirements"></a>Требования  

 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **.NET Framework версии:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также раздел

- [Интерфейсы отладки](debugging-interfaces.md)
- [Интерфейс ICorDebugRegisterSet2](icordebugregisterset2-interface.md)
