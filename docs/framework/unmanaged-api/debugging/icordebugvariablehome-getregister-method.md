---
title: 'Метод ICorDebugVariableHome::'
ms.date: 03/30/2017
api_name:
- ICorDebugVariableHome.GetRegister
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHome::GetRegister
helpviewer_keywords:
- ICorDebugVariableHome::GetRegister method [.NET Framework debugging]
- GetRegister method, ICorDebugVariableHome interface [.NET Framework debugging]
ms.assetid: a5eecd7b-b04c-4266-bff2-7c8771d519a8
topic_type:
- apiref
ms.openlocfilehash: 7f912f4b13620b567f5aa097604e98112d85f02d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2020
ms.locfileid: "95711758"
---
# <a name="icordebugvariablehomegetregister-method"></a>Метод ICorDebugVariableHome::

Возвращает регистр, содержащий переменную с типом расположения `VLT_REGISTER` , и базовый регистр для переменной с типом расположения `VLT_REGISTER_RELATIVE` .  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT GetRegister(  
    [out] CorDebugRegister *pRegister  
);  
```  
  
## <a name="parameters"></a>Параметры  

 `pRegister`  
 заполняет Значение перечисления CorDebugRegister, указывающее регистр для переменной с типом расположения `VLT_REGISTER` и базовый регистр для переменной с типом расположения `VLT_REGISTER_RELATIVE` .  
  
## <a name="return-value"></a>Возвращаемое значение  

 Метод возвращает следующие значения:  
  
|Значение|Описание|  
|-----------|-----------------|  
|`S_OK`|Переменная находится в регистре, указанном `pRegister` аргументом.|  
|`E_FAIL`|Переменная не находится в регистре или расположении, относительно регистра.|  
  
## <a name="requirements"></a>Требования  

 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **.NET Framework версии:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>См. также раздел

- [Перечисление VariableLocationType](variablelocationtype-enumeration.md)
- [Интерфейс ICorDebugVariableHome](icordebugvariablehome-interface.md)
